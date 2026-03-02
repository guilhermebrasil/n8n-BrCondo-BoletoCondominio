# n8n-BrCondo-BoletoCondominio

Automação usando n8n com o objetivo de extrair o PDF (boleto do condomínio) do email enviado pela BrCondo.

## Fluxo do Workflow

```
Gmail Trigger (8:30) → Tem Email? → Extrair Link → Acessar Página → Extrair URL PDF → Enviar Link via Telegram
```

### Nodes

1. **Gmail Trigger** — Polling às 8:30, filtra emails de `contato@brcondos.com.br` com "Boleto" no assunto
2. **Tem Email?** — Verifica se encontrou algum email
3. **Extrair Link do Boleto** — Decodifica o corpo do email e extrai o link `/Bill/{uuid}`
4. **Acessar Página do Boleto** — Faz GET na página do boleto para obter o HTML
5. **Extrair URL do PDF** — Extrai o link do PDF (`/BillPDF/{uuid}/...`) do HTML
6. **Enviar Link via Telegram** — Envia mensagem com o link do PDF para o ChatID `54859439`

> **Nota:** O download direto do PDF não é possível via n8n porque a BrCondo gera o PDF assincronamente via WebSocket/SignalR. O link enviado abre no browser e gera o PDF automaticamente.

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
