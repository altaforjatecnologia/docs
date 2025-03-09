# Fluxo de Trabalho dos Workflows

Este documento explica como os workflows funcionam no sistema, desde a criação até a execução das ações.

## Visão Geral

Os workflows permitem automatizar tarefas com base em eventos específicos. Cada workflow consiste em uma série de ações que são executadas em uma ordem definida. As ações podem ser agendadas para execução imediata ou para um momento futuro.

## Estados de um Workflow

Um workflow pode estar em um dos seguintes estados:

- **Pendente (PENDING)**: O workflow foi criado, mas ainda não começou a ser processado.
- **Agendado (SCHEDULED)**: O workflow está agendado para processamento.
- **Em Execução (RUNNING)**: O workflow está sendo processado atualmente.
- **Concluído (COMPLETED)**: Todas as ações do workflow foram concluídas com sucesso.
- **Falha (FAILED)**: Ocorreu um erro durante o processamento do workflow.

## Estados de uma Ação

Cada ação dentro de um workflow pode estar em um dos seguintes estados:

- **Agendada (SCHEDULED)**: A ação está agendada para execução.
- **Em Execução (RUNNING)**: A ação está sendo executada atualmente.
- **Concluída (COMPLETED)**: A ação foi concluída com sucesso.
- **Falha (FAILED)**: Ocorreu um erro durante a execução da ação.

## Tipos de Agendamento

As ações podem ser agendadas de diferentes formas:

- **Imediato**: A ação é executada assim que possível.
- **Minutos**: A ação é executada após o número especificado de minutos.
- **Horas**: A ação é executada após o número especificado de horas.
- **Dias**: A ação é executada após o número especificado de dias.

## Fluxo de Execução

1. **Criação do Workflow**:
   - Um workflow é criado quando uma ferramenta é executada ou através da API.
   - O workflow é criado com o status "Pendente".
   - As ações do workflow são agendadas de acordo com suas configurações.

2. **Verificação de Workflows Pendentes**:
   - O sistema verifica periodicamente se há workflows pendentes ou agendados.
   - Para cada workflow pendente, o sistema verifica se há ações prontas para execução.
   - Se houver ações prontas, o workflow é marcado como "Em Execução" e enviado para processamento.
   - Se todas as ações estiverem agendadas para o futuro, o workflow permanece no estado "Pendente".

3. **Processamento do Workflow**:
   - O sistema processa cada ação do workflow na ordem definida.
   - Se uma ação estiver agendada para o futuro, ela não será executada até que chegue o momento agendado.
   - Após a execução de uma ação, seu status é atualizado para "Concluída" ou "Falha".

4. **Conclusão do Workflow**:
   - Quando todas as ações do workflow forem concluídas, o workflow é marcado como "Concluído".
   - Se ocorrer um erro durante o processamento, o workflow é marcado como "Falha".

## Variáveis nos Workflows

Os workflows podem usar variáveis para tornar as ações mais dinâmicas. As variáveis são inseridas no formato `{nome_variavel}` e são substituídas pelos valores correspondentes durante a execução.

### Variáveis do Sistema

- `{_tool.name}`: Nome da ferramenta que acionou o workflow.
- `{_tool.description}`: Descrição da ferramenta.
- `{_context.project_id}`: ID do projeto atual.
- `{_context.chatbot_id}`: ID do chatbot.
- `{_context.timestamp}`: Data e hora da execução.

### Variáveis da Habilidade

Além das variáveis do sistema, todas as variáveis fornecidas pela habilidade que acionou o workflow também estão disponíveis.

## Exemplo de Uso

1. **Criação de um Workflow**:
   - Crie um novo workflow na seção "Workflows" do painel.
   - Defina um nome e uma descrição para o workflow.
   - Adicione ações ao workflow, como enviar um email ou fazer uma chamada de API.
   - Configure cada ação com os parâmetros necessários.
   - Defina o agendamento para cada ação (imediato, minutos, horas ou dias).

2. **Associação a uma Ferramenta**:
   - Associe o workflow a uma ferramenta na seção "Ferramentas" do painel.
   - Quando a ferramenta for executada, o workflow será acionado automaticamente.

3. **Monitoramento**:
   - Monitore o status dos workflows na seção "Workflows" do painel.
   - Verifique os logs para obter informações detalhadas sobre a execução.

## Dicas e Boas Práticas

- **Teste seus workflows**: Antes de usar um workflow em produção, teste-o para garantir que funcione como esperado.
- **Use variáveis**: Use variáveis para tornar seus workflows mais dinâmicos e reutilizáveis.
- **Monitore os logs**: Verifique regularmente os logs para identificar e corrigir problemas.
- **Planeje o agendamento**: Planeje cuidadosamente o agendamento das ações para garantir que sejam executadas na ordem correta e no momento adequado. 
