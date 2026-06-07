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

Verificar no PowerShell:

```powershell
git --version
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

- Reiniciar o computador;
- Abrir o Docker Desktop;
- Aguardar o Docker iniciar completamente.

Verificar:

```powershell
docker --version
```

---

# 4. Instalar Positron

Download:

https://positron.posit.co/

Instalar normalmente.

Na primeira execução recomenda-se instalar a extensão:

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

Escolha uma pasta local para os projetos.

Exemplo:

```powershell
cd "C:\Projetos"
```

Clone o repositório desejado:

```powershell
git clone git@github.com:Pericia-Contabil-Financeira/patrimonial-financeiro.git
```

Outros exemplos:

```powershell
git clone git@github.com:Pericia-Contabil-Financeira/licitacoes.git
git clone git@github.com:Pericia-Contabil-Financeira/exame-contabil.git
git clone git@github.com:Pericia-Contabil-Financeira/mercado-capitais.git
```

---

# 9. Abrir o Projeto no Positron

Após clonar o repositório, localize a pasta do projeto no Windows Explorer.

Exemplo:

```text
C:\Projetos\patrimonial-financeiro
```

Clique com o botão direito sobre a pasta e selecione:

```text
Open with Positron
```

ou

```text
Abrir com Positron
```

Caso essa opção não esteja disponível, abra o Positron e selecione:

```text
File
→ Open Folder
```

Em seguida escolha a pasta do projeto.

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

Nas execuções seguintes o tempo normalmente é menor.

---

# 11. Testar o Ambiente

Abrir o terminal do Positron.

Testar R:

```bash
R
```

Depois:

```r
library(data.table)
library(duckdb)

print("Ambiente R OK")
```

Testar Python:

```bash
python
```

Depois:

```python
import pandas
import pdfplumber

print("Ambiente Python OK")
```

---

# 12. Atualizar e Enviar Alterações

Para atualizar um repositório com as alterações do GitHub:

```powershell
git pull
```

Para enviar alterações locais para o GitHub:

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
├── Python/
├── Documentos/
├── Dados/
├── Saidas/
├── .devcontainer/
├── Dockerfile
├── README.md
└── *.Rproj
```

---

# Organização dos Diretórios

## R/

Contém scripts desenvolvidos em linguagem R.

Exemplos:

- Importação de dados;
- Limpeza de dados;
- Análise financeira;
- Relatórios;
- Dashboards;
- Integração com DuckDB;
- Integração com Inteligência Artificial.

Exemplo:

```text
R/
├── importar_simba.R
├── importar_dirpf.R
├── evolucao_patrimonial.R
└── gerar_relatorio.R
```

---

## Python/

Contém scripts desenvolvidos em linguagem Python.

Exemplos:

- OCR;
- Extração de PDFs;
- Processamento de documentos;
- Integração com APIs;
- Inteligência Artificial;
- Processamento de imagens.

Exemplo:

```text
Python/
├── extrair_pdf.py
├── ocr_documentos.py
└── indexar_documentos.py
```

---

## Documentos/

Contém os documentos originais do caso.

Exemplos:

- PDFs;
- Planilhas;
- Quebras de sigilo;
- Relatórios recebidos;
- Extratos bancários;
- Declarações fiscais.

Esses arquivos permanecem apenas no computador do usuário.

O GitHub **NÃO** realiza upload dessa pasta.

---

## Dados/

Contém os dados estruturados produzidos a partir dos documentos.

Exemplos:

- Bancos DuckDB;
- Arquivos Parquet;
- Arquivos CSV;
- Dados intermediários de processamento;
- Bases extraídas dos documentos.

Objetivo:

Transformar documentos em dados passíveis de consulta, análise, cruzamento e eventual uso em RAG.

O GitHub **NÃO** realiza upload dessa pasta.

---

## Saidas/

Contém os resultados gerados pelos scripts.

Exemplos:

- Relatórios Word;
- Relatórios PDF;
- Relatórios HTML;
- Relatórios em Markdown/Quarto;
- Planilhas Excel;
- Gráficos;
- Dashboards exportados.

O GitHub **NÃO** realiza upload dessa pasta.

---

## .devcontainer/

Configura o ambiente Docker utilizado pelo Positron.

Permite que diferentes usuários utilizem o mesmo ambiente de trabalho.

---

## Dockerfile

Define os componentes instalados automaticamente no ambiente.

Exemplos:

- R;
- Python;
- DuckDB;
- Bibliotecas;
- Ferramentas auxiliares.

---

## README.md

Documento principal do projeto.

Deve conter:

- Objetivo;
- Estrutura;
- Instruções de uso;
- Dependências;
- Exemplos.

---

## *.Rproj

Arquivo de projeto utilizado pelo Positron/R.

Facilita a organização dos scripts, diretórios e configurações do ambiente de trabalho.

---

# Importante

Não enviar ao GitHub:

- PDFs;
- Planilhas;
- Quebras de sigilo;
- Bases SIMBA;
- Declarações fiscais;
- Bancos DuckDB;
- Dados pessoais;
- Relatórios periciais;
- Arquivos de procedimentos;
- Qualquer documento sensível.

O GitHub deve ser utilizado apenas para compartilhamento de:

- Scripts;
- Modelos;
- Automações;
- Documentação técnica;
- Boas práticas;
- Estruturas reutilizáveis.

---

# Tecnologias Utilizadas

- GitHub
- Git
- Docker Desktop
- Positron
- R
- Python
- DuckDB
- Quarto
- Inteligência Artificial

---

# Suporte

Em caso de dúvidas, entre em contato com os administradores da organização.

Bem-vindo à comunidade Perícia Contábil-Financeira.
