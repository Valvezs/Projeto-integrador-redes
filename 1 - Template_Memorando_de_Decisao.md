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

[Escreva aqui, citando a fonte consultada]

## 4. Comparação



| Critério | Opção A — Dataset real | Opção B — API RIPE Atlas |
|---|---|---|
| Controle sobre a coleta | | |
| Diversidade geográfica | | |
| Custo / complexidade de implementação | | |
| Tempo até os primeiros dados estarem disponíveis | | |

## 5. Recomendação

<!-- Uma frase direta: qual opção você recomenda. -->


## 6. Justificativa

A API do RIPE Atlas é adequada ao projeto porque permite trabalhar com medições reais de rede e obter informações relacionadas ao comportamento das conexões. Os resultados das medições podem ser utilizados para extrair métricas importantes para o projeto, como latência e perda de pacotes. Além disso, a distribuição das sondas possibilita trabalhar com dados provenientes de diferentes localidades. Apesar de exigir maior complexidade de implementação em comparação com um dataset pronto, a API oferece maior flexibilidade para a obtenção dos dados necessários ao sistema de predição.

## 7. Riscos e limitações

<!-- O que pode dar errado com a opção escolhida, e como isso poderia ser mitigado. -->

[Escreva aqui]

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

### Integrante 2 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*:
`[]` 
`[]`

### Integrante 3 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

### Integrante 4 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

### Integrante 5 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

### Integrante 6 — `[Escreva nome completo do aluno ]`
- **O que fez nesta etapa:** `[]`
- **Tempo dedicado (aprox.):** `[ex.: 3h30]`
- **Evidência da contribuição** *(print de conversa, rascunho, e-mail, documento compartilhado etc.)*: 
`[]` 
`[]`

---

## Fontes consultadas

<!-- Mínimo de 3 fontes. Liste todas as páginas de documentação, artigos ou repositórios usados. -->

1. [ ]
2. [ ]
3. [ ]
