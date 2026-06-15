# Perguntas Frequentes (FAQ)

## O que é esta organização?

A organização Perícia Contábil-Financeira é um espaço colaborativo para compartilhamento de scripts, automações, modelos e boas práticas aplicadas à atividade pericial da Área 1.

---

## Quem pode participar?

Peritos e colaboradores interessados em automação, análise de dados, IA e desenvolvimento de ferramentas aplicadas à perícia contábil-financeira.

---

## Preciso saber programar?

Não.

Existem diversas formas de contribuir:

- Testando ferramentas;
- Relatando problemas;
- Compartilhando ideias;
- Documentando procedimentos;
- Desenvolvendo scripts.

---

## Quais linguagens são utilizadas?

Principalmente:

- R
- Python
- SQL

---

## Por que utilizar Docker?

O Docker permite criar ambientes reproduzíveis.

Dessa forma diferentes usuários conseguem executar os mesmos scripts utilizando exatamente as mesmas versões de bibliotecas e ferramentas.

Além da reprodutibilidade, o Docker oferece **portabilidade** (mover o projeto entre Windows, Linux, servidor ou nuvem sem reengenharia) e **escalabilidade operacional** (adaptar o ambiente de execução ao porte do caso pericial). Esses três conceitos são os princípios arquiteturais da organização. Consulte o arquivo GOVERNANCA.md.

---

## O que é o Rocker?

Rocker é um conjunto de imagens Docker baseadas em Linux já preparadas com R, pacotes e ferramentas científicas (por exemplo, `rocker/verse`, que inclui R, Quarto e o tidyverse).

O Rocker **não é um sistema operacional** e não pode receber boot diretamente. Ele é executado por cima do Docker, que por sua vez precisa de um sistema operacional hospedeiro (Windows ou Linux).

Uma analogia útil: Linux é o prédio, Docker é o condomínio e Rocker é o apartamento.

---

## Quantas camadas existem entre o hardware e o meu código?

Depende do sistema operacional hospedeiro.

No **Windows**, o Docker Desktop usa uma camada Linux (WSL2) para executar containers Linux:

```text
Windows → WSL2 (Linux) → Docker Engine → Container Rocker → Projeto
```

No **Linux nativo**, o Docker Engine usa diretamente o kernel Linux do host, eliminando o WSL2 e o Docker Desktop:

```text
Linux → Docker Engine → Container Rocker → Projeto
```

Em outras palavras, no Windows há três ambientes envolvidos (Windows, WSL2 e o container); no Linux nativo há apenas dois (Linux host e o container). O custo da camada do container Rocker é pequeno, porque ela compartilha o kernel do host.

---

## Preciso do Docker Desktop no Linux?

Não. No Windows o Docker Desktop é praticamente obrigatório, porque o Windows não executa containers Linux diretamente. No Linux basta instalar o Docker Engine (`docker` + `docker compose`), sem Docker Desktop e sem WSL2.

---

## Vale a pena usar Linux (dual boot) para casos grandes?

Pode valer como estratégia de escalabilidade operacional. Em casos periciais de grande porte, o ambiente Windows pode começar a "engasgar" pela concorrência de recursos (Docker Desktop, WSL2, antivírus, OneDrive, Teams, navegador, sistemas corporativos).

Iniciar a mesma máquina em Linux nativo (dual boot) tende a melhorar uso de memória, estabilidade, responsividade e desempenho de I/O — especialmente no processamento de muitos PDFs, OCR e tabelas grandes em DuckDB. Não se espera um ganho dramático de CPU.

Como o ambiente está encapsulado no container Rocker, a troca de Windows para Linux usa o mesmo repositório Git e praticamente o mesmo Dockerfile, sem reengenharia.

---

## O Cisco AnyConnect funciona no Linux?

Sim. O Cisco AnyConnect (atual Cisco Secure Client) possui versões para Linux (Ubuntu e Red Hat/RHEL). Ao avaliar a migração para Linux, o maior risco costuma não ser o Positron ou o Docker, mas a infraestrutura corporativa: VPN, certificados e sistemas internos. Recomenda-se testar esses itens (por exemplo, com um pendrive Ubuntu em modo Live) antes de adotar dual boot.

---

## Por que utilizar GitHub?

O GitHub permite:

- Versionamento;
- Compartilhamento;
- Colaboração;
- Documentação;
- Controle de alterações.

---

## O que é Positron?

Positron é uma IDE moderna desenvolvida pela Posit para ciência de dados, integrando:

- R;
- Python;
- SQL;
- Inteligência Artificial.

---

## Posso enviar dados reais de procedimentos?

Não.

Não devem ser enviados:

- PDFs;
- Planilhas;
- Bases SIMBA;
- Declarações fiscais;
- Relatórios periciais;
- Dados pessoais;
- Qualquer documento sensível.

Os repositórios devem conter apenas código, documentação e modelos reutilizáveis.

---

## Como obter acesso?

Envie seu usuário GitHub para um dos administradores da organização.

Após o convite ser aceito, os repositórios serão disponibilizados conforme as permissões concedidas.

---

## Preciso instalar algo?

Sim.

O ambiente utiliza:

- Git
- Docker Desktop
- Positron

Consulte o arquivo GUIA-INSTALACAO.md.

---

## Existe suporte para Inteligência Artificial?

Sim.

A infraestrutura foi concebida para permitir integração com ferramentas de IA, incluindo modelos locais e serviços externos, sempre observando os requisitos de segurança e sigilo aplicáveis.

---

## Qual o objetivo de longo prazo?

Construir uma base colaborativa de conhecimento e ferramentas que reduza retrabalho, facilite análises e acelere o desenvolvimento de soluções aplicadas à perícia contábil-financeira.
