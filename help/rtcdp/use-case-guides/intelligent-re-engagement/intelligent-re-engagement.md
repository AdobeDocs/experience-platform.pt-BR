---
title: Reengajamento inteligente
description: Ofereça experiências atraentes e conectadas durante os principais momentos de conversão para engajar novamente clientes pouco frequentes de forma inteligente.
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 7%

---

# Engaje novamente clientes de uma forma inteligente para que retornem

Reenvolva os clientes que abandonaram uma conversão antes de concluí-la de forma inteligente e responsável. Envolva os clientes obsoletos por meio de experiências, em vez de lembretes, para aprimorar a conversão e impulsionar o crescimento do valor vitalício do cliente.

Empregue considerações em tempo real, considere todas as qualidades e comportamentos do consumidor e ofereça requalificação rápida com base em eventos online e offline.

![Visão geral visual de alto nível passo a passo com reengajamento inteligente.](../intelligent-re-engagement/images/step-by-step.png)

## Visão geral do caso de uso

Você construirá esquemas, conjuntos de dados e públicos à medida que trabalhar com exemplos de jornadas de reengajamento. Você também descobrirá os recursos necessários para configurar as jornadas de exemplo no [!DNL Adobe Journey Optimizer] e os necessários para criar anúncios de mídia paga em destinos. Este guia usa exemplos de reengajamento dos clientes nas jornadas de caso de uso descritas abaixo:

* **Jornada de reengajamento** - Segmenta os clientes que abandonaram a navegação de produtos no site e no aplicativo móvel.
* **Jornada de carrinho abandonada** - Segmenta os clientes que colocaram produtos no carrinho, mas ainda não foram comprados no site e no aplicativo móvel.
* **Jornada de confirmação de pedido** - Concentra-se nas compras de produtos feitas pelo site e pelo aplicativo móvel.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao concluir as etapas para implementar o caso de uso, você usará a seguinte funcionalidade e elementos da interface da Real-Time CDP (listados na ordem em que serão usados). Verifique se tem as permissões de controle de acesso baseado em atributo necessárias para todas essas áreas, ou solicite ao(à) administrador(a) que as conceda a você.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integra dados em fontes de dados para alimentar a campanha. Esses dados são usados para criar os públicos-alvo da campanha e exibir elementos de dados personalizados usados no email e nos blocos promocionais da Web (por exemplo, nome ou informações relacionadas à conta). A CDP também é usada para ativar públicos-alvo no email e na Web (via [!DNL Adobe Target]).
   * [Esquemas](/help/xdm/home.md)
   * [Perfis](/help/profile/home.md)
   * [Conjuntos de dados](/help/catalog/datasets/overview.md)
   * [Públicos-alvo](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Destinos](/help/destinations/home.md)
   * [Acionador de evento ou público-alvo](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Públicos/ eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=pt-BR)
   * [Jornada ações](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

Abaixo está uma visão geral de alto nível das três jornadas de reengajamento de exemplo.

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

A jornada de reengajamento é direcionada à navegação abandonada de produtos no site e no aplicativo móvel. Essa jornada é disparada quando um produto foi visualizado, mas não foi comprado ou adicionado ao carrinho. O engajamento com a marca é acionado após três dias se não houver adições à lista nas últimas 24 horas.<p>![Visão geral visual de alto nível da jornada de reengajamento inteligente do cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Visão geral visual de alto nível da jornada de reengajamento inteligente do cliente."){width="2560" zoomable="yes"}</p>

1. Você cria esquemas e conjuntos de dados e, em seguida, marca para [!UICONTROL Perfil].
2. Os dados são integrados ao Experience Platform via SDK da Web, SDK de borda móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **cliente** fez um compromisso nos últimos três dias.
5. Você cria uma jornada de reengajamento no [!DNL Adobe Journey Optimizer].
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. [!DNL Adobe Journey Optimizer] O verifica o consentimento e envia as várias ações configuradas.

>[!TAB Jornada de carrinho abandonada]

A jornada do carrinho abandonado tem como alvo os produtos que foram colocados no carrinho, mas que ainda não foram comprados no site e no aplicativo móvel. Além disso, as campanhas de Mídia paga são iniciadas e interrompidas usando esse método.<p>![O cliente abandonou a visão geral de alto nível da jornada do carrinho.](../intelligent-re-engagement/images/abandoned-cart-journey.png "O cliente abandonou a visão geral de alto nível da jornada do carrinho."){width="2560" zoomable="yes"}</p>

1. Você cria esquemas e conjuntos de dados, a marca de [!UICONTROL Perfil].
2. Os dados são integrados ao Experience Platform via SDK da Web, SDK de borda móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **cliente** colocou um item no carrinho, mas não concluiu a compra. A variável **[!UICONTROL Adicionar ao carrinho]** O evento inicia um temporizador que aguarda 30 minutos e verifica a compra. Se nenhuma compra tiver sido feita, a variável **cliente** é adicionado à **[!UICONTROL Abandonar carrinho]** públicos-alvo.
5. Você cria uma jornada de carrinho abandonada no [!DNL Adobe Journey Optimizer].
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. [!DNL Adobe Journey Optimizer] O verifica o consentimento e envia as várias ações configuradas.

>[!TAB Jornada de confirmação de pedido]

A jornada de confirmação de pedido se concentra nas compras de produtos feitas pelo site e pelo aplicativo móvel.<p>![Visão geral visual de alto nível da jornada de confirmação de pedido do cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Visão geral visual de alto nível da jornada de confirmação de pedido do cliente."){width="2560" zoomable="yes"}</p>

1. Você cria esquemas e conjuntos de dados e, em seguida, marca para [!UICONTROL Perfil].
2. Os dados são integrados ao Experience Platform via SDK da Web, SDK de borda móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Você cria uma jornada de confirmação no [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] O envia uma mensagem de confirmação de pedido usando o canal preferencial.

>[!ENDTABS]

## Como obter o caso de uso {#achieve-use-case-instruction}

Para concluir cada uma das etapas das visões gerais de alto nível acima, leia as seções abaixo, que oferecem links para mais informações e instruções mais detalhadas.

### Elementos e funcionalidade da interface que serão utilizados {#ui-functionality-and-elements}

Ao concluir as etapas para implementar o caso de uso, você usará a funcionalidade do Real-Time CDP e os elementos da interface do usuário listados no início deste documento. Verifique se tem as permissões de controle de acesso baseado em atributo necessárias para todas essas áreas, ou solicite ao(à) administrador(a) que as conceda a você.

### Criar um design de esquema e especificar grupos de campos {#schema-design}

Os recursos do Experience Data Model (XDM) são gerenciados no [!UICONTROL Esquemas] espaço de trabalho no [!DNL Adobe Experience Platform]. Você pode visualizar e explorar os recursos principais fornecidos pelo [!DNL Adobe] (por exemplo, [!UICONTROL Grupos de campos]) e criar recursos e esquemas personalizados para sua organização.

Para obter mais informações sobre como criar [schemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR), leia o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md)

Há quatro designs de esquema que são usados para o caso de uso de reengajamento. Cada esquema requer a configuração de campos específicos e de alguns campos altamente sugeridos.

#### Esquema de atributos do cliente

Esse esquema é usado para estruturar e fazer referência aos dados do perfil que compõem as informações do cliente. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] por meio do seu CRM ou sistema semelhante e é necessário para consultar os detalhes do cliente usados para recursos de personalização, consentimento de marketing e segmentação aprimorada.

O esquema de atributos do cliente é representado por um [!UICONTROL Perfil individual XDM] que inclui os seguintes grupos de campos:

+++Detalhes de contato pessoal (grupo de campos)

[Detalhes de contato pessoal](/help/xdm/field-groups/profile/personal-contact-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM que descreve as informações de contato de uma pessoa individual.

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `mobilePhone.number` | Obrigatório | O número do celular da pessoa, que será usado para SMS. |
| `personalEmail.address` | Obrigatório | O endereço de email da pessoa. |

+++

+++Detalhes demográficos (Grupo de campos)

[Detalhes demográficos](/help/xdm/field-groups/profile/demographic-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM. O grupo de campos fornece um objeto de pessoa de nível raiz, cujos subcampos descrevem informações sobre uma pessoa individual.

| Campos | Requisito |
| --- | --- |
| `person.name.firstName` | Sugerido |
| `person.name.lastName` | Sugerido |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

[Atributos de auditoria do sistema de origem externa](/help/xdm/data-types/external-source-system-audit-attributes.md) é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

+++Grupos de campos de consentimento e preferência (Grupo de campos)

[Os consentimentos e preferências](/help/xdm/field-groups//profile/consents.md) grupo de campos fornece um único campo do tipo objeto, consentimentos, para capturar informações de consentimento e preferência.

| Campos | Requisito |
| --- | --- |
| `consents.marketing.email.val` | Obrigatório |
| `consents.marketing.preferred` | Obrigatório |
| `consents.marketing.push.val` | Obrigatório |
| `consents.marketing.sms.val` | Obrigatório |
| `consents.personalize.content.val` | Obrigatório |
| `consents.share.val` | Obrigatório |

+++

+++Detalhes do teste de perfil (grupo de campos)

Este grupo de campos é usado para prática recomendada.

+++

#### Esquema de transações digitais do cliente

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre no seu site e/ou plataformas digitais associadas. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] pelo SDK da Web e é necessário para fazer referência aos vários eventos de navegação e conversão usados para acionar jornadas, análises detalhadas de clientes online e recursos aprimorados de segmentação.

O schema de transações digitais do cliente é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++ExperienceEvent do SDK da Web do Adobe Experience Platform (Grupo de campos)

| Campos | Requisito |
| --- | --- |
| `device.model` | Sugerido |
| `environment.browserDetails.userAgent` | Sugerido |

+++

+++Detalhes da Web (Grupo de Campos)

Detalhes da Web é um grupo de campos de esquema padrão para a classe XDM ExperienceEvent, usado para descrever informações sobre eventos de detalhes da Web, como interação, detalhes da página e referenciador.

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Sugerido | A ID do link da Web ou URL que corresponde à interação. |
| `web.webInteraction.linkClicks.value` | Sugerido | O número de cliques do link da web ou URL que corresponde à interação. |
| `web.webInteraction.name` | Sugerido | O nome da página da Web. |
| `web.webInteraction.URL` | Sugerido | O URL da página da Web. |
| `web.webPageDetails.name` | Sugerido | O nome da página da Web onde ocorreu a interação da Web. |
| `web.webPageDetails.URL` | Sugerido | A URL da página da Web em que ocorreu a interação da Web. |
| `web.webReferrer.URL` | Sugerido | Descreve o referenciador de uma interação da web, que é o URL de onde um visitante veio imediatamente antes de a interação da web atual ser registrada. |

+++

+++Evento de experiência do consumidor (grupo de campos)

| Campos | Requisito |
| --- | --- |
| `commerce.cart.cartID` | Sugerido |
| `commerce.cart.cartSource` | Sugerido |
| `commerce.cartAbandons.id` | Sugerido |
| `commerce.cartAbandons.value` | Sugerido |
| `commerce.order.orderType` | Sugerido |
| `commerce.order.payments.paymentAmount` | Sugerido |
| `commerce.order.payments.paymentType` | Sugerido |
| `commerce.order.payments.transactionID` | Sugerido |
| `commerce.order.priceTotal` | Sugerido |
| `commerce.order.purchaseID` | Sugerido |
| `commerce.productListAdds.id` | Sugerido |
| `commerce.productListAdds.value` | Sugerido |
| `commerce.productListOpens.id` | Sugerido |
| `commerce.productListOpens.value` | Sugerido |
| `commerce.productListRemoval.id` | Sugerido |
| `commerce.productListRemoval.value` | Sugerido |
| `commerce.productListViews.id` | Sugerido |
| `commerce.productListViews.value` | Sugerido |
| `commerce.productViews.id` | Sugerido |
| `commerce.productViews.value` | Sugerido |
| `commerce.purchases.id` | Sugerido |
| `commerce.purchases.value` | Sugerido |
| `marketing.campaignGroup` | Sugerido |
| `marketing.campaignName` | Sugerido |
| `marketing.trackingCode` | Sugerido |
| `productListItems.name` | Sugerido |
| `productListItems.priceTotal` | Sugerido |
| `productListItems.product` | Sugerido |
| `productListItems.quantity` | Sugerido |

+++

+++Detalhes da ID do usuário final (Grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Obrigatório | Estado autenticado da ID do endereço de email do usuário final. |
| `endUserIDs._experience.emailid.id` | Obrigatório | ID do endereço de email do usuário final. |
| `endUserIDs._experience.emailid.namespace.code` | Obrigatório | Código de namespace da ID do endereço de email do usuário final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obrigatório | [!DNL Adobe] Estado autenticado da ID do Marketing Cloud (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obrigatório | [!DNL Adobe] ID DO Marketing Cloud (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obrigatório | [!DNL Adobe] Código de namespace da ID do Marketing Cloud (MCID). |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

#### Esquema de transações offline do cliente

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre em plataformas fora do site. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] de um PDV (ou sistema semelhante) e geralmente transmitido para a Platform por meio de uma conexão de API. Seu objetivo é fazer referência aos vários eventos de conversão offline usados para acionar jornadas, análises profundas de clientes online e offline e recursos aprimorados de segmentação.

O schema de transações offline do cliente é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++Detalhes do comércio (Grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `commerce.cart.cartID` | Obrigatório | Uma ID para o carrinho de compras. |
| `commerce.order.orderType` | Obrigatório | Um objeto que descreve o tipo de pedido do produto. |
| `commerce.order.payments.paymentAmount` | Obrigatório | Um objeto que descreve o valor do pagamento da ordem do produto. |
| `commerce.order.payments.paymentType` | Obrigatório | Um objeto que descreve o tipo de pagamento de ordem de produto. |
| `commerce.order.payments.transactionID` | Obrigatório | Um ID de transação de ordem de produto de objeto. |
| `commerce.order.purchaseID` | Obrigatório | Uma ID de compra da ordem de produto do objeto. |
| `productListItems.name` | Obrigatório | Uma lista de nomes de itens que representam os produtos selecionados por um cliente. |
| `productListItems.priceTotal` | Obrigatório | O preço total da lista de itens que representam os produtos selecionados por um cliente. |
| `productListItems.product` | Obrigatório | Os produtos selecionados. |
| `productListItems.quantity` | Obrigatório | A quantidade de itens da lista que representam os produtos selecionados por um cliente. |

+++

+++Detalhes de contato pessoal (grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `mobilePhone.number` | Obrigatório | O número do celular da pessoa, que será usado para SMS. |
| `personalEmail.address` | Obrigatório | O endereço de email da pessoa. |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

#### Esquema do conector web do Adobe

>[!NOTE]
>
>Essa é uma implementação opcional se você estiver usando o [!DNL Adobe Analytics Data Connector].

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre no seu site e/ou plataformas digitais associadas. Esse esquema é semelhante ao esquema Transações digitais do cliente, mas difere na medida em que deve ser usado quando o SDK da Web não é uma opção para a coleta de dados; portanto, esse esquema é necessário quando você está utilizando o [!DNL Adobe Analytics Data Connector] para enviar seus dados online para o [!DNL Adobe Experience Platform] como um fluxo de dados primário ou secundário.

A variável [!DNL Adobe] o esquema do conector da web é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++Modelo de evento de experiência do Adobe Analytics (grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Sugerido | A ID do link da Web ou URL que corresponde à interação. |
| `web.webInteraction.linkClicks.value` | Sugerido | O número de cliques do link da web ou URL que corresponde à interação. |
| `web.webInteraction.name` | Sugerido | O nome da página da Web. |
| `web.webInteraction.URL` | Sugerido | O URL da página da Web. |
| `web.webPageDetails.name` | Sugerido | O nome da página da Web onde ocorreu a interação da Web. |
| `web.webPageDetails.URL` | Sugerido | A URL da página da Web em que ocorreu a interação da Web. |
| `web.webReferrer.URL` | Sugerido | Descreve o referenciador de uma interação da web, que é o URL de onde um visitante veio imediatamente antes de a interação da web atual ser registrada. |
| `commerce.cart.cartID` | Sugerido | |
| `commerce.cart.cartSource` | Sugerido | |
| `commerce.cartAbandons.id` | Sugerido | |
| `commerce.cartAbandons.value` | Sugerido | |
| `commerce.order.orderType` | Sugerido | |
| `commerce.order.payments.paymentAmount` | Sugerido | |
| `commerce.order.payments.paymentType` | Sugerido | |
| `commerce.order.payments.transactionID` | Sugerido | |
| `commerce.order.priceTotal` | Sugerido | |
| `commerce.order.purchaseID` | Sugerido | |
| `commerce.productListAdds.id` | Sugerido | |
| `commerce.productListAdds.value` | Sugerido | |
| `commerce.productListOpens.id` | Sugerido | |
| `commerce.productListOpens.value` | Sugerido | |
| `commerce.productListRemoval.id` | Sugerido | |
| `commerce.productListRemoval.value` | Sugerido | |
| `commerce.productListViews.id` | Sugerido | |
| `commerce.productListViews.value` | Sugerido | |
| `commerce.productViews.id` | Sugerido | |
| `commerce.productViews.value` | Sugerido | |
| `commerce.purchases.id` | Sugerido | |
| `commerce.purchases.value` | Sugerido | |
| `marketing.campaignGroup` | Sugerido | |
| `marketing.campaignName` | Sugerido | |
| `marketing.trackingCode` | Sugerido | |
| `productListItems.name` | Sugerido | |
| `productListItems.priceTotal` | Sugerido | |
| `productListItems.product` | Sugerido | |
| `productListItems.quantity` | Sugerido | |
| `endUserIDs._experience.emailid.authenticatedState` | Obrigatório | Estado autenticado da ID do endereço de email do usuário final. |
| `endUserIDs._experience.emailid.id` | Obrigatório | ID do endereço de email do usuário final. |
| `endUserIDs._experience.emailid.namespace.code` | Obrigatório | Código de namespace da ID do endereço de email do usuário final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obrigatório | [!DNL Adobe] Estado autenticado da ID do Marketing Cloud (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obrigatório | [!DNL Adobe] ID DO Marketing Cloud (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obrigatório | [!DNL Adobe] Código de namespace da ID do Marketing Cloud (MCID). |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

### Criar um conjunto de dados a partir de um esquema {#dataset-from-schema}

Um conjunto de dados é uma estrutura de armazenamento e gerenciamento para um grupo de dados. Cada esquema para jornadas inteligentes de reengajamento tem um único conjunto de dados.

Para obter mais informações sobre como criar uma [conjunto de dados](/help/catalog/datasets/overview.md) de um esquema, leia o [Guia da interface do usuário de conjuntos de dados](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Semelhante à etapa para criar um esquema, é necessário ativar o conjunto de dados para ser incluído no Perfil do cliente em tempo real. Para obter mais informações sobre como habilitar o conjunto de dados para uso no perfil do cliente em tempo real, leia o [tutorial de criação de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Privacidade, consentimento e governança de dados {#privacy-consent}

#### Políticas de consentimento

>[!IMPORTANT]
>
>Oferecer aos clientes a capacidade de cancelar a inscrição para receber comunicações de uma marca é um requisito legal, bem como garantir que essa escolha seja respeitada. Saiba mais sobre a legislação aplicável na [Visão geral das regras de privacidade](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Ao criar um caminho de reengajamento, as seguintes [políticas de consentimento](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) deve ser considerada:

* Se `consents.marketing.email.val = "Y"` pode enviar email
* Se `consents.marketing.sms.val = "Y"` depois pode SMS
* Se `consents.marketing.push.val = "Y"` depois, pode enviar
* Se `consents.share.val = "Y"` depois, pode anunciar

#### Rótulo e aplicação da governança de dados

Ao criar um caminho de reengajamento, as seguintes [Rótulos de governança de dados](/help/data-governance/labels/overview.md) deve ser considerada:

* Os endereços de email pessoais são utilizados como dados diretos identificáveis usados para identificar ou entrar em contato com um indivíduo específico, em vez de com um dispositivo.
   * `personalEmail.address = I1`

#### Políticas de marketing

Não há [políticas de marketing](/help/data-governance/policies/overview.md) necessário para as jornadas de reengajamento, no entanto, os itens a seguir devem ser considerados conforme desejado:

* Restringir Dados Confidenciais
* Restringir publicidade no local
* Restringir o direcionamento de email
* Restringir o direcionamento entre sites
* Restringir a combinação de dados diretamente identificáveis com dados anônimos

### Criar um público-alvo {#create-audience}

#### Criação de público-alvo para jornadas de reengajamento da marca

As jornadas de reengajamento usam públicos para definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Os públicos-alvo podem ser criados de várias maneiras no [!DNL Adobe Experience Platform].

Para obter mais informações sobre como criar um público-alvo, leia a [Guia da interface do usuário do serviço de público-alvo](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Para obter mais informações sobre como compor diretamente [Públicos-alvo](/help/segmentation/home.md), leia o [Guia da interface do usuário da Composição de público-alvo](/help/segmentation/ui/audience-composition.md).

Para obter mais informações sobre como criar públicos-alvo por meio de definições de segmento derivadas da plataforma, leia a [Guia da interface do usuário do Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

Esse público-alvo é criado como um aprimoramento do cenário clássico de &quot;Abandono do carrinho&quot;. Enquanto o abandono do carrinho geralmente se concentra em uma adição ao carrinho sem uma compra subsequente em um determinado período de tempo, esse público-alvo busca um envolvimento anterior, especificamente aqueles que podem ter navegado em um produto específico, mas não o adicionaram ao carrinho e não tiveram nenhuma atividade de acompanhamento no site em um determinado período de tempo. Esse público-alvo ajuda a manter sua marca no topo da mente para os clientes que atendem a esse critério de inclusão e também pode ser aproveitado para clientes cujas propriedades digitais podem diferir de um modelo de comércio eletrônico tradicional.

Os eventos a seguir são usados para a jornada de reengajamento, em que os usuários visualizaram produtos online e não adicionaram ao carrinho nas próximas 24 horas, seguidos por nenhum engajamento da marca nos 3 dias seguintes.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

O descritor da jornada de reengajamento é exibido como:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Jornada de carrinho abandonada]

Esse público-alvo é criado para oferecer suporte ao cenário clássico de &quot;Abandono do carrinho&quot;. Seu objetivo é encontrar clientes que adicionaram um produto ao carrinho de compras, mas que não fizeram uma compra. Esse público-alvo ajudará a manter não apenas a sua marca no topo da mente dos seus clientes, mas também os produtos que eles deixaram para trás sem uma compra subsequente.

Os eventos a seguir são usados para a jornada de carrinho abandonada, em que os usuários adicionaram um produto ao carrinho, mas não concluíram a compra ou limparam o carrinho nas últimas 24 horas.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

O descritor da jornada do carrinho abandonado é exibido como:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Jornada de confirmação de pedido]

Esta jornada não requer a criação de públicos-alvo.

>[!ENDTABS]

### Configuração do Jornada no Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] não abrange tudo o que é mostrado nos diagramas. Todos [anúncios de mídia paga](/help/destinations/catalog/social/overview.md) são criados em [!UICONTROL Destinos].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) O ajuda a fornecer experiências conectadas, contextuais e personalizadas aos clientes. A jornada do cliente envolve todo o processo de interação do cliente com a marca. Cada jornada de caso de uso requer informações específicas. Os dados precisos necessários para cada ramificação de Jornada estão listados abaixo.

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

A jornada de reengajamento é direcionada à navegação abandonada de produtos no site e no aplicativo móvel.<p>![Visão geral visual de alto nível da jornada de reengajamento inteligente do cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Visão geral visual de alto nível da jornada de reengajamento inteligente do cliente."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 1: visualizações do produto
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType = commerce.productViews`
      * Campos:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 2: Adicionar ao carrinho
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType = commerce.productListAdds`
      * Campos:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Engajamento com a marca
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campos:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Lógica de Jornada de tecla

* Jornada Lógica de Entrada
   * Evento de exibição de produto

* Condições
   * Verifique pelo menos um evento de compra online ou offline desde a última visualização do produto.
      * Esquema: Transações digitais do cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Verifique pelo menos uma compra offline desde a última visualização do produto:
      * Esquema: Transações Offline do Cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Condições - Selecione o canal de público alvo
      * Email
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Personalização de canal
      * Conteúdo de canal personalizado com base na exibição do produto.

+++

>[!TAB Jornada de carrinho abandonada]

A jornada do carrinho abandonado tem como alvo os produtos que foram colocados no carrinho, mas que ainda não foram comprados no site e no aplicativo móvel.<p>![O cliente abandonou a visão geral de alto nível da jornada do carrinho.](../intelligent-re-engagement/images/abandoned-cart-journey.png "O cliente abandonou a visão geral de alto nível da jornada do carrinho."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 2: Adicionar ao carrinho
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType = commerce.productListAdds`
      * Campos:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 4: compras online
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType = commerce.purchases`
      * Campos:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Engajamento com a marca
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campos:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Lógica de Jornada de chave

* Jornada Lógica de Entrada
   * `AddToCart` Evento

* AuthenticatedState em autenticado

* Condição: compras offline desde que o carrinho foi abandonado pela última vez:
   * Esquema: Transações Offline do Cliente
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condição: carrinho limpo desde que o carrinho foi abandonado pela última vez:
   * Esquema: Transações digitais do cliente
   * `eventType = commerce.cartCleared`
   * `cartID` (ID do carrinho)
   * `timestamp > timestamp of cart was last abandoned`

* Selecionar canal de destino (selecione um ou vários canais para maior alcance)
   * Email
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Personalização de canal
      * Exibir informações detalhadas do carrinho e exibir vários produtos em formato de tabela.

+++

>[!TAB Jornada de confirmação de pedido]

A jornada de confirmação de pedido se concentra nas compras de produtos feitas pelo site e pelo aplicativo móvel.<p>![Visão geral visual de alto nível da jornada de confirmação de pedido do cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Visão geral visual de alto nível da jornada de confirmação de pedido do cliente."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 4: compras online
   * Esquema: Transações digitais do cliente
   * Campos:
      * `EventType`
   * Condição:
      * `EventType = commerce.purchases`
      * Campos:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Lógica de Jornada de tecla

* Jornada Lógica de Entrada
   * Evento de pedido

* Condições
   * Selecionar canal de destino (selecione um ou vários canais para maior alcance).
      * A confirmação do pedido é considerada de natureza pessoal, portanto, a verificação de consentimento geralmente é desnecessária.
      * Email
      * Push
      * SMS

   * Personalização de conteúdo do canal
      * Exibe informações detalhadas do pedido e pode exibir uma lista de produtos usando um formato de tabela.

+++

>[!ENDTABS]

Para obter mais informações sobre como criar jornadas no [!DNL Adobe Journey Optimizer], leia o [Introdução ao guia do jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Configuração de anúncios de mídia paga em destinos {#paid-media-ads}

A estrutura de destinos é usada para anúncios de mídia paga. Após verificar o consentimento, ele é enviado para os vários destinos configurados. Para obter mais informações sobre destinos, leia a [Visão geral dos destinos](/help/destinations/home.md) documento.

#### Dados exigidos para destinos

Os destinos de exportação de segmento de transmissão (como Facebook, Google Customer Match, Google DV360) oferecem suporte a várias identidades dos dados do cliente:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

O segmento do carrinho de abandono é de fluxo contínuo e, portanto, pode ser usado pela estrutura de destino neste caso de uso.

* Fluxo/Acionado
   * [Publicidade](/help/destinations/catalog/advertising/overview.md)/[Mídia paga e redes sociais](/help/destinations/catalog/social/overview.md)
   * [Dispositivo móvel](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destino do streaming](/help/destinations/catalog/streaming/http-destination.md)
   * [Destination SDK personalizado](/help/destinations/destination-sdk/overview.md)
