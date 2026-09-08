# Memorando de Decisão — Fonte de Dados do Projeto


| Campo | Informação |
|-------|------------|
| Curso / Disciplina | Ciências da Computação / Estrutura de Dados II        |
| Projeto Integrador | Preditor de Falha e Risco em Dispositivos de Rede     |
| Orientador(a) | Prof. Andréa Ono Sakai, Prof. Denise Braito de Souza       |
| Data de entrega desta etapa                                   | 08/09/2026 |
| Integrantes do grupo | Victor Gabriel Alves, Livia Freixo, Rodrigo Camargo |
---

## 1. Situação

Fase incial: Nosso grupo precisa decidir qual fonte de dados será utilizada na próxima etapa do projeto — um dataset real já publicado ou a API do RIPE Atlas — considerando qual alternativa oferece dados mais adequados para a construção das variáveis X = [latência, perda, jitter] utilizadas pelo Preditor de Falha e Risco em Dispositivos de Rede.

## 2. Opção A — Dataset real

- **Origem / link:** https://aws.amazon.com/pt/what-is/icmp/
- **Formato:** CSV / Arquivos.pcap
- **Período coberto:** Dados gerados em ambiente simulado/emulado (geralmente sob demanda para benchmarks de redes SDN e IoT, publicados e atualizados em repositórios abertos).
- **Campos disponíveis:** Timestamp, Source IP, Destination IP, Protocol, ICMP Type, ICMP Code, Packet Size / Length
- **Licença de uso:** Aberta para fins acadêmicos e de pesquisa (conforme os termos de plataformas de repositórios científicos como Mendeley Data e Zenodo)

**Resumo do que foi encontrado:**
Dataset de IoT para ICMP (Zenodo)
 Focado no comportamento do comando ping, criado para diferenciar o tráfego ICMP/Ping normal de tráfegos maliciosos originados de dispositivos IoT
 Os pacotes ICMP capturados na rede são convertidos em logs através da ferramenta de monitoramento Zeek e extraídos em formato .csv

Dataset "SDN ICMP Flood Dataset"
 É um conjunto de dados focado em ataques de inundação ICMP (ICMP Flood DDoS) dentro de uma infraestrutura moderna de Redes Definidas por Software (SDN)
 O tráfego analisa variáveis como o tipo de mensagem ICMP, tamanho dos pacotes, tempo de duração do fluxo e contagem de pacotes.

apresentarão a seguinte estrutura de colunas
Timestamp(registro exato de milissegundos em que o pacote ICMP passou pela rede),  Source / Destination IP( endereço IP de quem enviou e recebeu), Protocol(Onde o valor mapeia o ICMP), Length / Packet Size(tamanho do pacote em bytes )

## 3. Opção B — API do RIPE Atlas

