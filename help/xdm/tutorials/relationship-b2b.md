---
title: Definir uma relação entre dois esquemas no Real-time Customer Data Platform B2B Edition
description: Saiba como definir uma relação muitos para um entre dois schemas no Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Definir uma relação muitos para um entre dois esquemas no Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="esquema de referência"
>abstract="Selecione o schema com o qual deseja estabelecer uma relação. Dependendo da classe do schema, ele também pode ter relacionamentos existentes com outras entidades no contexto B2B. Consulte a documentação para saber como as classes de esquema B2B se relacionam umas às outras."

A Adobe Real-time Customer Data Platform B2B Edition fornece várias classes de Modelo de Dados de Experiência (XDM) que capturam entidades de dados B2B fundamentais, incluindo [contas](../classes/b2b/business-account.md), [oportunidades](../classes/b2b/business-opportunity.md), [campanhas](../classes/b2b/business-campaign.md)e muito mais. Ao criar schemas com base nessas classes e habilitá-las para uso no [Perfil do cliente em tempo real](../../profile/home.md), é possível mesclar dados de fontes diferentes em uma representação unificada chamada de schema de união.

No entanto, os esquemas de união só podem conter campos capturados por esquemas que compartilham a mesma classe. É aqui que os relacionamentos de esquema entram. Ao implementar relacionamentos em seus esquemas B2B, você pode descrever como essas entidades de negócios se relacionam entre si e podem incluir atributos de várias classes em casos de uso de segmentação downstream.

O diagrama a seguir fornece um exemplo de como as diferentes classes B2B podem se relacionar entre si em uma implementação básica:

![Relações de classe B2B](../images/tutorials/relationship-b2b/classes.png)

Este tutorial aborda as etapas para definir uma relação muitos para um entre dois schemas no Real-Time CDP B2B Edition.

