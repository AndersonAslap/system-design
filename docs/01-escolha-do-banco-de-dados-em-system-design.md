# 📚 Escolha de Bancos de Dados em System Design

---

## 🧠 Introdução

Ao projetar sistemas escaláveis, uma das decisões mais importantes é a **escolha do banco de dados**. Embora diferentes bancos de dados consigam atender aos mesmos **requisitos funcionais**, a escolha correta impacta diretamente os **requisitos não funcionais**, como:

* **Escalabilidade**
* **Desempenho**
* **Disponibilidade**
* **Latência**
* **Capacidade de armazenamento**

Em entrevistas de **System Design** e também em sistemas reais, diferentes tipos de banco de dados são escolhidos com base em características específicas do sistema, como:

* **estrutura dos dados**
* **padrões de consulta**
* **volume e crescimento dos dados**

Neste material, vamos explorar **os principais tipos de bancos de dados e soluções de armazenamento utilizados em arquiteturas modernas**, entendendo **quando e por que utilizar cada um deles**.

---

## 📖 Conceitos Fundamentais

Antes de escolher um banco de dados, é necessário analisar três fatores principais.

### 1️⃣ Estrutura dos dados

Os dados podem ser:

* **Estruturados** → organizados em tabelas (linhas e colunas)
* **Semiestruturados** → JSON ou documentos
* **Não estruturados** → imagens, vídeos, arquivos

Cada tipo de estrutura favorece um tipo diferente de armazenamento.

---

### 2️⃣ Padrões de consulta

Outro fator importante é **como os dados serão consultados**.

Alguns exemplos:

* consultas simples por ID
* consultas complexas com múltiplos filtros
* buscas textuais
* consultas por intervalo de tempo

Cada banco de dados é otimizado para **determinados padrões de acesso aos dados**.

---

### 3️⃣ Escala do sistema

A escala define:

* volume total de dados
* crescimento ao longo do tempo
* quantidade de leituras e gravações

Sistemas com **grande volume de dados ou crescimento acelerado** precisam de bancos otimizados para alta escalabilidade.

---

## 🔎 Explicação Detalhada

### 🔹 Soluções de Cache

Em praticamente **todo sistema escalável**, utiliza-se algum tipo de **cache**.

O objetivo do cache é **reduzir a carga em sistemas mais lentos**, como:

* bancos de dados
* APIs externas
* serviços remotos

Em vez de buscar sempre a informação na fonte original, o sistema armazena temporariamente a resposta em memória.

#### Funcionamento do cache

O cache geralmente funciona no formato:

```
chave → valor
```

Exemplo:

```
"user:123" → dados do usuário
```

A chave normalmente representa:

* parâmetros da requisição
* cláusula WHERE da consulta
* identificadores da API

E o valor representa **a resposta armazenada**.

#### Ferramentas comuns

Algumas soluções populares de cache incluem:

* **Redis**
* **Memcached**
* **etcd**
* **Hazelcast**

Entre elas, o **Redis** é uma das mais utilizadas em sistemas de grande escala.

---

### 🔹 Armazenamento de arquivos (Blob Storage)

Em muitos sistemas, precisamos armazenar **arquivos grandes**, como:

* imagens
* vídeos
* documentos
* arquivos de mídia

Esses dados **não são ideais para bancos de dados tradicionais**, pois normalmente **não são consultados**, apenas armazenados e servidos.

Para esses casos utilizamos **Blob Storage**.

Um dos serviços mais utilizados é:

* **Amazon S3**

Esse tipo de armazenamento é otimizado para **arquivos grandes e escaláveis**.

---

### 🔹 Content Delivery Network (CDN)

Quando arquivos são acessados globalmente, utilizar apenas um servidor pode gerar **alta latência**.

Para resolver isso, utiliza-se uma **Content Delivery Network (CDN)**.

Uma CDN distribui cópias do conteúdo em servidores espalhados pelo mundo.

