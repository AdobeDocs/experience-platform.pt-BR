---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;serviço de segmento;segmento;Segmento;Segmentos;segmentos
solution: Experience Platform
title: Visão geral do serviço de segmentação
description: Saiba mais sobre o Serviço de segmentação da Adobe Experience Platform e a função que ele desempenha no ecossistema da plataforma.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 11%

---

# Visão geral do [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] O fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos-alvo a partir da [!DNL Real-Time Customer Profile] dados. Esses segmentos são configurados e mantidos de forma centralizada [!DNL Platform]e são prontamente acessíveis por qualquer solução Adobe.

Este documento fornece uma visão geral de [!DNL Segmentation Service] e o papel que desempenha no Adobe Experience Platform.

## Introdução ao [!DNL Segmentation Service]

É importante entender os seguintes termos principais usados neste documento:

- **Segmentação**: dividir um grande grupo de indivíduos (como clientes, prospetos, usuários ou organizações) em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- **Definição de segmento**: o conjunto de regras usado para descrever as principais características ou o comportamento de um público-alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros do público-alvo qualificados para um segmento.
- **Público**: o conjunto de perfis que atendem aos critérios de uma definição de segmento.

## Como a segmentação funciona

A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seu tênis?&quot;, você pode querer um público de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra.

Depois que um segmento é definido conceitualmente, ele é incorporado [!DNL Experience Platform]. Normalmente, os segmentos são criados pelo profissional de marketing ou especialista em público-alvo, embora algumas organizações prefiram que sejam criados pelo departamento de marketing em colaboração com os analistas de dados. Ao examinar os dados enviados para o [!DNL Platform], o analista de dados compõe a definição do segmento selecionando quais campos e valores serão usados para criar as regras ou condições do segmento. Isso é feito usando a interface do usuário ou a API.

## Criar segmentos

Seja criado usando a API ou o [!DNL Segment Builder], os segmentos são definidos usando [!DNL Profile Query Language] (PQL). É aqui que a definição do segmento conceitual é descrita na linguagem criada para recuperar perfis que atendem aos critérios. Para obter mais informações, consulte [Visão geral do PQL](./pql/overview.md).

