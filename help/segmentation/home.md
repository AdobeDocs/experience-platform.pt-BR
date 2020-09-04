---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Serviço de segmentação do Adobe Experience Platform
topic: overview
description: Este documento fornece uma visão geral do Serviço de segmentação e o papel que ele desempenha no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

A Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform]e são prontamente acessíveis por qualquer solução de Adobe.

Este documento fornece uma visão geral sobre [!DNL Segmentation Service] e o papel que desempenha no Adobe Experience Platform.

## Getting started with [!DNL Segmentation Service]

É importante entender os seguintes termos principais usados em todo o documento:

- **Segmentação**: Dividindo um grande grupo de indivíduos (como clientes, prospectos, usuários ou organizações) em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- **Definição** do segmento: O conjunto de regras usado para descrever as principais características ou comportamento de uma audiência de público alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros da audiência qualificados para um segmento.
- **Audiência**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Como a segmentação funciona

A segmentação é o processo de definição de atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para diferenciar um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você esqueceu de comprar seus tênis?&quot;, você pode querer uma audiência de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra.

Depois que um segmento é definido conceitualmente, ele é incorporado [!DNL Experience Platform]. Normalmente, os segmentos são criados pelo profissional de marketing ou pelo especialista em audiências, embora algumas organizações prefiram que sejam criados pelo departamento de marketing, em colaboração com seus analistas de dados. Ao revisar os dados para [!DNL Platform]os quais estão sendo enviados, o analista de dados compõe a definição do segmento selecionando quais campos e valores serão usados para criar as regras ou condições do segmento. Isso é feito usando a interface do usuário ou a API.

## Criar segmentos

Independentemente de serem criados usando a API ou a API, os segmentos são definidos por meio do [!DNL Segment Builder]PQL [!DNL Profile Query Language] (apenas em inglês). É aqui que a definição do segmento conceitual é descrita na linguagem criada para recuperar perfis que atendem aos critérios. Para obter mais informações, consulte a visão geral [do](./pql/overview.md)PQL.

Para saber como criar e usar segmentos na [!DNL Segment Builder] (a implementação da interface do usuário de [!DNL Segmentation Service]), consulte o guia [do Construtor de](./ui/overview.md)segmentos.

