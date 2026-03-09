# 📚 Erros Comuns em Entrevistas de System Design e Como Evitá-los

---

## 🧠 Introdução

Entrevistas de **System Design** são comuns em processos seletivos para cargos de engenharia de software, especialmente em níveis mais avançados. Nessas entrevistas, o candidato é avaliado pela sua capacidade de **projetar sistemas escaláveis, robustos e eficientes**.

No entanto, muitos candidatos cometem erros que não estão necessariamente relacionados à falta de conhecimento técnico, mas sim à **forma como abordam o problema durante a entrevista**.

Esses erros podem comprometer a clareza da solução apresentada e dificultar a avaliação do entrevistador.

Neste material, vamos analisar **alguns dos erros mais comuns cometidos em entrevistas de System Design** e entender **como evitá-los**, adotando uma abordagem mais estruturada e estratégica para resolver problemas de arquitetura de sistemas.

---

## 📖 Conceitos Fundamentais

Antes de discutir os erros, é importante entender dois conceitos fundamentais que aparecem frequentemente em entrevistas de System Design.

### Design de Alto Nível (High-Level Design – HLD)

O **High-Level Design (HLD)** descreve a arquitetura geral do sistema.

Ele se concentra em aspectos como:

* principais **componentes do sistema**
* **interação entre serviços**
* **fluxo de dados**
* **escalabilidade**
* **infraestrutura**

Normalmente envolve diagramas com componentes como:

* APIs
* bancos de dados
* filas de mensagens
* sistemas de cache
* serviços externos

---

### Design de Baixo Nível (Low-Level Design – LLD)

O **Low-Level Design (LLD)** foca na implementação detalhada.

Ele inclui:

* **classes**
* **interfaces**
* **funções**
* **estruturas de dados**
* **lógica interna dos componentes**

Enquanto o **HLD mostra a arquitetura do sistema**, o **LLD mostra como cada parte será implementada**.

---

### Requisitos Funcionais e Não Funcionais

Outro conceito essencial é a diferença entre **requisitos funcionais** e **não funcionais**.

#### Requisitos Funcionais

Definem **o que o sistema deve fazer**.

Exemplos:

* enviar mensagens
* criar pedidos
* buscar produtos
* realizar pagamentos

---

#### Requisitos Não Funcionais

Definem **como o sistema deve se comportar**.

Exemplos:

* escalabilidade
* latência
* disponibilidade
* tolerância a falhas
* segurança

Esses requisitos influenciam diretamente **as decisões de arquitetura**.

---

## 🔎 Explicação Detalhada

### ❌ Erro 1: Não esclarecer o tipo de design esperado

Um erro muito comum é começar imediatamente a desenhar **diagramas de classes e funções**, assumindo que a entrevista exige um **design de baixo nível**.

No entanto, muitas entrevistas de System Design focam principalmente em **High-Level Design**.

Antes de começar a solução, é importante perguntar:

* Estamos discutindo **arquitetura de alto nível**?
* Ou o foco é **design de baixo nível**?

Isso evita que você desenvolva uma solução no **nível errado de abstração**.

---

### ❌ Erro 2: Não esclarecer os requisitos funcionais

Outro erro comum ocorre quando o entrevistador pede algo como:

> "Projete o sistema do Uber."

Alguns candidatos imediatamente começam a explicar **como o Uber funciona**, sem perguntar quais funcionalidades devem ser incluídas.

No entanto, o Uber possui muitas funcionalidades, como:

* solicitação de corrida
* cálculo de preço
* geolocalização
* sistema de pagamento
* avaliações
* correspondência entre motorista e passageiro

O entrevistador pode estar interessado apenas em **uma parte específica do sistema**.

Por isso, é essencial perguntar:

* quais funcionalidades devem ser consideradas?
* quais fluxos principais precisam ser modelados?

---

### ❌ Erro 3: Ignorar requisitos não funcionais

Muitos candidatos focam apenas nas funcionalidades e ignoram fatores críticos como **escala e desempenho**.

Por exemplo:

* um aplicativo de chat interno com **50 usuários**
* um aplicativo como **WhatsApp com bilhões de usuários**

Embora ambos sejam aplicativos de mensagens, suas arquiteturas seriam **completamente diferentes**.

Antes de projetar o sistema, é importante esclarecer:

* número de usuários
* volume de dados
* taxa de requisições por segundo
* requisitos de latência
* disponibilidade esperada

Essas informações ajudam a definir a **arquitetura correta**.

---

### ❌ Erro 4: Gerenciamento inadequado do tempo

Entrevistas de System Design geralmente duram cerca de **40 a 45 minutos**.

