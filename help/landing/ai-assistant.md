---
title: Assistente de IA para o Adobe Experience Platform
description: Saiba como usar o Assistente de IA para navegar e entender os conceitos do Experience Platform e do Real-time Customer Data Platform, além de informações de uso sobre seus objetos.
badge: Alfa
hide: true
hidefromtoc: true
source-git-commit: 704d47b0e37825508705402ab2401636f46ef23f
workflow-type: tm+mt
source-wordcount: '2369'
ht-degree: 0%

---

# Assistente de IA para o Adobe Experience Platform

>[!NOTE]
>
>O Assistente de IA do Adobe Experience Platform está atualmente em Alfa. O recurso e a documentação estão sujeitos a alterações.

O Assistente de IA para Adobe Experience Platform é um recurso de interface do usuário que você pode usar para navegar e entender os conceitos de Experience Platform e Real-time Customer Data Platform, além de informações de uso sobre seus objetos.

Você pode consultar o Assistente de IA para obter informações como:

* Orientação sobre como executar tarefas relacionadas a dados e públicos.
* Status e métricas dos objetos de dados existentes em sua organização.
* Exemplos de casos de uso e nuances para entender melhor seus objetos de dados, incluindo atributos, conjuntos de dados, destinos, esquemas, segmentos e fontes.

Este documento fornece informações sobre como acessar e usar o Assistente de IA para fazer perguntas e receber respostas sobre os conceitos do Experience Platform e do Real-Time CDP.

>[!BEGINSHADEBOX]

**Como funciona o Assistente de IA?**

O Assistente de IA responde às perguntas enviadas consultando um banco de dados e, em seguida, traduzindo os dados do banco de dados em uma resposta legível.

Essa representação interna de dados subjacentes também é conhecida como Gráfico de conhecimento - uma Web abrangente de conceitos, dados e metadados para uma determinada resposta.

O Gráfico de conhecimento consiste em subgráficos que são referenciados sempre que as consultas são enviadas:

* Dados de uso do cliente.
* Dados de uso do cliente em vários meta-armazenamentos.
* Documentação do Experience League.

Há duas classes de perguntas a serem consideradas antes de consultar o Assistente de IA:

* **Questões de Conceito**: As perguntas conceituais são sobre conceitos de Adobe relacionados a dados ou públicos. Alguns exemplos de questões de conceito incluem:
   * Qual é a diferença entre a segmentação em lote e por transmissão?
   * Existem modelos de dados do setor e como usá-los?
   * Para que o Real-Time CDP é melhor usado?
* **Perguntas sobre uso**: perguntas sobre o uso são sobre os objetos de dados dentro da organização. Alguns exemplos de perguntas de uso incluem:
   * Quantos conjuntos de dados eu tenho?
   * Quantos atributos de esquema nunca foram usados?
   * Quais segmentos foram ativados?

>[!ENDSHADEBOX]

## Acessar o assistente de IA para o Experience Platform na interface do usuário

Você pode acessar o Assistente de IA na navegação do cabeçalho na interface do usuário do Experience Platform.

Selecione o **[!UICONTROL Ícone do Assistente de IA]** no cabeçalho para iniciar o painel Assistente de IA.

![A página inicial da interface do usuário do Experience Platform com o ícone do Assistente do AI selecionado.](./images/ai-assistant/ai-assistant.png)

Aqui, você pode inserir sua pergunta na caixa de texto e consultar o Assistente de IA para obter conceitos sobre dados ou públicos. Você também pode fazer perguntas sobre os objetos de dados para entender melhor como usá-los no respectivo caso de uso.

### Exemplo de caso de uso: usar o Assistente de IA para acelerar o processo de criação de esquema

>[!NOTE]
>
>O exemplo de fluxo de trabalho a seguir usa o processo de criação de esquema ExperienceEvent para ilustrar como você pode usar o Assistente de IA ao usar a interface do usuário do Experience Platform.

Considere um caso de uso em que você esteja criando uma **Esquema de evento de troca de dispositivo**. Durante o processo de criação do schema ExperienceEvent, você encontra o `eventType` campo. Nesse ponto, é possível sair do workflow e consultar a documentação no [noções básicas de uma composição de esquema](../xdm/schema/composition.md), ou você pode usar o Assistente de IA para recuperar respostas imediatas para suas perguntas.

Para começar, insira sua pergunta na caixa de texto fornecida. No exemplo abaixo, o Assistente de IA recebe a pergunta: &quot;**O que é o campo eventType em um esquema de Evento de experiência?**&quot;

![O Assistente de IA para o Experience Platform com a seguinte pergunta preparada para consulta: &quot;Qual é o campo eventType em um esquema ExperienceEvent?](./images/ai-assistant/question.png)

