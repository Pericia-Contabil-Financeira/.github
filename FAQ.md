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

## Princípios Arquiteturais

### Quais são os princípios arquiteturais da organização?

A organização adota três princípios arquiteturais fundamentais:

1. Reprodutibilidade
2. Portabilidade
3. Escalabilidade Operacional

Esses princípios orientam as decisões relacionadas a Docker, Rocker, Git, DuckDB, Quarto, Positron e demais ferramentas utilizadas nos projetos.

---

# Reprodutibilidade

### O que significa reprodutibilidade em ciência de dados?

Reprodutibilidade é a capacidade de executar novamente uma análise e obter os mesmos resultados utilizando os mesmos dados, código e ambiente computacional.

Ela é um dos pilares da ciência de dados moderna, permitindo verificar resultados, corrigir erros e compartilhar conhecimento de forma confiável.

---

### O que significa reprodutibilidade em perícia?

Na atividade pericial, reprodutibilidade significa que outro perito deve ser capaz de reproduzir os procedimentos técnicos realizados utilizando os mesmos insumos, dados e metodologia.

Isso aumenta a transparência, a auditabilidade e a confiabilidade das conclusões produzidas.

---

### Como Docker, Git, Quarto e DuckDB contribuem para a reprodutibilidade?

**Git**
- Controla versões do código;
- Permite rastrear alterações;
- Preserva histórico e autoria.

**Docker/Rocker**
- Padroniza o ambiente computacional;
- Garante versões consistentes de ferramentas e bibliotecas;
- Evita diferenças entre computadores.

**DuckDB**
- Facilita a distribuição e reprodução de bases analíticas;
- Elimina dependências de servidores de banco de dados.

**Quarto**
- Integra código, texto e resultados em um único documento;
- Permite regenerar relatórios de forma automática.

---

### Quais riscos permanecem?

Mesmo com uma arquitetura reproduzível, ainda existem riscos:

- Dados de entrada incompletos;
- Dados de entrada incorretos;
- OCR com falhas de reconhecimento;
- Dependência de serviços externos;
- Mudanças em APIs;
- Erros de modelagem;
- Erros de interpretação;
- Bugs em bibliotecas;
- Falhas humanas na execução dos procedimentos;
- Uso inadequado de ferramentas de IA.

A reprodutibilidade reduz riscos operacionais, mas não elimina a necessidade de validação técnica.

---

# Portabilidade

### O que significa portabilidade em software?

Portabilidade é a capacidade de executar um sistema em diferentes ambientes sem necessidade de adaptações significativas.

O objetivo é reduzir a dependência de um computador, sistema operacional ou infraestrutura específica.

---

### Qual o papel dos containers?

Os containers encapsulam o ambiente da aplicação.

Em vez de depender das configurações do computador, o projeto passa a depender do ambiente definido pelo container.

Isso permite mover o projeto entre:

- Windows;
- Linux;
- Servidores;
- Máquinas mais potentes;
- Infraestruturas em nuvem.

---

### Como minimizar dependências do sistema operacional?

Algumas boas práticas incluem:

- Utilizar Docker/Rocker;
- Utilizar caminhos relativos;
- Evitar caminhos absolutos específicos do Windows;
- Evitar dependências exclusivas de Windows ou Linux;
- Armazenar configurações no repositório;
- Automatizar instalações e configurações;
- Evitar instalações manuais fora do Docker.

Exemplo de caminho pouco portátil:

```text
C:\Users\Usuario\Documentos\Projeto
```

Exemplo mais portátil:

```text
Dados/
Documentos/
Saidas/
```

---

### Como estruturar diretórios, dados e configurações para maximizar a portabilidade?

Uma estrutura recomendada é:

```text
Projeto/
├── Dados/
├── Documentos/
├── R/
├── Relatorios/
├── Saidas/
├── Dockerfile
├── README.qmd
├── FAQ.md
└── .devcontainer/
```

Essa organização facilita a movimentação do projeto entre diferentes ambientes.

---

# Escalabilidade Operacional

### O que significa escalabilidade operacional?

Escalabilidade operacional é a capacidade de adaptar o ambiente de execução ao porte e à complexidade do caso pericial.

O objetivo é preservar a mesma arquitetura enquanto aumenta a capacidade operacional disponível.

---

### Como ela difere da escalabilidade de software?

A escalabilidade de software normalmente trata de atender:

- Mais usuários;
- Mais requisições;
- Mais acessos simultâneos.

Já a escalabilidade operacional trata de:

- Processar mais documentos;
- Processar bases maiores;
- Executar OCR em larga escala;
- Utilizar hardware mais potente;
- Migrar para ambientes mais adequados.

Tudo isso sem reescrever a solução.

---

### Quais componentes do projeto escalam naturalmente?

Os seguintes componentes tendem a escalar bem:

- Git;
- Docker;
- Rocker;
- DuckDB;
- Quarto;
- Scripts R bem estruturados.

Esses componentes podem ser executados em diferentes máquinas e ambientes mantendo a mesma lógica operacional.

---

### Quais são os gargalos mais prováveis?

Os gargalos mais comuns em projetos periciais costumam ser:

1. Leitura e escrita em disco;
2. OCR;
3. Processamento de PDFs;
4. Memória RAM;
5. CPU;
6. Rede (quando houver serviços remotos).

Na maioria dos casos, o gargalo surge antes no armazenamento e na memória do que no processador.

---

### Como medir quando uma migração de ambiente se torna justificável?

Alguns indicadores importantes:

- Uso constante de memória acima de 80%;
- Uso frequente de swap;
- OCR demorando horas ou dias;
- Lentidão excessiva na leitura de milhares de arquivos;
- DuckDB consumindo praticamente toda a memória disponível;
- Sistema tornando-se pouco responsivo durante o processamento;
- Tempos de execução incompatíveis com a necessidade operacional.

Nesses casos pode ser vantajoso:

- Utilizar Linux em dual boot;
- Utilizar uma máquina mais potente;
- Utilizar um servidor Linux;
- Utilizar infraestrutura em nuvem.

---

### Como esses conceitos se relacionam?

Os três princípios estão conectados:

```text
Reprodutibilidade
        ↓
Portabilidade
        ↓
Escalabilidade Operacional
```

Sem reprodutibilidade não existe portabilidade.

Sem portabilidade a escalabilidade operacional torna-se difícil e custosa.

Assim, a organização busca construir soluções que possam crescer sem depender de uma máquina, sistema operacional ou infraestrutura específica.

Em outras palavras:

```text
Reprodutibilidade
        +
Portabilidade
        =
Base para Escalabilidade Operacional
```

---

### Por que utilizar Docker e Rocker?

O Docker e o Rocker não aumentam diretamente a capacidade de processamento da máquina.

O principal benefício é permitir que o mesmo projeto seja executado em diferentes ambientes preservando o mesmo comportamento.

Por exemplo:

```text
Windows
   ↓
Docker/Rocker
   ↓
Projeto
```

pode ser migrado para:

```text
Linux
   ↓
Docker/Rocker
   ↓
Projeto
```

ou para:

```text
Servidor Linux
   ↓
Docker/Rocker
   ↓
Projeto
```

sem necessidade de reconstruir todo o ambiente.

O Docker e o Rocker funcionam como mecanismos de reprodutibilidade e portabilidade, permitindo que a escalabilidade operacional seja alcançada quando necessário.

---

### Vale a pena utilizar Linux em dual boot?

Pode ser uma estratégia interessante para casos periciais de grande porte.

Em determinadas situações, o Windows pode começar a competir por recursos com:

- Docker Desktop;
- WSL2;
- Antivírus;
- OneDrive;
- Navegador;
- Sistemas corporativos;
- Outros processos em segundo plano.

Nesses casos, iniciar a mesma máquina em Linux pode proporcionar:

- Melhor uso de memória;
- Maior estabilidade;
- Melhor responsividade;
- Melhor desempenho de leitura e escrita de arquivos;
- Menor overhead operacional.

O ganho não costuma ser dramático em CPU, mas pode ser relevante em tarefas como:

- OCR;
- Processamento massivo de PDFs;
- DuckDB;
- Geração de relatórios;
- Indexação documental;
- Manipulação de grandes volumes de arquivos.

Como o ambiente está encapsulado no container Rocker, a migração de Windows para Linux pode ocorrer utilizando o mesmo repositório Git e praticamente o mesmo Dockerfile, sem necessidade de reengenharia.

Essa possibilidade existe porque a arquitetura foi concebida com base em reprodutibilidade e portabilidade, permitindo que o ambiente de execução seja adaptado ao porte do caso pericial.

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
