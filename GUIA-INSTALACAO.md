# Guia de Instalação – Perícia Contábil-Financeira

Este guia descreve os passos necessários para configurar o ambiente de desenvolvimento utilizado pela organização **Perícia Contábil-Financeira**.

A infraestrutura foi projetada para fornecer um ambiente reproduzível e padronizado para desenvolvimento de automações, análise de dados, exploração documental e Inteligência Artificial utilizando R, Python, DuckDB, Quarto e Docker.

---

# 1. Verificar o Computador

Antes de iniciar a instalação, verifique:

## Tipo de sistema

Verifique se o computador utiliza:

```text
x64 (AMD64)
```

ou

```text
ARM64
```

## Versão do Windows

Verifique se o sistema operacional é:

```text
Windows 10
```

ou

```text
Windows 11
```

Essas informações podem ser obtidas em:

```text
Configurações
→ Sistema
→ Sobre
```

---

# 2. Criar Conta no GitHub

Caso ainda não possua uma conta:

https://github.com

Após criar a conta, informe seu usuário GitHub ao administrador da organização para receber o convite de acesso.

---

# 3. Instalar Git

Download:

https://git-scm.com/download/win

## Opções recomendadas durante a instalação

### Componentes

Selecionar:

```text
☑ Open Git Bash here
☐ Open Git GUI here
☑ Git LFS
☑ Associate .git*
☑ Associate .sh
☐ Check daily for updates
☑ Add Git Bash Profile to Windows Terminal
☐ Scalar
```

### Editor padrão

Selecionar:

```text
Use Notepad as Git's default editor
```

### Branch principal

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
Use the native Windows Secure Channel library
```

### Line Endings

Selecionar:

```text
Checkout Windows-style, commit Unix-style line endings
```

### Terminal

Selecionar:

```text
Use Windows' default console window
```

### Git Pull

Selecionar:

```text
Fast-forward or merge
```

### Credential Helper

Selecionar:

```text
Git Credential Manager
```

### Opções Extras

Selecionar:

```text
☑ Enable file system caching
☐ Enable symbolic links
```

## Verificar instalação

Executar:

```powershell
git --version
```

---

# 4. Instalar Docker Desktop

Download:

https://www.docker.com/products/docker-desktop/

## Opções recomendadas

Selecionar:

```text
◉ All-users installation
```

e

```text
☑ Use WSL 2 instead of Hyper-V
☐ Allow Windows Containers
```

Também selecionar:

```text
☑ Add shortcut to desktop
```

## Após a instalação

Abrir o Docker Desktop.

Aguardar até aparecer:

```text
Docker is running
```

Verificar:

```powershell
docker info
```

Resultado esperado:

```text
Server:
...
```

Opcionalmente testar:

```powershell
docker run hello-world
```

---

# 5. Instalar Positron

Download:

https://positron.posit.co/

## Opções recomendadas

Selecionar:

```text
☐ Criar um atalho na área de trabalho

☑ Adicione a ação "Abrir com Positron" ao menu de contexto de arquivo
☑ Adicione a ação "Abrir com Positron" ao menu de contexto de diretório
☑ Registre Positron como um editor para tipos de arquivos suportados
☑ Adicione em PATH
```

Concluir a instalação.

---

# 6. Habilitar Dev Containers no Positron

Abrir o Positron.

Acessar:

```text
Manage
→ Settings
```

Pesquisar:

```text
dev container
```

Habilitar:

```text
Dev > Containers: Enable (Experimental)
```

Selecionar:

```text
☑ Dev > Containers: Enable (Experimental)
```

Fechar e reabrir o Positron.

---

# 7. Configurar Git

Executar:

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "seu_email@dominio"
```

Exemplo:

```powershell
git config --global user.name "Claudio Riella"
git config --global user.email "cgriella@gmail.com"
```

Observações:

- O nome pode ser qualquer texto que identifique o autor dos commits.
- Recomenda-se utilizar um e-mail cadastrado no GitHub.

Verificar:

```powershell
git config --global --list
```

---

# 8. Clonar um Repositório

Criar uma pasta para armazenar os repositórios.

Exemplo:

```powershell
mkdir "C:\ProjetosGit"
cd "C:\ProjetosGit"
```

Clonar o repositório:

```powershell
git clone https://github.com/Pericia-Contabil-Financeira/patrimonial-financeiro.git
```

