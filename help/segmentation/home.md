---
keywords: Experience Platform, home, tópicos populares, segmentação, Segmentação, serviço de segmento, segmento, Segmento, Segmentos, segmentos
solution: Experience Platform
title: Visão geral do serviço de segmentação
topic-legacy: overview
description: Saiba mais sobre o Adobe Experience Platform Segmentation Service e a função que ele desempenha no ecossistema da plataforma.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# [!DNL Segmentation Service]visão geral

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos-alvo a partir dos dados [!DNL Real-time Customer Profile]. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform] e são prontamente acessíveis por qualquer solução de Adobe.

Este documento fornece uma visão geral do [!DNL Segmentation Service] e a função que ele desempenha no Adobe Experience Platform.

## Introdução a [!DNL Segmentation Service]

É importante entender os seguintes termos principais usados em todo este documento:

- **Segmentação**: Dividir um grande grupo de indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- **Definição** do segmento: O conjunto de regras usado para descrever as principais características ou comportamento de um público-alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar membros de público-alvo qualificados para um segmento.
- **Público-alvo**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Como a segmentação funciona

A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis do seu armazenamento de perfil para distinguir um grupo comercializável de pessoas da base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você se esqueceu de comprar seus tênis?&quot;, talvez você queira um público-alvo de todos os usuários que procuraram por tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra.

Depois que um segmento é definido conceitualmente, ele é incorporado em [!DNL Experience Platform]. Normalmente, os segmentos são criados pelo profissional de marketing ou pelo especialista em público-alvo, embora algumas organizações prefiram que sejam criadas pelo departamento de marketing, em colaboração com os analistas de dados. Após analisar os dados que estão sendo enviados para [!DNL Platform], o analista de dados compõe a definição do segmento selecionando quais campos e valores serão usados para criar as regras ou condições do segmento. Isso é feito usando a interface do usuário ou a API.

## Criar segmentos

Quer sejam criados usando a API ou [!DNL Segment Builder], os segmentos são definidos usando [!DNL Profile Query Language] (PQL). É aqui que a definição de segmento conceitual é descrita na linguagem criada para recuperar perfis que atendem aos critérios. Para obter mais informações, consulte a [Visão geral da PQL](./pql/overview.md).