Um erro comum é gastar tempo demais em **um único componente** e não conseguir abordar o restante da arquitetura.

Uma abordagem mais eficiente é:

1. começar com um **design de alto nível**
2. identificar os **principais componentes**
3. mostrar **como eles interagem**
4. aprofundar em **um ou dois componentes críticos**

Isso demonstra visão arquitetural e capacidade de priorização.

---

### ❌ Erro 5: Fazer suposições sem validar com o entrevistador

Alguns candidatos tomam decisões importantes sem consultar o entrevistador.

Por exemplo:

* escolher um banco de dados
* definir arquitetura de serviços
* assumir determinados requisitos

Em vez disso, é recomendável envolver o entrevistador durante a discussão.

Perguntas úteis incluem:

* "Essa abordagem faz sentido para você?"
* "Devemos explorar esse componente com mais detalhes?"
* "Há alguma parte específica que você gostaria de discutir?"

Essa interação torna a entrevista **mais colaborativa**.

---

### ❌ Erro 6: Tentar esconder o que você não sabe

Muitos candidatos acreditam que precisam saber **tudo sobre todos os componentes do sistema**.

Isso não é verdade.

Se você não souber como implementar um determinado componente, é melhor ser transparente.

Exemplo:

> "Eu não tenho certeza de como implementar esse sistema de rate limiting, mas uma possível abordagem seria..."

Essa atitude demonstra:

* **honestidade**
* **pensamento crítico**
* **capacidade de raciocinar sobre soluções**

Em muitos casos, o entrevistador pode até oferecer uma dica para ajudar na discussão.

---

## 💡 Exemplos práticos

### Exemplo 1 — Abordagem incorreta

Pergunta:

> Projete um sistema de chat.

Resposta ruim:

* começar imediatamente desenhando classes
* não perguntar sobre escala
* ignorar requisitos de latência
* assumir funcionalidades

---

### Exemplo 2 — Abordagem correta

Resposta ideal:

1️⃣ Perguntar sobre os requisitos:

* quantos usuários?
* mensagens em tempo real?
* armazenamento de histórico?

2️⃣ Identificar requisitos não funcionais:

* latência
* escalabilidade
* disponibilidade

3️⃣ Criar arquitetura de alto nível:

```text
Cliente
   ↓
API Gateway
   ↓
Serviço de mensagens
   ↓
Banco de dados
   ↓
Sistema de cache
```

4️⃣ Aprofundar em componentes específicos.

---

## ⚠️ Pontos importantes

Alguns princípios importantes para entrevistas de System Design:

* Sempre **clareie os requisitos antes de projetar**
* Diferencie **High-Level Design de Low-Level Design**
* Considere **escala e desempenho**
* Gerencie bem o **tempo da entrevista**
* Não faça **suposições sem confirmar**
* Seja honesto sobre **limitações de conhecimento**

Esses fatores muitas vezes são mais importantes do que a tecnologia escolhida.

---

## 📝 Resumo do conteúdo

Nesta aula aprendemos que muitos erros em entrevistas de System Design não estão relacionados à falta de conhecimento técnico, mas sim à abordagem utilizada.

Os principais erros incluem:

* não esclarecer o tipo de design esperado
* não definir requisitos funcionais
* ignorar requisitos não funcionais
* gastar tempo excessivo em um único componente
* fazer suposições sem validar com o entrevistador
* tentar esconder lacunas de conhecimento

Adotar uma abordagem **estruturada e colaborativa** melhora significativamente o desempenho nessas entrevistas.

---

## 🎯 Perguntas para revisão

1. Qual é a diferença entre **High-Level Design e Low-Level Design**?
2. Por que é importante esclarecer **requisitos funcionais** antes de projetar um sistema?
3. Como os **requisitos não funcionais** influenciam a arquitetura de um sistema?
4. Qual estratégia ajuda a gerenciar melhor o tempo durante uma entrevista de System Design?
5. Por que é melhor admitir quando você não sabe algo durante a entrevista?

---

## 📌 Conclusão

Entrevistas de System Design avaliam muito mais do que conhecimento técnico: elas medem a **capacidade de raciocínio arquitetural, comunicação e tomada de decisões**.

Evitar erros comuns — como não esclarecer requisitos, ignorar escala ou tentar demonstrar conhecimento absoluto — permite que o candidato apresente soluções mais claras e estruturadas.

Ao adotar uma abordagem baseada em **questionamento, análise de requisitos e arquitetura progressiva**, é possível demonstrar maturidade técnica e aumentar significativamente as chances de sucesso em entrevistas de design de sistemas.