O Assistente de IA consulta sua base de conhecimento e calcula uma resposta. Após alguns minutos, o Assistente de IA retorna uma resposta e sugestões relacionadas que você pode usar como prompts de acompanhamento.

![O Assistente de IA para o Experience Platform com uma resposta à consulta anterior.](./images/ai-assistant/answer.png)

Você pode saber mais sobre um tópico específico fazendo uma pergunta complementar. No próximo exemplo, o Assistente de IA é perguntado como o eventType pode ser usado na segmentação.

![Uma pergunta e resposta de acompanhamento são exibidas no Assistente de IA para Experience Platform.](./images/ai-assistant/follow-up-answer.png)

Você também pode fazer perguntas ao Assistente de IA sobre o uso de dados. Ao perguntar sobre o uso de dados, você deve estar em uma sandbox ativa para que o Assistente de IA responda à sua consulta.

![Uma pergunta sobre o uso de dados, perguntando quantos segmentos um usuário tem.](./images/ai-assistant/data-usage-question.png)

Com cada resposta, o assistente de IA fornece uma maneira de validar a resposta visualizando a origem. Links para a documentação são fornecidos para perguntas de conceito, enquanto perguntas sobre o uso de dados podem ser verificadas com uma consulta SQL que demonstra como a resposta foi calculada.

>[!BEGINSHADEBOX]

**Seu feedback é solicitado**

Durante esse estágio Alfa, você é convidado a fornecer feedback sobre as respostas recebidas do Assistente de IA. Todas as respostas e comentários enviados são revisados para continuar a melhorar a experiência do Assistente de IA.

Para fornecer feedback, selecione polegares para cima ou para baixo depois de receber uma resposta do Assistente de IA e, em seguida, insira seu feedback na caixa de texto fornecida. Em seguida, selecione **[!UICONTROL Enviar feedback]** para enviar.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB Mostrar origem]

Selecionar **[!UICONTROL Mostrar origem]** para obter uma lista de links para a documentação que o Assistente de IA faz referência para calcular sua resposta.

![Os links para a origem exibidos no Assistente do AI.](./images/ai-assistant/show-sources.png)

>[!TAB Polegar para cima]

Selecione o ícone de miniatura para fornecer feedback sobre o que aconteceu de bom com a sua experiência com o Assistente de IA.

![A janela de feedback positivo.](./images/ai-assistant/positive-feedback.png)

>[!TAB Polegar para baixo]

Selecione o ícone com miniaturas para fornecer feedback sobre o que pode ser melhorado com base na sua experiência com o Assistente de IA. Durante essa etapa, você também pode fornecer comentários específicos sobre a sua experiência. O feedback fornecido nos comentários é revisado diariamente.

![A janela de feedback negativo.](./images/ai-assistant/negative-feedback.png)

>[!TAB Sinalizador]

Selecione o ícone de sinalizador para fornecer mais relatórios sobre a experiência usando o Assistente de IA.

