---
keywords: Experience Platform, home, tópicos populares, ativar dados de entrada, preencher perfil, preencher rtcp, perfil unificado preenchido
solution: Experience Platform
title: Ativar dados de origem de entrada para preencher perfis de cliente na interface do usuário
topic-legacy: overview
type: Tutorial
description: Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados do Perfil do cliente em tempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Ativar dados de origem de entrada para preencher perfis de cliente

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de [!DNL Real-time Customer Profile].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar diferentes conectores na interface do usuário pode ser encontrada na [visão geral dos conectores de origem](../../home.md).

## Preencha seus dados [!DNL Real-time Customer Profile]

Para enriquecer os perfis do cliente, o esquema de origem do conjunto de dados de destino deve ser compatível para uso em [!DNL Real-time Customer Profile]. Um schema compatível satisfaz os seguintes requisitos:

- O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O esquema tem uma propriedade de identidade definida como a identidade primária.
- Existe um mapeamento no fluxo de dados em que a identidade primária é um atributo de destino.

No espaço de trabalho Fontes, clique na guia **[!UICONTROL Browse]** para listar suas conexões básicas. Na lista exibida, encontre a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A tela **[!UICONTROL Source activity]** da conexão é exibida, exibindo os conjuntos de dados em que a conexão está assimilando dados de origem. Clique no nome do conjunto de dados que deseja ativar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

A tela **[!UICONTROL Dataset activity]** é exibida. A coluna **[!UICONTROL Properties]** no lado direito da tela exibe os detalhes do conjunto de dados e inclui um switch **[!UICONTROL Profile]** e um link para o esquema ao qual o conjunto de dados adere. Clique no nome do schema para exibir sua composição.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

O **[!UICONTROL Schema Editor]** é exibido, mostrando a estrutura do schema na tela central. Na tela, selecione o campo a ser definido como a identidade primária. Na guia **[!UICONTROL Field properties]** que aparece, marque a caixa de seleção **[!UICONTROL Identity]** e, em seguida, **[!UICONTROL Primary identity]**. Finalmente, selecione um **[!UICONTROL Identity namespace]** apropriado e clique em **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do schema e a coluna **[!UICONTROL Schema properties]** será exibida. Ative o esquema para [!DNL Profile] alternando o switch **[!UICONTROL Profile]**. Clique em **[!UICONTROL Save]** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Agora que o schema está ativado para [!DNL Profile], retorne à tela **[!UICONTROL Dataset activity]** e ative o conjunto de dados para [!DNL Profile] clicando no botão **[!UICONTROL Profile]** na coluna **[!UICONTROL Properties]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Com o esquema e o conjunto de dados habilitados para [!DNL Profile], os dados assimilados nesse conjunto de dados agora também preencherão os perfis do cliente.

>[!NOTE]
>
>Os dados existentes em um conjunto de dados habilitado recentemente não são consumidos por [!DNL Profile].

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada para a população [!DNL Profile]. Para obter mais informações, consulte a [[!DNL Real-time Customer Profile] visão geral](../../../profile/home.md).
