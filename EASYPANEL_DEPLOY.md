# n8n + runners no EasyPanel

Este projeto deve ser publicado como app Compose com a estrutura completa de pastas.

## Compose sozinho nao basta

O arquivo `docker-compose.easypanel.yml` depende de:

- `./runners/Dockerfile` (build do servico runners)
- `./runners/requirements.txt` (libs Python do runner)
- `./config/n8n-task-runners.json` (config dos task-runners)

Se publicar apenas o texto do compose, sem esses arquivos, o deploy falha.

## Estrutura minima obrigatoria

```text
.
├── docker-compose.easypanel.yml
├── .env.easypanel.example
├── config/
│   └── n8n-task-runners.json
└── runners/
    ├── Dockerfile
    └── requirements.txt
```

## 1) Criar repositório Git (do zero)

No diretório do projeto:

```bash
git init
git branch -M main
git add .
git commit -m "feat: bootstrap n8n easypanel stack"
```

Depois envie para GitHub/GitLab:

```bash
git remote add origin <URL_DO_REPOSITORIO>
git push -u origin main
```

## 2) Criar app Compose no EasyPanel

- No EasyPanel, crie um novo app do tipo Compose.
- Conecte ao repositório/pasta contendo a estrutura completa.
- Selecione o arquivo `docker-compose.easypanel.yml`.

## 3) Variáveis de ambiente

- Defina no painel as variáveis de `.env.easypanel.example`:
  - `N8N_HOST`
  - `N8N_RUNNERS_AUTH_TOKEN`

## 4) Roteamento de domínio

- No serviço `n8n`, configure domínio: `n8n.iaoptimize.com.br`.
- Porta do serviço para roteamento HTTP: `5678`.
- Ative HTTPS (Let's Encrypt).

## 5) DNS

- Registro A de `n8n.iaoptimize.com.br` para o IP do servidor EasyPanel.

## 6) Deploy e testes rápidos

- Faça deploy/redeploy.
- Teste acesso do editor: `https://n8n.iaoptimize.com.br`.
- Crie um workflow de teste com Code node (JS/Python) para validar runners.

## Notas

- O broker de runners fica interno na porta `5679` (somente rede interna do compose).
- O `n8n-task-runners.json` está corrigido com flags válidas do Node.
