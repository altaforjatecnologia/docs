# Usando Variáveis nos Workflows

Este documento explica como usar variáveis nos workflows para tornar suas ações mais dinâmicas e personalizadas.

## Introdução às Variáveis

As variáveis nos workflows permitem que você insira valores dinâmicos em suas ações. Isso é especialmente útil para personalizar mensagens, URLs, cabeçalhos e outros parâmetros com base em dados específicos.

## Sintaxe das Variáveis

Para usar uma variável em um workflow, você deve inseri-la no formato `{nome_variavel}`. Durante a execução do workflow, essa variável será substituída pelo seu valor correspondente.

Exemplo:
```
Olá {nome_usuario}, seu projeto {_context.project_id} foi atualizado.
```

## Tipos de Variáveis Disponíveis

### Variáveis do Sistema

Estas variáveis são fornecidas automaticamente pelo sistema e estão disponíveis em todos os workflows:

| Variável | Descrição |
|----------|-----------|
| `{_tool.name}` | Nome da ferramenta que acionou o workflow |
| `{_tool.description}` | Descrição da ferramenta |
| `{_context.project_id}` | ID do projeto atual |
| `{_context.chatbot_id}` | ID do chatbot |
| `{_context.timestamp}` | Data e hora da execução |

### Variáveis da Habilidade

Além das variáveis do sistema, todas as variáveis fornecidas pela habilidade que acionou o workflow também estão disponíveis. Estas variáveis dependem da habilidade específica e podem incluir dados como:

- Informações do usuário
- Dados de entrada fornecidos pelo usuário
- Resultados de processamento da habilidade

## Exemplos de Uso de Variáveis

### Em Emails

```
Assunto: Novo contato: {nome}

Corpo:
Olá {nome_destinatario},

Um novo contato foi registrado com os seguintes dados:
- Nome: {nome}
- Email: {email}
- Telefone: {telefone}

Data do registro: {_context.timestamp}

Atenciosamente,
Equipe de Suporte
```

### Em Cabeçalhos de API

```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer {token_api}",
  "X-Project-ID": "{_context.project_id}"
}
```

### Em Corpo de Requisição API

```json
{
  "user_id": "{_context.user_id}",
  "data": {
    "name": "{nome_usuario}",
    "email": "{email_usuario}",
    "project": "{_context.project_id}"
  },
  "timestamp": "{_context.timestamp}"
}
```

### Em Webhooks

```json
{
  "event": "new_contact",
  "project_id": "{_context.project_id}",
  "data": {
    "name": "{nome}",
    "email": "{email}"
  }
}
```

## Dicas para Usar Variáveis

1. **Verifique a disponibilidade**: Certifique-se de que as variáveis que você está usando estão disponíveis no contexto do seu workflow.

2. **Use valores padrão**: Em alguns casos, pode ser útil fornecer valores padrão para variáveis que podem não estar disponíveis.

3. **Teste suas variáveis**: Antes de usar um workflow em produção, teste-o com diferentes valores de variáveis para garantir que funcione como esperado.

4. **Formatação**: Lembre-se de que as variáveis são substituídas como texto simples. Se você precisar de formatação especial (como datas), você precisará garantir que os dados estejam formatados corretamente antes de serem passados para o workflow.

5. **Segurança**: Tenha cuidado ao usar variáveis em contextos sensíveis, como comandos SQL ou scripts. Certifique-se de que os dados são validados e sanitizados adequadamente.

## Resolução de Problemas

Se uma variável não estiver sendo substituída corretamente, verifique o seguinte:

- A variável está escrita corretamente, incluindo maiúsculas e minúsculas.
- A variável está disponível no contexto do workflow.
- O formato da variável está correto (`{nome_variavel}`).
- Não há espaços ou caracteres especiais dentro das chaves.

Se você ainda estiver tendo problemas, verifique os logs do sistema para obter mais informações sobre a execução do workflow. 
