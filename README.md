# 🧑‍🏫 PyMentor — Plataforma de Mentoria

> Plataforma web desenvolvida com Django para que mentores gerenciem seus mentorados, acompanhem progresso, criem tarefas e agendem reuniões.

![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?style=flat-square&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-5.2-092E20?style=flat-square&logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=flat-square&logo=sqlite&logoColor=white)
![HTMX](https://img.shields.io/badge/HTMX-2.0.4-3D72D7?style=flat-square)
![Chart.js](https://img.shields.io/badge/Chart.js-CDN-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)

Projeto desenvolvido durante a **13ª edição da Pystack Week**, promovida pela plataforma **[Pythonando](https://pythonando.com.br)**.

---

## 📋 Sumário

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Estrutura de Diretórios](#estrutura-de-diretórios)
- [Instalação e Configuração](#instalação-e-configuração)
- [Executando o Projeto](#executando-o-projeto)
- [Rotas Disponíveis](#rotas-disponíveis)
- [Fluxo do Mentor](#fluxo-do-mentor)
- [Fluxo do Mentorado](#fluxo-do-mentorado)
- [Painel Administrativo](#painel-administrativo)
- [⚠️ Avisos de Segurança](#️-avisos-de-segurança)
- [Testes](#testes)
- [Como Contribuir](#como-contribuir)
- [Licença](#licença)
- [Pendências e Informações a Confirmar](#pendências-e-informações-a-confirmar)

---

## Sobre o Projeto

O **PyMentor** é uma aplicação web que permite que **mentores** administrem seus **mentorados** (e navigators), acompanhando o progresso de cada um por meio de:

- Cadastro e organização de mentorados por estágio de receita
- Criação e atribuição de tarefas
- Upload de vídeos de referência para mentorados
- Agendamento e gerenciamento de reuniões
- Portal exclusivo para mentorados acessarem suas tarefas e vídeos via token único

---

## Funcionalidades

### Para o Mentor
- ✅ Cadastro e login de mentores
- ✅ Cadastro de mentorados com foto, estágio de receita e navigator responsável
- ✅ Visualização dos mentorados em tabela com gráfico de pizza por estágio
- ✅ Criação de **navigators** (assistentes/co-mentores)
- ✅ Criação de tarefas para cada mentorado
- ✅ Upload de vídeos vinculados a cada mentorado
- ✅ Abertura de horários disponíveis para reuniões
- ✅ Visualização das reuniões agendadas com descrição e tag temática

### Para o Mentorado (portal sem login)
- ✅ Acesso via **token único** gerado automaticamente pelo sistema
- ✅ Visualização das tarefas atribuídas pelo mentor
- ✅ Marcação de tarefas como realizadas (via HTMX, sem recarregar a página)
- ✅ Visualização de vídeos enviados pelo mentor
- ✅ Agendamento de reunião em horários disponibilizados pelo mentor, com escolha de tag temática e descrição

### Estágios de Receita dos Mentorados
| Código | Faixa de Receita |
|--------|-----------------|
| E1 | R$ 3k – R$ 10k |
| E2 | R$ 10k – R$ 100k |
| E3 | R$ 100k – R$ 1M |
| E4 | R$ 1M – R$ 10M |
| E5 | R$ 10M+ |

---

## Tecnologias Utilizadas

| Tecnologia | Versão | Uso |
|------------|--------|-----|
| Python | 3.12+ | Linguagem principal |
| Django | 5.2 | Framework web |
| Pillow | 11.1.0 | Processamento de imagens (fotos e uploads) |
| SQLite | 3 | Banco de dados (padrão de desenvolvimento) |
| asgiref | 3.8.1 | Suporte assíncrono ao Django |
| sqlparse | 0.5.3 | Formatação de SQL |
| tzdata | 2025.2 | Dados de fuso horário |
| HTMX | 2.0.4 (CDN) | Interatividade reativa (marcação de tarefas) |
| Chart.js | latest (CDN) | Gráfico de pizza por estágio |
| Tailwind CSS | CDN | Estilização das interfaces |

---

## Pré-requisitos

Antes de instalar, verifique se você possui:

- **Python 3.12 ou superior** — [download](https://www.python.org/downloads/)
- **pip** (geralmente incluído com o Python)
- **Git** — [download](https://git-scm.com/)

> ⚠️ **Usuários Linux/macOS:** O arquivo `mentorados/views.py` utiliza `locale.setlocale(locale.LC_TIME, 'pt_BR.utf8')` para formatar datas em português. Certifique-se de ter o locale `pt_BR.utf8` instalado no sistema:
> ```bash
> # Debian/Ubuntu
> sudo locale-gen pt_BR.UTF-8
> sudo update-locale
> ```
> **Usuários Windows:** Este locale pode não estar disponível nativamente e pode causar erros na view de agendamento. Veja a seção de [Pendências](#pendências-e-informações-a-confirmar).

---

## Estrutura de Diretórios

```
pymentor/
├── core/                       # Configuração central do projeto Django
│   ├── settings.py             # Configurações (BD, apps, idioma, timezone)
│   ├── urls.py                 # Roteamento raiz
│   ├── wsgi.py                 # Entrypoint WSGI
│   └── asgi.py                 # Entrypoint ASGI
│
├── usuarios/                   # App de autenticação de mentores
│   ├── views.py                # Cadastro e login
│   ├── urls.py                 # Rotas: /usuarios/cadastro/, /usuarios/login/
│   ├── models.py               # (sem modelos customizados — usa User do Django)
│   └── templates/
│       ├── cadastro.html
│       └── login.html
│
├── mentorados/                 # App principal de gestão de mentoria
│   ├── models.py               # Navigators, Mentorados, DisponibilidadeHorarios,
│   │                           # Reuniao, Tarefa, Upload
│   ├── views.py                # Lógica de negócio
│   ├── urls.py                 # Rotas da app
│   ├── auth.py                 # Validação de token do mentorado
│   ├── admin.py                # Modelos registrados no painel admin
│   ├── migrations/             # Migrações do banco de dados
│   └── templates/
│       ├── mentorados.html     # Dashboard do mentor
│       ├── reunioes.html       # Gestão de reuniões (mentor)
│       ├── tarefa.html         # Tarefas e uploads (visão mentor)
│       ├── tarefa_mentorado.html # Tarefas e vídeos (visão mentorado)
│       ├── auth_mentorado.html # Login via token (mentorado)
│       ├── escolher_dia.html   # Escolha de data para reunião (mentorado)
│       └── agendar_reuniao.html # Agendamento de horário (mentorado)
│
├── templates/                  # Templates globais
│   ├── base.html               # Template base (head, scripts globais)
│   └── static/
│       └── logo.png            # Logotipo da aplicação
│
├── media/                      # Arquivos enviados pelos usuários (fotos, vídeos)
├── db.sqlite3                  # Banco de dados SQLite (gerado após migrate)
└── manage.py                   # CLI do Django
```

---

## Instalação e Configuração

### 1. Clone o repositório

```bash
# Clonando diretamente
git clone https://github.com/leomatiazzz/pymentor.git
cd pymentor

# Ou via fork: faça o fork no GitHub, clone o seu fork e adicione o upstream:
git clone https://github.com/SEU_USUARIO/pymentor.git
cd pymentor
git remote add upstream https://github.com/leomatiazzz/pymentor.git
```

### 2. Crie e ative o ambiente virtual

```bash
# Criando o venv
python -m venv venv

# Ativando no Linux/macOS
source venv/bin/activate

# Ativando no Windows (PowerShell)
venv\Scripts\Activate.ps1

# Ativando no Windows (CMD)
venv\Scripts\activate.bat
```

### 3. Instale as dependências

```bash
pip install -r requirements.txt
```

### 4. Configure as variáveis de ambiente (produção)

Para desenvolvimento local, as configurações já estão definidas em `core/settings.py`. Para produção, é **obrigatório** alterar as seguintes configurações (idealmente via variáveis de ambiente ou arquivo `.env`):

```python
# core/settings.py
SECRET_KEY = 'sua-chave-secreta-gerada-aqui'  # Nunca use a chave padrão em produção!
DEBUG = False
ALLOWED_HOSTS = ['seu-dominio.com']
```

### 5. Execute as migrações

```bash
python manage.py migrate
```

### 6. (Opcional) Crie um superusuário

```bash
python manage.py createsuperuser
```

---

## Executando o Projeto

### Servidor de desenvolvimento

```bash
python manage.py runserver
```

Acesse em: **http://127.0.0.1:8000**

### Coletar arquivos estáticos (produção)

```bash
python manage.py collectstatic
```

---

## Rotas Disponíveis

### Mentor (requer login)
| Rota | Descrição |
|------|-----------|
| `/usuarios/cadastro/` | Cadastro de novo mentor |
| `/usuarios/login/` | Login do mentor |
| `/mentorados/` | Dashboard — lista e cadastro de mentorados |
| `/mentorados/reunioes/` | Gestão de reuniões |
| `/mentorados/tarefa/<id>` | Tarefas e uploads de um mentorado específico |
| `/admin/` | Painel administrativo do Django |

### Mentorado (acesso por token, sem login Django)
| Rota | Descrição |
|------|-----------|
| `/mentorados/auth/` | Autenticação via token único |
| `/mentorados/escolher_dia/` | Escolha do dia disponível para reunião |
| `/mentorados/agendar_reuniao/` | Agendamento de horário específico |
| `/mentorados/tarefa_mentorado/` | Visualização de tarefas e vídeos |
| `/mentorados/tarefa_alterar/<id>` | Alternar status de tarefa (HTMX) |

---

## Fluxo do Mentor

```
1. Acessa /usuarios/cadastro/ → cria sua conta
2. Faz login em /usuarios/login/
3. No dashboard /mentorados/:
   - Cadastra mentorados (nome, foto, estágio, navigator)
   - Visualiza gráfico de pizza com distribuição por estágio
4. Em /mentorados/reunioes/:
   - Abre horários disponíveis para reunião
   - Visualiza reuniões agendadas pelos mentorados
5. Em /mentorados/tarefa/<id>:
   - Cria tarefas para o mentorado
   - Faz upload de vídeos de referência
6. Compartilha o token do mentorado para que ele acesse o portal
```

> **Como obter o token do mentorado:** O token é gerado automaticamente no cadastro. Acesse o painel admin em `/admin/mentorados/mentorados/` para visualizá-lo.

---

## Fluxo do Mentorado

```
1. Recebe o token único do mentor
2. Acessa /mentorados/auth/ → insere o token
3. Um cookie de sessão (auth_token) é definido por 1 hora
4. Acessa /mentorados/tarefa_mentorado/ → visualiza tarefas e vídeos
5. Marca tarefas como realizadas (checkbox com HTMX)
6. Acessa /mentorados/escolher_dia/ → vê dias disponíveis
7. Acessa /mentorados/agendar_reuniao/?data=DD-MM-YYYY → escolhe horário e tag temática
```

---

## Painel Administrativo

Acesse em: **http://127.0.0.1:8000/admin/**

Modelos disponíveis no admin:
- **Navigators** — gerenciar navigators (co-mentores)
- **Mentorados** — gerenciar mentorados e visualizar tokens
- **DisponibilidadeHorarios** — gerenciar horários de reunião
- **Reuniao** — gerenciar reuniões agendadas

---

## ⚠️ Avisos de Segurança

> [!CAUTION]
> **Nunca suba a `SECRET_KEY` padrão para produção.** O arquivo `core/settings.py` contém uma chave de desenvolvimento hardcoded. Gere uma nova chave com:
> ```bash
> python -c "from django.core.utils.crypto import get_random_string; print(get_random_string(50))"
> ```
> Ou use `python -c "import secrets; print(secrets.token_urlsafe(50))"`.

> [!WARNING]
> **`DEBUG = True` e `ALLOWED_HOSTS = []` são configurações de desenvolvimento.** Antes de qualquer deploy em produção, defina `DEBUG = False` e liste os hosts permitidos em `ALLOWED_HOSTS`.

> [!WARNING]
> **O banco de dados `db.sqlite3` está incluído no repositório.** Para produção, considere usar PostgreSQL ou outro banco robusto.

---

## Testes

O projeto possui arquivos `tests.py` em ambos os apps (`usuarios/` e `mentorados/`), porém **ainda não há testes implementados**. Para executar o runner de testes do Django:

```bash
python manage.py test
```

Contribuições com cobertura de testes são bem-vindas! Veja a seção [Como Contribuir](#como-contribuir).

---

## Como Contribuir

Contribuições são bem-vindas! Consulte o [CONTRIBUTING.md](CONTRIBUTING.md) para o guia completo.

Resumo rápido:

1. **Fork** e clone o repositório
2. **Crie uma branch:** `git checkout -b feature/nome-da-feature`
3. **Commit** com mensagem descritiva: `git commit -m "feat: descrição"`
4. **Push** e abra um **Pull Request**

---

## Licença

Distribuído sob a licença **MIT**. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## Pendências e Informações a Confirmar

Itens ainda em aberto que requerem atenção futura:

| Item | Situação | Ação Sugerida |
|------|----------|---------------|
| **Locale `pt_BR.utf8` no Windows** | ⚠️ Pode causar erro na view de agendamento | Testar e implementar fallback para Windows |
| **Token do mentorado visível ao mentor** | ⚠️ Só acessível via painel admin | Considerar exibir token na tela de tarefas do mentor |
| **Chart.js sem versão fixada** | ⚠️ Usa `latest` via CDN | Fixar versão (ex: `chart.js@4.4.0`) para evitar quebras |

---

## ✨ Sobre

Projeto desenvolvido na **Pystack Week 13 – Pythonando**, com foco no uso de **Django** para construção de aplicações web completas com dois perfis de usuário distintos (mentor e mentorado).
