---
title: Definir uma relação entre dois esquemas no Real-time Customer Data Platform B2B Edition
description: Saiba como definir uma relação muitos para um entre dois esquemas no Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Definir uma relação muitos para um entre dois esquemas no Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Esquema de referência"
>abstract="Selecione o schema com o qual deseja estabelecer uma relação. Dependendo da classe do esquema, ele também pode ter relacionamentos existentes com outras entidades no contexto B2B. Consulte a documentação para saber como as classes de esquema B2B se relacionam."

O Adobe Real-time Customer Data Platform B2B Edition fornece várias classes do Experience Data Model (XDM) que capturam entidades fundamentais de dados B2B, incluindo [contas](../classes/b2b/business-account.md), [oportunidades](../classes/b2b/business-opportunity.md), [campanhas](../classes/b2b/business-campaign.md)e muito mais. Criando esquemas com base nessas classes e permitindo seu uso em [Perfil do cliente em tempo real](../../profile/home.md), você pode mesclar dados de fontes diferentes em uma representação unificada chamada esquema de união.

No entanto, os esquemas de união só podem conter campos capturados por esquemas que compartilham a mesma classe. É aqui que entram as relações de esquema. Ao implementar relacionamentos em seus esquemas B2B, você pode descrever como essas entidades de negócios se relacionam entre si e pode incluir atributos de várias classes em casos de uso de segmentação downstream.

O diagrama a seguir fornece um exemplo de como as diferentes classes B2B podem se relacionar entre si em uma implementação básica:

![Relacionamentos de classe B2B](../images/tutorials/relationship-b2b/classes.png)

Este tutorial aborda as etapas para definir uma relação muitos para um entre dois esquemas no Real-Time CDP B2B Edition.

>[!NOTE]
>
>Se você não estiver usando o Real-time Customer Data Platform B2B Edition ou quiser criar uma relação um para um, consulte o guia em [criação de uma relação um para um](./relationship-ui.md) em vez disso.
>
>Este tutorial foca em como estabelecer manualmente relações entre esquemas B2B na interface do usuário da plataforma. Se você estiver trazendo dados de uma conexão de origem B2B, poderá usar um utilitário de geração automática para criar os esquemas, identidades e relacionamentos necessários. Consulte a documentação de origens em namespaces e esquemas B2B para obter mais informações sobre [uso do utilitário de geração automática](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Introdução

Este tutorial requer um entendimento prático de [!DNL XDM System] e o Editor de esquemas no [!DNL Experience Platform] IU. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): uma visão geral do XDM e sua implementação no [!DNL Experience Platform].
* [Noções básicas da composição do esquema](../schema/composition.md): uma introdução dos blocos de construção de esquemas XDM.
* [Criar um esquema usando o [!DNL Schema Editor]](create-schema-ui.md): um tutorial que aborda as noções básicas sobre como criar e editar esquemas na interface do usuário.

## Definir um esquema de origem e de referência

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Para fins de demonstração, este tutorial cria uma relação entre oportunidades de negócios (definidas em uma &quot;[!DNL Opportunities]&quot;) e sua conta comercial associada (definida em uma &quot;[!DNL Accounts]&quot;).

Relacionamentos de esquema são representados por um campo dedicado em um **esquema de origem** que faz referência ao campo de identidade principal de um **esquema de referência**. Nas etapas a seguir, &quot;[!DNL Opportunities]&quot; serve como o esquema de origem, enquanto &quot;[!DNL Accounts]&quot;O atua como o schema de referência.

### Compreensão de identidades em relacionamentos B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Namespace de identidade de referência"
>abstract="O namespace (tipo) do campo de identidade principal do esquema de referência. O esquema de referência deve ter um campo de identidade principal estabelecido para participar de um relacionamento. Consulte a documentação para saber mais sobre identidades em relacionamentos B2B."

Para estabelecer uma relação, o schema de referência deve ter uma identidade primária definida. Ao definir uma identidade primária para uma entidade B2B, lembre-se de que as IDs de entidade baseadas em sequência podem se sobrepor se você as estiver coletando em diferentes sistemas ou locais, o que pode levar a conflitos de dados na Platform.

Para levar em conta isso, todas as classes B2B padrão contêm campos &quot;chave&quot; que estão em conformidade com a [[!UICONTROL Origem B2B] tipo de dados](../data-types/b2b-source.md). Esse tipo de dados fornece campos para um identificador de sequência para a entidade B2B, juntamente com outras informações contextuais sobre a origem do identificador. Um desses campos, `sourceKey`, concatena os valores dos outros campos no tipo de dados para produzir um identificador totalmente exclusivo para a entidade. Este campo deve ser sempre usado como a identidade principal para esquemas de entidade B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Quando [definição de um campo XDM como uma identidade](../ui/fields/identity.md), você deve fornecer um namespace de identidade para definir a identidade em. Pode ser um namespace padrão fornecido pelo Adobe ou um namespace personalizado definido por sua organização. Na prática, o namespace é simplesmente uma sequência contextual e pode ser definido com qualquer valor desejado, desde que seja significativo para sua organização categorizar o tipo de identidade. Consulte a visão geral em [namespaces de identidade](../../identity-service/namespaces.md) para obter mais informações.

Para fins de referência, as seções a seguir descrevem a estrutura de cada esquema usado neste tutorial antes que uma relação seja definida. Anote onde as identidades primárias foram definidas na estrutura do esquema e nos namespaces personalizados que elas usam.

