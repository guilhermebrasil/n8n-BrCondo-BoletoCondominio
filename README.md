# n8n-BrCondo-BoletoCondominio

Automação usando n8n com o objetivo de extrair o PDF (boleto do condomínio) do email enviado pela BrCondo.

## Fluxo do Workflow

```
Agendamento (8h) → Gmail → Tem Email? → Extrair Link → Acessar Página → Extrair URL PDF → Baixar PDF → Enviar via Telegram
```

### Nodes

1. **Agendamento Diário 8h** — Schedule Trigger, executa todos os dias às 8h (fuso: America/Sao_Paulo)
2. **Gmail - Buscar Emails** — Busca emails não lidos de `contato@brcondos.com.br` com "Boleto" no assunto
3. **Tem Email?** — Verifica se encontrou algum email
4. **Extrair Link do Boleto** — Decodifica o corpo do email e extrai o link `/Bill/{uuid}`
5. **Acessar Página do Boleto** — Faz GET na página do boleto para obter o HTML
6. **Extrair URL do PDF** — Extrai o link direto do PDF (`/BillPDF/{uuid}/...`) do HTML
7. **Baixar PDF do Boleto** — Faz download do arquivo PDF
8. **Enviar PDF via Telegram** — Envia o PDF para o ChatID `54859439`

## Como usar

1. Importe o arquivo `workflow-boleto-condominio.json` no n8n
2. Configure as credenciais:
   - **Gmail** (OAuth2)
   - **Telegram Bot** (API Token)
3. Ative o workflow

## Requisitos

- n8n >= 2.9.4
- Conta Gmail com acesso OAuth2
- Bot do Telegram configurado
