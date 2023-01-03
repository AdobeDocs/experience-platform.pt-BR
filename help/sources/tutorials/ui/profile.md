---
keywords: Experience Platform, home, tópicos populares, ativar dados de entrada, preencher perfil, preencher rtcp, perfil unificado preenchido
solution: Experience Platform
title: Ativar dados de origem de entrada para preencher perfis de cliente na interface do usuário
topic-legacy: overview
type: Tutorial
description: Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados do Perfil do cliente em tempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Ativar dados de origem de entrada para preencher perfis de cliente

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher [!DNL Real-Time Customer Profile] dados.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar diferentes conectores na interface do usuário pode ser encontrada no [visão geral dos conectores de origem](../../home.md).

## Preencha seu [!DNL Real-Time Customer Profile] dados

Para enriquecer os perfis do cliente, o esquema de origem do conjunto de dados de destino deve ser compatível para uso no [!DNL Real-Time Customer Profile]. Um schema compatível satisfaz os seguintes requisitos:

- O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O esquema tem uma propriedade de identidade definida como a identidade primária.
- Existe um mapeamento no fluxo de dados em que a identidade primária é um atributo de destino.

Na área de trabalho Fontes , clique no botão **[!UICONTROL Procurar]** para listar suas conexões básicas. Na lista exibida, encontre a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A conexão **[!UICONTROL Atividade de origem]** for exibida, exibindo os conjuntos de dados em que a conexão está assimilando dados de origem. Clique no nome do conjunto de dados que deseja ativar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

O **[!UICONTROL Atividade do conjunto de dados]** será exibida. O **[!UICONTROL Propriedades]** no lado direito da tela exibe os detalhes do conjunto de dados e inclui um **[!UICONTROL Perfil]** e um link para o schema ao qual o conjunto de dados adere. Clique no nome do schema para exibir sua composição.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

O **[!UICONTROL Editor de esquema]** for exibida, mostrando a estrutura do schema na tela central. Na tela, selecione o campo a ser definido como a identidade primária. Em **[!UICONTROL Propriedades do campo]** que aparece, selecione a **[!UICONTROL Identidade]** caixa de seleção, em seguida **[!UICONTROL Identidade primária]**. Finalmente, selecione um **[!UICONTROL Namespace de identidade]**, depois clique em **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do schema e na guia **[!UICONTROL Propriedades do schema]** é exibida. Habilite o esquema para [!DNL Profile] alternando a **[!UICONTROL Perfil]** switch. Clique em **[!UICONTROL Salvar]** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Agora que o esquema está ativado para [!DNL Profile], retorne ao **[!UICONTROL Atividade do conjunto de dados]** e ativar o conjunto de dados para [!DNL Profile] clicando no botão **[!UICONTROL Perfil]** alternar dentro do **[!UICONTROL Propriedades]** coluna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Com o esquema e o conjunto de dados habilitados para [!DNL Profile], os dados assimilados nesse conjunto de dados também preencherão os perfis do cliente.

>[!NOTE]
>
>Os dados existentes em um conjunto de dados recentemente habilitado não são consumidos por [!DNL Profile].

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada para [!DNL Profile] população. Para obter mais informações, consulte o [[!DNL Real-Time Customer Profile] visão geral](../../../profile/home.md).
