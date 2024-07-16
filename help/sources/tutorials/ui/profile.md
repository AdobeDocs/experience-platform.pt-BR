---
keywords: Experience Platform;página inicial;tópicos populares;ativar dados de entrada;preencher perfil;preencher perfil unificado;preencher perfil unificado;;home;popular topics;ativate inbound data;populate profile;rtcp;populated unified profile
solution: Experience Platform
title: Ativar dados de entrada do Source para preencher perfis de clientes na interface do
type: Tutorial
description: Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados do Perfil do cliente em tempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Ativar dados de origem de entrada para preencher perfis de clientes

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados do [!DNL Real-Time Customer Profile].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar diferentes conectores na interface do usuário pode ser encontrada na [visão geral dos conectores de origem](../../home.md).

## Preencha seus dados do [!DNL Real-Time Customer Profile]

Para enriquecer perfis de clientes, o esquema de origem do conjunto de dados de destino deve ser compatível para uso em [!DNL Real-Time Customer Profile]. Um esquema compatível satisfaz os seguintes requisitos:

- O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O esquema tem uma propriedade de identidade definida como a identidade principal.
- Existe um mapeamento no fluxo de dados em que a identidade primária é um atributo de destino.

No espaço de trabalho de Fontes, clique na guia **[!UICONTROL Procurar]** para listar suas conexões de base. Na lista exibida, localize a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A tela **[!UICONTROL Atividade Source]** da conexão é exibida, exibindo os conjuntos de dados nos quais a conexão está assimilando dados de origem. Clique no nome do conjunto de dados que você deseja habilitar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

A tela **[!UICONTROL Atividade do conjunto de dados]** é exibida. A coluna **[!UICONTROL Propriedades]** no lado direito da tela exibe os detalhes do conjunto de dados e inclui uma opção de **[!UICONTROL Perfil]** e um link para o esquema ao qual o conjunto de dados adere. Clique no nome do schema para exibir sua composição.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

O **[!UICONTROL Editor de esquemas]** é exibido, mostrando a estrutura do esquema na tela central. Na tela de desenho, selecione o campo a ser definido como a identidade principal. Na guia **[!UICONTROL Propriedades do campo]** exibida, marque a caixa de seleção **[!UICONTROL Identidade]** e, em seguida, **[!UICONTROL Identidade principal]**. Finalmente, selecione um **[!UICONTROL Namespace de identidade]** apropriado e clique em **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do esquema e a coluna **[!UICONTROL Propriedades do esquema]** será exibida. Habilite o esquema para [!DNL Profile] alternando a opção **[!UICONTROL Perfil]**. Clique em **[!UICONTROL Salvar]** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Agora que o esquema está habilitado para [!DNL Profile], retorne à tela **[!UICONTROL Atividade do conjunto de dados]** e habilite o conjunto de dados para [!DNL Profile] clicando na opção de alternância **[!UICONTROL Perfil]** na coluna **[!UICONTROL Propriedades]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Com o esquema e o conjunto de dados habilitados para [!DNL Profile], os dados assimilados nesse conjunto de dados agora também preencherão os perfis do cliente.

>[!NOTE]
>
>Os dados existentes em um conjunto de dados habilitado recentemente não são consumidos por [!DNL Profile].

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada da população [!DNL Profile]. Para obter mais informações, consulte a [[!DNL Real-Time Customer Profile] visão geral](../../../profile/home.md).
