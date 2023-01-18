---
keywords: Experience Platform; home; tópicos populares; controle de acesso; controle de acesso baseado em atributos;
title: Guia completo do controle de acesso baseado em atributos
description: Este documento fornece um guia completo sobre o controle de acesso baseado em atributos no Adobe Experience Platform
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: bf6fd07404ac6d937aa8660a0de024173f24f5c9
workflow-type: tm+mt
source-wordcount: '2425'
ht-degree: 1%

---

# Guia completo do controle de acesso baseado em atributos

O controle de acesso baseado em atributos é um recurso da Adobe Experience Platform que oferece aos clientes com várias marcas e privacidade maior flexibilidade para gerenciar o acesso dos usuários. O acesso a objetos individuais, como campos de esquema e segmentos, pode ser concedido/negado com políticas com base nos atributos e na função do objeto. Esse recurso permite que você conceda ou revogue o acesso a objetos individuais para usuários específicos da Plataforma em sua organização.

Essa funcionalidade permite categorizar campos de esquema, segmentos e assim por diante com rótulos que definem escopos organizacionais ou de uso de dados. É possível aplicar esses mesmos rótulos a jornadas, Ofertas e outros objetos no Adobe Journey Optimizer. Em paralelo, os administradores podem definir políticas de acesso em torno dos campos de esquema do Experience Data Model (XDM) e gerenciar melhor quais usuários ou grupos (usuários internos, externos ou de terceiros) podem acessar esses campos.

>[!NOTE]
>
>Este documento foca no caso de uso das políticas de controle de acesso. Se você estiver tentando configurar políticas para administrar a variável **use** de dados em vez de quais usuários da Platform têm acesso a eles, consulte o guia completo sobre [governança de dados](../../data-governance/e2e.md) em vez disso.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da plataforma:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md): O mecanismo de segmentação em [!DNL Platform] usado para criar segmentos de público-alvo a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.

### Visão geral do caso de uso

Você passará por um exemplo de fluxo de trabalho de controle de acesso baseado em atributos, onde criará e atribuirá funções, rótulos e políticas para configurar se os usuários podem ou não acessar recursos específicos em sua organização. Este guia usa um exemplo de restrição de acesso a dados confidenciais para demonstrar o fluxo de trabalho. Este caso de uso é descrito abaixo:

Você é um provedor de assistência médica e deseja configurar o acesso aos recursos em sua organização.

* Sua equipe interna de marketing deve poder acessar o **[!UICONTROL PHI/ Dados de integridade regulamentados]** dados.
* Sua agência externa não deve poder acessar **[!UICONTROL PHI/ Dados de integridade regulamentados]** dados.

Para fazer isso, você deve configurar funções, recursos e políticas.

Você irá:

* [Rotular as funções para seus usuários](#label-roles): Use o exemplo de um provedor de saúde (ACME Business Group) cujo grupo de marketing trabalha com agências externas.
* [Rotular os recursos (campos de esquema e segmentos)](#label-resources): Atribua o **[!UICONTROL PHI/ Dados de integridade regulamentados]** para recursos e segmentos do schema.
* [Crie a política que os vinculará](#policy): Crie uma política para vincular os rótulos em seus recursos aos rótulos em sua função, negando acesso aos campos e segmentos do esquema. Isso concederá acesso ao campo de esquema e ao segmento em todas as sandboxes para usuários que tenham rótulos correspondentes.

## Permissões

[!UICONTROL Permissões] é a área do Experience Cloud, onde os administradores podem definir funções de usuário e políticas para gerenciar permissões para recursos e objetos em um aplicativo de produto.

Através de [!UICONTROL Permissões], é possível criar e gerenciar funções e atribuir as permissões de recurso desejadas para essas funções. [!UICONTROL As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica.]

Entre em contato com o administrador do sistema para obter acesso se você não tiver privilégios de administrador.

Depois de ter privilégios de administrador, acesse [Adobe Experience Cloud](https://experience.adobe.com/) e faça logon usando suas credenciais do Adobe. Depois de conectado, a variável **[!UICONTROL Visão geral]** for exibida para sua organização, para a qual você tem privilégios de administrador. Esta página mostra os produtos aos quais sua organização está inscrita, juntamente com outros controles para adicionar usuários e administradores à organização. Selecionar **[!UICONTROL Permissões]** para abrir o espaço de trabalho para a integração com a plataforma.

![Imagem que mostra o produto Permissões sendo selecionado no Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

O espaço de trabalho Permissões da interface do usuário da plataforma é exibido, abrindo no **[!UICONTROL Funções]** página.

## Aplicar rótulos a uma função {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="O que são rótulos?"
>abstract="Rótulos permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. A Platform fornece vários rótulos de uso de dados &quot;principais&quot; definidos por Adobe, que abrangem uma grande variedade de restrições comuns aplicáveis à governança de dados. Por exemplo, rótulos &quot;S&quot; sensíveis, como RHD (Dados Regulamentados de Integridade) permitem categorizar dados que se referem a Informações de Integridade Protegidas (PHI). Você também pode definir seus próprios rótulos personalizados que atendem às necessidades de sua organização."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Visão geral dos rótulos de uso de dados"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Criar novo rótulo"
>abstract="Você pode criar seus próprios rótulos personalizados para atender às necessidades de sua organização. Os rótulos personalizados podem ser usados para aplicar as configurações de controle de dados e de controle de acesso aos seus dados."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Gerenciar rótulos personalizados"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Quais são as funções?"
>abstract="As funções são formas de categorizar os tipos de usuários que interagem com sua instância da plataforma e são blocos fundamentais das políticas de controle de acesso. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso de exibição ou gravação necessário."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Gerenciar funções"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Criar nova função"
>abstract="Você pode criar uma nova função para categorizar melhor os usuários que estão acessando sua instância da plataforma. Por exemplo, você pode criar uma função para uma Equipe de marketing interno e aplicar o rótulo de RHD a essa função, permitindo que sua Equipe de marketing interno acesse Informações de integridade protegida (PHI). Como alternativa, você também pode criar uma função para uma Agência Externa e negar esse acesso de função aos dados de PHI ao não aplicar o rótulo de RHD a essa função."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Criar uma nova função"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Visão geral da função"
>abstract="A caixa de diálogo Visão geral da função exibe os recursos e as sandboxes que uma determinada função tem permissão para acessar."

As funções são formas de categorizar os tipos de usuários que interagem com sua instância da plataforma e são blocos fundamentais das políticas de controle de acesso. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso necessário.

Para começar, selecione **[!UICONTROL Grupo Funcional ACME]** do **[!UICONTROL Funções]** página.

![Imagem mostrando a função comercial ACME selecionada nas funções](../images/abac-end-to-end-user-guide/abac-select-role.png)

Em seguida, selecione **[!UICONTROL Rótulos]** e depois selecione **[!UICONTROL Adicionar rótulos]**.

![Imagem que mostra Adicionar rótulos sendo selecionado na guia Rótulos](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Uma lista de todos os rótulos em sua organização é exibida. Selecionar **[!UICONTROL RHD]** para adicionar o rótulo de **[!UICONTROL PHI/Dados de saúde regulamentados]**. Aguarde alguns instantes até que uma marca de seleção azul apareça ao lado do rótulo e selecione **[!UICONTROL Salvar]**.

![Imagem que mostra o rótulo RHD que está sendo selecionado e salvo](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Ao adicionar um grupo de organizações a uma função, todos os usuários desse grupo serão adicionados à função . Quaisquer alterações no grupo da organização (usuários removidos ou adicionados) serão automaticamente atualizadas na função.

## Aplicar rótulos a campos de esquema {#label-resources}

Agora que você configurou uma função de usuário com o [!UICONTROL RHD] , a próxima etapa é adicionar esse mesmo rótulo aos recursos que você deseja controlar para essa função.

Selecionar **[!UICONTROL Esquemas]** no menu de navegação esquerdo e selecione **[!UICONTROL Assistência médica ACME]** na lista de schemas que são exibidos.

![Imagem que mostra o esquema ACME Healthcare que está sendo selecionado na guia Schemas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Em seguida, selecione **[!UICONTROL Rótulos]** para ver uma lista que exibe os campos associados ao esquema. Aqui, é possível atribuir rótulos a um ou vários campos ao mesmo tempo. Selecione o **[!UICONTROL Glicose no sangue]** e **[!UICONTROL InsulinLevel]** e selecione **[!UICONTROL Aplicar rótulos de acesso e governança de dados]**.

![Imagem que mostra o BloodGlicose e o InsulinLevel selecionados e que aplica rótulos de acesso e de governança de dados selecionados](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

O **[!UICONTROL Editar rótulos]** for exibida, permitindo escolher os rótulos que deseja aplicar aos campos de esquema. Para esse caso de uso, selecione a variável **[!UICONTROL PHI/ Dados de integridade regulamentados]** rótulo, depois selecione **[!UICONTROL Salvar]**.

![Imagem que mostra o rótulo RHD que está sendo selecionado e salvo](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando um rótulo é adicionado a um campo, esse rótulo é aplicado ao recurso pai desse campo (uma classe ou um grupo de campos). Se a classe pai ou o grupo de campos for empregado por outros schemas, esses schemas herdarão o mesmo rótulo.

## Aplicar rótulos a segmentos

Após concluir a rotulagem dos campos de esquema, você pode começar a rotular os segmentos.

Selecionar **[!UICONTROL Segmentos]** no painel de navegação esquerdo. Uma lista de segmentos disponíveis na organização é exibida. Neste exemplo, os dois segmentos a seguir devem ser rotulados, pois contêm dados confidenciais de integridade:

* Glicose no sangue >100
* Insulina &lt;50

Selecionar **[!UICONTROL Glicose no sangue >100]** para começar a rotular o segmento.

![Imagem que mostra a seleção de glucose no sangue >100 na guia Segmentos](../images/abac-end-to-end-user-guide/abac-select-segment.png)

O segmento **[!UICONTROL Detalhes]** será exibida. Selecionar **[!UICONTROL Gerenciar acesso]**.

![Imagem que mostra a seleção do acesso Gerenciar](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

O **[!UICONTROL Editar rótulos]** for exibida, permitindo escolher os rótulos que deseja aplicar ao segmento. Para esse caso de uso, selecione a variável **[!UICONTROL PHI/ Dados de integridade regulamentados]** rótulo, depois selecione **[!UICONTROL Salvar]**.

![Imagem que mostra a seleção do rótulo RHD e salvamento selecionado](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Repita as etapas acima com **[!UICONTROL Insulina &lt;50]**.

## Criar uma política de controle de acesso {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Quais são as políticas?"
>abstract="Políticas são declarações que reúnem atributos para estabelecer ações admissíveis e não permissíveis. Cada organização vem com uma política padrão que você deve ativar para definir regras para recursos como segmentos e campos de esquema. As políticas padrão não podem ser editadas nem excluídas. No entanto, as políticas padrão podem ser ativadas ou desativadas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Gerenciar políticas"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Criar uma política"
>abstract="Crie uma política para definir as ações que seus usuários podem ou não realizar em relação aos seus segmentos e campos de esquema."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Criar uma política"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configurar as ações permitidas e não permitidas para uma política"
>abstract="A <b>negar acesso ao</b> a política negará aos usuários acesso quando os critérios forem atendidos. Combinado com <b>Sendo falso</b> - o acesso será negado a todos os usuários, a menos que eles atendam aos critérios correspondentes definidos. Esse tipo de política permite proteger um recurso sensível e permitir acesso somente a usuários com rótulos correspondentes. <br>A <b>permitir o acesso a</b> a política permitirá que os usuários acessem quando os critérios forem atendidos. Quando combinado com <b>Sendo verdadeiro o seguinte</b> - os usuários receberão acesso se atenderem aos critérios correspondentes definidos. Isso não nega explicitamente o acesso aos usuários, mas adiciona um acesso de permissão. Esse tipo de política permite que você dê acesso adicional ao recurso e, além dos usuários que já podem ter acesso por meio de permissões de função.&quot;</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Editar uma política"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configurar permissões para um recurso"
>abstract="Um recurso é o ativo ou objeto que um usuário pode ou não acessar. Os recursos podem ser segmentos ou campos de esquemas. Você pode configurar permissões de gravação, leitura ou exclusão para segmentos e campos de esquema."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Editar condições"
>abstract="Aplique declarações condicionais à sua política para configurar o acesso do usuário a determinados recursos. Selecione corresponder tudo para exigir que os usuários tenham funções com os mesmos rótulos de um recurso para ter acesso permitido. Selecione qualquer correspondência para exigir que os usuários tenham uma função com apenas um rótulo correspondente a um rótulo em um recurso. Os rótulos podem ser definidos como rótulos principais ou personalizados, com rótulos principais representando rótulos criados e fornecidos por rótulos Adobe e personalizados representando rótulos criados para sua organização."

As políticas de controle de acesso usam rótulos para definir quais funções de usuário têm acesso a recursos específicos da plataforma. As políticas podem ser locais ou globais e podem substituir outras políticas. Neste exemplo, o acesso aos campos e segmentos do schema será negado em todas as sandboxes para usuários que não tenham os rótulos correspondentes no campo schema .

>[!NOTE]
>
>Uma &quot;política de negação&quot; é criada para conceder acesso a recursos confidenciais porque a função concede permissão para os assuntos. A política escrita neste exemplo **nega** você acessa se não tiver os rótulos obrigatórios.

Para criar uma política de controle de acesso, selecione **[!UICONTROL Permissões]** no menu de navegação esquerdo e selecione **[!UICONTROL Políticas]**. Em seguida, selecione **[!UICONTROL Criar política]**.

![Imagem que mostra a opção Criar política selecionada nas Permissões](../images/abac-end-to-end-user-guide/abac-create-policy.png)

O **[!UICONTROL Criar nova política]** for exibida, solicitando a inserção de um nome e uma descrição opcional. Selecionar **[!UICONTROL Confirmar]** quando terminar.

![Imagem que mostra a caixa de diálogo Criar nova política e selecionar Confirmar](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Para negar acesso aos campos do schema, use a seta suspensa e selecione **[!UICONTROL Negar acesso a]** e depois selecione **[!UICONTROL Nenhum recurso selecionado]**. Em seguida, selecione **[!UICONTROL Campo de esquema]** e depois selecione **[!UICONTROL Todos]**.

![Imagem que mostra o acesso Negar e os recursos selecionados](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

A tabela abaixo mostra as condições disponíveis ao criar uma política:

| Condições | Descrição |
| --- | --- |
| Sendo falso | Quando a opção &quot;Negar acesso a&quot; estiver definida, o acesso será restrito se o usuário não atender aos critérios selecionados. |
| Sendo verdadeiro o seguinte | Quando a opção &quot;Permitir acesso a&quot; estiver definida, o acesso será permitido se o usuário atender aos critérios selecionados. |
| Corresponde a qualquer | O usuário tem um rótulo que corresponde a qualquer rótulo aplicado a um recurso. |
| Corresponde a tudo | O usuário tem todos os rótulos que correspondem a todos os rótulos aplicados a um recurso. |
| Rótulo principal | Um rótulo principal é um rótulo definido por Adobe que está disponível em todas as instâncias da plataforma. |
| Rótulo personalizado | Um rótulo personalizado é um rótulo que foi criado pela sua organização. |

Selecionar **[!UICONTROL Sendo falso]** e depois selecione **[!UICONTROL Nenhum atributo selecionado]**. Em seguida, selecione o usuário **[!UICONTROL Rótulo principal]**, em seguida selecione **[!UICONTROL Corresponde a tudo]**. Selecionar o recurso **[!UICONTROL Rótulo principal]** e finalmente selecione **[!UICONTROL Adicionar recurso]**.

![Imagem que mostra as condições que estão sendo selecionadas e Adicionar recurso que está sendo selecionado](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Um recurso é o ativo ou objeto que um assunto pode ou não acessar. Os recursos podem ser segmentos ou esquemas.

Para negar acesso aos segmentos, use a seta suspensa e selecione **[!UICONTROL Negar acesso a]** e depois selecione **[!UICONTROL Nenhum recurso selecionado]**. Em seguida, selecione **[!UICONTROL Segmento]** e depois selecione **[!UICONTROL Todos]**.

Selecionar **[!UICONTROL Sendo falso]** e depois selecione **[!UICONTROL Nenhum atributo selecionado]**. Em seguida, selecione o usuário **[!UICONTROL Rótulo principal]**, em seguida selecione **[!UICONTROL Corresponde a tudo]**. Selecionar o recurso **[!UICONTROL Rótulo principal]** e finalmente selecione **[!UICONTROL Salvar]**.

![Imagem mostrando as condições selecionadas e Salvar sendo selecionado](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Selecionar **[!UICONTROL Ativar]** para ativar a política, é exibida uma caixa de diálogo que solicita que você confirme a ativação. Selecionar **[!UICONTROL Confirmar]** e depois selecione **[!UICONTROL Fechar]**.

![Imagem que mostra a Política sendo ativada ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Próximas etapas

Você concluiu a aplicação de rótulos a uma função, campos de esquema e segmentos. A agência externa atribuída a essas funções é restrita de visualizar esses rótulos e seus valores no esquema, conjunto de dados e exibição de perfil. Esses campos também não podem ser usados na definição do segmento ao usar o Construtor de segmentos.

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte o [visão geral do controle de acesso baseado em atributos](./overview.md).
