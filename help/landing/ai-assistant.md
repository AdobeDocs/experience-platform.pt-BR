---
title: Assistente para Adobe Experience Platform
description: Saiba como usar o Assistente para navegar e entender os conceitos do Experience Platform e do Real-time Customer Data Platform, além de informações de uso sobre os objetos.
badge: Alfa
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: 5bdfc5282e71d05ff0db39c32fc02c60fd8d1c34
workflow-type: tm+mt
source-wordcount: '2383'
ht-degree: 0%

---

# Assistente para Adobe Experience Platform

>[!NOTE]
>
>O assistente para Adobe Experience Platform está atualmente em Alpha. O recurso e a documentação estão sujeitos a alterações.

O Assistente é um recurso da interface do usuário que você pode usar para navegar e compreender os conceitos do Adobe Experience Platform e do Real-time Customer Data Platform e as informações de uso sobre os objetos.

Você pode consultar o Assistente para obter informações como:

* Orientação sobre como executar tarefas relacionadas a dados e públicos.
* Status e métricas dos objetos de dados existentes em sua organização.
* Exemplos de casos de uso e nuances para entender melhor seus objetos de dados, incluindo atributos, conjuntos de dados, destinos, esquemas, segmentos e fontes.

Leia o guia abaixo para saber como você pode usar o Assistente para navegar e entender seus fluxos de trabalho de Experience Platform e Real-Time CDP.

>[!BEGINSHADEBOX]

**Como funciona o Assistente?**

O Assistente responde às perguntas enviadas consultando um banco de dados e convertendo os dados do banco de dados em uma resposta legível.

Essa representação interna de dados subjacentes também é conhecida como Gráfico de conhecimento - uma Web abrangente de conceitos, dados e metadados para uma determinada resposta.

O Gráfico de conhecimento consiste em subgráficos que são referenciados sempre que as consultas são enviadas:

* Dados de uso do cliente.
* Dados de uso do cliente em vários meta-armazenamentos.
* Documentação do Experience League.

Há duas classes de perguntas a serem consideradas antes de consultar o Assistente:

* **Questões de Conceito**: As perguntas conceituais são sobre conceitos de Adobe relacionados a dados ou públicos. Alguns exemplos de questões de conceito incluem:
   * Qual é a diferença entre a segmentação em lote e por transmissão?
   * Existem modelos de dados do setor e como usá-los?
   * Para que o Real-Time CDP é melhor usado?
* **Perguntas sobre uso**: perguntas sobre o uso são sobre os objetos de dados dentro da organização. Alguns exemplos de perguntas de uso incluem:
   * Quantos conjuntos de dados eu tenho?
   * Quantos atributos de esquema nunca foram usados?
   * Quais segmentos foram ativados?

>[!ENDSHADEBOX]

## Assistente de acesso na interface do Experience Platform

Para iniciar o Assistente, selecione o **[!UICONTROL Ícone do assistente]** no cabeçalho superior da interface do Experience Platform.

![A página inicial do Experience Platform, com o ícone Assistente selecionado e a interface do Assistente aberta.](./images/ai-assistant/ai-assistant.png)

A interface do Assistente é exibida, fornecendo imediatamente informações para começar. Você pode usar as opções fornecidas em [!UICONTROL Ideias para começar] para responder a perguntas e comandos como:

* [!UICONTROL Quais dos meus segmentos estão ativados?]
* [!UICONTROL O que é um esquema?]
* [!UICONTROL Conte-me alguns casos de uso comuns do Real-Time CDP]

![A seção &quot;ideias de introdução&quot; do Assistente.](./images/ai-assistant/ideas-to-get-started.png)

Para interagir com o Assistente, use a caixa de entrada para digitar suas consultas ou comandos. Você também pode usar o (**`+`**) para utilizar a função de preenchimento automático e o ícone de marcador para acessar suas consultas e comandos marcados.

![A caixa de entrada Assistente está realçada.](./images/ai-assistant/interact.png)

