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

Após a instalação, abrir o PowerShell e verificar:

```powershell
git --version
```

Exemplo de retorno:

```text
git version 2.54.0.windows.1
```

---

# 3. Instalar Docker Desktop

Download:

https://www.docker.com/products/docker-desktop/

Após a instalação:

* Reiniciar o computador;
* Abrir o Docker Desktop;
* Aguardar o Docker iniciar.

Verificar:

```powershell
docker --version
```

---

# 4. Instalar Positron

Download:

https://positron.posit.co/

Instalar normalmente.

---

# 5. Configurar Git

Executar:

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "seu_email@dominio"
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

---

# 7. Configurar SSH no GitHub

No GitHub:

Settings → SSH and GPG Keys → New SSH Key

Colar o conteúdo da chave pública.

Testar:

```powershell
ssh -T git@github.com
```

Resultado esperado:

```text
Hi usuario-github!
You've successfully authenticated.
```

---

# 8. Clonar o Repositório

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
File → Open Folder
```

Escolher a pasta do projeto.

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

Na primeira execução o processo pode levar alguns minutos.

---

# 11. Testar o Ambiente

No terminal do Positron:

```bash
R
```

Executar:

```r
library(data.table)
library(duckdb)

print("Ambiente OK")
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
* Bancos DuckDB;
* Dados pessoais;
* Relatórios periciais;
* Arquivos de procedimentos.

O GitHub deve ser utilizado apenas para compartilhamento de:

* Scripts;
* Modelos;
* Automações;
* Documentação técnica;
* Boas práticas.

---

# Suporte

Em caso de dúvidas, entre em contato com os administradores da organização.
