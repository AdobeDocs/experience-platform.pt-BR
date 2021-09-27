---
title: Definir um relacionamento entre dois esquemas na Plataforma de dados do cliente em tempo real B2B Edition
description: Saiba como definir uma relação muitos para um entre dois esquemas na Plataforma de dados do cliente em tempo real B2B Edition.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Definir uma relação entre dois esquemas na Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>A Plataforma de dados do cliente em tempo real B2B Edition está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

>[!NOTE]
>
>Se você não estiver usando a Plataforma de dados do cliente em tempo real B2B Edition, consulte o guia sobre [como criar um relacionamento não-B2B](./relationship-ui.md) em vez disso.

A Plataforma de dados do cliente em tempo real B2B Edition fornece várias classes de Modelo de dados de experiência (XDM) que capturam entidades fundamentais de dados B2B, incluindo [accounts](../classes/b2b/business-account.md), [Oportunidades](../classes/b2b/business-opportunity.md), [campanhas](../classes/b2b/business-campaign.md) e muito mais. Ao criar schemas com base nessas classes e permitir o uso delas em [Real-time Customer Profile](../../profile/home.md), é possível mesclar dados de fontes diferentes em uma representação unificada chamada de schema de união.

No entanto, os esquemas de união só podem conter campos capturados por esquemas que compartilham a mesma classe. É aqui que os relacionamentos de esquema entram. Ao implementar relacionamentos em seus esquemas B2B, você pode descrever como essas entidades de negócios se relacionam entre si e podem incluir atributos de várias classes em casos de uso de segmentação downstream.

O diagrama a seguir fornece um exemplo de como as diferentes classes B2B podem se relacionar entre si em uma implementação básica:

![Relações de classe B2B](../images/tutorials/relationship-b2b/classes.png)

Este tutorial aborda as etapas para definir uma relação muitos para um entre dois schemas na CDP B2B Edition em tempo real.

>[!NOTE]
>
>Este tutorial foca em como estabelecer relações manualmente entre esquemas B2B na interface do usuário da plataforma. Se estiver trazendo dados de uma conexão de origem B2B, você pode usar um utilitário de geração automática para criar os esquemas, identidades e relacionamentos necessários. Consulte a documentação de fontes em namespaces e esquemas B2B para obter mais informações sobre [usando o utilitário de geração automática](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Introdução

Este tutorial requer uma compreensão funcional de [!DNL XDM System] e do Editor de esquemas na interface do usuário [!DNL Experience Platform]. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no  [!DNL Experience Platform].
* [Noções básicas da composição](../schema/composition.md) do schema: Uma introdução dos blocos de construção dos esquemas XDM.
* [Crie um schema usando o [!DNL Schema Editor]](create-schema-ui.md): Um tutorial sobre as noções básicas de como criar e editar esquemas na interface do usuário do .

## Definir um esquema de origem e de destino

Espera-se que você já tenha criado os dois schemas que serão definidos na relação. Para fins de demonstração, este tutorial cria uma relação entre oportunidades de negócios (definidas em um schema &quot;[!DNL Opportunities]&quot;) e sua conta de negócios associada (definida em um schema &quot;[!DNL Accounts]&quot;).

As relações de esquema são representadas por um campo dedicado dentro de um **schema de origem** que faz referência ao campo de identidade primário de um **schema de destino**. Nas etapas a seguir, &quot;[!DNL Opportunities]&quot; serve como o schema de origem, enquanto &quot;[!DNL Accounts]&quot; atua como o schema de destino.

### Noções básicas sobre identidades em relacionamentos B2B

Para estabelecer uma relação, ambos os esquemas devem ter identidades primárias definidas e devem ser habilitados para [!DNL Real-time Customer Profile]. Ao definir uma identidade primária para uma entidade B2B, lembre-se de que as IDs de entidade com base em sequência podem se sobrepor se você estiver coletando em diferentes sistemas ou locais, o que pode levar a conflitos de dados na Platform.

Para considerar isso, todas as classes B2B padrão contêm campos &quot;chave&quot; que estão em conformidade com o tipo de dados [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Esse tipo de dados fornece campos para um identificador de string para a entidade B2B, juntamente com outras informações contextuais sobre a fonte do identificador. Um desses campos, `sourceKey`, concatena os valores dos outros campos no tipo de dados para produzir um identificador totalmente exclusivo para a entidade. Este campo deve ser sempre usado como a identidade primária para esquemas de entidade B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Ao [definir um campo XDM como uma identidade](../ui/fields/identity.md), você deve fornecer um namespace de identidade para definir a identidade. Pode ser um namespace padrão fornecido pelo Adobe ou um namespace personalizado definido pela organização. Na prática, o namespace é simplesmente uma string contextual e pode ser definido como qualquer valor desejado, desde que seja significativo para sua organização categorizar o tipo de identidade. Consulte a visão geral em [namespaces de identidade](../../identity-service/namespaces.md) para obter mais informações.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que um relacionamento seja definido. Anote onde as identidades primárias foram definidas na estrutura do esquema e os namespaces personalizados que usam.

### [!DNL Opportunities] schema

O schema de origem &quot;[!DNL Opportunities]&quot; é baseado na classe [!UICONTROL Oportunidade de Negócios XDM]. Um dos campos fornecidos pela classe, `opportunityKey`, serve como o identificador do schema. Especificamente, o campo `sourceKey` no objeto `opportunityKey` é definido como a identidade primária do esquema em um namespace personalizado chamado [!DNL B2B Opportunity].
Conforme visto em **[!UICONTROL Propriedades do Esquema]**, este esquema foi ativado para uso em [!DNL Real-time Customer Profile].

![Esquema de Oportunidades](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

O esquema de destino &quot;[!DNL Accounts]&quot; é baseado na classe [!UICONTROL Conta XDM]. O campo `accountKey` de nível raiz contém o `sourceKey` que atua como sua identidade primária em um namespace personalizado chamado [!DNL B2B Account]. Este esquema também foi ativado para uso no Perfil.

![Esquema de contas](../images/tutorials/relationship-b2b/accounts.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado que faça referência à identidade primária do schema de destino. As classes B2B padrão incluem campos de chave de origem dedicados para entidades de negócios comumente relacionadas. Por exemplo, a classe [!UICONTROL Oportunidade de Negócios XDM] contém campos de chave de origem para uma conta relacionada (`accountKey`) e uma campanha relacionada (`campaignKey`). No entanto, também é possível adicionar outros campos [!UICONTROL B2B Source] ao esquema usando grupos de campos personalizados, se você precisar de mais do que os componentes padrão.

>[!NOTE]
>
>Atualmente, apenas relações muitos para um podem ser definidas de um schema de origem para um schema de destino. Para relacionamentos um para muitos, você deve definir o campo de relacionamento no schema que representa o &quot;muitos&quot;.

Para definir um campo de relação, selecione o ícone de seta (![Ícone de seta](../images/tutorials/relationship-b2b/arrow.png)) ao lado do campo em questão na tela. No caso do schema [!DNL Opportunities], esse é o campo `accountKey.sourceKey`, pois o objetivo é estabelecer uma relação muitos para um com uma conta.

![Botão Relacionamento](../images/tutorials/relationship-b2b/relationship-button.png)

Uma caixa de diálogo é exibida e permite especificar os detalhes da relação. O tipo de relacionamento é automaticamente definido como **[!UICONTROL Many-to-one]**.

![Diálogo de Relacionamento](../images/tutorials/relationship-b2b/relationship-dialog.png)

Em **[!UICONTROL Esquema de referência]**, use a barra de pesquisa para localizar o nome do esquema de destino. Quando você destaca o nome do esquema de destino, o campo **[!UICONTROL Namespace de identidade de referência]** atualiza automaticamente para o namespace da identidade primária do esquema.

![Esquema de referência](../images/tutorials/relationship-b2b/reference-schema.png)

Em **[!UICONTROL Relationship Name From Current Schema]** e **[!UICONTROL Relationship Name From Reference Schema]**, forneça nomes amigáveis para a relação no contexto dos esquemas de origem e de destino, respectivamente. Quando terminar, selecione **[!UICONTROL Save]** para aplicar as alterações e salvar o esquema.

![Nome do relacionamento](../images/tutorials/relationship-b2b/relationship-name.png)

A tela é exibida novamente, com o campo de relacionamento agora marcado com o nome amigável fornecido anteriormente. O nome do relacionamento também está listado no painel esquerdo para facilitar a referência.

![Relação Aplicada](../images/tutorials/relationship-b2b/relationship-applied.png)

Se você exibir a estrutura do schema de destino, o marcador de relação aparecerá ao lado do campo de identidade principal do schema e no painel esquerdo.

![Marcador de relacionamento do esquema de destino](../images/tutorials/relationship-b2b/destination-relationship.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação muitos para um entre dois schemas usando o [!DNL Schema Editor]. Depois que os dados forem assimilados usando conjuntos de dados baseados nesses esquemas e os dados tiverem sido ativados no armazenamento de dados do Perfil, você poderá usar atributos de ambos os esquemas para casos de uso de segmentação de várias classes. Consulte a documentação da Real-time CDP B2B Edition para obter mais informações.