## Exemplo de caso de uso: usar o assistente para acelerar o processo de criação de esquema

>[!NOTE]
>
>O fluxo de trabalho a seguir é um exemplo que usa o processo de criação de esquema do evento de experiência para ilustrar como você pode usar o Assistente ao usar a interface do usuário do Experience Platform.

Considere um caso de uso em que você esteja criando uma **Esquema de evento de troca de dispositivo**. Durante o processo de criação do schema de evento de experiência, você encontra o `eventType` campo. &quot;Nesse ponto, você tem a opção de sair do workflow e consultar a [noções básicas de uma composição de esquema](../xdm/schema/composition.md) ou você pode usar o Assistente para recuperar respostas para suas perguntas e encontrar recursos adicionais através dos links de documentação recomendados pelo Assistente.&quot;

Para começar, digite sua pergunta na caixa de texto fornecida. No exemplo abaixo, o Assistente recebe a pergunta: &quot;**O que é o campo eventType em um esquema ExperienceEvent?**&quot;

![Assistente de Experience Platform com a seguinte pergunta preparada para consulta: &quot;Qual é o campo eventType em um esquema ExperienceEvent?](./images/ai-assistant/question.png)

O assistente então consulta sua base de conhecimento e calcula uma resposta. Após alguns instantes, o Assistente retornará uma resposta e sugestões relacionadas que você poderá usar como prompts de acompanhamento.

![Assistente de Experience Platform com uma resposta à consulta anterior.](./images/ai-assistant/answer.png)

Depois de receber uma resposta do Assistente, você pode selecionar entre várias opções para decidir como deseja continuar.

### Salve sua consulta {#save-your-query}

+++Selecione para exibir um exemplo de como salvar uma consulta

Para salvar a consulta, selecione o ícone de marcador ao lado da pergunta.

![Captura de tela de um marcador selecionado.](./images/ai-assistant/save-your-query.png)

Para acessar as consultas salvas, selecione o ícone de marcador abaixo da caixa de entrada e selecione a consulta que deseja executar.

![Captura de tela do ícone do marcador e uma lista de consultas salvas.](./images/ai-assistant/bookmarks.png)

+++

### Exibir dados em sua sandbox {#view-data-in-your-sandbox}

+++Selecione para exibir o exemplo

Dependendo do query, o Assistente fornece informações adicionais relacionadas aos dados da sandbox. Para exibir como a resposta à sua consulta se aplica à sandbox, selecione **[!UICONTROL Em sua sandbox].**

Durante essa etapa, o Assistente pode fornecer links diretos para as páginas da interface do usuário de determinados objetos em questão. No exemplo abaixo, o Assistente fornece links diretos para o [!UICONTROL Esquemas] e [!UICONTROL Segmentos] Páginas de interface do usuário.

![Captura de tela da opção &quot;Em sua sandbox&quot;.](./images/ai-assistant/in-your-sandbox.png)

+++

### Verificar a resposta {#verify-the-response}

+++Selecione para exibir um exemplo de como exibir fontes

Para exibir citações e validar a resposta do Assistente, selecione **[!UICONTROL Mostrar fontes]**. O assistente fornece links para a documentação que confirma sua resposta. Também é possível usar as consultas fornecidas pelo Assistente em [!UICONTROL Sugestões relacionadas] para explorar mais tópicos relacionados à sua consulta original.

![Captura de tela de &quot;Mostrar fontes&quot;.](./images/ai-assistant/show-sources.png)

+++

### Uso e visualização de dados {#data-usage-and-visualization}

+++Selecione para exibir um exemplo de perguntas de uso de dados e visualização de dados

Você pode consultar o Assistente sobre o uso de dados. Você deve estar em uma sandbox ativa para que o Assistente responda a uma pergunta de uso de dados relacionada aos dados em sua organização.

![Pergunta de acompanhamento sobre uso de dados.](./images/ai-assistant/data-usage-question.png)

