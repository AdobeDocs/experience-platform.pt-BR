---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Importação e uso de públicos externos
description: Siga este tutorial para saber como usar públicos externos com o Adobe Experience Platform.
topic: tutorial
translation-type: tm+mt
source-git-commit: 400e4d9007212ed2693d031ae912a4f1cca97c57
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Importação e uso de públicos externos

O Adobe Experience Platform oferece suporte à capacidade de importar público externo, que pode ser usado posteriormente como componentes para uma nova definição de segmento. Este documento fornece um tutorial para configurar o Experience Platform para importar e usar públicos externos.

## Introdução

- [Serviço](../home.md) de segmentação: Permite criar segmentos de público-alvo a partir de dados do Perfil do cliente em tempo real.
- [Perfil](../../profile/home.md) do cliente em tempo real: Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
- [Conjuntos de dados](../../catalog/datasets/overview.md): A construção de armazenamento e gerenciamento para a persistência de dados no Experience Platform.
- [Assimilação](../../ingestion/streaming-ingestion/overview.md) de fluxo: Como o Experience Platform assimila e armazena dados de dispositivos cliente e servidor em tempo real.

## Criar um namespace de identidade para o público externo

A primeira etapa para usar públicos externos é criar um namespace de identidade. Os namespaces de identidade permitem que a Platform associe o local de origem de um segmento.

Para criar um namespace de identidade, siga as instruções no [guia do namespace de identidade](../../identity-service/namespaces.md#manage-namespaces). Ao criar seu namespace de identidade, adicione os detalhes da origem ao namespace de identidade e marque seu [!UICONTROL Type] como um **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Criar um esquema para os metadados do segmento

Depois de criar um namespace de identidade, é necessário criar um novo schema para o segmento que você criará.

Para começar a compor um schema, primeiro selecione **[!UICONTROL Schemas]** na barra de navegação esquerda, seguida pelo **[!UICONTROL Create schema]** no canto superior direito do espaço de trabalho Esquemas. Aqui, selecione **[!UICONTROL Browse]** para ver uma seleção completa dos tipos de Esquema disponíveis.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Como você está criando uma definição de segmento, que é uma classe predefinida, selecione **[!UICONTROL Use existing class]**. Agora, selecione a classe **[!UICONTROL Segment definition]**, seguida por **[!UICONTROL Assign class]**.

![](../images/tutorials/external-audiences/assign-class.png)

Agora que o esquema foi criado, será necessário especificar qual campo conterá a ID do segmento. Esse campo deve ser marcado como a identidade primária e atribuído aos namespaces criados anteriormente.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Depois de marcar o campo `_id` como a identidade primária, selecione o título do esquema, seguido pelo botão rotulado **[!UICONTROL Profile]**. Selecione **[!UICONTROL Enable]** para habilitar o schema para [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Agora, esse esquema é ativado para o Perfil, com a identificação primária atribuída ao namespace de identidade de não pessoa que você criou. Como resultado, isso significa que os metadados de segmento importados para a Plataforma usando esse esquema serão assimilados no Perfil sem serem unidos aos dados de Perfil relacionados a pessoas.

## Criar um conjunto de dados para o esquema

Após configurar o esquema, será necessário criar um conjunto de dados para os metadados do segmento.

Para criar um conjunto de dados, siga as instruções no [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#create). Siga a opção **[!UICONTROL Create dataset from schema]** usando o schema criado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Depois de criar o conjunto de dados, continue seguindo as instruções no [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#enable-profile) para ativar esse conjunto de dados para o Perfil do cliente em tempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar dados do público

Com o conjunto de dados ativado, agora os dados podem ser enviados para a Platform por meio da interface do usuário ou usando as APIs do Experience Platform. Para assimilar esses dados na Platform, será necessário criar uma conexão de transmissão.

Para criar uma conexão de transmissão, siga as instruções no [tutorial de API](../../sources/tutorials/api/create/streaming/http.md) ou no [tutorial de interface do usuário](../../sources/tutorials/ui/create/streaming/http.md).

Depois de criar a conexão de transmissão, você terá acesso ao seu endpoint de transmissão exclusivo para o qual poderá enviar seus dados. Para saber como enviar dados para esses endpoints, leia o tutorial [sobre dados de registro de transmissão](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Criação de segmentos usando públicos importados

Depois que os públicos importados forem configurados, eles poderão ser usados como parte do processo de segmentação. Para encontrar públicos externos, vá para o Construtor de segmentos e selecione a guia **[!UICONTROL Audiences]** na seção **[!UICONTROL Fields]**.

![](../images/tutorials/external-audiences/external-audiences.png)

## Próximas etapas

Agora que você pode usar públicos externos em seus segmentos, pode usar o Construtor de segmentos para criar segmentos. Para saber como criar segmentos, leia o tutorial [sobre como criar segmentos](./create-a-segment.md).