Benefícios:

* menor latência
* melhor performance
* menor carga no servidor principal

Fluxo comum:

```
Usuário → CDN → S3
```

---

### 🔹 Motores de busca de texto

Alguns sistemas exigem **busca textual avançada**, como:

* pesquisa de produtos (Amazon)
* pesquisa de filmes (Netflix)
* busca por endereços (Uber / Google Maps)

Esses casos utilizam **motores de busca especializados**.

Ferramentas comuns:

* **Elasticsearch**
* **Solr**

Ambos são construídos sobre o **Apache Lucene**.

---

### 🔹 Fuzzy Search

Uma funcionalidade importante desses motores é a **fuzzy search**.

Ela permite que o sistema **encontre resultados mesmo com erros de digitação**.

Exemplo:

Usuário digita:

```
AIRPROT
```

O sistema entende que o usuário quis dizer:

```
AIRPORT
```

Isso é possível através de **distância de edição**, que mede quantas alterações são necessárias para transformar uma palavra em outra.

---

### 🔹 Observação importante

Motores de busca **não devem ser a fonte principal de dados**.

Isso porque:

* eles priorizam **performance**
* não garantem **durabilidade total dos dados**

Por isso, o fluxo comum é:

```
Banco principal → Indexação → Elasticsearch
```

---

### 🔹 Bancos de dados de séries temporais

Alguns sistemas trabalham com **dados que evoluem ao longo do tempo**, como:

* métricas de CPU
* latência de aplicações
* monitoramento de sistemas

Esses dados possuem características específicas:

* inserções sequenciais
* raramente são atualizados
* consultas por intervalo de tempo

Esses sistemas utilizam **Time Series Databases**.

Ferramentas comuns:

* **InfluxDB**
* **OpenTSDB**

Eles são otimizados para:

* escrita contínua
* consultas temporais

---

### 🔹 Data Warehouse

Empresas frequentemente precisam realizar **análises em grande escala**, como:

* relatórios de vendas
* análise de receita
* comportamento de usuários

Para isso utilizamos **Data Warehouses**.

Características:

* grande volume de dados
* consultas analíticas complexas
* processamento offline

Uma tecnologia bastante utilizada é:

* **Hadoop**

---

### 🔹 Bancos de dados relacionais (SQL)

Bancos relacionais são ideais para **dados estruturados**.

Exemplo de estrutura:

| id | nome | email |
| -- | ---- | ----- |

Eles oferecem garantias **ACID**, fundamentais para sistemas críticos.

ACID significa:

* **Atomicidade**
* **Consistência**
* **Isolamento**
* **Durabilidade**

Essas propriedades são essenciais em sistemas como:

* pagamentos
* controle de estoque
* transações financeiras

Exemplos:

* **MySQL**
* **PostgreSQL**
* **Oracle**
* **SQL Server**

---

### 🔹 Bancos de dados de documentos

Quando os dados são **flexíveis ou sem estrutura fixa**, bancos de documentos são mais adequados.

Exemplo: catálogo de produtos.

Cada produto pode ter atributos diferentes:

Camisa:

```
tamanho
cor
```

Geladeira:

```
capacidade
consumo energético
```

Leite:

```
volume
data de validade
```

Bancos relacionais lidam mal com esse tipo de estrutura variável.

Por isso usamos **Document Databases**.

Exemplos:

* **MongoDB**
* **Couchbase**

---

### 🔹 Bancos de dados colunares

Alguns sistemas possuem:

* **crescimento contínuo de dados**
* poucas consultas diferentes
* altíssimo volume de gravação

Exemplo clássico: **rastreamento de localização de motoristas (Uber)**.

Cada motorista envia continuamente sua posição.

Nesse cenário, bancos **orientados a colunas** são ideais.

Exemplos:

* **Apache Cassandra**
* **HBase**

Eles são projetados para:

