---
keywords: Experience Platform;página inicial;tópicos populares;ativar dados de entrada;preencher perfil;preencher perfil unificado;preencher perfil unificado;;home;popular topics;ativate inbound data;populate profile;rtcp;populated unified profile
solution: Experience Platform
title: Ativar dados de origem de entrada para preencher perfis de clientes na interface do
type: Tutorial
description: Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados do Perfil do cliente em tempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Ativar dados de origem de entrada para preencher perfis de clientes

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os [!DNL Real-Time Customer Profile] dados.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Tutorial do Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar diferentes conectores na interface do usuário pode ser encontrada no [visão geral dos conectores de origem](../../home.md).

## Preencha seu [!DNL Real-Time Customer Profile] dados

Para enriquecer os perfis do cliente, o esquema de origem do conjunto de dados de destino deve ser compatível para uso no [!DNL Real-Time Customer Profile]. Um esquema compatível satisfaz os seguintes requisitos:

- O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O esquema tem uma propriedade de identidade definida como a identidade principal.
- Existe um mapeamento no fluxo de dados em que a identidade primária é um atributo de destino.

No espaço de trabalho Origens, clique no botão **[!UICONTROL Procurar]** para listar suas conexões básicas. Na lista exibida, localize a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A conexão é **[!UICONTROL Atividade de origem]** é exibida, exibindo os conjuntos de dados aos quais a conexão está assimilando dados de origem. Clique no nome do conjunto de dados que você deseja ativar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

A variável **[!UICONTROL Atividade do conjunto de dados]** é exibida. A variável **[!UICONTROL Propriedades]** no lado direito da tela exibe os detalhes do conjunto de dados e inclui uma **[!UICONTROL Perfil]** e um link para o esquema ao qual o conjunto de dados adere. Clique no nome do schema para exibir sua composição.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

A variável **[!UICONTROL Editor de esquema]** é exibida, mostrando a estrutura do esquema na tela central. Na tela de desenho, selecione o campo a ser definido como a identidade principal. No **[!UICONTROL Propriedades do campo]** que for exibida, selecione a guia **[!UICONTROL Identidade]** , depois **[!UICONTROL Identidade principal]**. Por fim, selecione um apropriado **[!UICONTROL Namespace de identidade]** e, em seguida, clique em **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do esquema e na **[!UICONTROL Propriedades do esquema]** é exibida. Ativar o esquema para [!DNL Profile] alternando a variável **[!UICONTROL Perfil]** interruptor. Clique em **[!UICONTROL Salvar]** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Agora que o esquema foi ativado para [!DNL Profile], retorne à guia **[!UICONTROL Atividade do conjunto de dados]** e habilitar o conjunto de dados para [!DNL Profile] clicando no link **[!UICONTROL Perfil]** alternar dentro do **[!UICONTROL Propriedades]** coluna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Com o esquema e o conjunto de dados habilitados para [!DNL Profile], os dados assimilados nesse conjunto de dados agora também preencherão os perfis do cliente.

>[!NOTE]
>
>Os dados existentes em um conjunto de dados habilitado recentemente não são consumidos pelo [!DNL Profile].

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada para [!DNL Profile] população. Para obter mais informações, consulte [[!DNL Real-Time Customer Profile] visão geral](../../../profile/home.md).
