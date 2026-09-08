# Memorando de Decisão — Fonte de Dados do Projeto

| Campo | Informação |
|-------|------------|
| Curso / Disciplina | Ciências da Computação / Estrutura de Dados II |
| Projeto Integrador | Preditor de Falha e Risco em Dispositivos de Rede |
| Orientador(a) | Prof. Andréa Ono Sakai, Prof. Denise Braito de Souza |
| Data de entrega desta etapa | 08/09/2026 |
| Integrantes do grupo | Victor Gabriel Alves, Livia Freixo, Rodrigo Camargo |

---

## 1. Situação

Nesta etapa do projeto, o grupo precisa selecionar a fonte de dados que será utilizada na próxima fase do desenvolvimento. A decisão deve considerar qual alternativa oferece informações mais adequadas para a construção das variáveis X = [latência, perda, jitter], necessárias ao sistema de predição de falhas e riscos em dispositivos de rede.

A análise comparativa será realizada entre duas opções: um dataset real já publicado e a API do RIPE Atlas. A escolha deve priorizar a qualidade, a relevância e a capacidade de coleta dos dados para o objetivo do projeto.

## 2. Opção A — Dataset real

- **Origem / link:** datasets públicos disponíveis em plataformas acadêmicas e científicas, como Zenodo, Mendeley Data e outros repositórios abertos relacionados a ICMP e DDoS.
- **Formato:** CSV, arquivos de log gerados por ferramentas de monitoramento e, em alguns casos, arquivos `.pcap`.
- **Período coberto:** depende do conjunto de dados selecionado; geralmente representa dados coletados em redes simuladas ou em ambientes emulados.
- **Campos disponíveis:** timestamp, endereço IP de origem e destino, protocolo, tipo e código ICMP, tamanho do pacote e outras métricas relacionadas ao tráfego.
- **Licença de uso:**, em geral, aberta para fins acadêmicos e de pesquisa, conforme os termos da plataforma onde o dataset é hospedado.

### Resumo do que foi encontrado

Existem datasets públicos focados em tráfego ICMP e em ataques do tipo ICMP Flood, especialmente em contextos de redes SDN e IoT. Esses conjuntos costumam reunir registros detalhados de pacotes, incluindo marca temporal, origem e destino, tipo de mensagem ICMP, tamanho dos pacotes e contagem de fluxos. Esse tipo de dado é útil para análise de padrões de tráfego e para treinamento de modelos de detecção, porém apresenta menor flexibilidade para coleta sob demanda.

## 3. Opção B — API do RIPE Atlas

- **Documentação consultada (links):** RIPE Atlas API v2, RIPE Atlas Docs e RIPE Atlas Ping Statistics.
- **Autenticação exigida:** autenticação por API key ou parâmetro na URL. Em algumas medições, é necessário consumir créditos do RIPE Atlas.
- **Como se cria uma medição:** envio de uma requisição HTTP `POST` para o endpoint `/api/v2/measurements/`, com um corpo JSON contendo o tipo de medição (`type: "ping"`), o alvo (`target`), o número de pacotes, o intervalo entre as medições e o tipo de sonda desejado.
- **Como se consultam os resultados:** requisição HTTP `GET` para o endpoint `/api/v2/measurements/{id}/results/`, recebendo respostas em JSON detalhado com os valores de RTT e métricas por pacote e por sonda.

### Resumo do que foi encontrado

A API do RIPE Atlas permite coletar medições reais de rede, com dados de latência, perda de pacotes e jitter obtidos por sondas distribuídas geograficamente. Essa alternativa é especialmente relevante para um projeto que busca analisar o comportamento de conexões em cenários reais, além de oferecer maior flexibilidade para ajustar parâmetros de coleta e comparar resultados entre localidades distintas.

## 4. Comparação

| Critério | Opção A — Dataset real | Opção B — API RIPE Atlas |
|---|---|---|
| Controle sobre a coleta | Baixo a médio; o conjunto já foi coletado e a estrutura é fixa | Alto; é possível definir alvo, frequência, número de pacotes e tipo de medição |
| Diversidade geográfica | Limitada ao ambiente e à região do dataset original | Alta; permite obter dados de diferentes localidades por meio das sondas |
| Custo / complexidade de implementação | Baixa complexidade inicial, mas exige pré-processamento e análise dos dados | Média a alta complexidade, pois exige autenticação, criação de medições e consumo de créditos |
| Tempo até os primeiros dados estarem disponíveis | Imediato, pois o dataset já existe | Dependente da criação da medição e da sua execução em tempo real |

## 5. Recomendação

Recomenda-se a utilização da API do RIPE Atlas como fonte principal de dados para o projeto.

## 6. Justificativa

A API do RIPE Atlas é a opção mais adequada para o objetivo do projeto, pois oferece medições reais de rede com informações diretamente relacionadas ao comportamento das conexões. Os dados gerados por essa plataforma permitem extrair indicadores fundamentais para a predição de falhas e riscos, como latência, perda de pacotes e jitter.

Além disso, a presença de sondas distribuídas geograficamente amplia a representatividade dos dados e possibilita a análise de diferentes cenários de rede. Embora datasets públicos sejam úteis como referência e possam complementar a etapa de validação, eles normalmente representam contextos históricos ou específicos e apresentam menor adaptabilidade às necessidades do projeto.

## 7. Riscos e limitações

A principal limitação da API do RIPE Atlas é a dependência de autenticação, créditos e disponibilidade de sondas em tempo real. Além disso, os resultados podem variar conforme o horário da coleta, a qualidade da rede e a localização da sonda utilizada.

Para mitigar esses riscos, o grupo pode planejar medições em horários distintos, registrar a duração das coletas e manter um conjunto de dados de apoio em formato local para comparação e validação posterior.

## 8. Contribuição Individual dos Integrantes

### Integrante 1 — Victor Gabriel Alves
- **O que fez nesta etapa:** pesquisou a API do RIPE Atlas, identificou os principais endpoints e parâmetros de medição, e contribuiu na análise comparativa entre as opções.
- **Tempo dedicado (aprox.):** 4h00
- **Evidência da contribuição:** registros de pesquisa, notas de estudo e discussões do grupo sobre a escolha da solução.

### Integrante 2 — Livia Freixo
- **O que fez nesta etapa:** analisou a recomendação e a justificativa do projeto, revisou a estrutura do memorando e contribuiu na definição dos riscos e limitações da alternativa escolhida.
- **Tempo dedicado (aprox.):** 3h30
- **Evidência da contribuição:** rascunho do documento, organização das ideias e revisão textual do texto final.

### Integrante 3 — Rodrigo Camargo
- **O que fez nesta etapa:** pesquisou os datasets reais e suas principais características, além de auxiliar na comparação entre dataset e RIPE Atlas.
- **Tempo dedicado (aprox.):** 3h30
- **Evidência da contribuição:** material pesquisado sobre datasets ICMP, notas comparativas e contribuição na redação do memorando.

---

## Fontes consultadas

1. RIPE Atlas API v2 Documentation — https://atlas.ripe.net/docs/apis/
2. RIPE Atlas — Ping Statistics — https://atlas.ripe.net/docs/apis/rest-api-reference/measurements/measurements_ping_stats/
3. AWS — What is ICMP — https://aws.amazon.com/pt/what-is/icmp/
4. Zenodo / datasets públicos relacionados a ICMP e SDN — repositórios abertos de dados acadêmicos