>[!NOTE]
>
>Se você não estiver usando o Real-time Customer Data Platform B2B Edition ou quiser criar um relacionamento um para um, consulte o guia sobre [criação de uma relação um para um](./relationship-ui.md) em vez disso.
>
>Este tutorial foca em como estabelecer relações manualmente entre esquemas B2B na interface do usuário da plataforma. Se estiver trazendo dados de uma conexão de origem B2B, você pode usar um utilitário de geração automática para criar os esquemas, identidades e relacionamentos necessários. Consulte a documentação de fontes em namespaces e esquemas B2B para obter mais informações sobre [uso do utilitário de geração automática](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Introdução

Este tutorial requer uma compreensão funcional do [!DNL XDM System] e o Editor de esquemas na [!DNL Experience Platform] IU. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no [!DNL Experience Platform].
* [Noções básicas da composição do schema](../schema/composition.md): Uma introdução dos blocos de construção dos esquemas XDM.
* [Crie um schema usando o [!DNL Schema Editor]](create-schema-ui.md): Um tutorial sobre as noções básicas de como criar e editar esquemas na interface do usuário do .

## Definir um schema de referência e de origem

Espera-se que você já tenha criado os dois schemas que serão definidos na relação. Para fins de demonstração, este tutorial cria uma relação entre oportunidades de negócios (definidas em um &quot;[!DNL Opportunities]&quot; e sua conta comercial associada (definida em um &quot;[!DNL Accounts]&quot; schema).

Os relacionamentos de schema são representados por um campo dedicado em um **esquema de origem** que faz referência ao campo de identidade principal de um **schema de referência**. Nas etapas a seguir, &quot;[!DNL Opportunities]&quot; serve como o schema de origem, enquanto &quot;[!DNL Accounts]&quot; atua como o schema de referência.

### Noções básicas sobre identidades em relacionamentos B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Namespace de identidade de referência"
>abstract="O namespace (tipo) do campo de identidade principal do esquema de referência. O schema de referência deve ter um campo de identidade primário estabelecido para participar de um relacionamento. Consulte a documentação para saber mais sobre identidades em relacionamentos B2B."

Para estabelecer uma relação, o schema de referência deve ter uma identidade primária definida. Ao definir uma identidade primária para uma entidade B2B, lembre-se de que as IDs de entidade com base em sequência podem se sobrepor se você estiver coletando em diferentes sistemas ou locais, o que pode levar a conflitos de dados na Platform.

Para isso, todas as classes B2B padrão contêm campos &quot;chave&quot; que estão em conformidade com [[!UICONTROL Origem B2B] tipo de dados](../data-types/b2b-source.md). Esse tipo de dados fornece campos para um identificador de string para a entidade B2B, juntamente com outras informações contextuais sobre a fonte do identificador. Um desses campos, `sourceKey`, concatena os valores dos outros campos no tipo de dados para produzir um identificador totalmente exclusivo para a entidade. Este campo deve ser sempre usado como a identidade primária para esquemas de entidade B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>When [definir um campo XDM como uma identidade](../ui/fields/identity.md), você deve fornecer um namespace de identidade para definir a identidade em. Pode ser um namespace padrão fornecido pelo Adobe ou um namespace personalizado definido pela organização. Na prática, o namespace é simplesmente uma string contextual e pode ser definido como qualquer valor desejado, desde que seja significativo para sua organização categorizar o tipo de identidade. Consulte a visão geral em [namespaces de identidade](../../identity-service/namespaces.md) para obter mais informações.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que um relacionamento seja definido. Anote onde as identidades primárias foram definidas na estrutura do esquema e os namespaces personalizados que usam.

### [!DNL Opportunities] schema

O schema de origem &quot;[!DNL Opportunities]&quot; se baseia no [!UICONTROL Oportunidade de negócios XDM] classe . Um dos campos fornecidos pela classe , `opportunityKey`, serve como o identificador do schema. Especificamente, a variável `sourceKey` no campo `opportunityKey` objeto é definido como a identidade primária do esquema em um namespace personalizado chamado [!DNL B2B Opportunity].

Conforme visto em **[!UICONTROL Propriedades do esquema]**, este esquema foi ativado para uso em [!DNL Real-Time Customer Profile].

![Esquema de Oportunidades](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

O schema de referência &quot;[!DNL Accounts]&quot; se baseia no [!UICONTROL Conta XDM] classe . O nível raiz `accountKey` contém o `sourceKey` que atua como sua identidade primária em um namespace personalizado chamado [!DNL B2B Account]. Este esquema também foi ativado para uso no Perfil.

![Esquema de contas](../images/tutorials/relationship-b2b/accounts.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nome do relacionamento do esquema atual"
>abstract="Um rótulo que descreve a relação do schema atual com o schema de referência (por exemplo, &quot;Conta relacionada&quot;). Esse rótulo é usado em Perfil e segmentação para dar contexto aos dados de entidades B2B relacionadas. Consulte a documentação para saber mais sobre a criação de relações de esquema B2B."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nome do relacionamento do schema de referência"
>abstract="Um rótulo que descreve a relação do schema de referência com o schema atual (por exemplo, &quot;Oportunidades Relacionadas&quot;). Esse rótulo é usado em Perfil e segmentação para dar contexto aos dados de entidades B2B relacionadas. Consulte a documentação para saber mais sobre a criação de relações de esquema B2B."

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado que indique a identidade primária do schema de referência. As classes B2B padrão incluem campos de chave de origem dedicados para entidades de negócios comumente relacionadas. Por exemplo, a variável [!UICONTROL Oportunidade de negócios XDM] classe contém campos de chave de origem para uma conta relacionada (`accountKey`) e uma campanha relacionada (`campaignKey`). No entanto, também é possível adicionar outros [!UICONTROL Origem B2B] campos para o esquema usando grupos de campos personalizados, se você precisar de mais do que os componentes padrão.

>[!NOTE]
>
>Atualmente, apenas relações muitos para um e um para um podem ser definidas de um schema de origem para um schema de referência. Para relacionamentos um para muitos, você deve definir o campo de relacionamento no schema que representa o &quot;muitos&quot;.

Para definir um campo de relacionamento, selecione o ícone de seta (![Ícone de seta](../images/tutorials/relationship-b2b/arrow.png)) ao lado do campo em questão dentro da tela. No caso de [!DNL Opportunities] schema, este é o `accountKey.sourceKey` já que o objetivo é estabelecer uma relação muitos para um com uma conta.

![Botão Relacionamento](../images/tutorials/relationship-b2b/relationship-button.png)

Uma caixa de diálogo é exibida e permite especificar os detalhes da relação. O tipo de relacionamento é automaticamente definido como **[!UICONTROL Muitos para um]**.

![Diálogo de Relacionamento](../images/tutorials/relationship-b2b/relationship-dialog.png)

Em **[!UICONTROL Esquema de referência]**, use a barra de pesquisa para localizar o nome do schema de referência. Quando você destaca o nome do schema de referência, a variável **[!UICONTROL Namespace de identidade de referência]** O campo atualiza automaticamente para o namespace da identidade primária do esquema.

![Esquema de referência](../images/tutorials/relationship-b2b/reference-schema.png)

Em **[!UICONTROL Nome do relacionamento do esquema atual]** e **[!UICONTROL Nome do relacionamento a partir do esquema de referência]**, fornecer nomes amigáveis para o relacionamento no contexto dos schemas de origem e referência, respectivamente. Quando terminar, selecione **[!UICONTROL Salvar]** para aplicar as alterações e salvar o schema.

![Nome do relacionamento](../images/tutorials/relationship-b2b/relationship-name.png)

A tela é exibida novamente, com o campo de relacionamento agora marcado com o nome amigável fornecido anteriormente. O nome do relacionamento também está listado no painel esquerdo para facilitar a referência.

![Relação Aplicada](../images/tutorials/relationship-b2b/relationship-applied.png)

Se você exibir a estrutura do schema de referência, o marcador de relação aparecerá ao lado do campo de identidade principal do schema e no painel esquerdo.

![Marcador de relacionamento do esquema de destino](../images/tutorials/relationship-b2b/destination-relationship.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação muitos para um entre dois schemas usando o [!DNL Schema Editor]. Depois que os dados forem assimilados usando conjuntos de dados baseados nesses esquemas e os dados tiverem sido ativados no armazenamento de dados do Perfil, você poderá usar atributos de ambos os esquemas para [casos de uso de segmentação de várias classes](../../rtcdp/segmentation/b2b.md).
