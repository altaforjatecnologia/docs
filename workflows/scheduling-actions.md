# Agendamento de Ações nos Workflows

Este documento explica como configurar o agendamento de ações nos workflows para controlar quando elas serão executadas.

## Introdução ao Agendamento

O agendamento de ações permite que você controle quando cada ação em um workflow será executada. Isso é útil para:

- Criar sequências de ações com intervalos específicos
- Agendar notificações para serem enviadas em momentos específicos
- Implementar lógica de espera entre etapas de um processo
- Distribuir a carga de trabalho ao longo do tempo

## Tipos de Agendamento

O sistema oferece quatro tipos de agendamento para ações:

### 1. Imediato

A ação é executada assim que possível, sem atraso intencional.

- **Uso recomendado**: Para ações que precisam ser executadas imediatamente após o acionamento do workflow ou após a ação anterior.
- **Configuração**: Selecione "Imediato" no campo "Tipo de Agendamento".

### 2. Minutos

A ação é executada após o número especificado de minutos.

- **Uso recomendado**: Para atrasos curtos, como enviar uma mensagem de acompanhamento alguns minutos após um evento.
- **Configuração**: Selecione "Minutos" no campo "Tipo de Agendamento" e especifique o número de minutos no campo "Valor".
- **Exemplo**: Configurar para 15 minutos fará com que a ação seja executada 15 minutos após o início do workflow.

### 3. Horas

A ação é executada após o número especificado de horas.

- **Uso recomendado**: Para atrasos médios, como enviar um lembrete algumas horas após um evento.
- **Configuração**: Selecione "Horas" no campo "Tipo de Agendamento" e especifique o número de horas no campo "Valor".
- **Exemplo**: Configurar para 2 horas fará com que a ação seja executada 2 horas após o início do workflow.

### 4. Dias

A ação é executada após o número especificado de dias.

- **Uso recomendado**: Para atrasos longos, como enviar um follow-up alguns dias após um evento.
- **Configuração**: Selecione "Dias" no campo "Tipo de Agendamento" e especifique o número de dias no campo "Valor".
- **Exemplo**: Configurar para 3 dias fará com que a ação seja executada 3 dias após o início do workflow.

## Como Configurar o Agendamento

1. No construtor de workflows, selecione ou adicione uma ação.
2. Na seção "Agendamento", selecione o tipo de agendamento desejado (Imediato, Minutos, Horas ou Dias).
3. Se você selecionar Minutos, Horas ou Dias, especifique o valor correspondente no campo "Valor".
4. Salve a ação.

## Considerações Importantes

### Tempo de Referência

O tempo de agendamento é calculado a partir do momento em que o workflow é iniciado, não a partir do momento em que a ação anterior é concluída.

### Ações Sequenciais vs. Paralelas

- **Ações Sequenciais**: Para garantir que as ações sejam executadas em sequência, configure-as com tempos de agendamento crescentes.
- **Ações Paralelas**: Para executar ações em paralelo, configure-as com o mesmo tempo de agendamento.

### Dependências entre Ações

Atualmente, o sistema não suporta dependências diretas entre ações (onde uma ação só é executada após a conclusão de outra). Para simular esse comportamento, você deve estimar o tempo necessário para a conclusão da ação anterior e configurar o agendamento adequadamente.

### Falhas e Recuperação

Se uma ação falhar, as ações subsequentes ainda serão executadas de acordo com seu agendamento. O sistema não interrompe automaticamente o workflow em caso de falha de uma ação.

## Exemplos de Cenários de Agendamento

### Cenário 1: Sequência de Lembretes

Um workflow para enviar uma sequência de lembretes sobre um evento:

1. **Ação 1**: Enviar email inicial - Agendamento: Imediato
2. **Ação 2**: Enviar primeiro lembrete - Agendamento: 1 dia
3. **Ação 3**: Enviar segundo lembrete - Agendamento: 3 dias
4. **Ação 4**: Enviar lembrete final - Agendamento: 6 dias

### Cenário 2: Processo de Onboarding

Um workflow para o processo de onboarding de um novo usuário:

1. **Ação 1**: Enviar email de boas-vindas - Agendamento: Imediato
2. **Ação 2**: Enviar guia de primeiros passos - Agendamento: 2 horas
3. **Ação 3**: Verificar se o usuário completou o perfil - Agendamento: 1 dia
4. **Ação 4**: Enviar dicas avançadas - Agendamento: 3 dias
5. **Ação 5**: Solicitar feedback inicial - Agendamento: 7 dias

### Cenário 3: Processamento em Lote

Um workflow para processar dados em lote para evitar sobrecarga:

1. **Ação 1**: Processar primeiro lote - Agendamento: Imediato
2. **Ação 2**: Processar segundo lote - Agendamento: 30 minutos
3. **Ação 3**: Processar terceiro lote - Agendamento: 60 minutos
4. **Ação 4**: Enviar relatório de conclusão - Agendamento: 90 minutos

## Dicas e Boas Práticas

1. **Planeje com antecedência**: Desenhe o fluxo completo do seu workflow antes de configurar o agendamento.

2. **Considere fusos horários**: Lembre-se de que o agendamento é baseado no fuso horário do servidor.

3. **Teste com tempos reduzidos**: Durante o desenvolvimento e teste, use tempos reduzidos (como minutos em vez de dias) para verificar se o workflow funciona como esperado.

4. **Monitore a execução**: Verifique regularmente os logs para garantir que as ações estão sendo executadas nos momentos esperados.

5. **Evite agendamentos muito curtos**: Evite agendar muitas ações com intervalos muito curtos para evitar sobrecarga do sistema.

6. **Documente suas decisões**: Mantenha documentação sobre por que você escolheu determinados tempos de agendamento para referência futura. 