### [!DNL Opportunities] schema

O schema de origem &quot;[!DNL Opportunities]&quot; baseia-se no [!UICONTROL Oportunidade de negócios XDM] classe. Um dos campos fornecidos pela classe, `opportunityKey`, serve como o identificador do esquema. Especificamente, o `sourceKey` sob o campo `opportunityKey` objeto é definido como a identidade primária do esquema em um namespace personalizado chamado [!DNL B2B Opportunity].

Como visto em **[!UICONTROL Propriedades do esquema]**, este esquema foi ativado para uso no [!DNL Real-Time Customer Profile].

![Esquema de Oportunidades](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

O schema de referência &quot;[!DNL Accounts]&quot; baseia-se no [!UICONTROL Conta XDM] classe. O nível raiz `accountKey` o campo contém o `sourceKey` que atua como sua identidade primária em um namespace personalizado chamado [!DNL B2B Account]. Este esquema também foi ativado para uso no Perfil.

![Esquema de contas](../images/tutorials/relationship-b2b/accounts.png)

## Definir um campo de relacionamento para o esquema de origem {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nome do relacionamento do esquema atual"
>abstract="Um rótulo que descreve a relação do esquema atual com o esquema de referência (por exemplo, &quot;Conta relacionada&quot;). Esse rótulo é usado em Perfil e segmentação para fornecer contexto aos dados de entidades B2B relacionadas. Consulte a documentação para saber mais sobre a criação de relacionamentos de esquema B2B."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nome do relacionamento do esquema de referência"
>abstract="Um rótulo que descreve o relacionamento entre o schema de referência e o schema atual (por exemplo, &quot;Oportunidades relacionadas&quot;). Esse rótulo é usado em Perfil e segmentação para fornecer contexto aos dados de entidades B2B relacionadas. Consulte a documentação para saber mais sobre a criação de relacionamentos de esquema B2B."

Para definir uma relação entre dois esquemas, o esquema de origem deve ter um campo dedicado que indique a identidade primária do esquema de referência. As classes B2B padrão incluem campos de chave de origem dedicada para entidades de negócios comumente relacionadas. Por exemplo, a variável [!UICONTROL Oportunidade de negócios XDM] A classe contém campos de chave de origem para uma conta relacionada (`accountKey`) e uma campanha relacionada (`campaignKey`). No entanto, também é possível adicionar outros [!UICONTROL Origem B2B] ao esquema usando grupos de campos personalizados se você precisar de mais do que os componentes padrão.

>[!NOTE]
>
>Atualmente, somente as relações muitos para um e um para um podem ser definidas de um esquema de origem para um esquema de referência. Para relações um para muitos, você deve definir o campo de relacionamento no esquema que representa o &quot;muitos&quot;.

Para definir um campo de relacionamento, selecione o ícone de seta (![Ícone de seta](../images/tutorials/relationship-b2b/arrow.png)) ao lado do campo em questão dentro da tela. No caso do [!DNL Opportunities] esquema, este é o `accountKey.sourceKey` já que o objetivo é estabelecer uma relação muitos para um com uma conta.

![Botão de relacionamento](../images/tutorials/relationship-b2b/relationship-button.png)

Uma caixa de diálogo é exibida, permitindo especificar os detalhes sobre o relacionamento. O tipo de relacionamento é automaticamente definido como **[!UICONTROL De muitos para um]**.

![Caixa de diálogo Relacionamento](../images/tutorials/relationship-b2b/relationship-dialog.png)

Em **[!UICONTROL Esquema de referência]**, use a barra de pesquisa para localizar o nome do schema de referência. Ao realçar o nome do esquema de referência, a variável **[!UICONTROL Namespace de identidade de referência]** O campo é atualizado automaticamente para o namespace da identidade principal do esquema.

![Esquema de referência](../images/tutorials/relationship-b2b/reference-schema.png)

Em **[!UICONTROL Nome do relacionamento do esquema atual]** e **[!UICONTROL Nome do relacionamento do esquema de referência]**, forneça nomes amigáveis para o relacionamento no contexto dos esquemas de origem e referência, respectivamente. Quando terminar, selecione **[!UICONTROL Salvar]** para aplicar as alterações e salvar o esquema.

![Nome do relacionamento](../images/tutorials/relationship-b2b/relationship-name.png)

A tela será exibida novamente, com o campo de relacionamento agora marcado com o nome amigável fornecido anteriormente. O nome do relacionamento também está listado no painel esquerdo para facilitar a referência.

![Relação Aplicada](../images/tutorials/relationship-b2b/relationship-applied.png)

Se você visualizar a estrutura do esquema de referência, o marcador de relacionamento aparecerá ao lado do campo de identidade principal do esquema e no painel esquerdo.

![Marcador de Relacionamento de Esquema de Destino](../images/tutorials/relationship-b2b/destination-relationship.png)

## Próximas etapas

Ao seguir este tutorial, você criou uma relação muitos para um entre dois esquemas usando o [!DNL Schema Editor]. Depois que os dados forem assimilados usando conjuntos de dados com base nesses esquemas e que os dados forem ativados no armazenamento de dados do Perfil, você poderá usar atributos de ambos os esquemas para [casos de uso de segmentação de várias classes](../../rtcdp/segmentation/b2b.md).
