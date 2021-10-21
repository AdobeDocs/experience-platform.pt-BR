---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Importação e uso de públicos externos
description: Siga este tutorial para saber como usar públicos externos com o Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---

# Importação e uso de públicos externos

O Adobe Experience Platform oferece suporte à capacidade de importar público externo, que pode ser usado posteriormente como componentes para uma nova definição de segmento. Este documento fornece um tutorial para configurar o Experience Platform para importar e usar públicos externos.

## Introdução

Este tutorial requer uma compreensão funcional das várias [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de público-alvo. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Serviço de segmentação](../home.md): Permite criar segmentos de público-alvo a partir de dados do Perfil do cliente em tempo real.
- [Perfil do cliente em tempo real](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [Conjuntos de dados](../../catalog/datasets/overview.md): A construção de armazenamento e gerenciamento para a persistência de dados no Experience Platform.
- [Assimilação de fluxo](../../ingestion/streaming-ingestion/overview.md): Como o Experience Platform assimila e armazena dados de dispositivos cliente e servidor em tempo real.

### Dados do segmento versus metadados do segmento

Antes de começar a importar e usar públicos externos, é importante entender a diferença entre os dados do segmento e os metadados do segmento.

Os dados do segmento se referem aos perfis que atendem aos critérios de qualificação de segmento e, portanto, fazem parte do público-alvo.

Os metadados do segmento são informações sobre o próprio segmento, que incluem o nome, a descrição, a expressão (se aplicável), a data de criação, a data da última modificação e uma ID. A ID vincula os metadados do segmento aos perfis individuais que atendem à qualificação de segmento e fazem parte do público-alvo resultante.

| Dados do segmento | Metadados do segmento |
| ------------ | ---------------- |
| Perfis que atendem à qualificação de segmentos | Informações sobre o próprio segmento |

## Criar um namespace de identidade para o público externo

A primeira etapa para usar públicos externos é criar um namespace de identidade. Os namespaces de identidade permitem que a Platform associe o local de origem de um segmento.

Para criar um namespace de identidade, siga as instruções em [guia do namespace de identidade](../../identity-service/namespaces.md#manage-namespaces). Ao criar seu namespace de identidade, adicione os detalhes da origem ao namespace de identidade e marque sua [!UICONTROL Tipo] como **[!UICONTROL Identificador de não pessoas]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Criar um esquema para os metadados do segmento

Depois de criar um namespace de identidade, é necessário criar um novo schema para o segmento que você criará.

Para começar a compor um schema, primeiro selecione **[!UICONTROL Esquemas]** na barra de navegação esquerda, seguida pela variável **[!UICONTROL Criar esquema]** no canto superior direito do espaço de trabalho Esquemas. Aqui, selecione **[!UICONTROL Procurar]** para ver uma seleção completa dos tipos de Esquema disponíveis.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Como você está criando uma definição de segmento, que é uma classe predefinida, selecione **[!UICONTROL Usar classe existente]**. Em seguida, selecione o **[!UICONTROL Definição de segmento]** classe , seguida de **[!UICONTROL Atribuir classe]**.

![](../images/tutorials/external-audiences/assign-class.png)

Agora que o esquema foi criado, será necessário especificar qual campo conterá a ID do segmento. Esse campo deve ser marcado como a identidade primária e atribuído aos namespaces criados anteriormente.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Depois de marcar a `_id` como a identidade primária, selecione o título do esquema, seguido pelo botão rotulado **[!UICONTROL Perfil]**. Selecionar **[!UICONTROL Habilitar]** para ativar o schema de [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Agora, esse esquema é ativado para o Perfil, com a identificação primária atribuída ao namespace de identidade de não pessoa que você criou. Como resultado, isso significa que os metadados de segmento importados para a Plataforma usando esse esquema serão assimilados no Perfil sem serem unidos aos dados de Perfil relacionados a pessoas.

## Criar um conjunto de dados para o esquema

Após configurar o esquema, será necessário criar um conjunto de dados para os metadados do segmento.

Para criar um conjunto de dados, siga as instruções em [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#create). Você vai querer seguir o **[!UICONTROL Criar conjunto de dados a partir do esquema]** , usando o schema criado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Depois de criar o conjunto de dados, continue seguindo as instruções em [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#enable-profile) para ativar esse conjunto de dados no Perfil do cliente em tempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar dados do público

Com o conjunto de dados ativado, agora os dados podem ser enviados para a Platform por meio da interface do usuário ou usando as APIs do Experience Platform. Para assimilar esses dados na Platform, será necessário criar uma conexão de transmissão.

Para criar uma conexão de transmissão, siga as instruções em [Tutorial de API](../../sources/tutorials/api/create/streaming/http.md) ou [Tutorial da interface do usuário](../../sources/tutorials/ui/create/streaming/http.md).

Depois de criar a conexão de transmissão, você terá acesso ao seu endpoint de transmissão exclusivo para o qual poderá enviar seus dados. Para saber como enviar dados para esses endpoints, leia o [tutorial sobre dados de registro de transmissão](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Criação de segmentos usando públicos importados

Depois que os públicos importados forem configurados, eles poderão ser usados como parte do processo de segmentação. Para encontrar públicos externos, acesse o Construtor de segmentos e selecione **[!UICONTROL Públicos-alvo]** na guia no **[!UICONTROL Campos]** seção.

![](../images/tutorials/external-audiences/external-audiences.png)

## Próximas etapas

Agora que você pode usar públicos externos em seus segmentos, pode usar o Construtor de segmentos para criar segmentos. Para saber como criar segmentos, leia o [tutorial sobre a criação de segmentos](./create-a-segment.md).
