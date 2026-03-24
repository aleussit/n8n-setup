# n8n + External Runners (EasyPanel)

Este repositorio contem tudo que o Compose precisa para subir o n8n com runners externos.

## Compose sozinho nao basta

O arquivo Compose referencia outros caminhos do projeto:

- build do servico `runners`: `./runners/Dockerfile`
- dependencias Python: `./runners/requirements.txt`
- configuracao de task-runners: `./config/n8n-task-runners.json`

Se esses arquivos/pastas nao existirem, o deploy falha.

## Estrutura obrigatoria

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

## Setup do zero com Git

```bash
git init
git branch -M main
git add .
git commit -m "feat: bootstrap n8n easypanel stack"
```

Depois, crie um repositorio remoto (GitHub/GitLab) e envie:

```bash
git remote add origin <URL_DO_REPOSITORIO>
git push -u origin main
```

## Deploy no EasyPanel

Siga o guia em [EASYPANEL_DEPLOY.md](EASYPANEL_DEPLOY.md).
