# Memorando de Decisão — Fonte de Dados do Projeto


| Campo | Informação |
|---|---|
| Curso / Disciplina | Ciências da Computação / Estrutura de Dados II   |
| Projeto Integrador | Preditor de Falha e Risco em Dispositivos de Rede |
| Projeto integrador | Reditor de Falha e Risco em Dispositivos de Rede |
| Orientador(a) | Prof. Andréa Ono Sakai, Prof. Denise Braito de Souza |
| Data de entrega desta etapa                                   | 08/09 |
| Integrantes do grupo | Victor Gabriel Alves, Livia Freixo, Rodrigo Camargo |
---

## 1. Situação

Fase incial: o nosso grupo precisa verificar a API do RIPE Atlas para a coleta de dados de medição ICMP, garantindo que o pipeline receba dados válidos para extração de latência, perda e resposta.

## 2. Opção A — Dataset real

<!-- O que foi encontrado sobre um dataset real de ICMP. Cite a fonte de cada informação. -->

- **Origem / link:** [ ]
- **Formato:** [ ]
- **Período coberto:** [ ]
- **Campos disponíveis:** [ ]
- **Licença de uso:** [ ]

**Resumo do que foi encontrado:**

[Escreva aqui, citando a fonte consultada]

## 3. Opção B — API do RIPE Atlas

<!-- O que foi encontrado sobre a API: autenticação, criação e consulta de medições. Cite a fonte de cada informação. -->

- **Documentação consultada (link):** RIPE Atlas API v2 Documentation ([https://ripe-atlas-api.readthedocs.io/](https://www.google.com/search?q=https://ripe-atlas-api.readthedocs.io/) e [https://atlas.ripe.net/docs/apis/](https://atlas.ripe.net/docs/apis/))
- **Autenticação exigida:** API Key (Chave de API) enviada via cabeçalho HTTP (`Authorization: Key \<sua-chave\>`) ou parâmetro de URL. Para criar medições, necessário consumir créditos do RIPE Atlas.

- **Como se cria uma medição:** - **Como se cria uma medição:** Envia-se uma requisição HTTP `POST` para o endpoint `/api/v2/measurements/` com um corpo JSON definindo o tipo (`type: "ping"`), os alvos (`target`), o número de pacotes, o intervalo e o tipo de sondas a serem utilizadas.

- **Como se consultam os resultados:** Através de requisição HTTP `GET` no endpoint `/api/v2/measurements/\{id\}/results/`. Os resultados retornam em formato JSON detalhado, contendo arrays com os valores individuais de RTT de cada pacote ICMP enviada por cada sonda.

**Resumo do que foi encontrado:**

A API do RIPE Atlas pode ser uma boa opção para o projeto, pois permite trabalhar com medições reais de rede. Os resultados de medições do tipo ping possuem informações que podem ser usadas para analisar latência e perda de pacotes. Outro ponto positivo é de poder utilizar medições realizadas por diferentes sondas, permitindo trabalhar com dados de diferentes localidades. (RIPE Atlas — Ping Statistics e RIPE Atlas — What is RIPE Atlas? (https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats)

## 4. Comparação

<!-- Preencha a tabela com base no que você levantou nas seções 2 e 3. -->

| Critério | Opção A — Dataset real | Opção B — API RIPE Atlas |
|---|---|---|
| Controle sobre a coleta | Limitado, pois os dados já foram coletados anteriormente.| Maior controle, pois permite consultar medições e configurar novas medições.|
| Diversidade geográfica | | Alta, devido à distribuição das sondas do RIPE Atlas.|
| Custo / complexidade de implementação |Menor complexidade inicial, pois os dados já estão disponíveis. |Maior complexidade, pois exige integração com a API e tratamento dos dados. |
| Tempo até os primeiros dados estarem disponíveis || Pode ser rápido utilizando resultados de medições já existentes.|

## 5. Recomendação

Recomenda-se a utilização da API do RIPE Atlas como fonte de dados para o projeto, devido à possibilidade de trabalhar com medições reais de rede e obter dados de diferentes localidades.


## 6. Justificativa

A API do RIPE Atlas é adequada ao projeto porque permite trabalhar com medições reais de rede e obter informações relacionadas ao comportamento das conexões. Os resultados das medições podem ser utilizados para extrair métricas importantes para o projeto, como latência e perda de pacotes. Além disso, a distribuição das sondas possibilita trabalhar com dados provenientes de diferentes localidades. Apesar de exigir maior complexidade de implementação em comparação com um dataset pronto, a API oferece maior flexibilidade para a obtenção dos dados necessários ao sistema de predição.

## 7. Riscos e limitações

Entre os principais riscos estão a necessidade de integração com a API, o tratamento dos dados recebidos e a possível necessidade de créditos para a realização de novas medições. Também podem ocorrer variações nos resultados devido às condições da rede durante as medições. Para reduzir esses riscos, o grupo pode utilizar inicialmente resultados de medições já existentes para testar o processamento dos dados e, posteriormente, realizar novas medições conforme a necessidade do projeto.


## 8. Contribuição Individual dos Integrantes

<!-- cada integrante deve descrever, com suas próprias palavras, o que efetivamente fez nesta etapa. Contribuições genéricas como "ajudei em tudo" não serão aceitas. Use verbos de ação e seja específico (ex.: "pesquisei , analisei, testei, ... apresentei prós/contras ao grupo, ...").-->

### Integrante 1 — Victor Gabriel Alves
- **O que fez nesta etapa:** pesquisa e documentação 1(situação), 3(API RIPE Atlas)
- **Tempo dedicado (aprox.):** ex.: 3h00
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*:
`[]` 
`[]`

### Integrante 2 — Livia Ribeiro Freixo
- **O que fez nesta etapa:** analisei as alternativas de fonte de dados para o projeto, comparei o uso de dataset real e da API do RIPE Atlas, considerando controle sobre a coleta, complexidade de implementação e disponibilidade dos dados. Também analisei os benefícios, riscos e limitações das alternativas e elaborei breve resumo do que encontrei a respeito.
- **Tempo dedicado (aprox.):** 
- **Evidência da contribuição** 

### Integrante 3 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

## Fontes consultadas

<!-- Mínimo de 3 fontes. Liste todas as páginas de documentação, artigos ou repositórios usados. -->
1. RIPE Atlas Documentation — What is RIPE Atlas?
https://atlas.ripe.net/docs/getting-started/what-is-ripe-atlas
2. RIPE Atlas Documentation — Creating Measurements
https://atlas.ripe.net/docs/apis/rest-api-manual/measurements/creating-measurements/
3. RIPE Atlas Documentation — GET /measurements/{msm}/ping-stats/https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats
4.RIPE Atlas Documentation — Ping Statistics — https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats
5.
6.
