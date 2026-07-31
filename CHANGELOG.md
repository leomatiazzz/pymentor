# Changelog — PyMentor

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/),
e este projeto adere ao [Semantic Versioning](https://semver.org/lang/pt-BR/).

---

## [1.0.0] — 2026-07

### Adicionado
- Cadastro e autenticação de mentores (username + senha)
- Cadastro de mentorados com nome, foto, estágio de receita e navigator
- Categorização de mentorados por estágio (E1 a E5: R$3k até R$10M+)
- Visualização de mentorados em tabela com gráfico de pizza (Chart.js)
- Cadastro de navigators (co-mentores/assistentes)
- Criação de tarefas por mentor para cada mentorado
- Upload de vídeos de referência vinculados ao mentorado
- Abertura de horários disponíveis para reuniões (blocos de 50 minutos)
- Agendamento de reuniões pelo mentorado com tag temática e descrição
- Portal de acesso para mentorados via **token único** (sem login Django)
- Cookie de autenticação com expiração de 1 hora para mentorados
- Marcação de tarefas como realizadas via **HTMX** (sem reload de página)
- Painel administrativo Django com Navigators, Mentorados, Horários e Reuniões
- Suporte a localização em português do Brasil (timezone `America/Sao_Paulo`)

### Projeto base
- Desenvolvido durante a **Pystack Week 13 — Pythonando**
- Stack: Django 5.2, Python 3.12+, SQLite, Pillow, HTMX 2.0.4, Chart.js, Tailwind CSS

---

<!-- 
Para versões futuras, use o formato:

## [Unreleased]

## [x.y.z] — AAAA-MM-DD

### Adicionado
### Alterado
### Corrigido
### Removido
### Depreciado
### Segurança
-->