- **Documentação consultada (link):** RIPE Atlas API v2 Documentation ([https://ripe-atlas-api.readthedocs.io/](https://www.google.com/search?q=https://ripe-atlas-api.readthedocs.io/) e [https://atlas.ripe.net/docs/apis/](https://atlas.ripe.net/docs/apis/))
- **Autenticação exigida:** Autenticação via API Ke (Chave de API) ou parâmetro de URL. Para criar medições, necessário consumir créditos do RIPE Atlas.

- **Como se cria uma medição:** - **Como se cria uma medição:** Envia-se uma requisição HTTP `POST` para o endpoint `/api/v2/measurements/` com um corpo JSON definindo o tipo (`type: "ping"`), os alvos (`target`), o número de pacotes, o intervalo e o tipo de sondas a serem utilizadas.

- **Como se consultam os resultados:** Através de requisição HTTP `GET` no endpoint `/api/v2/measurements/\{id\}/results/`. Os resultados retornam em formato JSON detalhado, contendo arrays com os valores individuais de RTT de cada pacote ICMP enviada por cada sonda.

**Resumo do que foi encontrado:**
A API do RIPE Atlas pode ser uma boa opção para o projeto, pois permite trabalhar com medições reais de rede. Os resultados de medições do tipo ping possuem informações que podem ser usadas para analisar latência e perda de pacotes. Outro ponto positivo é de poder utilizar medições realizadas por diferentes sondas, permitindo trabalhar com dados de diferentes localidades. (RIPE Atlas — Ping Statistics e RIPE Atlas — What is RIPE Atlas? (https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats)

Autenticação via API Key
Endpoints POST (criar) e GET (recuperar resultados)
Exemplos de payload e resposta JSON
Sistema de créditos (50/mês grátis)

## 4. Comparação



| Critério | Opção A — Dataset real | Opção B — API RIPE Atlas |
|----------|------------------------|--------------------------|
| Controle sobre a coleta                          | baixo, são dados previamente gerados em ambientes simulados sendo assim não é feito o controle direto de onde ou quando o trafegpo/dado foi coletado| Alto - É possivel comprolar a medição definindo o tipo de teste, destino, quantidade de pacotes e sondas uitizadas       |
| Diversidade geográfica                           |É limitada ao ambinete que o dataset foi construidos. Os conjuntos analisados são voltados principalmente para cenários específicos de IoT, SDN e tráfego ICMP.  |A utilização de diferentes sondas do RIPE Atlas permite medições a partir de diferentes pontos da rede e localidades.|
| Custo / complexidade de implementação            |Os arquivos já estão disponíveis em formatos como CSV e PCAP, possibilitando análise direta sem necessidade de desenvolver um mecanismo de coleta |Exige integração com a API, autenticação por API Key, criação de requisições HTTP, processamento de respostas JSON e gerenciamento dos créditos disponíveis.|
| Tempo até os primeiros dados estarem disponíveis |Imediato. Após o download do dataset, os dados podem ser utilizados diretamente no projeto.|Rápido, porém dependente da execução das medições. É necessário configurar a requisição, criar a medição e aguardar a geração dos resultados pelas sondas.|

## 5. Recomendação

Recomenda-se a utilização da API do RIPE Atlas como fonte de dados para o projeto, devido à possibilidade de trabalhar com medições reais de rede e obter dados de diferentes localidades


## 6. Justificativa

A API do RIPE Atlas é adequada ao projeto porque permite trabalhar com medições reais de rede e obter informações relacionadas ao comportamento das conexões. Os resultados das medições podem ser utilizados para extrair métricas importantes para o projeto, como latência e perda de pacotes. Além disso, a distribuição das sondas possibilita trabalhar com dados provenientes de diferentes localidades. Apesar de exigir maior complexidade de implementação em comparação com um dataset pronto, a API oferece maior flexibilidade para a obtenção dos dados necessários ao sistema de predição.

## 7. Riscos e limitações

Entre os principais riscos estão a necessidade de integração com a API, o tratamento dos dados recebidos e a possível necessidade de créditos para a realização de novas medições. Também podem ocorrer variações nos resultados devido às condições da rede durante as medições. Para reduzir esses riscos, o grupo pode utilizar inicialmente resultados de medições já existentes para testar o processamento dos dados e, posteriormente, realizar novas medições conforme a necessidade do projeto.

## 8. Contribuição Individual dos Integrantes

<!-- cada integrante deve descrever, com suas próprias palavras, o que efetivamente fez nesta etapa. Contribuições genéricas como "ajudei em tudo" não serão aceitas. Use verbos de ação e seja específico (ex.: "pesquisei , analisei, testei, ... apresentei prós/contras ao grupo, ...").-->

Victor - realizai a verificação de situção, pesquisei sobre a API do RIPE Atlas,  auxiliei na comparação.

Livia - efetuei o levantameto da recoimentação com base nos materias disponiveis, apresentei a justificativa efetui a analise de riscos e limitações.

Rodrigo - efetuei a pesquisa sobre o data set real, auxiliei na comparação e justificativa.

### Integrante 1 — Victor Gabriel Alves
- **O que fez nesta etapa:** pesquisa e documentação 1(situação), 3(API RIPE Atlas)
- **Tempo dedicado (aprox.):** ex.: 4h00
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*:
`[]` 
`[]`

### Integrante 2 — `Rodrigo Camargo Vieira`
- **O que fez nesta etapa:** `Pesquisa e documentação Dataset Real`
- **Tempo dedicado (aprox.):** 1h30
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*:
`[]` 
`[]`

### Integrante 3 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `analisei as alternativas de fonte de dados para o projeto, comparei o uso de dataset real e da API do RIPE Atlas, considerando controle sobre a coleta, complexidade de implementação e disponibilidade dos dados. Também analisei os benefícios, riscos e limitações das alternativas e elaborei breve resumo do que encontrei a respeito.`
- **Tempo dedicado (aprox.):** 4h30
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

## Fontes consultadas


 https://www.openaire.eu/zenodo-guide, https://datamanagement.hms.harvard.edu/share-publish/data-repositories/zenodo, https://zenodo.org/records/7772015
medições reais de latência Round-Trip Time (RTT) https://portalinvestigacion.upct.es/datos/69a55c918c94a2342eb6b5a2?lang=en&utm_source=chatgpt.com
RIPE Atlas Documentation — What is RIPE Atlas? https://atlas.ripe.net/docs/getting-started/what-is-ripe-atlas
RIPE Atlas Documentation — Creating Measurements https://atlas.ripe.net/docs/apis/rest-api-manual/measurements/creating-measurements/
RIPE Atlas Documentation — GET /measurements/{msm}/ping-stats/https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats 4.RIPE Atlas Documentation — Ping Statistics — https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats