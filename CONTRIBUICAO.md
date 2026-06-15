# Como Contribuir

Obrigado pelo interesse em contribuir com a organização Perícia Contábil-Financeira.

O objetivo desta organização é compartilhar conhecimento, automações, scripts, modelos e boas práticas aplicadas à atividade pericial da Área 1.

## Formas de Contribuição

São bem-vindas contribuições relacionadas a:

- Scripts em R;
- Scripts em Python;
- Consultas SQL;
- Modelos de relatórios;
- Automações;
- Ferramentas de análise documental;
- Ferramentas de análise financeira;
- Dashboards;
- Documentação técnica;
- Tutoriais;
- Boas práticas.

## Regras Gerais

### Compartilhe apenas código e conhecimento

Não devem ser enviados para os repositórios:

- PDFs;
- Planilhas contendo dados reais;
- Bases SIMBA;
- Declarações fiscais;
- Quebras de sigilo;
- Relatórios periciais;
- Dados pessoais;
- Qualquer documento sensível.

### Prefira exemplos fictícios

Sempre que possível utilize:

- Dados simulados;
- Dados anonimizados;
- Casos de teste.

### Documente seu código

Procure incluir:

- Objetivo do script;
- Dependências necessárias;
- Exemplo de uso;
- Comentários relevantes.

## Princípios Arquiteturais

As contribuições devem respeitar os três princípios que orientam a infraestrutura da organização: **reprodutibilidade**, **portabilidade** e **escalabilidade operacional** (descritos em GOVERNANCA.md). Na prática, isso significa escrever código que rode da mesma forma em diferentes máquinas e sistemas operacionais.

### Escreva código portátil

Para que o mesmo projeto rode em Windows, Linux ou servidor sem ajustes:

- Use **caminhos relativos** (`Dados/`, `Documentos/`, `Saidas/`) em vez de caminhos absolutos do Windows (`C:/Users/...`);
- Evite separadores de caminho fixos; prefira funções como `file.path()` (R) ou `os.path.join` / `pathlib` (Python);
- Não dependa de programas instalados apenas no host; declare as dependências no Dockerfile/ambiente;
- Atenção a codificação (prefira UTF-8) e a diferenças de fim de linha entre sistemas.

### Prefira formatos de dados neutros

Para preservar portabilidade e reprodutibilidade, prefira formatos abertos e multiplataforma:

- DuckDB;
- Parquet;
- CSV;
- XLSX (quando necessário).

## Organização dos Repositórios

Cada repositório representa uma área temática.

Exemplos:

- patrimonial-financeiro
- licitacoes
- mercado-capitais
- rpps
- exame-contabil

Antes de criar novos diretórios ou estruturas, procure seguir o padrão já existente.

## Boas Práticas

- Utilize Git para versionamento;
- Faça alterações pequenas e frequentes;
- Mantenha os scripts reproduzíveis;
- Escreva código portátil (caminhos relativos, formatos neutros);
- Evite dependências desnecessárias;
- Priorize simplicidade e clareza.

## Dúvidas e Sugestões

Sugestões de melhoria são sempre bem-vindas.

O objetivo é construir uma base colaborativa de conhecimento para apoiar a atividade pericial.