Quando solicitado com uma pergunta sobre o uso de dados, o Assistente também fornece uma explicação de como ele calculou a resposta. No exemplo abaixo, o Assistente descreve as etapas executadas para exibir segmentos com mais de 1000 perfis e seus respectivos status de ativação.

![Faça uma pergunta complementar sobre segmentos que ilustram como o Assistente calculou a resposta.](./images/ai-assistant/results-explained.png)

Além disso, o Assistente renderiza gráficos para visualizar seus dados. Você também pode fornecer filtros e modificações aos seus queries e pode instruir o Assistente a renderizar seus achados com base nos filtros incluídos. Por exemplo, você pode pedir ao Assistente para mostrar uma tendência dos segmentos de contagem na ordem de sua data de criação, remover segmentos com total de perfis zero e usar nomes de meses em vez de números inteiros ao exibir os dados.

![Pergunta de acompanhamento que ilustra a visualização de dados.](./images/ai-assistant/data-visualization.png)

+++

### Usar preenchimento automático {#use-auto-complete}

+++Selecione para exibir um exemplo de preenchimento automático

Você pode usar a função de preenchimento automático para receber uma lista de objetos de dados que existem na sandbox. As recomendações de preenchimento automático estão disponíveis para os seguintes domínios: segmentos, esquemas, conjuntos de dados, fontes e destinos.

Você pode usar o preenchimento automático incluindo o símbolo de mais (**`+`**) na sua query. Como alternativa, você também pode selecionar o sinal de mais (**`+`**) localizado na parte inferior da caixa de entrada de texto. Uma janela é exibida com uma lista de objetos de dados recomendados da sandbox.

![Exemplo de preenchimento automático](./images/ai-assistant/auto-complete-one.png)

Em seguida, selecione o objeto de dados que deseja consultar para concluir a pergunta e, em seguida, envie a pergunta.

![Exemplo de preenchimento automático com pergunta e resposta](./images/ai-assistant/auto-complete-two.png)

+++

### Usar voltas múltiplas {#use-multi-turn}

+++Selecione para exibir um exemplo de curva múltipla

Você pode usar os recursos de várias rodadas do Assistant para ter uma conversa mais natural durante sua experiência. O assistente é capaz de responder perguntas de acompanhamento, fornecidas. contexto pode ser deduzido de uma interação anterior.

No exemplo abaixo, o Assistente é solicitado a fornecer o número total de fluxos de dados na organização atual.

![Exemplo de voltas múltiplas](./images/ai-assistant/multi-turn-one.png)

Em seguida, o Assistente recebe outra solicitação de acompanhamento. Desta vez, o Assistente responde listando os fluxos de dados que existem atualmente em sua organização.

![Exemplo de turno múltiplo com pergunta e resposta](./images/ai-assistant/multi-turn-two.png)

+++

## Escopo {#scope}

O assistente pode responder a perguntas sobre os conceitos do Real-Time CDP e do Experience Platform, bem como sobre o uso de dados específico da sua conta de usuário. O assistente também pode inferir o contexto com base na página da interface do usuário em que você está. Ele pode identificar:

* A conta de usuário que você está usando.
* A organização à qual você pertence.
* A página que você está visualizando na tela.
* O recurso (incluindo o tipo e a ID) que você está visualizando na tela.
* Como você está no processo de um determinado fluxo de trabalho de Experience Platform ou Real-Time CDP, o Assistente pode deduzir sua intenção.

### Documentação {#documentation}

Atualmente, o índice de documentação abrange o Adobe Experience Platform (Real-Time CDP e Públicos-alvo). O índice é atualizado periodicamente.

O modelo de recuperação de documentação é treinado em Experience Platform (Real-Time CDP e Audiences). Perguntas fora do escopo do Adobe Experience Platform, como, perguntas sobre outros produtos de Adobe como o Adobe Target e o Creative Cloud suite não podem ser respondidas.

### Uso de dados {#data-usage}

Você também pode fazer perguntas ao assistente sobre o uso de dados nos seguintes domínios:

* Atributos
* Conjuntos de dados
* Destinos _(Perguntas sobre contas e algumas perguntas sobre fluxo de dados não podem ser respondidas no momento.)_
* Esquemas _(Perguntas relacionadas a grupos de campos não podem ser respondidas neste momento.)_
* Segmentos
* Origens _(Perguntas relacionadas a contas não podem ser respondidas neste momento.)_

Para consultas de dados de uso, as respostas podem não refletir o estado atual da interface do usuário. Os dados que apóiam essas perguntas são atualizados uma vez a cada 24 horas. Por exemplo, as alterações que os usuários fazem no Real-Time CDP durante o dia são sincronizadas com os armazenamentos de dados à noite e, em seguida, ficam disponíveis para perguntas do usuário de manhã. Talvez seja necessário formatar as perguntas como: &quot;Quando foi o segmento com o título {TITLE} criado?&quot; em vez de, &quot;Quando foi o {TITLE} segmento criado?&quot;

Você precisará fazer logon em uma sandbox para consultar sobre dados específicos relacionados a objetos como esquemas, conjuntos de dados, atributos, destinos e segmentos.

### Exemplo de perguntas de uso de dados {#example-data-usage-questions}

+++Selecione para ver uma lista de perguntas de exemplo sobre uso de dados

| Tipo de pergunta | Descrição | Exemplos |
| --- | --- | --- | 
| Linhagem de dados | Rastrear o uso de um ou vários objetos em outros objetos Experience Platform | <ul><li>Quais conjuntos de dados usam {SCHEMA_NAME} esquema?</li><li>Quantos conjuntos de dados foram assimilados usando o mesmo esquema?</li><li>Quais conjuntos de dados foram usados nos segmentos ativados?</li><li>Liste os esquemas que têm atributos usados em segmentos ativados.</li><li>Mostrar os segmentos que estão ativados para {DESTINATION_ACCOUNT_NAME} e têm mais de 1000 perfis.</li><li>Mostrar os atributos usados nos segmentos ativados que foram modificados após janeiro de 2023.</li><li>Quais são os conjuntos de dados assimilados via {SOURCE_NAME}?</li><li>A quais fluxos de dados estão associados {DATAFLOW_NAME}</li><li>Liste os esquemas relacionados a segmentos ativados e que foram criados nos últimos 1 ano.</li></ul> |
| Distribuição e agregações | Perguntas baseadas em resumo sobre o uso do objeto Experience Platform | <ul><li>Qual é a porcentagem de segmentos ativados?</li><li>Quantos campos são usados na segmentação?</li><li>Quais segmentos são ativados para o maior número de destinos?</li><li>Listar segmentos duplicados.</li><li>Mostrar os segmentos ativados para {DESTINATION_ACCOUNT_NAME} e classificá-los por tamanho de perfil.</li><li>Qual é a porcentagem dos segmentos que não foram ativados, mas têm mais de 100 perfis. Mostre-me os nomes deles.</li><li>Listar os 3 conectores de origem que assimilam dados nos meus conjuntos de dados.</li><li>Liste os 5 principais atributos usados em segmentos ativados com base em sua ocorrência.</li></ul> |
| Pesquisa de objeto | Recupere ou acesse um objeto Experience Platform ou suas propriedades. | <ul><li>Quais conjuntos de dados não têm nenhum esquema associado a eles</li><li>Listar os atributos usados para {SEGMENT_NAME}?</li><li>Forneça a lista de esquemas que estão habilitados para perfil, mas que não foram modificados desde sua criação.</li><li>Quais segmentos foram modificados na última semana?</li><li>Liste os segmentos que têm as mesmas definições de segmento junto com sua data de criação.</li><li>Quais conjuntos de dados são ativados por perfil e também incluem quantos segmentos foram criados de cada conjunto de dados.</li><li>Quais contas de origem estão associadas ao conjunto de dados XYZ?</li><li>Mostrar a definição do segmento e a data de modificação de {SEGMENT_NAME}.</li></ul> |

+++

