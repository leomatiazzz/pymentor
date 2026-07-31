# Guia de Contribuição — PyMentor

Obrigado por querer contribuir com o PyMentor! 🎉  
Este documento explica como configurar o ambiente de desenvolvimento e o fluxo para enviar contribuições.

---

## Índice

- [Código de Conduta](#código-de-conduta)
- [Como Reportar Bugs](#como-reportar-bugs)
- [Como Sugerir Melhorias](#como-sugerir-melhorias)
- [Ambiente de Desenvolvimento](#ambiente-de-desenvolvimento)
- [Fluxo de Contribuição](#fluxo-de-contribuição)
- [Padrões de Código](#padrões-de-código)
- [Testes](#testes)

---

## Código de Conduta

Ao participar deste projeto, você concorda em manter um ambiente respeitoso e inclusivo. Comportamentos agressivos, discriminatórios ou desrespeitosos não serão tolerados.

---

## Como Reportar Bugs

1. Verifique se o bug já foi reportado nas [Issues](https://github.com/leomatiazzz/pymentor/issues).
2. Se não encontrou, abra uma **nova Issue** com:
   - Título claro e descritivo
   - Passos para reproduzir o problema
   - Comportamento esperado vs. comportamento atual
   - Versão do Python e do Django (`python --version`, `python -m django --version`)
   - Sistema operacional
   - Screenshots ou tracebacks, se aplicável

---

## Como Sugerir Melhorias

1. Abra uma **Issue** com o label `enhancement`.
2. Descreva a funcionalidade desejada e o caso de uso.
3. Aguarde feedback antes de começar a implementar, para evitar trabalho duplicado.

---

## Ambiente de Desenvolvimento

### 1. Fork e clone

```bash
# Faça o fork pelo GitHub e depois clone:
git clone https://github.com/SEU_USUARIO/pymentor.git
cd pymentor
```

### 2. Crie o ambiente virtual e instale dependências

```bash
python -m venv venv

# Linux/macOS
source venv/bin/activate

# Windows (PowerShell)
venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

### 3. Configure o banco e rode o servidor

```bash
python manage.py migrate
python manage.py createsuperuser  # opcional
python manage.py runserver
```

---

## Fluxo de Contribuição

```
main (branch protegida)
 └── feature/nome-da-feature   ← abra um PR para main
 └── fix/descricao-do-bug      ← abra um PR para main
```

### Passo a passo

1. Atualize sua branch `main` local:
   ```bash
   git checkout main
   git pull upstream main
   ```

2. Crie sua branch de trabalho:
   ```bash
   git checkout -b feature/nome-da-feature
   # ou
   git checkout -b fix/descricao-do-bug
   ```

3. Faça commits atômicos e descritivos:
   ```bash
   git commit -m "feat: adiciona validação de token expirado"
   git commit -m "fix: corrige duplicação de DisponibilidadeHorarios"
   git commit -m "docs: atualiza instruções de instalação"
   ```

   **Prefixos recomendados** (baseados em Conventional Commits):
   | Prefixo | Uso |
   |---------|-----|
   | `feat:` | Nova funcionalidade |
   | `fix:` | Correção de bug |
   | `docs:` | Documentação |
   | `refactor:` | Refatoração sem mudança de comportamento |
   | `test:` | Adição ou correção de testes |
   | `chore:` | Tarefas de manutenção (deps, CI, etc.) |

4. Envie sua branch:
   ```bash
   git push origin feature/nome-da-feature
   ```

5. Abra um **Pull Request** no GitHub descrevendo:
   - O que foi alterado e por quê
   - Como testar as mudanças
   - Issue relacionada (se houver): `Closes #42`

---

## Padrões de Código

- **Python:** siga o [PEP 8](https://peps.python.org/pep-0008/)
- **Django:** siga as [boas práticas do Django](https://docs.djangoproject.com/en/5.2/misc/design-philosophies/)
- **Templates:** use indentação de 2 espaços no HTML
- **Commits:** mensagens em português ou inglês, seja consistente

---

## Testes

O projeto ainda não possui testes implementados. Contribuições que adicionem cobertura de testes são especialmente bem-vindas!

Para rodar a suíte de testes:

```bash
python manage.py test
```

---

Dúvidas? Abra uma [Issue](https://github.com/leomatiazzz/pymentor/issues) ou entre em contato! 💬
