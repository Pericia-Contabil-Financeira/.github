# Guia de Instalação – Perícia Contábil-Financeira

Este guia descreve os passos necessários para configurar o ambiente de desenvolvimento utilizado pela organização **Perícia Contábil-Financeira**.

A infraestrutura foi projetada para fornecer um ambiente reproduzível e padronizado para desenvolvimento de automações, análise de dados e exploração documental utilizando R, Python, DuckDB, Quarto e Inteligência Artificial.

---

# 1. Criar Conta no GitHub

Caso ainda não possua uma conta:

https://github.com

Após criar a conta, informe seu usuário GitHub ao administrador da organização para receber o convite de acesso.

---

# 2. Instalar Git

Download:

https://git-scm.com/download/win

## Opções recomendadas durante a instalação

### Editor padrão

Selecionar:

```text
Use Notepad as Git's default editor
```

### Nome padrão da branch principal

Selecionar:

```text
Override the default branch name for new repositories
```

Informar:

```text
main
```

### PATH

Selecionar:

```text
Git from the command line and also from 3rd-party software
```

### SSH

Selecionar:

```text
Use bundled OpenSSH
```

### HTTPS

Selecionar:

```text
Use the OpenSSL library
```

### Line Endings

Selecionar a opção padrão:

```text
Checkout Windows-style, commit Unix-style line endings
```

Após a instalação, abrir o PowerShell e verificar:

```powershell
git --version
```

Exemplo:

```text
git version 2.54.0.windows.1
```

---

# 3. Instalar Docker Desktop

Download:

https://www.docker.com/products/docker-desktop/

## Opções recomendadas

Utilizar:

```text
WSL2
```

e

```text
Linux Containers
```

Após a instalação:

* Reiniciar o computador;
* Abrir o Docker Desktop;
* Aguardar o Docker iniciar completamente.

Verificar:

```powershell
docker --version
```

Exemplo:

```text
Docker version 28.x.x
```

---

# 4. Instalar Positron

Download:

https://positron.posit.co/

Instalar normalmente.

Na primeira execução, recomenda-se instalar a extensão:

```text
Dev Containers
```

---

# 5. Configurar Git

Executar:

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "seu_email@dominio"
```

Verificar:

```powershell
git config --global --list
```

---

# 6. Criar Chave SSH

Executar:

```powershell
ssh-keygen -t ed25519 -C "seu_email@dominio"
```

Pressionar ENTER para aceitar os valores padrão.

Visualizar a chave pública:

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

Copiar o conteúdo exibido.

---

# 7. Configurar SSH no GitHub

No GitHub:

```text
Settings
→ SSH and GPG Keys
→ New SSH Key
```

Colar a chave pública.

Testar:

```powershell
ssh -T git@github.com
```

Resultado esperado:

```text
Hi usuario-github!
You've successfully authenticated, but GitHub does not provide shell access.
```

---

# 8. Clonar um Repositório

Exemplo:

```powershell
cd "C:\Projetos"

git clone git@github.com:Pericia-Contabil-Financeira/patrimonial-financeiro.git
```

---

# 9. Abrir o Projeto no Positron

Abrir o Positron.

Selecionar:

```text
File
→ Open Folder
```

Selecionar a pasta do projeto.

---

# 10. Criar o Dev Container

Ao abrir o projeto, o Positron identificará automaticamente:

```text
.devcontainer
Dockerfile
```

Selecionar:

```text
Reopen in Container
```

ou

```text
Open Folder in Container
```

Na primeira execução poderão ser baixadas imagens Docker e instaladas dependências.

Esse processo pode levar vários minutos.

Nas execuções seguintes o tempo normalmente é muito menor.

---

# 11. Testar o Ambiente

Abrir o terminal do Positron.

Executar:

```bash
R
```

Depois:

```r
library(data.table)
library(duckdb)

print("Ambiente OK")
```

Resultado esperado:

```text
[1] "Ambiente OK"
```

---

# 12. Atualizar Repositórios

Para atualizar um repositório:

```powershell
git pull
```

Para enviar alterações:

```powershell
git add .
git commit -m "Descrição da alteração"
git push
```

---

# Estrutura dos Repositórios

Os repositórios compartilham uma estrutura semelhante:

```text
Projeto/
├── R/
├── Documentos/
├── Dados/
├── Saidas/
├── .devcontainer/
├── Dockerfile
├── README.md
└── *.Rproj
```

---

# Importante

Não enviar ao GitHub:

* PDFs;
* Planilhas;
* Quebras de sigilo;
* Bases SIMBA;
* Declarações fiscais;
* Bancos DuckDB;
* Dados pessoais;
* Relatórios periciais;
* Arquivos de procedimentos;
* Qualquer documento sensível.

O GitHub deve ser utilizado apenas para compartilhamento de:

* Scripts;
* Modelos;
* Automações;
* Documentação técnica;
* Boas práticas;
* Estruturas reutilizáveis.

---

# Tecnologias Utilizadas

* GitHub
* Git
* Docker Desktop
* Positron
* R
* Python
* DuckDB
* Quarto
* Inteligência Artificial

---

# Suporte

Em caso de dúvidas, entre em contato com os administradores da organização.

Bem-vindo à comunidade Perícia Contábil-Financeira.
