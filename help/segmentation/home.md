---
solution: Experience Platform
title: Visão geral do serviço de segmentação
description: Saiba mais sobre o Serviço de segmentação da Adobe Experience Platform e a função que ele desempenha no ecossistema da Experience Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 12%

---

# Visão geral do [!DNL Segmentation Service]

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma API RESTful que permite criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Experience Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

Este documento fornece uma visão geral do [!DNL Segmentation Service] e sua função no Adobe Experience Platform.

## Introdução ao [!DNL Segmentation Service]

Você deve entender os seguintes termos principais usados neste documento:

- **Público-alvo**: uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Essa coleção de pessoas pode ser gerada pelo Adobe Experience Platform usando definições de segmento (público-alvo gerado pela Experience Platform) ou de fontes externas (público-alvo gerado externamente).
- **Definição de segmento**: o conjunto de regras que a Adobe Experience Platform usa para descrever as principais características ou o comportamento de um público-alvo.
- **Segmento**: o ato de separar perfis em públicos.

## Como a segmentação funciona

A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de Perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seu tênis?&quot;, você pode querer um público de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra.

Depois que um público-alvo é definido conceitualmente, ele é incorporado no [!DNL Experience Platform]. Normalmente, os públicos-alvo são criados pelo profissional de marketing ou especialista em público-alvo, embora algumas organizações prefiram que sejam criados pelo departamento de marketing em colaboração com os analistas de dados. Ao revisar os dados que estão sendo enviados para [!DNL Experience Platform], o analista de dados pode criar o público-alvo de duas maneiras: criando uma definição de segmento e selecionando quais campos e valores serão usados para criar as regras ou condições do público-alvo, ou compondo um público-alvo usando a Composição de público-alvo.

## Criar públicos-alvo

Você pode criar públicos-alvo de várias maneiras no Adobe Experience Platform, incluindo por meio de composições, definições de segmento, dados federados e Data Distiller.

### Composição de público-alvo

Ao compor um público diretamente no Experience Platform, você pode usar a Composição de público. Para saber como usar a Composição de público-alvo para criar um público-alvo, leia o [Guia de Composição de Público-alvo](./ui/audience-composition.md) para obter mais informações.

### Definições de segmento

Quer sejam criadas usando a API ou o [!DNL Segment Builder], as definições de segmento são finalmente definidas usando o [!DNL Profile Query Language] (PQL). É aqui que a definição do segmento conceitual é descrita na linguagem criada para recuperar perfis que atendem aos critérios. Para obter mais informações, consulte a [visão geral do PQL](./pql/overview.md).