![A janela de resultados do relatório.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### Ideias para começar

Você também pode usar os prompts predefinidos fornecidos pelo Assistente de IA para começar.

![Os prompts fornecidos no painel do Assistente de IA.](./images/ai-assistant/ideas.png)

## Informações adicionais

Consulte esta seção para obter informações adicionais sobre o Assistente de IA para o Experience Platform.

### Escopo

O Assistente de IA pode responder a consultas com base na documentação e no uso de dados.

#### Documentação

Você pode fazer perguntas sobre a documentação com base no Real-time Customer Data Platform e no Audiences. Atualmente, o índice de documentação abrange o Adobe Experience Platform (Real-Time CDP e Públicos-alvo). O índice é atualizado periodicamente.

O modelo de recuperação de documentação é treinado em Experience Platform (Real-Time CDP e Audiences). Perguntas fora do escopo do Adobe Experience Platform, como, perguntas sobre outros produtos de Adobe como o Adobe Target e o Creative Cloud suite não podem ser respondidas.

#### Uso de dados

Você também pode fazer perguntas ao Assistente de IA sobre o uso de dados nos seguintes domínios:

* Atributos
* Conjuntos de dados
* Destinos (Perguntas sobre contas e algumas perguntas sobre o fluxo de dados não podem ser respondidas no momento.)
* Esquemas (perguntas relacionadas a grupos de campos não podem ser respondidas no momento.)
* Segmentos
* Fontes (Perguntas relacionadas a contas não podem ser respondidas neste momento.)

Para consultas de dados de uso, as respostas podem não refletir o estado atual da interface do usuário. Os dados que apóiam essas perguntas são atualizados uma vez a cada 24 horas. Por exemplo, as alterações que os usuários fazem no Real-Time CDP durante o dia são sincronizadas com os armazenamentos de dados à noite e, em seguida, ficam disponíveis para perguntas do usuário de manhã. Talvez seja necessário formatar as perguntas como: &quot;Quando foi o segmento com o título {TITLE} criado?&quot; em vez de, &quot;Quando foi o {TITLE} segmento criado?&quot;

Você precisará fazer logon em uma sandbox para consultar sobre dados específicos relacionados a objetos como esquemas, conjuntos de dados, atributos, destinos e segmentos.

### Perguntas de uso de dados compatíveis

+++Selecione para exibir uma lista de perguntas sobre o uso de dados com suporte

Veja a seguir uma lista de perguntas sobre o uso de dados com suporte no momento, agrupadas por domínio.

* Listar os atributos usados para este segmento?
* Quantos segmentos há no total?
* Mostre-me uma lista de segmentos que foram modificados pela última vez no mês passado.
* Quais segmentos foram modificados na última semana?
* Para que serve a contagem de perfis? {SEGMENT_NAME} segmento?
* Listar todos os segmentos duplicados.
* Mostre-me os segmentos criados ou atualizados nos últimos 7 dias.
* Qual é a distribuição do número de perfis entre segmentos?
* Quantos campos são usados na segmentação?
* Qual é a contagem total de segmentos ativados?
* Quais segmentos são ativados?
* Quantos segmentos duplicados são ativados?
* Listar segmentos que foram criados no ano passado.
* Mostrar os segmentos que foram modificados pela última vez antes {DATE}.
* Quantos nomes de segmento exclusivos estão associados à variável {SCHEMA_NAME} esquema?
* Quais esquemas são usados com mais frequência em segmentos?
* Quantos esquemas eu tenho?
* Quais conjuntos de dados usam {SCHEMA_NAME} esquema?
* Lista todos os esquemas modificados na última semana.
* Quantos esquemas são ativados por perfil?
* Listar todos os esquemas da classe de evento de experiência?
* Quais conjuntos de dados são assimilados na {SCHEMA_NAME} esquema?
* Quantos conjuntos de dados foram assimilados usando o mesmo esquema?
* Quantos conjuntos de dados eu tenho?
* Quais conjuntos de dados são usados em cada segmento?
* Quais segmentos usam {ATTRIBUTE_NAME} atributo?
* Quais esquemas têm {ATTRIBUTE_NAME} atributo nelas?
* Quantos atributos de esquema XDM não são usados em nenhum segmento?
* Em quais conjuntos de dados estão {ATTRIBUTE_NAME} Campos XDM preenchidos?
* Quais conjuntos de dados têm dados para {ATTRIBUTE_NAME} atributo?
* Quantos segmentos são ativados para cada destino?
* Quais segmentos são ativados para o maior número de destinos?
* Algum dos meus segmentos tem 0 perfis?
* Quantos fluxos de dados eu tenho?

+++

### Experiência de conversa

Você deve considerar várias nuances relacionadas à experiência de conversação ao consultar o Assistente de IA.

>[!NOTE]
>
>Essas limitações são temporárias e estão sendo aprimoradas durante todo o trajeto alfa.

>[!BEGINTABS]

>[!TAB Não foi possível inferir o contexto da discussão anterior]

No momento, o Assistente de IA não pode fazer referência a discussões anteriores como contexto para uma determinada pergunta. Consulte a tabela abaixo para obter exemplos:

| Pergunta ambígua | Limpar pergunta | Observação |
| --- | --- | --- |
| <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Há diferentes tipos deles?&quot;</li></ul> | <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Há diferentes tipos de **segmentos**?&quot;</li></ul> | O Assistente de IA não pode inferir o que &quot;eles&quot; significa. |
| <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Você pode elaborar mais?&quot;</li></ul> | <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Explicar o que é um segmento em profundidade&quot;</li></ul> | O Assistente de IA não pode fazer referência inteligente à documentação com base em &quot;mais&quot;. |
| <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Você pode me dar um exemplo de um?&quot;</li></ul> | <ul><li>Primeira pergunta: &quot;O que é um segmento?&quot;</li><li>Pergunta complementar: &quot;Você pode me dar um exemplo de um segmento?&quot;</li></ul> | O Assistente de IA não pode inferir o que você deseja como exemplo de. |
| <ul><li>Primeira pergunta: &quot;O que é um segmento em lote?&quot;</li><li>Pergunta complementar: &quot;Como ele se compara a um segmento de transmissão?&quot;</li></ul> | <ul><li>Primeira pergunta: &quot;O que é um segmento em lote?&quot;</li><li>Pergunta de acompanhamento: &quot;É possível comparar um segmento de transmissão a um segmento em lote?&quot;</li></ul> | O Assistente de IA não consegue inferir o que &quot;ele&quot; está referindo e, portanto, não pode comparar o segmento de transmissão. |
| <ul><li>Primeira pergunta: &quot;Quantos segmentos eu tenho?&quot;</li><li>Pergunta complementar: &quot;Quantos deles usam o Facebook como destino?&quot;</li></ul> | <ul><li>Primeira pergunta: &quot;Quantos segmentos eu tenho?&quot;</li><li>Pergunta de acompanhamento: &quot;Quantos segmentos que tenho estão usando o Facebook como destino?&quot;</li></ul> | O Assistente de IA não pode inferir a que &quot;eles&quot; se refere. |

{style="table-layout:auto"}

>[!TAB Não é possível inferir o contexto de uma página]

Ao perguntar ao Assistente de IA sobre um elemento específico da página de interface do usuário do Experience Platform em que você está, é necessário definir claramente o elemento específico na pergunta.

| Pergunta ambígua | Limpar pergunta | Observação |
| --- | --- | --- |
| &quot;O que isso faz?&quot; | &quot;O que {PAGE_NAME} fazer? | O Assistente de IA não pode inferir a que &quot;isso&quot; se refere. Você deve fornecer o elemento de página específico sobre o qual está consultando. |
| &quot;Por que não economiza?&quot; | &quot;Por que não posso salvar uma nova sandbox chamada {NAME}?&quot; | O Assistente de IA não pode inferir o que &quot;ele&quot; está referindo e não pode saber que você está tendo problemas com uma entidade. |

{style="table-layout:auto"}

Além disso, o Assistente de IA só pode responder a perguntas relacionadas a mensagens de erro, já que o erro está documentado no Experience League.

>[!TAB Ambiguidade]

Você deve formular suas perguntas claramente e defini-las em um produto, aplicativo ou domínio, já que o Assistente de IA não pode atualmente desfazer a ambiguidade das perguntas.

| Pergunta ambígua | Limpar pergunta | Observação |
| --- | --- | --- |
| &quot;Como criar um filtro? | Como criar um filtro na Linguagem de consulta de perfil? | Você deve especificar o recurso para o qual está filtrando, pois vários recursos de Experience Platform suportam filtragem. |
| &quot;Como começar? | Como começar a usar destinos? | Você deve esclarecer suas metas e caso de uso, pois conceitos muito amplos podem resultar em respostas genéricas ou desnecessariamente específicas. |

{style="table-layout:auto"}

>[!ENDTABS]

### Conversa pequena limitada

Você pode iniciar uma pequena conversa com o Assistente de IA, mas essa capacidade é limitada no momento.

### Perguntas sobre recursos

O Assistente de IA pode dar uma impressão imprecisa do que pode fazer. Ele pode responder incorretamente aos seguintes tipos de perguntas:

| Exemplo de pergunta | Observação |
| --- | --- |
| &quot;Você pode responder perguntas sobre {ENTITY}?&quot; | Desde que o Assistente de IA possa encontrar uma única página fazendo referência a uma determinada entidade em seu índice, ele responderá sim. |
| &quot;Você sabe **x** idioma?&quot; | Atualmente, o Assistente de IA só oferece suporte ao inglês, mas pode responder &quot;sim&quot;, pois o modelo subjacente é compatível. |
| &quot;Você pode fazer...?&quot; | O Assistente de IA pode responder sim, mesmo que não possa. |

### Dicas

#### As perguntas podem ser respondidas com a fonte de informações errada

Há casos em que sua pergunta sobre os dados de uso pode resultar em uma resposta com base na documentação. Isso ocorre porque o Assistente de IA pode rotear incorretamente sua pergunta para a fonte de informações errada. Você pode evitar isso ao:

* Reformular sua pergunta para usar uma linguagem mais SQL
* Explicitamente chamando a fonte de informações a ser usada.

Leia a tabela abaixo para ver exemplos:

| Pergunta inválida | Boa pergunta | Notas |
| --- | --- | --- |
| Qual é meu maior segmento? | Qual é meu maior segmento? Uso de dados. | Informe explicitamente ao Assistente de IA que você deseja que a resposta seja baseada em dados. |
| Qual é meu maior segmento? | Listar meu maior segmento. | Há casos em que uma pergunta &quot;o que...&quot; pode ser confundida com uma pergunta baseada em documentação. Usar um comando como &quot;lista&quot; é um indicador mais forte de que você está fazendo uma pergunta com dados em contexto. |
| Quantos conjuntos de dados eu tenho? | Contar meus conjuntos de dados. | A pergunta original funciona para segmentos, mas pode não funcionar com conjuntos de dados. |