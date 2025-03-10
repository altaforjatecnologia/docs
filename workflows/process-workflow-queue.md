---
title: 'Processamento de Workflows na Fila'
description: 'Documentação técnica sobre o processamento de workflows a partir da fila RabbitMQ'
---

# Processamento de Workflows na Fila

Esta documentação técnica descreve o funcionamento do sistema de processamento de workflows a partir da fila RabbitMQ, implementado pelo comando `ProcessWorkflowFromQueue`.

## Visão Geral

O `ProcessWorkflowFromQueue` é um comando do Laravel responsável por consumir mensagens da fila RabbitMQ e processar workflows. Este componente é fundamental para a execução assíncrona de workflows no IntegraBot, permitindo que ações sejam executadas em segundo plano sem bloquear a interface do usuário.

## Arquitetura

O processamento de workflows segue uma arquitetura baseada em filas, onde:

1. Os workflows são enfileirados no RabbitMQ quando acionados
2. O comando `ProcessWorkflowFromQueue` consome as mensagens da fila
3. Cada workflow é processado de acordo com suas ações configuradas
4. Os resultados são armazenados no banco de dados

## Configuração do RabbitMQ

O sistema utiliza o RabbitMQ como broker de mensagens, com as seguintes configurações:

- **Fila**: `workflows.process`
- **Durabilidade**: Sim (mensagens persistem mesmo se o servidor for reiniciado)
- **Exclusividade**: Não (múltiplos consumidores podem acessar a fila)
- **Auto-delete**: Não (a fila não é excluída quando não há consumidores)

As configurações de conexão são definidas através de variáveis de ambiente:

```
RABBITMQ_HOST=
RABBITMQ_PORT=
RABBITMQ_USER=
RABBITMQ_PASSWORD=
```

## Ciclo de Vida do Processamento

### 1. Consumo da Fila

O comando inicia uma conexão com o RabbitMQ e configura um consumidor para a fila `workflows.process`. Ele permanece em execução, aguardando novas mensagens.

### 2. Processamento de Mensagens

Quando uma mensagem é recebida, o sistema:

1. Decodifica o conteúdo JSON da mensagem
2. Extrai o ID da execução do workflow
3. Chama o método `processWorkflow()` para processar o workflow
4. Confirma o recebimento da mensagem (ack) após o processamento

### 3. Processamento do Workflow

O método `processWorkflow()` é responsável por:

1. Buscar a execução do workflow no banco de dados
2. Verificar o status atual da execução
3. Processar as ações associadas à execução
4. Atualizar o status da execução

### 4. Processamento de Ações

Cada ação do workflow é processada pelo método `processActionExecution()`, que:

1. Verifica o status atual da ação
2. Executa a ação de acordo com seu tipo (email, webhook, etc.)
3. Atualiza o status da ação
4. Armazena o resultado ou erro da execução

### 5. Finalização do Workflow

Após processar todas as ações, o sistema:

1. Verifica se todas as ações foram concluídas
2. Atualiza o status do workflow para "concluído" ou "agendado"
3. Registra a data de conclusão, se aplicável

## Estados de Execução

### Estados do Workflow

- **PENDING**: Workflow criado, mas ainda não iniciado
- **SCHEDULED**: Workflow agendado para execução futura
- **RUNNING**: Workflow em execução
- **COMPLETED**: Workflow concluído com sucesso
- **FAILED**: Workflow falhou durante a execução

### Estados das Ações

- **PENDING**: Ação criada, mas ainda não iniciada
- **SCHEDULED**: Ação agendada para execução futura
- **RUNNING**: Ação em execução
- **COMPLETED**: Ação concluída com sucesso
- **FAILED**: Ação falhou durante a execução

## Tratamento de Erros

O sistema implementa um robusto tratamento de erros:

1. Erros durante o processamento são capturados e registrados
2. Ações com erro são marcadas como "falhas"
3. Informações detalhadas sobre o erro são armazenadas
4. Workflows com erros críticos são marcados como "falhos"
5. Erros de conexão com o RabbitMQ são tratados adequadamente

## Agendamento de Ações

O sistema suporta o agendamento de ações para execução futura:

1. Ações com `scheduled_for` definido são executadas apenas quando o horário chegar
2. Workflows com ações futuras são marcados como "agendados"
3. O sistema verifica periodicamente se há ações agendadas prontas para execução

## Tipos de Ações Suportados

Atualmente, o sistema suporta os seguintes tipos de ações:

- **Email**: Envio de emails com suporte a templates e variáveis
- **Webhook**: Envio de requisições HTTP para endpoints externos (em desenvolvimento)
- **API**: Chamadas a APIs externas (em desenvolvimento)
- **Database**: Operações no banco de dados (em desenvolvimento)

## Execução Manual

Para executar o processador de workflows manualmente, utilize o seguinte comando:

```bash
php artisan workflow:process-queue
```

Este comando iniciará o consumidor da fila e permanecerá em execução até ser interrompido manualmente (CTRL+C).

## Execução como Serviço

Para ambientes de produção, recomenda-se configurar o processador como um serviço do sistema, utilizando ferramentas como Supervisor ou systemd.

### Exemplo de Configuração do Supervisor

```ini
[program:workflow-processor]
process_name=%(program_name)s_%(process_num)02d
command=php /caminho/para/seu/projeto/artisan workflow:process-queue
autostart=true
autorestart=true
user=www-data
numprocs=1
redirect_stderr=true
stdout_logfile=/caminho/para/seu/projeto/storage/logs/workflow-processor.log
```

## Considerações de Performance

- O processador utiliza o padrão de qualidade de serviço (QoS) do RabbitMQ para limitar o número de mensagens processadas simultaneamente
- Cada ação é processada em sua própria transação de banco de dados para evitar bloqueios longos
- O sistema implementa mecanismos para evitar o processamento repetido de workflows já concluídos

## Logs e Monitoramento

O sistema gera logs detalhados sobre o processamento de workflows:

- Informações sobre o início e conclusão de workflows
- Detalhes sobre a execução de cada ação
- Erros e exceções durante o processamento
- Métricas de performance e tempo de execução

Os logs são armazenados no sistema de logs padrão do Laravel e podem ser configurados para envio a sistemas de monitoramento externos.

## Resolução de Problemas

### Mensagens não estão sendo processadas

- Verifique se o RabbitMQ está em execução e acessível
- Confirme se as credenciais de acesso estão corretas
- Verifique se a fila `workflows.process` existe

### Ações não estão sendo executadas

- Verifique o status das ações no banco de dados
- Confirme se as ações estão configuradas corretamente
- Verifique se há erros nos logs relacionados às ações específicas

### Workflows ficam presos no estado "running"

- Verifique se há ações em execução que não foram concluídas
- Confirme se o processador está em execução
- Verifique se há erros nos logs que possam indicar problemas no processamento 
