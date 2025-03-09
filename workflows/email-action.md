# Ação de Email em Workflows

Esta documentação explica como configurar e usar a ação de email nos workflows da plataforma IntegraBot.

## Configuração do AWS SES

A plataforma utiliza o Amazon Simple Email Service (SES) para envio de emails. Para configurar o AWS SES, siga os passos abaixo:

1. Acesse o [Console da AWS](https://aws.amazon.com/console/) e faça login na sua conta.
2. Navegue até o serviço SES (Simple Email Service).
3. Verifique os domínios e endereços de email que você deseja usar como remetentes.
4. Crie credenciais de acesso (Access Key e Secret Key) com permissões para o SES.
5. Configure as seguintes variáveis de ambiente no arquivo `.env` do projeto:

```
MAIL_MAILER=ses
MAIL_FROM_ADDRESS="noreply@seudominio.com"
MAIL_FROM_NAME="Nome da Sua Empresa"

AWS_ACCESS_KEY_ID=sua_access_key
AWS_SECRET_ACCESS_KEY=sua_secret_key
AWS_DEFAULT_REGION=regiao_do_ses (ex: us-east-1)
```

## Criando uma Ação de Email no Workflow

Para criar uma ação de email em um workflow:

1. Acesse o builder de workflows.
2. Clique em "Adicionar Ação".
3. Selecione "Email" como aplicativo e "Enviar" como ação.
4. Configure os seguintes campos:

### Campos Disponíveis

- **Assunto**: O assunto do email. Suporta variáveis no formato `{variavel}`.
- **Remetente (opcional)**: O endereço de email do remetente. Se não informado, será usado o valor de `MAIL_FROM_ADDRESS`.
- **Destinatário**: O endereço de email do destinatário. Para múltiplos destinatários, separe por vírgula. Suporta variáveis.
- **CC (opcional)**: Endereços para cópia. Separe múltiplos endereços por vírgula. Suporta variáveis.
- **BCC (opcional)**: Endereços para cópia oculta. Separe múltiplos endereços por vírgula. Suporta variáveis.
- **Conteúdo do Email**: O corpo do email. Suporta HTML e variáveis.

### Usando Variáveis

Você pode usar variáveis no formato `{variavel}` em qualquer campo do email. As variáveis disponíveis incluem:

- Todas as variáveis fornecidas pela habilidade que acionou o workflow.
- Variáveis de contexto:
  - `{_tool.name}`: Nome da ferramenta que acionou o workflow.
  - `{_tool.description}`: Descrição da ferramenta.
  - `{_tool.id}`: ID da ferramenta.
  - `{_context.project_id}`: ID do projeto.
  - `{_context.chatbot_id}`: ID do chatbot.
  - `{_context.timestamp}`: Data e hora da execução.

### Exemplo de Uso

Assunto:
```
Novo lead recebido: {nome}
```

Destinatário:
```
vendas@seudominio.com, {email_responsavel}
```

Conteúdo:
```html
<h2>Novo lead recebido!</h2>
<p>Um novo lead foi registrado pelo chatbot <strong>{_tool.name}</strong>.</p>
<p>Detalhes do lead:</p>
<ul>
  <li><strong>Nome:</strong> {nome}</li>
  <li><strong>Email:</strong> {email}</li>
  <li><strong>Telefone:</strong> {telefone}</li>
  <li><strong>Mensagem:</strong> {mensagem}</li>
</ul>
<p>Data e hora: {_context.timestamp}</p>
```

## Solução de Problemas

### Emails não estão sendo enviados

1. Verifique se as credenciais da AWS estão corretas.
2. Verifique se o domínio ou email do remetente está verificado no AWS SES.
3. Se estiver em ambiente de sandbox do SES, verifique se os destinatários também estão verificados.
4. Verifique os logs do sistema para mensagens de erro relacionadas ao envio de email.

### Variáveis não estão sendo substituídas

1. Verifique se o nome da variável está correto, incluindo maiúsculas e minúsculas.
2. Verifique se a variável está disponível no contexto da execução do workflow.
3. Para variáveis aninhadas, use a notação de ponto: `{objeto.propriedade}`.