* alta escalabilidade
* grandes volumes de escrita
* distribuição horizontal

---

## 💡 Exemplos práticos

### Sistema de e-commerce (Amazon)

Um sistema como a Amazon utiliza **vários bancos de dados simultaneamente**.

Exemplo de arquitetura:

| Função               | Banco utilizado |
| -------------------- | --------------- |
| Controle de estoque  | MySQL           |
| Histórico de pedidos | Cassandra       |
| Busca de produtos    | Elasticsearch   |
| Imagens de produtos  | S3              |
| Cache de consultas   | Redis           |

Essa abordagem é chamada de **Polyglot Persistence**.

---

### Sistema de métricas

Ferramentas como **Grafana ou Prometheus** utilizam bancos de séries temporais.

Fluxo:

```
Aplicações → métricas → Time Series DB → dashboards
```

---

## ⚠️ Pontos importantes

Alguns conceitos importantes:

* **Nenhum banco de dados resolve todos os problemas**
* Sistemas reais usam **vários tipos de bancos**
* Bancos de busca **não são fontes primárias de dados**
* Cache é essencial para performance
* Escala influencia fortemente a escolha do banco

---

## 📝 Resumo do conteúdo

Principais aprendizados:

* A escolha do banco de dados depende de **estrutura, consultas e escala**.
* **Caches** reduzem latência e carga no sistema.
* **Blob storage** é usado para arquivos grandes.
* **Motores de busca** oferecem pesquisa textual eficiente.
* **Time series databases** armazenam métricas temporais.
* **RDBMS** oferecem garantias ACID.
* **Document databases** lidam bem com dados flexíveis.
* **Column databases** são ideais para dados massivos.

Sistemas reais utilizam **combinação de vários bancos de dados**.

---

## 🎯 Perguntas para revisão

1. Quais fatores influenciam a escolha de um banco de dados em um sistema?
2. Em quais cenários devemos utilizar **Redis**?
3. Qual é a diferença entre **Elasticsearch e um banco de dados tradicional**?
4. Quando utilizar **bancos de documentos como MongoDB**?
5. Em quais situações **Cassandra é mais adequado que bancos relacionais**?

---

## 📌 Conclusão

A escolha do banco de dados é uma das decisões mais estratégicas no **design de sistemas escaláveis**.

Cada tipo de banco é otimizado para um conjunto específico de problemas. Por isso, arquiteturas modernas adotam uma abordagem híbrida, utilizando diferentes tecnologias para diferentes necessidades.

Ao compreender **as características dos dados, os padrões de acesso e a escala do sistema**, é possível escolher a solução mais adequada e construir sistemas **mais eficientes, escaláveis e resilientes**.

# dicas

1- Impacto dos Bancos de Dados: Embora os bancos de dados não afetem os requisitos funcionais, eles impactam significativamente os requisitos não funcionais como escalabilidade e padrões de consulta.

2- Importância do Caching: Use soluções de caching para reduzir consultas ao banco de dados e melhorar o desempenho. Exemplo: Redis, Memcached e Hazelcast, com o Redis sendo o preferido pela sua estabilidade.

3- Armazenamento de Arquivos: Para armazenar imagens e vídeos, recomenda-se o Amazon S3 para armazenamento de blobs e o uso de Redes de Distribuição de Conteúdo (CDNs) para distribuição geográfica eficiente.

4- Capacidades de Pesquisa de Texto: Considerar ferramentas como Elastic Search e Solr para implementar funcionalidades de busca, incluindo busca fuzzy que melhora a experiência do usuário.

5- Bancos de Dados para Séries Temporais: Para aplicações que rastreiam métricas ao longo do tempo, opções como InfluxDB e OpenTSDB são sugeridas.

6- Armazenamento de Dados para Análise: Os Data Warehouses são importantes para análises, com o Hadoop sendo uma solução viável para relatórios offline.