Para saber como criar e usar segmentos no [!DNL Segment Builder] (a implementação da interface do usuário de [!DNL Segmentation Service]), consulte o [guia do Construtor de segmentos](./ui/overview.md).

Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial em [criar segmentos de público-alvo usando a API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Caso um esquema seja estendido, todos os uploads futuros devem atualizar os campos recém-adicionados de acordo. Para obter mais informações sobre como personalizar [!DNL Experience Data Model] (XDM), visite o [Tutorial do Editor de Esquema](../xdm/tutorials/create-schema-ui.md).

## Avaliar segmentos

Atualmente, a plataforma suporta três métodos de avaliação de segmentos: segmentação de streaming, segmentação em lote e segmentação de borda.

### Segmentação de streaming

A segmentação de streaming é um processo contínuo de seleção de dados que atualiza seus segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos em [!DNL Real-time Customer Profile]. Adições e remoções de segmentos são processadas regularmente, garantindo que o público-alvo permaneça relevante.

Para saber mais sobre a segmentação de transmissão, leia a [documentação de segmentação de transmissão](./api/streaming-segmentation.md).

### Segmentação em lote

Como alternativa a um processo de seleção de dados contínuo, a segmentação em lote move todos os dados do perfil de uma só vez por meio das definições de segmento para produzir públicos correspondentes. Depois de criado, esse segmento é salvo e armazenado, para que você possa exportá-lo para uso.

**Segmentação incremental (beta)**

Segmentos em lote são avaliados a cada 24 horas. No entanto, para segmentos existentes, a segmentação incremental mantém os segmentos atualizados por até uma hora.

A segmentação incremental é executada em novos dados que entram no armazenamento de perfis. No entanto, os seguintes avisos se aplicam à segmentação incremental:

- Para qualquer segmento novo ou modificado recentemente, os perfis com novos dados começarão a se qualificar na próxima execução incremental. No entanto, os perfis sem alterações aparecerão no próximo trabalho de segmentação de lote completo.
- Segmentos de várias entidades serão atualizados na segmentação incremental. Se houver atualizações de entidade, todos os perfis com novos dados começarão a usá-los na próxima execução incremental. No entanto, os perfis sem alterações aparecerão no próximo trabalho de segmentação de lote completo.
- Os eventos que soltarem a janela de tempo de um segmento serão reconciliados no próximo trabalho de segmentação de lote completo.

Para saber como avaliar segmentos, consulte o [tutorial de avaliação de segmento](./tutorials/evaluate-a-segment.md).

### Segmentação de borda

A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização de página da mesma página e da próxima página.

Para saber mais sobre a segmentação de borda, leia a [documentação da API](./api/edge-segmentation.md) ou a [documentação da interface do usuário](./ui/edge-segmentation.md).

## Acesse os resultados da segmentação

Para saber como acessar um segmento exportado, consulte o [tutorial de avaliação de segmento](./tutorials/evaluate-a-segment.md).

## Metadados do segmento

Metadados de segmento facilitam a indexação no caso de qualquer um de seus segmentos ser reutilizado e/ou combinado.

A composição de seus segmentos (por meio da API ou [!DNL Segment Builder]) requer a definição de um nome de segmento e uma política de mesclagem.

### Nomes do segmento

Ao criar um novo segmento, é necessário fornecer um nome de segmento. O nome do segmento é usado para identificar um segmento específico entre a coleção criada por [!DNL Segmentation Service]. Portanto, os nomes de segmentos devem ser descritivos, concisos e exclusivos.

>[!NOTE]
>
>Ao planejar um segmento, lembre-se de que os segmentos podem ser referenciados e combinados com qualquer outro segmento. Ao selecionar um nome, considere a possibilidade de seu segmento conter partes reutilizáveis.

### Mesclar políticas

As políticas de mesclagem são regras usadas pelo [!DNL Profile] para determinar como os dados serão priorizados e combinados em uma exibição unificada em determinadas condições.
Se uma política de mesclagem não estiver definida, a política de mesclagem padrão [!DNL Platform] será usada. Se preferir usar uma política de mesclagem específica da sua organização, você pode criar a sua própria e marcá-la como padrão da sua organização.

Mais informações sobre as políticas de mesclagem podem ser encontradas no [guia de políticas de mesclagem](../profile/api/merge-policies.md).

>[!NOTE]
>
>A estimativa dos tamanhos do público-alvo é baseada na política de mesclagem de perfis padrão da organização.

### Outros metadados de segmento

Além do nome do segmento e da política de mesclagem, [!DNL Segment Builder] oferece um campo de metadados de &quot;descrição do segmento&quot; adicional, onde você pode resumir a finalidade da definição do segmento.

## Recursos avançados de segmentação

Os segmentos podem ser configurados para gerar continuamente um público-alvo de forma contínua ao combinar [assimilação de dados de fluxo](../ingestion/streaming-ingestion/overview.md) com qualquer um dos seguintes recursos de segmentação avançada:
- [Segmentação sequencial](#sequential)
- [Segmentação dinâmica](#dynamic)
- [Segmentação de várias entidades](#multi-entity)

Esses recursos avançados são discutidos com mais detalhes nas seções a seguir.

## Segmentação sequencial {#sequential}

Uma jornada padrão do usuário é sequencial por natureza. O Adobe Experience Platform permite definir uma série ordenada de segmentos para refletir essa jornada, portanto, capturando sequências de eventos à medida que ocorrem. Você pode organizar os eventos na ordem desejada usando a linha do tempo do evento visual no [!DNL Segment Builder].

Um exemplo de uma jornada do cliente que exigiria segmentação sequencial seria exibição de produto > adição de produto > check-out > Nenhuma compra.

## Segmentação dinâmica {#dynamic}

A segmentação dinâmica resolve os problemas de escalabilidade que os profissionais de marketing enfrentam tradicionalmente ao criar segmentos para campanhas de marketing.

Ao contrário da segmentação estática que requer a captura explícita e repetida de todos os casos de uso possíveis, a segmentação dinâmica usa variáveis para criar a lógica da regra e as relações dinamicamente expressas.

### Caso de uso: Procurando clientes que fazem compras fora do seu estado de origem

Para ilustrar o valor desse recurso de segmentação avançado, considere um arquiteto de dados colaborando com um profissional de marketing para identificar os clientes que fizeram compras fora do estado inicial.

**O problema**

A segmentação estática requer que você defina segmentos individuais com um atributo de estado inicial exclusivo, antes de filtrar eventos de compra que não sejam iguais ao estado inicial. Um segmento explícito desse tipo diria &quot;Estou procurando pessoas de Utah, onde o estado de sua compra não seja Utah&quot;. A criação de um público-alvo usando esse método exige a definição de um segmento para cada estado dos EUA, para um total de 50 segmentos.

Como resultado das diferentes combinações de segmentos que inevitavelmente surgem à medida que você dimensiona, o processo manual necessário para a segmentação estática torna-se mais demorado, reduzindo sua eficiência geral.

**A solução**

Ao atribuir uma variável ao atributo de estado da compra, o segmento dinâmico simplifica &quot;encontrar-me uma compra em que o estado dessa compra não seja igual ao estado inicial do cliente&quot;. Isso permite consolidar 50 segmentos estáticos em um único segmento dinâmico.

## Segmentação de várias entidades {#multi-entity}

Com o recurso avançado de segmentação de várias entidades, é possível estender [!DNL Real-time Customer Profile] dados com dados adicionais baseados em produtos, lojas ou outros não-pessoas, também conhecidos como entidades &quot;de dimensão&quot;. Como resultado, [!DNL Segmentation Service] pode acessar campos adicionais durante a definição do segmento como se fossem nativos no armazenamento de dados [!DNL Profile]. A segmentação de várias entidades proporciona flexibilidade ao identificar públicos com base em dados relevantes para suas necessidades comerciais exclusivas. Para obter mais informações, incluindo casos de uso e fluxos de trabalho, consulte o [guia de segmentação de várias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de dados

[!DNL Segmentation Service] O suporta uma variedade de tipos de dados primitivos e complexos. Informações detalhadas, incluindo uma lista de tipos de dados suportados podem ser encontradas no [guia de tipos de dados suportado](./data-types.md).

## Próximas etapas

[!DNL Segmentation Service] O fornece um fluxo de trabalho consolidado para criar segmentos a partir de  [!DNL Real-time Customer Profile] dados. Em resumo:

- [!DNL Segmentation] é o processo de definir um subconjunto de perfis no armazenamento de perfis, permitindo caracterizar o comportamento ou os atributos de um grupo comercializável desejado. [!DNL Segmentation Service] possibilita esse processo.
- Ao planejar um segmento, lembre-se de que um segmento pode ser referenciado e combinado a partir de qualquer outro segmento.
- Um segmento pode ser criado a partir de regras baseadas em dados de perfil, dados de séries de tempo relacionados ou ambos.
- Os segmentos podem ser avaliados sob demanda ou continuamente. Quando avaliados sob demanda, todos os dados do perfil são passados pelas definições de segmento de uma só vez. Quando avaliados continuamente, os dados são transmitidos por meio de definições de segmento à medida que entram [!DNL Platform].

Para saber como definir segmentos na interface do usuário, consulte o [Guia do Construtor de segmentos](./ui/overview.md). Para obter informações sobre como criar definições de segmento usando a API, consulte o tutorial em [criar segmentos usando a API](./tutorials/create-a-segment.md).