Para saber como criar e usar segmentos no [!DNL Segment Builder] (a implementação da interface do usuário do [!DNL Segmentation Service]), consulte o [guia do Construtor de segmentos](./ui/segment-builder.md).

Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial sobre [criação de definições de segmento usando a API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Caso um esquema seja estendido, todos os uploads futuros devem atualizar os campos recém-adicionados de acordo. Para obter mais informações sobre a personalização do [!DNL Experience Data Model] (XDM), visite o [tutorial do Editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Além disso, se um valor de expiração de Evento de experiência estiver ativado no conjunto de dados, isso pode afetar a associação da definição de segmento criada. Leia o guia em [Expirações do evento de experiência](../profile/event-expirations.md) para obter mais informações sobre como esse recurso pode afetar a segmentação.

### Composição de público-alvo federado {#fac}

Além das composições de público-alvo e definições de segmento, você pode usar a Adobe Federated Audience Composition para criar novos públicos-alvo a partir de conjuntos de dados corporativos sem copiar os dados subjacentes e armazená-los no Adobe Experience Platform Audience Portal. Você também pode enriquecer os públicos-alvo existentes no Adobe Experience Platform utilizando dados de público-alvo compostos que foram federados a partir do data warehouse corporativo. Leia o guia em [Composição de Público-Alvo Federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/home).

## Avaliar públicos-alvo {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Métodos de avaliação"
>abstract="Atualmente, a Experience Platform aceita três métodos de avaliação de públicos-alvo: segmentação de transmissão, segmentação em lote e segmentação de borda."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Avaliação de transmissão"
>abstract="A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza os públicos-alvo em resposta à atividade do usuário."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/streaming-segmentation.html" text="Avaliar eventos em tempo quase real com a segmentação de transmissão"

Atualmente, a Experience Platform aceita três métodos de avaliação de públicos-alvo: segmentação de transmissão, segmentação em lote e segmentação de borda.

### Segmentação de transmissão {#streaming}

A segmentação por transmissão é um processo contínuo de seleção de dados que atualiza os públicos-alvo em resposta à atividade do usuário. Depois que um público-alvo é criado e salvo, a definição do segmento é aplicada contra os dados recebidos para [!DNL Real-Time Customer Profile]. As adições e remoções para o público-alvo são processadas regularmente, garantindo que o público-alvo permaneça relevante.

Para saber mais sobre a segmentação por transmissão, leia a [documentação sobre segmentação por transmissão](./methods/streaming-segmentation.md).

### Segmentação em lote {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Avaliação em lote"
>abstract="Como alternativa a um processo de seleção de dados contínuo, a segmentação em lote move todos os dados do perfil de uma só vez por meio das definições de segmento para produzir públicos-alvos correspondentes. Depois de criado, o público-alvo é salvo e armazenado para que você possa exportá-lo para uso."

Como alternativa a um processo de seleção de dados contínuo, a segmentação em lote move todos os dados do perfil de uma só vez por meio das definições de segmento para produzir públicos-alvos correspondentes. Depois de criado, o público-alvo resultante é salvo e armazenado para que você possa exportá-lo para uso.

Os públicos-alvo em lote são avaliados automaticamente a cada 24 horas. Se quiser avaliar um público-alvo em lote sob demanda, você pode usar um trabalho de segmento. Para saber mais sobre trabalhos de segmento, leia a [documentação de trabalhos de segmento](./api/segment-jobs.md).

### Segmentação de borda {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Avaliação da borda"
>abstract="A segmentação de borda é a capacidade de avaliar segmentos na Edge Network da Experience Platform instantaneamente, permitindo casos de uso de personalização da mesma página ou da próxima página."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/edge-segmentation.html" text="Guia de segmentação de borda"

A segmentação do Edge é a capacidade de avaliar segmentos no Experience Platform instantaneamente [no Edge Network](../landing/edge-and-hub-comparison.md), permitindo casos de uso de personalização de mesma página e próxima página.

Para saber mais sobre a segmentação de borda, leia a [visão geral da segmentação de borda](./methods/edge-segmentation.md).

## Acessar resultados de segmentação

Para saber como acessar um público exportado, consulte o [tutorial de avaliação de definição de segmento](./tutorials/evaluate-a-segment.md).

## Metadados de definição de segmento

Os metadados de definição de segmento facilitam a indexação caso qualquer um dos públicos-alvo seja reutilizado e/ou combinado.

A composição de uma definição de segmento (por meio da API ou do [!DNL Segment Builder]) requer a definição de um nome e uma política de mesclagem.

### Nomes de definição de segmento

Ao criar uma nova definição de segmento, você deve fornecer um nome. O nome da definição de segmento é usado para identificar uma definição de segmento específica entre a coleção criada por [!DNL Segmentation Service]. Portanto, os nomes de definição de segmento devem ser descritivos, concisos e exclusivos.

>[!NOTE]
>
>Ao planejar uma definição de segmento, lembre-se de que as definições de segmento podem ser referenciadas e combinadas com qualquer outra definição de segmento. Ao selecionar um nome, considere a possibilidade de que a definição do segmento possa conter partes reutilizáveis.

### Mesclar políticas

As políticas de mesclagem são regras usadas por [!DNL Profile] para determinar como os dados serão priorizados e combinados em uma exibição unificada em determinadas condições.

Se uma política de mesclagem não estiver definida, a política de mesclagem padrão [!DNL Experience Platform] será usada. Se você preferir usar uma política de mesclagem específica para sua organização, poderá criar a sua própria e marcá-la como o padrão da organização.

Mais informações sobre políticas de mesclagem podem ser encontradas no [guia de políticas de mesclagem](../profile/api/merge-policies.md).

>[!NOTE]
>
>A estimativa de tamanhos de público-alvo é baseada na política de mesclagem de perfis padrão da organização.

### Outros metadados de definição de segmento

Além da política de nome e mesclagem, o [!DNL Segment Builder] oferece um campo de metadados de descrição adicional, onde você pode resumir a finalidade da definição do segmento.

## Recursos avançados de segmentação

As definições de segmento podem ser configuradas para gerar continuamente um público-alvo de forma contínua, combinando a [assimilação de dados por transmissão](../ingestion/streaming-ingestion/overview.md) com qualquer um dos seguintes recursos avançados de segmentação:

- [Segmentação sequencial](#sequential)
- [Segmentação dinâmica](#dynamic)
- [Segmentação de várias entidades](#multi-entity)

Esses recursos avançados são discutidos com mais detalhes nas seções a seguir.

### Segmentação sequencial {#sequential}

Uma jornada de usuário padrão é de natureza sequencial. O Adobe Experience Platform permite definir uma série ordenada de públicos para refletir essa jornada, capturando assim as sequências de eventos que ocorrem. Você pode organizar os eventos na ordem desejada usando a linha do tempo do evento visual no [!DNL Segment Builder].

Um exemplo de jornada de cliente que exigiria segmentação sequencial seria exibição do produto > adição do produto > check-out > Sem compra.

### Segmentação dinâmica {#dynamic}

A segmentação dinâmica soluciona os problemas de escalabilidade que os profissionais de marketing costumam enfrentar ao criar públicos-alvo para campanhas de marketing.

Diferentemente da segmentação estática, que requer que você capture explicitamente e repetidamente todos os casos de uso possíveis, a segmentação dinâmica usa variáveis para criar a lógica da regra e expressar relações dinamicamente.

Para ilustrar o valor desse recurso avançado de segmentação, considere um arquiteto de dados colaborando com um profissional de marketing para identificar clientes que fizeram compras fora de seu estado inicial.

A segmentação estática exige que você defina segmentos individuais com um atributo exclusivo de estado inicial, antes de filtrar eventos de compra que não são iguais ao estado inicial. Uma definição de segmento explícita desse tipo diria &quot;Estou procurando pessoas de Utah, onde o estado de sua compra não é Utah&quot;. A criação de um público-alvo usando esse método requer a definição de um segmento para cada estado dos EUA, para um total de 50 segmentos.

Como resultado das diferentes combinações de definição de segmento que inevitavelmente surgem à medida que você dimensiona, o processo manual necessário para a segmentação estática se torna mais demorado, reduzindo a eficiência geral.

Ao atribuir uma variável ao atributo de estado de compra, a definição de segmento dinâmico simplifica para &quot;Encontre-me uma compra em que o estado dessa compra não é igual ao estado inicial do cliente&quot;. Dessa forma, você pode consolidar 50 segmentos estáticos em uma única definição de segmento dinâmico.

### Segmentação de várias entidades {#multi-entity}

Com o recurso avançado de segmentação de várias entidades, você pode estender dados do [!DNL Real-Time Customer Profile] com dados adicionais com base em produtos, lojas ou outras entidades que não sejam de pessoas, também conhecidas como entidades de &quot;dimensão&quot;. Como resultado, [!DNL Segmentation Service] pode acessar campos adicionais durante a definição do segmento como se fossem nativos do armazenamento de dados [!DNL Profile]. A segmentação de várias entidades oferece flexibilidade ao identificar públicos com base em dados relevantes para suas necessidades comerciais exclusivas. Para obter mais informações, incluindo casos de uso e fluxos de trabalho, consulte o [guia de segmentação de várias entidades](./tutorials/multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de dados

[!DNL Segmentation Service] dá suporte a uma variedade de tipos de dados primitivos e complexos. Informações detalhadas, incluindo uma lista de tipos de dados com suporte, podem ser encontradas no [guia de tipos de dados com suporte](./data-types.md).

## Próximas etapas

[!DNL Segmentation Service] fornece um fluxo de trabalho consolidado para compilar audiências a partir de dados [!DNL Real-Time Customer Profile].

Para obter mais informações sobre como usar a interface do usuário do Serviço de segmentação, leia a [Visão geral da interface do usuário do serviço de segmentação](./ui/overview.md).

Para saber como compor públicos-alvo na interface do usuário, leia o [Guia de composição de público-alvo](./ui/audience-composition.md). Para saber como definir definições de segmentos na interface, consulte o [guia do Construtor de segmentos](./ui/overview.md). Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial sobre [criação de definições de segmento usando a API](./tutorials/create-a-segment.md).