Na primeira execução será solicitada autenticação.

O Git Credential Manager abrirá automaticamente o navegador para autenticação no GitHub.

Após a autenticação:

```text
git clone
git pull
git push
```

normalmente funcionarão sem solicitar senha novamente.

---

# 9. Construir a Imagem Docker

Entrar no diretório do projeto:

```powershell
cd patrimonial-financeiro
```

Construir a imagem:

```powershell
docker build -t patrimonial-financeiro .
```

Esse processo pode levar vários minutos na primeira execução.

---

# 10. Abrir o Projeto no Positron

Localize o diretório do projeto.

Exemplo:

```text
C:\ProjetosGit\patrimonial-financeiro
```

Clique com o botão direito sobre a pasta:

```text
Abrir com Positron
```

ou

```text
Open with Positron
```

Alternativamente:

```text
File
→ Open Folder
```

---

# 11. Ajustar Política do PowerShell (Se Necessário)

Caso o Positron apresente erro semelhante a:

```text
UnauthorizedAccess
A execução de scripts foi desabilitada neste sistema
```

Verificar:

```powershell
Get-ExecutionPolicy
```

Se retornar:

```text
Restricted
```

executar:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Confirmar:

```text
A
```

(Yes to All)

Verificar novamente:

```powershell
Get-ExecutionPolicy
```

Resultado esperado:

```text
RemoteSigned
```

---

# 12. Criar o Dev Container

Ao abrir o projeto, o Positron identificará automaticamente:

```text
.devcontainer
Dockerfile
```

e iniciará a construção do ambiente.

Durante esse processo poderão ser criadas:

```text
Imagem Docker do Projeto
Imagem Dev Container
Container Docker
```

A primeira execução pode levar vários minutos.

---

# 13. Configurar Git Dentro do Container

Após o Dev Container iniciar, abrir o terminal do Positron.

Configurar:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu_email@dominio"
```

Exemplo:

```bash
git config --global user.name "Claudio Riella"
git config --global user.email "cgriella@gmail.com"
```

Verificar:

```bash
git config --global --list
```

---

# 14. Testar o Ambiente

No console R:

```r
sessionInfo()
```

Verificar:

```text
R version 4.x
```

Verificar diretório:

```r
getwd()
```

Resultado esperado:

```text
/workspaces/nome-do-projeto
```

Testar pacotes:

```r
library(data.table)
library(duckdb)
library(arrow)

print("Ambiente R OK")
```

---

# 15. Atualizar e Enviar Alterações

Atualizar o repositório:

```bash
git pull
```

Adicionar alterações:

```bash
git add .
```

Criar commit:

```bash
git commit -m "Descrição da alteração"
```

Enviar alterações:

```bash
git push
```

Também é possível utilizar a interface gráfica do Positron:

```text
Source Control
→ Commit
→ Push
```

---

# Estrutura dos Repositórios

```text
Projeto/
├── R/
├── Python/
├── Documentos/
├── Dados/
├── Saidas/
├── Relatorios/
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

O GitHub NÃO realiza upload dessa pasta.

---

## Dados/

Contém os dados estruturados produzidos a partir dos documentos.

Exemplos:

- Bancos DuckDB;
- Arquivos Parquet;
- Arquivos CSV;
- Dados intermediários.

Objetivo:

Transformar documentos em dados passíveis de consulta, análise, cruzamento e eventual uso em RAG.

O GitHub NÃO realiza upload dessa pasta.

---

## Saidas/

Contém os resultados gerados pelos scripts.

Exemplos:

- Relatórios Word;
- Relatórios PDF;
- Relatórios HTML;
- Relatórios Quarto;
- Planilhas Excel;
- Gráficos;
- Dashboards.

O GitHub NÃO realiza upload dessa pasta.

---

## .devcontainer/

Configura o ambiente Docker utilizado pelo Positron.

Permite que diferentes usuários utilizem exatamente o mesmo ambiente de trabalho.

---

## Dockerfile

Define os componentes instalados automaticamente no ambiente.

Exemplos:

- R;
- Python;
- DuckDB;
- Quarto;
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

Arquivo de projeto utilizado pelo Positron.

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
- Dev Containers
- R
- Python
- DuckDB
- Quarto
- Inteligência Artificial

---

# Suporte

Em caso de dúvidas, entre em contato com os administradores da organização.

Bem-vindo à comunidade Perícia Contábil-Financeira.
