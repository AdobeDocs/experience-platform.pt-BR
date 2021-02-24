---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Impor conformidade de uso de dados para segmentos de audiência
topic: tutorial
translation-type: tm+mt
source-git-commit: 2ca0768c951cf67a775fdfc2c1f9440596d118bf
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Importação e uso de audiências externas

A Adobe Experience Platform suporta a capacidade de importar audiências externas, que podem ser usadas subsequentemente como componentes para uma nova definição de segmento. Este documento fornece um tutorial para configurar o Experience Platform para importar e usar audiências externas.

## Introdução

- [Serviço](../home.md) de segmentação: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [Perfil](../../profile/home.md) do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
- [Conjuntos de dados](../../catalog/datasets/overview.md): A construção de armazenamento e gerenciamento para a persistência de dados no Experience Platform.
- [Inclusão](../../ingestion/streaming-ingestion/overview.md) de transmissão: Como o Experience Platform ingere e armazena dados de dispositivos do cliente e do servidor em tempo real.

## Criar uma namespace de identidade para a audiência externa

A primeira etapa para usar audiências externas é criar uma namespace de identidade. Namespaces de identidade permitem que a Plataforma associe de onde um segmento se origina.

Para criar uma namespace de identidade, siga as instruções no [guia de namespace de identidade](../../identity-service/namespaces.md#manage-namespaces). Ao criar sua namespace de identidade, adicione os detalhes da fonte à namespace de identidade e marque seu [!UICONTROL Type] como um **[!UICONTROL identificador de não pessoas]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Criar um schema para os metadados do segmento

Depois de criar uma namespace de identidade, é necessário criar um novo schema para o segmento que será criado.

Para começar a compor um schema, primeiro selecione **[!UICONTROL Schemas]** na barra de navegação esquerda, seguido por **[!UICONTROL Criar schema]** no canto superior direito da área de trabalho dos Schemas. Aqui, selecione **[!UICONTROL Procurar]** para ver uma seleção completa dos tipos de Schemas disponíveis.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Como você está criando uma definição de segmento, que é uma classe predefinida, selecione **[!UICONTROL Usar classe existente]**. Agora, selecione a classe **[!UICONTROL Definição de segmento]**, seguida por **[!UICONTROL Atribuir classe]**.

![](../images/tutorials/external-audiences/assign-class.png)

Agora que seu schema foi criado, será necessário especificar qual campo conterá a ID do segmento. Esse campo deve ser marcado como a identidade principal e atribuído às namespaces que você criou anteriormente.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Depois de marcar o campo `_id` como a identidade primária, selecione o título do schema, seguido da alternância chamada **[!UICONTROL Perfil]**. Selecione **[!UICONTROL Ativar]** para ativar o schema para [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Agora, esse schema está ativado para Perfil, com a identificação principal atribuída à namespace de identidade pessoal que você criou. Como resultado, isso significa que os metadados de segmento importados para a Plataforma usando esse schema serão ingeridos no Perfil sem serem unidos aos dados de Perfis relacionados a outras pessoas.

## Criar um conjunto de dados para o schema

Após configurar o schema, será necessário criar um conjunto de dados para os metadados do segmento.

Para criar um conjunto de dados, siga as instruções no [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#create). Siga a opção **[!UICONTROL Criar conjunto de dados a partir do schema]**, usando o schema criado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Depois de criar o conjunto de dados, continue seguindo as instruções no [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#enable-profile) para ativar esse conjunto de dados para o Perfil do cliente em tempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar dados de audiência

Com o conjunto de dados ativado, os dados agora podem ser enviados para a Plataforma por meio da interface do usuário ou usando as APIs do Experience Platform. Para assimilar esses dados na Plataforma, será necessário criar uma conexão de streaming.

Para criar uma conexão de transmissão, siga as instruções no [tutorial da API](../../sources/tutorials/api/create/streaming/http.md) ou no tutorial da interface [a3/>.](../../sources/tutorials/ui/create/streaming/http.md)

Depois de criar sua conexão de streaming, você terá acesso ao seu terminal de streaming exclusivo para o qual pode enviar seus dados. Para saber como enviar dados para esses pontos de extremidade, leia o tutorial [em streaming record data](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Criação de segmentos usando audiências importadas

Depois que as audiências importadas forem configuradas, elas poderão ser usadas como parte do processo de segmentação. Para localizar audiências externas, vá para o Construtor de segmentos e selecione a guia **[!UICONTROL Audiência]** na seção **[!UICONTROL Campos]**.

![](../images/tutorials/external-audiences/external-audiences.png)

## Próximas etapas

Agora que você pode usar audiências externas em seus segmentos, pode usar o Construtor de segmentos para criar segmentos. Para saber como criar segmentos, leia o tutorial [sobre como criar segmentos](./create-a-segment.md).