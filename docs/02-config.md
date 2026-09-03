## Pré-requisitos

- Uma **conta na ShardCloud** com plano que suporte apps + banco de dados
  anexado
- Nenhuma conta externa é necessária para começar — a instância do WhatsApp é
  conectada depois, via QR Code

## 1. Deploy do template

Ao implantar este template pela ShardCloud, um app Node.js é criado com um
banco **PostgreSQL** anexado automaticamente. As variáveis de ambiente abaixo
já vêm pré-preenchidas — revise antes de iniciar o app pela primeira vez.

| Variável                 | Descrição                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| `AUTHENTICATION_API_KEY` | Chave de admin da API — **troque o valor padrão antes de usar em produção** |
| `DATABASE_PROVIDER`      | Mantenha `postgresql` (é o que o banco anexado fornece)          |
| `CACHE_REDIS_ENABLED`    | `false` por padrão — a Evolution API funciona sem Redis, ele só acelera cache |
| `SERVER_URL`             | Já vem como `{DOMAIN}` — preenchido automaticamente com a URL pública do app assim que você escolhe o subdomínio |

## 2. Primeira inicialização

No primeiro start, o app aplica as migrations do Prisma no banco Postgres
anexado, gera o client do Prisma e compila o projeto antes de subir a API —
isso pode levar um pouco mais que um restart comum. Acompanhe os logs do app
até aparecer a mensagem de servidor pronto.

## 3. Criar sua primeira instância

Com a API no ar, crie uma instância do WhatsApp:

```bash
curl -X POST https://SEU-APP.shardweb.app/instance/create \
  -H "apikey: SUA_AUTHENTICATION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"instanceName": "minha-instancia"}'
```

A resposta traz um QR Code — escaneie no WhatsApp em **Aparelhos
conectados** para ativar a instância.

## 4. Configurar webhooks (opcional)

Para receber eventos (mensagens, status de conexão, etc.) em outro sistema:

```bash
curl -X POST https://SEU-APP.shardweb.app/webhook/set/minha-instancia \
  -H "apikey: SUA_AUTHENTICATION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"webhook": {"url": "https://seu-endpoint.com/webhook", "enabled": true}}'
```

## Referências

- [Documentação oficial da Evolution API](https://doc.evolution-api.com)
- [Repositório original](https://github.com/EvolutionAPI/evolution-api)
