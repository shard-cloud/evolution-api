## O que é este template?

**Evolution API** é uma API REST open-source para integração com WhatsApp
(via [Baileys](https://github.com/WhiskeySockets/Baileys)), com suporte a
múltiplas instâncias, webhooks e integrações prontas com Typebot, Chatwoot,
n8n, Dify e OpenAI. Este template implanta a Evolution API na ShardCloud como
um app **Node.js** com um banco **PostgreSQL** anexado automaticamente.

## O que a Evolution API faz?

- Cria e gerencia múltiplas instâncias de WhatsApp por uma única API
- Envia e recebe mensagens de texto, mídia, botões e listas
- Dispara **webhooks** para eventos (mensagens recebidas, status de conexão,
  etc.)
- Integra nativamente com Typebot, Chatwoot, n8n, Dify e OpenAI para
  automação de atendimento

### Fluxo básico de uso

```
Deploy do template → App conectado ao Postgres → API no ar
                                                        ↓
POST /instance/create → QR Code gerado → Escaneia no WhatsApp
                                                        ↓
Instância conectada → Envia/recebe mensagens via API ou webhook
```

## Estrutura do projeto

```
evolution-api/
├── src/                  ← Código-fonte da API
├── prisma/               ← Schemas e migrations (Postgres/MySQL)
├── Docker/               ← Scripts auxiliares de deploy
├── package.json          ← Dependências e scripts (build, db:deploy, ...)
├── .shardcloud           ← Config de deploy da ShardCloud
└── docs/
    ├── _manifest.json
    ├── 01-intro.md       ← Esta página
    └── 02-config.md      ← Configuração
```

## Próximos passos

1. **[Configurar o app](02-config.md)** — variáveis de ambiente, banco de
   dados e como criar sua primeira instância
