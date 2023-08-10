---
title: Reengajamento inteligente
description: Ofereça experiências atraentes e conectadas durante os principais momentos de conversão para reengajar clientes pouco frequentes de forma inteligente.
hide: true
hidefromtoc: true
source-git-commit: 7ff623626b557cbf67ad6164157d1a5ef4820cb1
workflow-type: tm+mt
source-wordcount: '3259'
ht-degree: 5%

---

# Reenvolva seus clientes de forma inteligente para retornar

O reengajamento inteligente permite que você configure uma campanha personalizada com informações em vários canais para persuadir os clientes a executar uma ação específica. A campanha de incentivo deve operar por um período limitado, que inclui o envio de clientes que mostraram emails de intenção, SMS e veiculação de anúncios pagos. Depois que o cliente tomar a ação apropriada, a campanha de incentivo será encerrada imediatamente.

![Visão geral visual de alto nível passo a passo com reengajamento inteligente.](../intelligent-re-engagement/images/step-by-step.png)

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao concluir as etapas para implementar o caso de uso, você usará a seguinte funcionalidade do Real-Time CDP e os elementos da interface do usuário (listados na ordem em que serão usados). Verifique se você tem as permissões de controle de acesso baseadas em atributos necessárias para todas essas áreas ou peça ao administrador do sistema para conceder as permissões necessárias.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Agrega dados em fontes de dados para alimentar a campanha. Esses dados são usados para criar os públicos-alvo da campanha e exibir elementos de dados personalizados usados no email e nos blocos promocionais da Web (por exemplo, nome ou informações relacionadas à conta). A CDP também é usada para ativar públicos-alvo no email e na Web (via Adobe Target).
   * [Esquemas](/help/xdm/home.md)
   * [Perfis](/help/profile/home.md)
   * [Conjuntos de dados](/help/catalog/datasets/overview.md)
   * [Públicos-alvo](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Destinos](/help/destinations/home.md)
   * [Acionador de evento ou público-alvo](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Públicos/ eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Jornada ações](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

Atualmente, três jornadas diferentes de reengajamento foram desenvolvidas.

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

A jornada de reengajamento é direcionada à navegação de produto abandonada no site e no aplicativo. Essa jornada é disparada quando um produto foi visualizado, mas não foi comprado ou adicionado ao carrinho. O engajamento com a marca é acionado após três dias se não houver adições à lista nas últimas 24 horas.

![Visão geral visual de alto nível da jornada de reengajamento inteligente do cliente.](../intelligent-re-engagement/images/re-engagement-journey.png)

1. Os dados são agregados ao SDK da Web, SDK móvel ou assimilação da API da rede de borda por meio da rede de borda (o método preferido).
2. Como um **cliente**, você cria conjuntos de dados marcados para [!UICONTROL Perfil].
3. Como um **cliente**, você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Como um **cliente**, você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **usuário** fez um envolvimento com a marca nos últimos três dias.
5. Como um **cliente**, você criará uma jornada de reengajamento no Adobe Journey Optimizer.
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. O Adobe Journey Optimizer verifica o consentimento e envia as várias ações configuradas.

>[!TAB Jornada de carrinho abandonada]

A jornada do carrinho abandonado tem como alvo os produtos que foram colocados no carrinho, mas que ainda não foram comprados no site e no aplicativo. Além disso, as campanhas de Mídia paga são iniciadas e interrompidas usando esse método.

![O cliente abandonou a visão geral de alto nível da jornada do carrinho.](../intelligent-re-engagement/images/abandoned-cart-journey.png)

1. Os dados são agregados ao SDK da Web, SDK móvel ou assimilação da API da rede de borda por meio da rede de borda (o método preferido).
2. Como um **cliente**, você cria conjuntos de dados marcados para [!UICONTROL Perfil].
3. Como um **cliente**, você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Como um **cliente**, você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **usuário** colocou um item no carrinho, mas não concluiu a compra. A variável **[!UICONTROL Adicionar ao carrinho]** O evento inicia um temporizador que aguarda 30 minutos e verifica a compra. Se nenhuma compra tiver sido feita, a variável **usuário** é adicionado à **[!UICONTROL Abandonar carrinho]** públicos-alvo.
5. Como um **cliente**, você criará uma jornada de carrinho abandonada no Adobe Journey Optimizer
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. O Adobe Journey Optimizer verifica o consentimento e envia as várias ações configuradas.

>[!TAB Jornada de confirmação de pedido]

A jornada de confirmação de pedido se concentra nas compras de produtos feitas pelo site e pelo aplicativo móvel.

![Visão geral visual de alto nível da jornada de confirmação de pedido do cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png)

1. Os dados são agregados ao SDK da Web, SDK móvel ou assimilação da API da rede de borda por meio da rede de borda (o método preferido).
2. Como um **cliente**, você cria conjuntos de dados marcados para [!UICONTROL Perfil].
3. Como um **cliente**, você carrega perfis no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Como um **cliente**, você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **usuário** fez uma compra.
5. Como um **cliente**, você criará uma jornada de confirmação no Adobe Journey Optimizer.
6. O Adobe Journey Optimizer envia uma mensagem de confirmação de pedido usando o canal preferencial.

>[!ENDTABS]

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Para concluir cada uma das etapas das visões gerais de alto nível acima, leia as seções abaixo, que oferecem links para mais informações e instruções mais detalhadas.

### Funcionalidade e elementos da interface do usuário que você usará {#ui-functionality-and-elements}

Ao concluir as etapas para implementar o caso de uso, você usará a funcionalidade do Real-Time CDP e os elementos da interface do usuário listados no início deste documento. Verifique se você tem as permissões de controle de acesso baseadas em atributos necessárias para todas essas áreas ou peça ao administrador do sistema para conceder as permissões necessárias.

### Criar um design de esquema e especificar grupos de campos

Os recursos do Experience Data Model (XDM) são gerenciados no [!UICONTROL Esquemas] espaço de trabalho no Adobe Experience Platform. Você pode visualizar e explorar os recursos principais fornecidos pelo Adobe e criar recursos e esquemas personalizados para sua organização.

<!--
To create a schema, complete the steps below:

1. Navigate to **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]** and select **[!UICONTROL Create schema]**.
2. Select **[!UICONTROL XDM Individual Profile]/[!UICONTROL XDM ExperienceEvent]**.
3. Navigate to **[!UICONTROL Field groups]** and select **[!UICONTROL Add]**.
4. Use the search box to find and select the field group, then select **[!UICONTROL Add field groups]**.
5. Give your schema a name and optionally a description.
6. Select **[!UICONTROL Save]**.

