# Governança

Este documento reúne as regras de sigilo e os princípios técnicos que orientam a organização Perícia Contábil-Financeira.

## Regras de Sigilo

- Não enviar documentos sigilosos.
- Não enviar dados de investigados.
- Não enviar PDFs de quebras de sigilo.
- Compartilhar apenas scripts, modelos e automações.

## Princípios Arquiteturais

As decisões de infraestrutura da organização são orientadas por três princípios centrais. Eles justificam o uso de Docker/Rocker, Git, DuckDB, Quarto e scripts versionados como base técnica dos projetos.

### Reprodutibilidade

Capacidade de executar o projeto em momentos, máquinas e ambientes diferentes obtendo o mesmo comportamento técnico esperado. O ambiente é descrito e versionado, em vez de depender de instalações manuais específicas de cada computador.

### Portabilidade

Capacidade de mover o projeto entre diferentes ambientes de execução sem reengenharia. O mesmo repositório e o mesmo Dockerfile rodam em Windows (Docker Desktop), em Linux nativo (Docker Engine), em servidor Linux ou em nuvem. O container Rocker funciona como o "computador" da aplicação; o sistema operacional hospedeiro é apenas o anfitrião.

### Escalabilidade Operacional

Capacidade de adaptar o ambiente de execução ao porte e à complexidade do caso pericial sem alterar a arquitetura. Escalar pode significar tanto migrar para hardware mais potente quanto escolher o ambiente operacional mais eficiente para o mesmo hardware (por exemplo, dual boot em Linux nativo quando o ambiente Windows se tornar um gargalo).

### Relação entre os Princípios

Os três conceitos se encadeiam:

- Sem reprodutibilidade, cada ambiente exigiria configuração própria.
- Sem portabilidade, o projeto ficaria preso a uma máquina ou sistema operacional.
- Sem essas duas bases, a escalabilidade operacional ficaria cara, lenta e arriscada.

Em síntese: **reprodutibilidade + portabilidade = base para escalabilidade operacional**.

O objetivo é que os projetos não dependam de uma máquina específica, mas preservem o mesmo ambiente analítico em diferentes contextos operacionais, permitindo que o processamento pericial seja adaptado ao porte do caso.
