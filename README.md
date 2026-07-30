
# 🧑‍🏫 PyMentor - Plataforma de Mentoria

Este projeto foi desenvolvido durante a **13ª edição da Pystack Week**, promovida pela plataforma **Pythonando**.

A aplicação tem como objetivo permitir que **mentores administrem seus mentorados (e navigators)**, acompanhando o progresso, criando tarefas e agendando reuniões com uma interface simples e funcional.

---

## 🛠️ Tecnologias Utilizadas

- **Python 3**
- **Django**
- **HTML + CSS + HTMX**

---

## 🚀 Como rodar o projeto

Você pode clonar ou forkar o projeto para executar localmente:

### 🔁 Fork no GitHub

1. Acesse o repositório no GitHub e clique em **"Fork"**
2. Após isso, clone o seu fork com:
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
```

### 📥 Clonando diretamente

```bash
git clone https://github.com/usuario-original/repositorio-original.git
```

### ▶️ Executando localmente

```bash
cd nome-do-projeto
python -m venv venv
source venv/bin/activate  # (Windows: venv\Scripts\activate)
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

Acesse no navegador:  
🔗 **http://127.0.0.1:8000**

---

## 👥 Acesso ao sistema

- A tela inicial de login está em:  
  🔑 **http://127.0.0.1:8000/usuarios/login/**

- Se ainda não tiver conta, o mentor pode se cadastrar em:
  📝 **http://127.0.0.1:8000/usuarios/cadastro/**

- Ambas as páginas estarão indexadas, de qualquer maneira.  

- Também é possível criar um **superusuário do Django** com o comando:

```bash
python manage.py createsuperuser
```

E acessar o painel administrativo por:  
🛠️ **http://127.0.0.1:8000/admin/**

---

## ✨ Sobre

Projeto desenvolvido na **Pystack Week 13 – Pythonando**, com foco no uso de Django para construção de aplicações web completas.