Para saber como criar e usar segmentos na [!DNL Segment Builder] (a implementação da interface do usuário do [!DNL Segmentation Service]), consulte a [Guia do Construtor de segmentos](./ui/overview.md).

Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial sobre [criação de segmentos de público-alvo usando a API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Caso um esquema seja estendido, todos os uploads futuros devem atualizar os campos recém-adicionados de acordo. Para obter mais informações sobre personalização [!DNL Experience Data Model] (XDM), visite o [Tutorial do Editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Além disso, se um valor de expiração de Evento de experiência estiver ativado no conjunto de dados, isso pode afetar a associação do segmento criado. Leia o guia em [Expirações do evento de experiência](../profile/event-expirations.md) para obter mais informações sobre como esse recurso pode afetar a segmentação.

## Avaliar segmentos {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Métodos de avaliação"
>abstract="Atualmente, a Platform aceita três métodos de avaliação de segmentos: segmentação de transmissão, segmentação em lote e segmentação de borda."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Avaliação de transmissão"
>abstract="A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza os segmentos em resposta à atividade do usuário."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=pt-BR" text="Avaliar eventos em tempo quase real com a segmentação de transmissão"

Atualmente, a Platform aceita três métodos de avaliação de segmentos: segmentação de transmissão, segmentação em lote e segmentação de borda.

### Segmentação de transmissão {#streaming}

A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza os segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada aos dados recebidos para [!DNL Real-Time Customer Profile]. As adições e remoções de segmentos são processadas regularmente, garantindo que o público-alvo permaneça relevante.

Para saber mais sobre a segmentação por transmissão, leia o [documentação de segmentação por transmissão](./api/streaming-segmentation.md).

### Segmentação em lote {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Avaliação em lote"
>abstract="Como alternativa a um processo de seleção de dados contínuo, a segmentação em lote move todos os dados do perfil de uma só vez por meio das definições de segmento para produzir públicos correspondentes. Depois de criado, o segmento é salvo e armazenado para que você possa exportá-lo para uso."

Como alternativa a um processo de seleção de dados contínuo, a segmentação em lote move todos os dados do perfil de uma só vez por meio das definições de segmento para produzir públicos correspondentes. Depois de criado, esse segmento é salvo e armazenado para que você possa exportá-lo para uso.

Os segmentos em lote são avaliados automaticamente a cada 24 horas. Se quiser avaliar um segmento em lote sob demanda, você poderá usar um trabalho de segmento. Para saber mais sobre tarefas do segmento, leia o [documentação de tarefas do segmento](./api/segment-jobs.md).

### Segmentação de borda {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Avaliação da borda"
>abstract="A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na Experience Edge, permitindo casos de uso de personalização da mesma página ou da próxima página."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=pt-BR" text="Guia da interface de segmentação de borda"

A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente [no Experience Edge](../edge/home.md), permitindo casos de uso de personalização de mesma página e próxima página.

Para saber mais sobre a segmentação de borda, leia as seções [Documentação da API](./api/edge-segmentation.md) ou o [Documentação da interface](./ui/edge-segmentation.md).

## Acessar resultados de segmentação

Para saber como acessar um segmento exportado, consulte [tutorial de avaliação de segmento](./tutorials/evaluate-a-segment.md).

## Metadados do segmento

Os metadados de segmento facilitam a indexação caso qualquer um dos segmentos seja reutilizado e/ou combinado.

Compor seus segmentos (por meio da API ou [!DNL Segment Builder]) exige a definição de um nome de segmento e uma política de mesclagem.

### Nomes de segmentos

Ao criar um novo segmento, você deve fornecer um nome de segmento. O nome do segmento é usado para identificar um segmento específico entre a coleção criada pelo [!DNL Segmentation Service]. Os nomes de segmentos devem, portanto, ser descritivos, concisos e exclusivos.

>[!NOTE]
>
>Ao planejar um segmento, lembre-se de que os segmentos podem ser referenciados de qualquer outro segmento e combinados com ele. Ao selecionar um nome, considere a possibilidade de seu segmento conter partes reutilizáveis.

### Políticas de mesclagem

As políticas de mesclagem são regras usadas pelo [!DNL Profile] para determinar como os dados serão priorizados e combinados em uma visualização unificada em determinadas condições.
Se uma política de mesclagem não estiver definida, o padrão [!DNL Platform] a política de mesclagem é usada. Se você preferir usar uma política de mesclagem específica para sua organização, poderá criar a sua própria e marcá-la como o padrão da organização.

Mais informações sobre políticas de mesclagem podem ser encontradas no [guia de políticas de mesclagem](../profile/api/merge-policies.md).

>[!NOTE]
>
>A estimativa de tamanhos de público-alvo é baseada na política de mesclagem de perfis padrão da organização.

### Outros metadados de segmento

Além do nome do segmento e da política de mesclagem, [!DNL Segment Builder] O oferece um campo de metadados &quot;descrição do segmento&quot; adicional, onde é possível resumir a finalidade da definição do segmento.

## Recursos avançados de segmentação

Os segmentos podem ser configurados para gerar continuamente um público-alvo de forma contínua ao combinar [assimilação de dados por transmissão](../ingestion/streaming-ingestion/overview.md) com qualquer um dos seguintes recursos avançados de segmentação:
- [Segmentação sequencial](#sequential)
- [Segmentação dinâmica](#dynamic)
- [Segmentação de várias entidades](#multi-entity)

Esses recursos avançados são discutidos com mais detalhes nas seções a seguir.

## Segmentação sequencial {#sequential}

Uma jornada de usuário padrão é de natureza sequencial. O Adobe Experience Platform permite definir uma série ordenada de segmentos para refletir essa jornada, capturando assim as sequências de eventos à medida que ocorrem. Organize os eventos na ordem desejada usando a linha do tempo do evento visual na [!DNL Segment Builder].

Um exemplo de jornada de cliente que exigiria segmentação sequencial seria exibição do produto > adição do produto > check-out > Sem compra.

## Segmentação dinâmica {#dynamic}

A segmentação dinâmica soluciona os problemas de escalabilidade que os profissionais de marketing costumam enfrentar ao criar segmentos para campanhas de marketing.

Diferentemente da segmentação estática, que requer que você capture explicitamente e repetidamente todos os casos de uso possíveis, a segmentação dinâmica usa variáveis para criar a lógica da regra e expressar relações dinamicamente.

### Caso de uso: procurar clientes que fazem compras fora de seu estado inicial

Para ilustrar o valor desse recurso avançado de segmentação, considere um arquiteto de dados colaborando com um profissional de marketing para identificar clientes que fizeram compras fora de seu estado inicial.

**O problema**

A segmentação estática exige que você defina segmentos individuais com um atributo exclusivo de estado inicial, antes de filtrar eventos de compra que não são iguais ao estado inicial. Um segmento explícito desse tipo diria &quot;Estou procurando pessoas de Utah, onde o estado de sua compra não é Utah&quot;. A criação de um público-alvo usando esse método requer a definição de um segmento para cada estado dos EUA, para um total de 50 segmentos.

Como resultado das diferentes combinações de segmentos que inevitavelmente surgem à medida que você dimensiona, o processo manual necessário para a segmentação estática se torna mais demorado, reduzindo a eficiência geral.

**A solução**

Ao atribuir uma variável ao atributo de estado de compra, o segmento dinâmico simplifica para &quot;Encontre-me uma compra em que o estado dessa compra não é igual ao estado inicial do cliente&quot;. Dessa forma, você pode consolidar 50 segmentos estáticos em um único segmento dinâmico.

## Segmentação de várias entidades {#multi-entity}

Com o recurso avançado de segmentação de várias entidades, você pode estender [!DNL Real-Time Customer Profile] dados com dados adicionais com base em produtos, lojas ou outras entidades não pessoais, também conhecidas como entidades de &quot;dimensão&quot;. Como resultado, [!DNL Segmentation Service] podem acessar campos adicionais durante a definição do segmento como se fossem nativos da variável [!DNL Profile] armazenamento de dados. A segmentação de várias entidades oferece flexibilidade ao identificar públicos com base em dados relevantes para suas necessidades comerciais exclusivas. Para obter mais informações, incluindo casos de uso e fluxos de trabalho, consulte [guia de segmentação de várias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de dados

[!DNL Segmentation Service] O suporta uma variedade de tipos de dados primitivos e complexos. Informações detalhadas, incluindo uma lista dos tipos de dados compatíveis, podem ser encontradas no [guia de tipos de dados suportados](./data-types.md).

## Próximas etapas

[!DNL Segmentation Service] O fornece um fluxo de trabalho consolidado para criar segmentos a partir do [!DNL Real-Time Customer Profile] dados. Em resumo:

- [!DNL Segmentation] é o processo de definir um subconjunto de perfis na sua loja de perfis, permitindo caracterizar o comportamento ou os atributos de um grupo comercializável desejado. [!DNL Segmentation Service] torna esse processo possível.
- Ao planejar um segmento, lembre-se de que ele pode ser referenciado de qualquer outro segmento e combinado com ele.
- Um segmento pode ser criado a partir de regras com base em dados de perfil, dados de séries de tempo relacionadas ou ambos.
- Os segmentos podem ser avaliados sob demanda ou continuamente. Quando avaliados sob demanda, todos os dados do perfil são transmitidos pelas definições de segmento de uma só vez. Quando avaliados continuamente, os dados fluem pelas definições de segmento à medida que entram [!DNL Platform].

Para saber como definir segmentos na interface do usuário do, consulte [Guia do Construtor de segmentos](./ui/overview.md). Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial sobre [criação de segmentos usando a API](./tutorials/create-a-segment.md).