![A recording of the steps to create a schema.](../intelligent-re-engagement/images/create-a-schema.gif) 
-->

Para obter mais informações sobre como criar schemas, leia a [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md)

Há quatro designs de esquema usados para a jornada de reengajamento. Cada esquema requer a configuração de campos específicos, bem como de alguns campos altamente sugeridos.

#### Esquema de atributos do cliente

O esquema de atributos do cliente é representado por um [!UICONTROL Perfil individual XDM] que inclui os seguintes grupos de campos:

+++Detalhes de contato pessoal (grupo de campos)

[Detalhes de contato pessoal](/help/xdm/field-groups/profile/personal-contact-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM que descreve as informações de contato de uma pessoa individual.

| Campos | Requisito | Descrição |
| --- | --- | --- |
| mobilePhone.number | Obrigatório | O número do celular da pessoa, que será usado para SMS. |
| personalEmail.address | Obrigatório | O endereço de email da pessoa. |

+++

+++Detalhes demográficos (Grupo de campos)

[Detalhes demográficos](/help/xdm/field-groups/profile/demographic-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM. O grupo de campos fornece um objeto de pessoa de nível raiz, cujos subcampos descrevem informações sobre uma pessoa individual.

| Campos | Requisito |
| --- | --- |
| person.name.firstName | Sugerido |
| person.name.lastName | Sugerido |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

[Atributos de auditoria do sistema de origem externa](/help/xdm/data-types/external-source-system-audit-attributes.md) é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

+++Grupos de campos de consentimento e preferência (Grupo de campos)

[Os consentimentos e preferências](/help/xdm/field-groups//profile/consents.md) grupo de campos fornece um único campo do tipo objeto, consentimentos, para capturar informações de consentimento e preferência.

| Campos | Requisito |
| --- | --- |
| consents.marketing.email.val | Obrigatório |
| consents.marketing.preferred | Obrigatório |
| consents.marketing.push.val | Obrigatório |
| consents.marketing.sms.val | Obrigatório |
| consents.personalize.content.val | Obrigatório |
| consents.share.val | Obrigatório |

+++

+++Detalhes do teste de perfil (grupo de campos)

Este grupo de campos é usado para prática recomendada.

+++

<!--
![Customer attributes schema highlighting the list of field groups.](../intelligent-re-engagement/images/customer-attributes.png) 
-->

#### Esquema de transações digitais do cliente

O schema de transações digitais do cliente é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++ExperienceEvent do SDK da Web do Adobe Experience Platform (Grupo de campos)

| Campos | Requisito |
| --- | --- |
| device.model | Sugerido |
| environment.browserDetails.userAgent | Sugerido |

+++

+++Detalhes da Web (Grupo de Campos)

Detalhes da Web é um grupo de campos de esquema padrão para a classe XDM ExperienceEvent, usado para descrever informações sobre eventos de detalhes da Web, como interação, detalhes da página e referenciador.

| Campos | Requisito | Descrição |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Sugerido | A ID do link da Web ou URL que corresponde à interação. |
| web.webInteraction.linkClicks.value | Sugerido | O número de cliques do link da web ou URL que corresponde à interação. |
| web.webInteraction.name | Sugerido | O nome da página da Web. |
| web.webInteraction.URL | Sugerido | O URL da página da Web. |
| web.webPageDetails.name | Sugerido | O nome da página da Web onde ocorreu a interação da Web. |
| web.webPageDetails.URL | Sugerido | A URL da página da Web em que ocorreu a interação da Web. |
| web.webReferrer.URL | Sugerido | Descreve o referenciador de uma interação da web, que é o URL de onde um visitante veio imediatamente antes de a interação da web atual ser registrada. |

+++

+++Evento de experiência do consumidor (grupo de campos)

| Campos | Requisito |
| --- | --- |
| commerce.cart.cartID | Sugerido |
| commerce.cart.cartSource | Sugerido |
| commerce.cartAbandons.id | Sugerido |
| commerce.cartAbandons.value | Sugerido |
| commerce.order.orderType | Sugerido |
| commerce.order.payments.paymentAmount | Sugerido |
| commerce.order.payments.paymentType | Sugerido |
| commerce.order.payments.transactionID | Sugerido |
| commerce.order.priceTotal | Sugerido |
| commerce.order.purchaseID | Sugerido |
| commerce.productListAdds.id | Sugerido |
| commerce.productListAdds.value | Sugerido |
| commerce.productListOpens.id | Sugerido |
| commerce.productListOpens.value | Sugerido |
| commerce.productListRemoval.id | Sugerido |
| commerce.productListRemoval.value | Sugerido |
| commerce.productListViews.id | Sugerido |
| commerce.productListViews.value | Sugerido |
| commerce.productViews.id | Sugerido |
| commerce.productViews.value | Sugerido |
| commerce.purchases.id | Sugerido |
| commerce.purchases.value | Sugerido |
| marketing.campaignGroup | Sugerido |
| marketing.campaignName | Sugerido |
| marketing.trackingCode | Sugerido |
| productListItems.name | Sugerido |
| productListItems.priceTotal | Sugerido |
| productListItems.product | Sugerido |
| productListItems.quantity | Sugerido |

+++

+++Detalhes da ID do usuário final (Grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| endUserIDs._experience.emailid.authenticatedState | Obrigatório | Estado autenticado da ID do endereço de email do usuário final. |
| endUserIDs._experience.emailid.id | Obrigatório | ID do endereço de email do usuário final. |
| endUserIDs._experience.emailid.namespace.code | Obrigatório | Código de namespace da ID do endereço de email do usuário final. |
| endUserIDs._experience.mcid.authenticatedState | Obrigatório | Estado autenticado da Adobe Marketing Cloud ID (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| endUserIDs._experience.mcid.id | Obrigatório | Adobe Marketing Cloud ID (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| endUserIDs._experience.mcid.namespace.code | Obrigatório | Código de namespace da Adobe Marketing Cloud ID (MCID). |

+++

+++Valor da classe (grupo de campos)

| Campos | Requisito |
| --- | --- |
| eventType | Obrigatório |
| carimbo de data e hora | Obrigatório |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

<!--
![Customer digital transactions schema highlighting the list of field groups.](../intelligent-re-engagement/images/customer-digital-transactions.png) 
-->

#### Esquema de transações offline do cliente

O schema de transações offline do cliente é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++Detalhes do comércio (Grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| commerce.cart.cartID | Obrigatório | Uma ID para o carrinho de compras. |
| commerce.order.orderType | Obrigatório | Um objeto que descreve o tipo de pedido do produto. |
| commerce.order.payments.paymentAmount | Obrigatório | Um objeto que descreve o valor do pagamento da ordem do produto. |
| commerce.order.payments.paymentType | Obrigatório | Um objeto que descreve o tipo de pagamento de ordem de produto. |
| commerce.order.payments.transactionID | Obrigatório | Um ID de transação de ordem de produto de objeto. |
| commerce.order.purchaseID | Obrigatório | Uma ID de compra da ordem de produto do objeto. |
| productListItems.name | Obrigatório | Uma lista de nomes de itens que representam os produtos selecionados por um cliente. |
| productListItems.priceTotal | Obrigatório | O preço total da lista de itens que representam os produtos selecionados por um cliente. |
| productListItems.product | Obrigatório | Os produtos selecionados. |
| productListItems.quantity | Obrigatório | A quantidade de itens da lista que representam os produtos selecionados por um cliente. |

+++

+++Detalhes de contato pessoal (grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| mobilePhone.number | Obrigatório | O número do celular da pessoa, que será usado para SMS. |
| personalEmail.address | Obrigatório | O endereço de email da pessoa. |

+++

+++Valor da classe (grupo de campos)

| Campos | Requisito |
| --- | --- |
| eventType | Obrigatório |
| carimbo de data e hora | Obrigatório |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

<!--
![Customer offline transactions schema highlighting the list of field groups.](../intelligent-re-engagement/images/customer-offline-transactions.png) 
-->

#### Esquema do conector web do Adobe

O esquema do conector web Adobe é representado por um [!UICONTROL XDM ExperienceEvent] que inclui os seguintes grupos de campos:

+++Modelo de evento de experiência do Adobe Analytics (grupo de campos)

| Campos | Requisito | Descrição |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Sugerido | A ID do link da Web ou URL que corresponde à interação. |
| web.webInteraction.linkClicks.value | Sugerido | O número de cliques do link da web ou URL que corresponde à interação. |
| web.webInteraction.name | Sugerido | O nome da página da Web. |
| web.webInteraction.URL | Sugerido | O URL da página da Web. |
| web.webPageDetails.name | Sugerido | O nome da página da Web onde ocorreu a interação da Web. |
| web.webPageDetails.URL | Sugerido | A URL da página da Web em que ocorreu a interação da Web. |
| web.webReferrer.URL | Sugerido | Descreve o referenciador de uma interação da web, que é o URL de onde um visitante veio imediatamente antes de a interação da web atual ser registrada. |
| commerce.cart.cartID | Sugerido | |
| commerce.cart.cartSource | Sugerido | |
| commerce.cartAbandons.id | Sugerido | |
| commerce.cartAbandons.value | Sugerido | |
| commerce.order.orderType | Sugerido | |
| commerce.order.payments.paymentAmount | Sugerido | |
| commerce.order.payments.paymentType | Sugerido | |
| commerce.order.payments.transactionID | Sugerido | |
| commerce.order.priceTotal | Sugerido | |
| commerce.order.purchaseID | Sugerido | |
| commerce.productListAdds.id | Sugerido | |
| commerce.productListAdds.value | Sugerido | |
| commerce.productListOpens.id | Sugerido | |
| commerce.productListOpens.value | Sugerido | |
| commerce.productListRemoval.id | Sugerido | |
| commerce.productListRemoval.value | Sugerido | |
| commerce.productListViews.id | Sugerido | |
| commerce.productListViews.value | Sugerido | |
| commerce.productViews.id | Sugerido | |
| commerce.productViews.value | Sugerido | |
| commerce.purchases.id | Sugerido | |
| commerce.purchases.value | Sugerido | |
| marketing.campaignGroup | Sugerido | |
| marketing.campaignName | Sugerido | |
| marketing.trackingCode | Sugerido | |
| productListItems.name | Sugerido | |
| productListItems.priceTotal | Sugerido | |
| productListItems.product | Sugerido | |
| productListItems.quantity | Sugerido | |
| endUserIDs._experience.emailid.authenticatedState | Obrigatório | Estado autenticado da ID do endereço de email do usuário final. |
| endUserIDs._experience.emailid.id | Obrigatório | ID do endereço de email do usuário final. |
| endUserIDs._experience.emailid.namespace.code | Obrigatório | Código de namespace da ID do endereço de email do usuário final. |
| endUserIDs._experience.mcid.authenticatedState | Obrigatório | Estado autenticado da Adobe Marketing Cloud ID (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| endUserIDs._experience.mcid.id | Obrigatório | Adobe Marketing Cloud ID (MCID). O MCID agora é conhecido como Experience Cloud ID (ECID). |
| endUserIDs._experience.mcid.namespace.code | Obrigatório | Código de namespace da Adobe Marketing Cloud ID (MCID). |

+++

+++Valor da classe (grupo de campos)

| Campos | Requisito |
| --- | --- |
| eventType | Obrigatório |
| carimbo de data e hora | Obrigatório |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

Atributos de auditoria do sistema de origem externa é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

<!--
![Adobe web connector schema highlighting the list of field groups.](../intelligent-re-engagement/images/adobe-web-connector.png) 
-->

### Criar um conjunto de dados a partir de um esquema

Um conjunto de dados é uma estrutura de armazenamento e gerenciamento para um grupo de dados, geralmente uma tabela com campos (linhas) e um esquema (colunas). Cada esquema para jornadas inteligentes de reengajamento terá um único conjunto de dados.

Para obter mais informações sobre como criar um conjunto de dados a partir de um esquema, leia a [Guia da interface do usuário de conjuntos de dados](/help/catalog/datasets/user-guide.md).
<!-- 
To create a dataset from a schema, complete the steps below:

1. Navigate to **[!UICONTROL Data Management]** > **[!UICONTROL Datasets]** and select **[!UICONTROL Create dataset]**.
2. Select **[!UICONTROL Create dataset from schema]**.
3. Select the relevant re-engagement schema you created.
4. Give your dataset a name and optionally a description.
5. Select **[!UICONTROL Finish]**.

![A recording of the steps to create a dataset from a schema.](../intelligent-re-engagement/images/dataset-from-schema.gif)
-->

>Observação
>
>Semelhante à etapa para criar um esquema, é necessário ativar o conjunto de dados para ser incluído no Perfil do cliente em tempo real. Para obter mais informações sobre como ativar o conjunto de dados para uso no Perfil do cliente em tempo real, leia o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile).

<!-- 
![Enable dataset for profile.](../intelligent-re-engagement/images/enable-dataset-for-profile.png)
-->

### Privacidade, consentimento e governança de dados

#### Políticas de consentimento

>[!IMPORTANT]
>
>Oferecer aos clientes a capacidade de cancelar a inscrição para receber comunicações de uma marca é um requisito legal, bem como garantir que essa escolha seja respeitada. Saiba mais sobre a legislação aplicável na [documentação da Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Ao criar um caminho de reengajamento, as seguintes políticas de consentimento devem ser consideradas e usadas:

* Se consents.marketing.email.val = &quot;Y&quot;, poderá enviar um email
* Se consents.marketing.sms.val = &quot;Y&quot;, então Pode SMS
* Se consentimentos.marketing.push.val = &quot;Y&quot;, em seguida, Pode enviar
* Se consents.share.val = &quot;Y&quot;, então Pode anunciar
* Necessidade definida pela implementação do cliente

#### Rótulo e aplicação do DULE

Os endereços de email pessoais são utilizados como dados diretos identificáveis usados para identificar ou entrar em contato com um indivíduo específico, em vez de com um dispositivo.

* personalEmail.address = I1

#### Políticas de marketing

Não há políticas de marketing adicionais necessárias para as jornadas de reengajamento, no entanto, as seguintes opções devem ser consideradas conforme desejado:

* Restringir Dados Confidenciais
* Restringir publicidade no local
* Restringir o direcionamento de email
* Restringir o direcionamento entre sites
* Restringir a combinação de dados diretamente identificáveis com dados anônimos

### Criar um público-alvo

<!--
To create an audience, complete the steps below:

1. Navigate to **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** and select **[!UICONTROL Create audience]**.
2. Select **[!UICONTROL Build rule]** and select **[!UICONTROL Create]**.
3. Navigate to **[!UICONTROL Field]** and select **[!UICONTROL Events]** tab.
4. Navigate or use the search box to find the event type, then drag this to the builder. Finally add event rules by dragging event types.
5. Give your schema a name and optionally a description.
6. Select **[!UICONTROL Save]**.

![A recording of the steps to create an audience.](../intelligent-re-engagement/images/create-an-audience.gif)
-->

#### Criação de público-alvo para jornadas de reengajamento da marca

As jornadas de reengajamento usam públicos para definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Os públicos-alvo podem ser criados de duas maneiras diferentes no Adobe Experience Platform: diretamente compostos como públicos-alvo ou por meio de definições de segmentos derivadas da plataforma.

Para obter mais informações sobre como compor públicos diretamente, leia a [Guia da interface do usuário da Composição de público-alvo](/help/segmentation/ui/audience-composition.md).

Para obter mais informações sobre como criar públicos-alvo por meio de definições de segmento derivadas da plataforma, leia a [Guia da interface do usuário do Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

Os eventos a seguir são usados para a jornada de reengajamento, em que os usuários visualizaram produtos online e não adicionaram ao carrinho nas próximas 24 horas, seguidos por nenhum engajamento da marca nos 3 dias seguintes.

Inclua público que tenha pelo menos 1 EventType = ProductViews event THEN que tenha pelo menos 1 Qualquer evento em que (EventType não é igual a commerce.productListAdds) e ocorra nas últimas 24 horas e, depois de 3 dias, não tenha nenhum evento em que (EventType = application.launch ou web.webpagedetails.pageViews ou commerce.purchases) e ocorra nos últimos 2 dias.

<!--
![A screenshot of the re-engagement audience showing the set of rules.](../intelligent-re-engagement/images/re-engagement-audience.png) 
-->

>[!TAB Jornada de carrinho abandonada]

Os eventos a seguir são usados para perfis que adicionaram um produto ao carrinho, mas não concluíram a compra ou limparam o carrinho nas últimas 24 horas.

Inclua EventType = commerce.productListAdds entre 30 minutos e 1440 minutos antes de agora.
excluir EventType = commerce.purchases 30 minutos antes OU EventType = commerce.productListRemovals E ID do carrinho é igual a Lista de produtos Adiciona1 ID do carrinho (o evento de inclusão).

<!--
![A screenshot of the re-engagement audience showing the set of rules.](../intelligent-re-engagement/images/abandoned-cart-audience.png) 
-->

>[!ENDTABS]

### Configuração do Jornada no Adobe Journey Optimizer

>[!NOTE]
>
>O Adobe Journey Optimizer não abrange tudo o que é mostrado nos diagramas na parte superior desta página. Todos os anúncios de mídia paga são criados no [!UICONTROL Destinos].

O Adobe Journey Optimizer ajuda você a fornecer experiências conectadas, contextuais e personalizadas aos seus clientes. A jornada do cliente envolve todo o processo de interação do cliente com a marca. Cada caso de uso pode ter várias jornadas diferentes, cada uma exigindo informações específicas. Os dados precisos necessários para cada ramificação de Jornada estão listados abaixo.

>[!BEGINTABS]

>[!TAB Jornada de reengajamento]

<!--
![Customer re-engagemnt journey in Adobe Journey Optimizer overview](../intelligent-re-engagement/images/re-engagement-ajo.png) 
-->

+++Eventos

* Visualizações de produto
   * Esquema: Transações digitais do cliente
   * Campos:
      * EventType
   * Condição:
      * EventType = commerce.productViews
      * Campos:
         * Commerce.productViews.id
         * Commerce.productViews.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Adicionar ao carrinho
   * Esquema: Transações digitais do cliente
   * Campos:
      * Tipo de evento
   * Condição:
      * Tipo de evento = commerce.productListAdds
      * Campos:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Engajamento com a marca
   * Esquema: Transações digitais do cliente
   * Campos:
      * EventType
   * Condição:
      * EventType em application.launch, commerce.purchases, web.webpagedetails.pageViews
      * Campos:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Lógica de Jornada de tecla

* Jornada Lógica de Entrada
   * Evento de exibição de produto

* Condições
   * Verifique pelo menos um evento de compra online ou offline desde a última visualização do produto.
      * Esquema: Transações digitais do cliente
      * eventType = commerce.purchases
      * timestamp > timestamp do último produto exibido

   * Verifique pelo menos uma compra offline desde a última visualização do produto:
      * Esquema: Transações off-line do cliente v.1
      * eventType = commerce.purchases
      * timestamp > timestamp do último produto exibido

   * Condições - Selecione o canal de público alvo
      * Email
         * consentimentos.marketing.email.val = y
      * Push
         * consents.marketing.push.val=y
      * SMS
         * consents.marketing.sms.val = y

   * Personalização de canal
      * Conteúdo de canal personalizado com base na exibição do produto.

+++

>[!TAB Jornada de carrinho abandonada]

<!--
![Customer abandoned cart journey in Adobe Journey Optimizer overview](../intelligent-re-engagement/images/abandoned-cart-ajo.png) 
-->

+++Eventos

* Adicionar ao carrinho
   * Esquema: Transações digitais do cliente
   * Campos:
      * Tipo de evento
   * Condição:
      * Tipo de evento = commerce.productListAdds
      * Campos:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Compras on-line
   * Esquema: Transações digitais do cliente
   * Campos:
      * Tipo de evento
   * Condição:
      * Tipo de evento = commerce.purchases
      * Campos:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Engajamento com a marca
   * Esquema: Transações digitais do cliente
   * Campos:
      * EventType
   * Condição:
      * EventType em application.launch, commerce.purchases, web.webpagedetails.pageViews
      * Campos:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Lógica de Jornada de chave

* Jornada Lógica de Entrada
   * Evento AddToCart

* AuthenticatedState em autenticado

* Condição: compras offline desde que o carrinho foi abandonado pela última vez:
   * Esquema: Transações off-line do cliente v.1
   * eventType = commerce.purchases
   * timestamp > timestamp do carrinho foi abandonado pela última vez

* Condição: carrinho limpo desde que o carrinho foi abandonado pela última vez:
   * Esquema: Transações digitais do cliente v.1
   * eventType = commerce.cartCleared
   * cartID (ID do carrinho)
   * timestamp > timestamp do carrinho foi abandonado pela última vez

* Selecionar canal de destino (selecione um ou vários canais para maior alcance)
   * Email
      * consentimentos.marketing.email.val = y
   * Push
      * consentimentos.marketing.push.val = y
   * SMS
      * consents.marketing.sms.val = y
   * Personalização de canal
      * Exibir informações detalhadas do carrinho e exibir vários produtos em formato de tabela.

+++

>[!TAB Jornada de confirmação de pedido]

<!--
![Customer order confirmation journey in Adobe Journey Optimizer overview](../intelligent-re-engagement/images/order-confirmation-ajo.png) 
-->

+++Eventos

* Compras on-line
   * Esquema: Transações digitais do cliente
   * Campos:
      * EventType
   * Condição:
      * Tipo de evento = commerce.purchases
      * Campos:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * carimbo de data e hora
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

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

Para obter mais informações sobre como criar jornadas no [Adobe Journey Optimizer], leia o [Introdução ao guia do jornada](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Configuração de anúncios de mídia pagos em Destinos

A estrutura de destinos é usada para anúncios de mídia paga. Após verificar o consentimento, ele será enviado para os vários destinos configurados. Por exemplo, correspondência direta, email e assim por diante.

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

* Arquivo/Agendado a cada três horas
   * [Marketing por email](/help/destinations/catalog/email-marketing/overview.md)