Para obter informações sobre como criar definições de segmentos usando a API, consulte o tutorial sobre como [criar segmentos de audiência usando a API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>No evento em que um schema é estendido, todos os uploads futuros devem atualizar os campos recém-adicionados de acordo. Para obter mais informações sobre a personalização [!DNL Experience Data Model] (XDM), visite o tutorial [do Editor de](../xdm/tutorials/create-schema-ui.md)Schemas.

## Avaliar segmentos

### Segmentação em streaming

A segmentação de fluxo é um processo contínuo de seleção de dados que atualiza seus segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos para [!DNL Real-time Customer Profile]. Adições e remoções do segmento são processadas regularmente, garantindo que sua audiência do público alvo permaneça relevante.

Para saber mais sobre a segmentação de streaming, leia a documentação [de segmentação de](./api/streaming-segmentation.md)streaming.

### Segmentação em lote

Como alternativa a um processo de seleção de dados em andamento, a segmentação em lote move todos os dados do perfil de uma só vez pelas definições de segmento para produzir audiências correspondentes. Depois de criado, esse segmento é salvo e armazenado para que você possa exportá-lo para uso.

Para saber como avaliar segmentos, consulte o tutorial [de avaliação de](./tutorials/evaluate-a-segment.md)segmentos.

## Acessar resultados da segmentação

Para saber como acessar um segmento exportado, consulte o tutorial [de avaliação de](./tutorials/evaluate-a-segment.md)segmento.

## Metadados do segmento

Os metadados do segmento facilitam a indexação no evento para que qualquer um de seus segmentos seja reutilizado e/ou combinado.

A composição de seus segmentos (por meio da API ou [!DNL Segment Builder]) requer que você defina um nome de segmento e uma política de mesclagem.

### Nomes de segmentos

Ao criar um novo segmento, é necessário fornecer um nome de segmento. O nome do segmento é usado para identificar um segmento específico entre a coleção criada por [!DNL Segmentation Service]. Os nomes de segmentos devem, portanto, ser descritivos, concisos e exclusivos.

>[!NOTE]
>
>Ao planejar um segmento, lembre-se de que os segmentos podem ser referenciados e combinados a qualquer outro segmento. Ao selecionar um nome, considere a possibilidade de seu segmento conter partes reutilizáveis.

### Mesclar políticas

As políticas de mesclagem são regras usadas [!DNL Profile] para determinar como os dados serão priorizados e combinados em uma visualização unificada em determinadas condições.
Se uma política de mesclagem não estiver definida, a política de [!DNL Platform] mesclagem padrão será usada. Se você preferir usar uma política de mesclagem específica para a sua organização, poderá criar sua própria política e marcá-la como padrão da sua organização.

Mais informações sobre as políticas de mesclagem podem ser encontradas no guia [de políticas de](../profile/api/merge-policies.md)mesclagem.

>[!NOTE]
>
>A estimativa de tamanhos de audiência é baseada na política padrão de mesclagem de perfis da organização.

### Outros metadados de segmento

Além do nome do segmento e da política de mesclagem, [!DNL Segment Builder] oferta um campo de metadados de &quot;descrição do segmento&quot; adicional no qual você pode resumir a finalidade da definição do segmento.

## Recursos avançados de segmentação

Os segmentos podem ser configurados para gerar uma audiência continuamente, combinando a assimilação [de dados de](../ingestion/streaming-ingestion/overview.md) fluxo contínuo com qualquer um dos seguintes recursos de segmentação avançada:
- [Segmentação sequencial](#sequential)
- [Segmentação dinâmica](#dynamic)
- [Segmentação de várias entidades](#multi-entity)

Esses recursos avançados são discutidos com mais detalhes nas seções a seguir.

## Segmentação sequencial {#sequential}

Uma jornada padrão do usuário é sequencial por natureza. A Adobe Experience Platform permite que você defina uma série ordenada de segmentos para refletir essa jornada, capturando assim sequências de eventos à medida que ocorrem. Você pode organizar os eventos na ordem desejada usando a linha do tempo do evento visual no [!DNL Segment Builder].

Um exemplo de uma jornada do cliente que exigiria segmentação sequencial seria visualização do produto > adição do produto > finalização > Nenhuma compra.

## Segmentação dinâmica {#dynamic}

A segmentação dinâmica resolve os problemas de escalabilidade que os comerciantes enfrentam tradicionalmente ao criar segmentos para campanhas de marketing.

Diferentemente da segmentação estática que exige que você capture explícita e repetidamente todos os casos de uso possíveis, a segmentação dinâmica usa variáveis para criar a lógica da regra e as relações dinamicamente expressas.

### Caso de uso: Procurando clientes que fazem compras fora do seu país

Para ilustrar o valor desse recurso de segmentação avançada, considere a colaboração de um arquiteto de dados com um profissional de marketing para identificar os clientes que fizeram compras fora do estado de origem.

**O problema**

A segmentação estática exige que você defina segmentos individuais com um atributo de estado inicial exclusivo, antes de filtrar eventos de compra que não sejam iguais ao estado inicial. Um segmento explícito desse tipo diria &quot;Estou procurando pessoas de Utah onde o estado de sua compra não é Utah&quot;. A criação de uma audiência usando esse método exige a definição de um segmento para cada estado dos EUA, para um total de 50 segmentos.

Como resultado das diferentes combinações de segmentos que inevitavelmente surgem à medida que você dimensiona, o processo manual necessário para a segmentação estática se torna mais demorado, reduzindo a eficiência geral.

**A solução**

Ao atribuir uma variável ao atributo de estado da compra, seu segmento dinâmico simplifica para &quot;localizar uma compra em que o estado dessa compra não seja igual ao estado inicial do cliente&quot;. Isso permite consolidar 50 segmentos estáticos em um único segmento dinâmico.

## Segmentação de várias entidades {#multi-entity}

Com o recurso avançado de segmentação de várias entidades, você pode estender [!DNL Real-time Customer Profile] dados com dados adicionais baseados em produtos, lojas ou outras entidades não-pessoais, também conhecidas como entidades de &quot;dimensão&quot;. Como resultado, [!DNL Segmentation Service] é possível acessar campos adicionais durante a definição do segmento como se eles fossem nativos do armazenamento de [!DNL Profile] dados. A segmentação de várias entidades proporciona flexibilidade ao identificar audiências com base em dados relevantes às suas necessidades comerciais exclusivas. Para obter mais informações, incluindo casos de uso e workflows, consulte o guia [de segmentação de](multi-entity-segmentation.md)várias entidades.

## [!DNL Segmentation Service] tipos de dados

[!DNL Segmentation Service] suporta uma variedade de tipos de dados primitivos e complexos. Informações detalhadas, incluindo uma lista de tipos de dados suportados, podem ser encontradas no guia [de tipos de dados](./data-types.md)suportados.

## Próximas etapas

[!DNL Segmentation Service] fornece um fluxo de trabalho consolidado para criar segmentos a partir de [!DNL Real-time Customer Profile] dados. Em resumo:

- [!DNL Segmentation] é o processo de definição de um subconjunto de perfis da sua loja de perfis, permitindo que você caracterize o comportamento ou os atributos de um grupo comercializável desejado. [!DNL Segmentation Service] possibilita esse processo.
- Ao planejar um segmento, lembre-se de que um segmento pode ser referenciado e combinado a qualquer outro segmento.
- Um segmento pode ser criado a partir de regras baseadas em dados de perfil, dados de séries de tempo relacionados ou ambos.
- Os segmentos podem ser avaliados sob demanda ou continuamente. Quando avaliados sob demanda, todos os dados do perfil são passados pelas definições do segmento de uma só vez. Quando avaliados continuamente, os dados são transmitidos pelas definições de segmento à medida que entram [!DNL Platform].

Para saber como definir segmentos na interface do usuário, consulte o guia [Construtor de](./ui/overview.md)segmentos. Para obter informações sobre como criar definições de segmentos usando a API, consulte o tutorial sobre como [criar segmentos usando a API](./tutorials/create-a-segment.md).