## Fornecer feedback {#feedback}

>[!BEGINSHADEBOX]

**Seu feedback é solicitado**

Durante esse estágio de Alpha, você é convidado a fornecer feedback sobre as respostas recebidas do Assistente. Todas as respostas e comentários enviados são revisados para continuar a melhorar a experiência do Assistente.

Para fornecer feedback, selecione polegares para cima ou para baixo depois de receber uma resposta do assistente e, em seguida, insira seu feedback na caixa de texto fornecida. Em seguida, selecione **[!UICONTROL Enviar feedback]** para enviar.

>[!ENDSHADEBOX]

+++Fornecer feedback

>[!BEGINTABS]

>[!TAB Polegar para cima]

Selecione o ícone de miniaturas para fornecer feedback sobre o que deu certo com sua experiência com o Assistente.

![A janela de feedback positivo.](./images/ai-assistant/thumbs-up.png)

>[!TAB Polegar para baixo]

Selecione o ícone com miniaturas para fornecer feedback sobre o que pode ser melhorado com base na sua experiência com o Assistente. Durante essa etapa, você também pode fornecer comentários específicos sobre a sua experiência. O feedback fornecido nos comentários é revisado diariamente.

![A janela de feedback negativo.](./images/ai-assistant/thumbs-down.png)

>[!TAB Sinalizador]

Selecione o ícone de sinalizador para fornecer mais relatórios sobre a sua experiência usando o Assistente.

![A janela de resultados do relatório.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Informações adicionais {#additional-information}

Consulte esta seção para obter informações adicionais sobre o Assistente de Experience Platform.

### Avisos e limitações {#caveats-and-limitations}

A seção a seguir descreve as limitações e limitações atuais a serem consideradas ao usar o Assistente.
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### Conversa pequena limitada

Você pode iniciar uma pequena conversa com o assistente, mas essa capacidade é atualmente limitada.

#### Perguntas sobre recursos

O assistente pode dar uma impressão imprecisa do que ele pode fazer. Ele pode responder incorretamente aos seguintes tipos de perguntas:

| Exemplo de pergunta | Observação |
| --- | --- |
| &quot;Você pode responder perguntas sobre {ENTITY}?&quot; | Se o Assistente conseguir encontrar uma única página fazendo referência a uma determinada entidade em seu índice, ele responderá sim. |
| &quot;Você sabe **x** idioma?&quot; | Atualmente, o Assistente só oferece suporte ao inglês, mas pode responder &quot;sim&quot;, pois o modelo subjacente é compatível com ele. |
| &quot;Você pode fazer...?&quot; | O assistente pode responder sim, mesmo que não possa. |

### Dicas {#tips}

A seção a seguir descreve algumas dicas e soluções alternativas a serem consideradas ao usar o Assistente.

#### As perguntas podem ser respondidas com a fonte de informações errada

Há casos em que sua pergunta sobre os dados de uso pode resultar em uma resposta com base na documentação. Isso ocorre porque o Assistente pode rotear incorretamente sua pergunta para a fonte de informações errada. Você pode evitar isso ao:

* Reformular sua pergunta para usar uma linguagem mais SQL
* Explicitamente chamando a fonte de informações a ser usada.

Leia a tabela abaixo para ver exemplos:

| Pergunta inválida | Boa pergunta | Notas |
| --- | --- | --- |
| Qual é meu maior segmento? | Qual é meu maior segmento? Uso de dados. | Informe explicitamente ao Assistente que você deseja que a resposta seja baseada em dados. |
| Qual é meu maior segmento? | Listar meu maior segmento. | Há casos em que uma pergunta &quot;o que...&quot; pode ser confundida com uma pergunta baseada em documentação. Usar um comando como &quot;lista&quot; é um indicador mais forte de que você está fazendo uma pergunta com dados em contexto. |
| Quantos conjuntos de dados eu tenho? | Contar meus conjuntos de dados. | A pergunta original funciona para segmentos, mas pode não funcionar com conjuntos de dados. |