7- Escolha entre Bancos de Dados Relacionais e Não Relacionais: Use um fluxograma para decidir entre bancos de dados relacionais e não relacionais com base na estrutura dos dados e nos requisitos transacionais.

8- Dados Estruturados vs. Não Estruturados: Dados estruturados geralmente se encaixam bem em bancos de dados relacionais, enquanto dados não estruturados podem exigir bancos de dados de documentos como MongoDB ou Couchbase.

9- Crescimento de Dados: Para grandes volumes de dados com tipos de consulta limitados, recomenda-se bancos de dados em coluna como Cassandra e HBase.

10- Combinação de Diferentes Tipos de Bancos de Dados: É fundamental combinar diferentes tipos de bancos de dados para atender a vários requisitos funcionais e não funcionais em aplicações do mundo real.

Essas dicas oferecem uma diretriz abrangente para selecionar o banco de dados apropriado com base em casos de uso específicos e requisitos. Se você tiver mais perguntas ou precisar de esclarecimentos, sinta-se à vontade para perguntar!

---

### diagrama

O diagrama montado pelo professor é uma ferramenta visual que ajuda a escolher o banco de dados adequado com base na estrutura dos dados e nos requisitos específicos de uma aplicação. Vamos quebrar o funcionamento do diagrama:

Estrutura de Dados: O diagrama começa perguntando se os dados são estruturados. Se a resposta for "sim", avança para a próxima pergunta sobre a necessidade de ACID.

Necessidade de ACID: Se os dados requerem propriedades ACID (Atomicidade, Consistência, Isolamento e Durabilidade), a escolha recai sobre bancos de dados relacionais (RDBMS), como MySQL, Oracle, SQL Server e PostgreSQL. Esses bancos são ideais para transações que exigem alto grau de confiabilidade.

Dados Não Estruturados: Se os dados não são estruturados, se faz uma nova distinção com base em dois critérios:

Tipos e Consultas de Dados: Se os dados têm muitos tipos e consultas, isso implica a escolha de um banco de dados de documentos, como MongoDB ou Couchbase. Esses bancos são ótimos para armazenar documentos JSON e realizar consultas flexíveis.
Crescimento de Dados: Se os dados estão em um padrão de crescimento contínuo e têm consultas finitas, o diagrama sugere um banco de dados columnar, como Cassandra ou HBase, que é projetado para lidar eficientemente com grandes volumes de dados.
Abordagem Prática: O professor ressalta que essa estrutura é um guia inicial. Dependendo do caso de uso real, pode ser necessário explorar mais sobre as opções e combinações de bancos de dados para atender a requisitos funcionais e não funcionais.

Este resumo fornece uma visão clara de como usar o diagrama para tomar decisões informadas sobre a escolha de bancos de dados em contextos de design de sistemas. Se precisar de mais detalhes ou tiver perguntas específicas, estou à disposição!

### como utilizar o diagrama

Para utilizar o diagrama de escolha de banco de dados, siga este passo a passo:

Início: Avalie se os dados são estruturados.
Sim: Prossiga para a próxima pergunta.
Não: Considere bancos de dados de documentos ou columnar, dependendo das necessidades subsequentes.

Necessidade de ACID: Pergunte se há a necessidade de propriedades ACID.
Sim: Escolha um RDBMS (MySQL, Oracle, PostgreSQL).
Não: Avalie mais detalhes sobre os dados.

Tipos e Consultas de Dados: Determine se os dados têm muitos tipos e consultas.
Sim: Opte por um banco de dados de documentos (MongoDB, Couchbase).
Não: Avance para a próxima consideração.

Crescimento de Dados: Pergunte se os dados são crescentes e têm consultas finitas.
Sim: Escolha um banco de dados columnar (Cassandra, HBase).
Não: Reavalie os critérios ou opções.

Decisão Final: Com base nas respostas, escolha o banco

Esse conteúdo foi relevante para você?
