---
title: Reengajamento inteligente
description: Ofereça experiências atraentes e conectadas durante os principais momentos de conversão para engajar novamente clientes pouco frequentes de forma inteligente.
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: df82431f87f725a12cbc5b8f88fff6d4cc065450
workflow-type: tm+mt
source-wordcount: '3594'
ht-degree: 5%

---

# Engaje novamente clientes de uma forma inteligente para que retornem

>[!NOTE]
>
>Esta é uma amostra de implementação e os exemplos nesta página, como sintaxe de segmento, são apenas exemplos. Você deve usar os exemplos como um guia, pois sua implementação pode ser diferente.

Reenvolva os clientes que abandonaram uma conversão de forma inteligente e responsável. Envolva os clientes obsoletos com experiências para aumentar a conversão e o valor vitalício do cliente.

Empregue considerações em tempo real, considere todas as qualidades e comportamentos do consumidor e ofereça requalificação rápida com base em eventos online e offline.

![Visão geral visual de alto nível de reengajamento inteligente.](../intelligent-re-engagement/images/step-by-step.png)

## Visão geral do caso de uso {#overview}

Você construirá esquemas, conjuntos de dados e públicos à medida que trabalhar com exemplos de cenários de reengajamento. Você também descobrirá os recursos necessários para configurar as jornadas de exemplo no [!DNL Adobe Journey Optimizer] e os necessários para criar anúncios de mídia paga em destinos. Este guia usa exemplos de reengajamento dos clientes nas jornadas de caso de uso descritas abaixo:

* **Cenário de navegação de produto abandonado** - Clientes do Target que abandonaram a navegação de produtos no site e no aplicativo móvel.
* **Cenário de carrinho abandonado** : clientes do Target que colocaram produtos no carrinho, mas ainda não foram comprados no site e no aplicativo móvel.
* **Cenário de confirmação de pedido** - Concentre-se nas compras de produtos feitas por meio do site e do aplicativo móvel.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao concluir as etapas para implementar o caso de uso, você usará a seguinte funcionalidade do Real-Time CDP e do Adobe Journey Optimizer (listada na ordem em que será usada). Verifique se tem as [permissões de controle de acesso baseado em atributo](/help/access-control/home.md) necessárias para todas essas áreas, ou solicite ao(à) administrador(a) que as conceda a você.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integra dados em fontes de dados para alimentar a campanha. Esses dados são usados para criar os públicos-alvo da campanha e exibir elementos de dados personalizados usados no email e nos blocos promocionais da Web (por exemplo, nome ou informações relacionadas à conta). A CDP também é usada para ativar públicos-alvo no email e na Web (via [!DNL Adobe Target]).
   * [Esquemas](/help/xdm/home.md)
   * [Perfis](/help/profile/home.md)
   * [Conjuntos de dados](/help/catalog/datasets/overview.md)
   * [Públicos-alvo](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Destinos](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=pt-BR) - Ajuda a fornecer experiências conectadas, contextuais e personalizadas aos clientes.
   * [Acionador de evento ou público-alvo](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Públicos/ eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=pt-BR)
   * [Jornada ações](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Como obter o caso de uso {#achieve-use-case-instruction}

Abaixo está uma visão geral de alto nível dos três exemplos de cenários de reengajamento.

>[!BEGINTABS]

>[!TAB Cenário de pesquisa de produtos abandonada]

O cenário de navegação de produto abandonado segmenta a navegação de produto abandonada no site e no aplicativo móvel. Esse cenário é acionado quando um produto foi visualizado, mas não foi comprado ou adicionado ao carrinho. Neste exemplo, o engajamento da marca é acionado após três dias se não houver adições à lista nas últimas 24 horas.<p>![Visão geral visual de alto nível do cenário de navegação inteligente de produto abandonada do cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Visão geral visual de alto nível do cenário de navegação inteligente de produto abandonada do cliente."){width="1920" zoomable="yes"}</p>

1. Crie esquemas e conjuntos de dados e ative para [!UICONTROL Perfil].
2. Você assimila dados no Experience Platform via SDK da Web, SDK móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você assimila dados adicionais ativados por perfil, que podem ser vinculados ao visitante da Web e/ou do aplicativo móvel autenticado por meio de gráficos de identidade.
4. Você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **cliente** fez um compromisso nos últimos três dias.
5. Você cria uma jornada de navegação de produto abandonada no [!DNL Adobe Journey Optimizer].
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. [!DNL Adobe Journey Optimizer] O verifica o consentimento e envia as várias ações configuradas.

>[!TAB Cenário de carrinho abandonado]

O cenário de carrinho abandonado se aplica quando os produtos foram colocados no carrinho, mas ainda não foram comprados no site e no aplicativo móvel. Além disso, as campanhas de Mídia paga são iniciadas e interrompidas usando esse método.<p>![Visão geral visual de alto nível do cenário de carrinho abandonado pelo cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Visão geral visual de alto nível do cenário de carrinho abandonado pelo cliente."){width="1920" zoomable="yes"}</p>

1. Crie esquemas e conjuntos de dados, a habilitação para [!UICONTROL Perfil].
2. Você assimila dados no Experience Platform via SDK da Web, SDK móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você assimila dados adicionais ativados por perfil, que podem ser vinculados ao visitante da Web e/ou do aplicativo móvel autenticado por meio de gráficos de identidade.
4. Você cria públicos-alvo focados a partir da lista de perfis para verificar se uma **cliente** colocou um item no carrinho, mas não concluiu a compra. A variável **[!UICONTROL Adicionar ao carrinho]** O evento inicia um temporizador que aguarda 30 minutos e verifica a compra. Se nenhuma compra tiver sido feita, a variável **cliente** é adicionado à **[!UICONTROL Abandonar carrinho]** públicos-alvo.
5. Você cria uma jornada de carrinho abandonada no [!DNL Adobe Journey Optimizer].
6. Se necessário, trabalhe com a **parceiro de dados** para a ativação de públicos para os destinos de mídia paga desejados.
7. [!DNL Adobe Journey Optimizer] O verifica o consentimento e envia as várias ações configuradas.

>[!TAB Cenário de confirmação de pedido]

O cenário de confirmação de pedido se concentra nas compras de produtos feitas pelo site e pelo aplicativo móvel.<p>![Visão geral visual de alto nível do cenário de confirmação de pedido do cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Visão geral visual de alto nível do cenário de confirmação de pedido do cliente."){width="1920" zoomable="yes"}</p>

1. Crie esquemas e conjuntos de dados e ative para [!UICONTROL Perfil].
2. Você assimila dados no Experience Platform via SDK da Web, SDK móvel ou API. O Conector de dados do Analytics também pode ser usado, mas pode resultar em latência de jornada.
3. Você assimila dados adicionais ativados por perfil, que podem ser vinculados ao visitante da Web e/ou do aplicativo móvel autenticado por meio de gráficos de identidade.
4. Você cria uma jornada de confirmação no [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] O envia uma mensagem de confirmação de pedido usando o canal preferencial.

>[!ENDTABS]

Para concluir cada uma das etapas das visões gerais de alto nível acima, leia as seções abaixo, que oferecem links para mais informações e instruções mais detalhadas.

### Criar esquemas e especificar grupos de campos {#schema-design}

Os recursos do Experience Data Model (XDM) são gerenciados no [!UICONTROL Esquemas] espaço de trabalho no [!DNL Adobe Experience Platform]. Você pode visualizar e explorar os recursos principais fornecidos pelo [!DNL Adobe] (por exemplo, grupos de campos) e crie recursos e esquemas personalizados para sua organização.

Para obter mais informações sobre como criar [schemas](/help/xdm/home.md), consulte o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md) e [Modelar seus dados de experiência do cliente com o XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Há quatro designs de esquema que são usados para o caso de uso de reengajamento. Cada esquema requer a configuração de campos específicos. Você precisa ativar o esquema para ser incluído no Perfil de cliente em tempo real. Para obter mais informações sobre como ativar o esquema para uso no Perfil do cliente em tempo real, leia [ativar um esquema para o Perfil de cliente em tempo real](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Esquema de atributos do cliente

Esse esquema é usado para estruturar e fazer referência aos dados do perfil que compõem as informações do cliente. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] por meio do seu CRM ou sistema semelhante e é necessário para consultar os detalhes do cliente usados para personalização, consentimento de marketing e recursos aprimorados do público-alvo.

O esquema de atributos do cliente é representado por um [[!UICONTROL Perfil individual XDM]](/help/xdm/classes/individual-profile.md) que inclui os seguintes grupos de campos:

+++Detalhes de contato pessoal (grupo de campos)

[Detalhes de contato pessoal](/help/xdm/field-groups/profile/personal-contact-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM que descreve as informações de contato de uma pessoa individual.

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `mobilePhone.number` | Obrigatório | O número do celular da pessoa, que será usado para SMS. |
| `personalEmail.address` | Obrigatório | O endereço de email da pessoa. |

+++

+++Detalhes de auditoria do sistema de origem externo (grupo de campos)

[Atributos de auditoria do sistema de origem externa](/help/xdm/data-types/external-source-system-audit-attributes.md) é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

+++

+++Grupos de campos de consentimento e preferência (Grupo de campos)

A variável [Consentimentos e preferências](/help/xdm/field-groups//profile/consents.md) grupo de campos fornece um único campo do tipo objeto, consentimentos, para capturar informações de consentimento e preferência.

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

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre no seu site e/ou plataformas digitais associadas. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] via [SDK da Web](/help/edge/home.md) e é necessário fazer referência aos vários eventos de navegação e conversão usados para acionar jornadas, análises detalhadas de clientes online e recursos aprimorados de público-alvo.

O schema de transações digitais do cliente é representado por um [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe.

+++XDM ExperienceEvent (Classe)

A variável [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) A classe inclui os seguintes grupos de campos:

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `_id` | Obrigatório | Identifica exclusivamente eventos individuais que são assimilados em [!DNL Adobe Experience Platform]. |
| `timestamp` | Obrigatório | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu, formatado de acordo com RFC 3339 Seção 5.6. Esse carimbo de data e hora deve ocorrer no passado. |
| `eventType` | Obrigatório | Uma string que indica o tipo de categoria do evento. |

+++

+++Detalhes da ID do usuário final (Grupo de campos)

A variável [Detalhes da ID do usuário final](/help/xdm/field-groups/event/enduserids.md) grupo de campos é usado para descrever as informações de identidade de um indivíduo em vários aplicativos Adobe.

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

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre em plataformas fora do site. Normalmente, esses dados são assimilados na [!DNL Adobe Experience Platform] de um PDV (ou sistema semelhante) e geralmente transmitido para a Platform por meio de uma conexão de API. Seu objetivo é fazer referência aos vários eventos de conversão offline usados para acionar jornadas, análises profundas online e offline do cliente e recursos aprimorados de público-alvo.

O schema de transações offline do cliente é representado por um [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe.

+++XDM ExperienceEvent (Classe)

A variável [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) A classe inclui os seguintes grupos de campos:

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `_id` | Obrigatório | Identifica exclusivamente eventos individuais que são assimilados em [!DNL Adobe Experience Platform]. |
| `timestamp` | Obrigatório | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu, formatado de acordo com RFC 3339 Seção 5.6. Esse carimbo de data e hora deve ocorrer no passado. |
| `eventType` | Obrigatório | Uma string que indica o tipo de categoria do evento. |

+++

+++Detalhes do comércio (Grupo de campos)

A variável [Detalhes do comércio](/help/xdm/field-groups/event/commerce-details.md) o grupo de campos é usado para descrever dados de comércio, como informações do produto (SKU, nome, quantidade) e operações padrão do carrinho (pedido, check-out, abandono).

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

[Detalhes de contato pessoal](/help/xdm/field-groups/profile/personal-contact-details.md) é um grupo de campos de esquema padrão para a classe Perfil individual XDM que descreve as informações de contato de uma pessoa individual.

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
>Essa é uma implementação opcional se você estiver usando o [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md).

Esse esquema é usado para estruturar e fazer referência aos dados do evento que compõem a atividade do cliente que ocorre no seu site e/ou plataformas digitais associadas. Este esquema é semelhante ao esquema de Transações digitais do cliente, mas difere na medida em que deve ser usado quando [SDK da Web](/help/edge/home.md) não é uma opção para a coleta de dados; portanto, esse esquema é necessário ao utilizar a variável [!DNL Adobe Analytics Source Connector] para enviar seus dados online para o [!DNL Adobe Experience Platform] como um fluxo de dados primário ou secundário.

A variável [!DNL Adobe] o esquema do conector da web é representado por um [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe.

+++XDM ExperienceEvent (Classe)

A variável [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) A classe inclui os seguintes grupos de campos:

| Campos | Requisito | Descrição |
| --- | --- | --- |
| `_id` | Obrigatório | Identifica exclusivamente eventos individuais que são assimilados em [!DNL Adobe Experience Platform]. |
| `timestamp` | Obrigatório | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu, formatado de acordo com RFC 3339 Seção 5.6. Esse carimbo de data e hora deve ocorrer no passado. |
| `eventType` | Obrigatório | Uma string que indica o tipo de categoria do evento. |

+++

+++Modelo de evento de experiência do Adobe Analytics (grupo de campos)

A variável [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) o grupo de campos captura métricas comuns coletadas pelo Adobe Analytics.

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

### Criar um conjunto de dados a partir de um esquema {#create-datasets}

Um conjunto de dados é uma estrutura de armazenamento e gerenciamento para um grupo de dados. Cada esquema para cenários inteligentes de reengajamento deve ter seu próprio conjunto de dados.

Para obter mais informações sobre como criar uma [conjunto de dados](/help/catalog/datasets/overview.md) de um esquema, leia o [Guia da interface do usuário de conjuntos de dados](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Semelhante à etapa para criar um esquema, é necessário ativar o conjunto de dados para ser incluído no Perfil do cliente em tempo real. Para obter mais informações sobre como ativar o conjunto de dados para uso no Perfil do cliente em tempo real, consulte o tutorial em [trazendo dados para o Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=pt-BR).

### Consentimento e governança de dados {#privacy-consent}

>[!IMPORTANT]
>
>Oferecer aos clientes a capacidade de cancelar a inscrição para receber comunicações de uma marca, bem como garantir que essa escolha seja respeitada, é um requisito legal. Saiba mais sobre a legislação aplicável na [Visão geral das regras de privacidade](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

#### Políticas de consentimento

Ao criar um caminho de reengajamento, considere adicionar o seguinte [políticas de consentimento](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html):

* Se `consents.marketing.email.val = "Y"` pode enviar email
* Se `consents.marketing.sms.val = "Y"` depois pode SMS
* Se `consents.marketing.push.val = "Y"` depois, pode enviar
* Se `consents.share.val = "Y"` depois, pode anunciar

#### Rotulagem e aplicação da governança de dados

Ao criar um caminho de reengajamento, considere adicionar o seguinte [Rótulos de governança de dados](/help/data-governance/labels/overview.md):

* Os endereços de email pessoais são utilizados como dados diretos identificáveis usados para identificar ou entrar em contato com um indivíduo específico, em vez de com um dispositivo.
   * `personalEmail.address = I1`

#### Políticas de uso de dados

Não há [políticas de uso de dados](/help/data-governance/policies/overview.md) necessário para o cenário de pesquisa de produto abandonado. No entanto, você deve considerar o seguinte:

* Restringir Dados Confidenciais
* Restringir publicidade no local
* Restringir o direcionamento de email
* Restringir o direcionamento entre sites
* Restringir a combinação de dados diretamente identificáveis com dados anônimos

### Criar públicos {#create-audience}

Os cenários de reengajamento usam públicos para definir atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Os públicos-alvo podem ser criados de várias maneiras no [!DNL Adobe Experience Platform].

Para obter mais informações sobre como criar um público-alvo, leia a [guia da interface do usuário do audience service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Para obter mais informações sobre como compor diretamente [Públicos-alvo](/help/segmentation/home.md), leia o [Guia da interface do usuário da Composição de público-alvo](/help/segmentation/ui/audience-composition.md).

Para obter mais informações sobre como criar públicos-alvo por meio de definições de público-alvo derivadas da Platform, leia o [Guia da interface do usuário do Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Cenário de pesquisa de produtos abandonada]

Esse público-alvo é criado como um aprimoramento do cenário clássico de &quot;Abandono do carrinho&quot;. Enquanto o abandono do carrinho geralmente se concentra em uma adição ao carrinho sem uma compra subsequente em um determinado período de tempo, esse público-alvo busca um envolvimento anterior, especificamente aqueles que podem ter navegado em um produto específico, mas não o adicionaram ao carrinho e não tiveram nenhuma atividade de acompanhamento no site em um determinado período de tempo. Esse público-alvo ajuda a manter sua marca no topo da mente para os clientes que atendem a esse critério de inclusão e também pode ser aproveitado para clientes cujas propriedades digitais podem diferir de um modelo de comércio eletrônico tradicional.

+++Exibição de produto abandonada sem engajamento nos últimos três dias

O evento a seguir é usado para o cenário de navegação de produto abandonada em que os usuários visualizaram produtos online e não se envolveram (visitas ao site, visitas a aplicativos, compras online, compras offline e eventos de adição ao carrinho) nos 3 dias seguintes.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `eventType: commerce.productViews`
* E `THEN` (evento sequencial) excluir `eventType: commerce.procuctListAdds` ou `application.launch` ou `web.webpagedetails.pageViews` ou `commerce.purchases` (isso inclui online e offline)
   * `Timestamp: > 3 days after productView`

+++

+++Exibição do produto com envolvimento nos últimos três dias

O evento a seguir é usado para o cenário de navegação de produto abandonado em que os usuários visualizaram produtos online e se envolveram (visitas a sites, visitas a aplicativos, compras online, compras offline e eventos de adição ao carrinho) nos 3 dias seguintes.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `eventType: commerce.productViews`
* E `THEN` (evento sequencial) incluir `eventType: commerce.procuctListAdds` ou `application.launch` ou `web.webpagedetails.pageViews` ou `commerce.purchases` (isso inclui online e offline)
   * `Timestamp: > 3 days after productView`

+++Transmissão do engajamento no último dia

O evento a seguir é usado para o cenário de navegação de produto abandonado em que os usuários se envolveram (visitas ao site, visitas de aplicativos, compras online, compras offline e eventos de adição ao carrinho) nos últimos 1 dia.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `eventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 1 day` (Transmissão)

+++

+++Lote de participação nos últimos três dias

O evento a seguir é usado para o cenário de navegação de produto abandonado em que os usuários se envolveram (visitas a sites, visitas a aplicativos, compras online, compras offline e eventos de adição ao carrinho) nos últimos 3 dias.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `EventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 3 days` (Lote)

+++

>[!TAB Cenário de carrinho abandonado]

Esse público-alvo é criado para oferecer suporte ao cenário clássico de &quot;Abandono do carrinho&quot;. Seu objetivo é encontrar clientes que adicionaram um produto ao carrinho de compras, mas que não fizeram uma compra. Esse público-alvo ajudará a manter não apenas a sua marca no topo da mente dos seus clientes, mas também os produtos que eles deixaram para trás sem uma compra subsequente.

Os eventos a seguir são usados para o cenário de carrinho abandonado em que os usuários adicionaram um produto ao carrinho entre 1 e 4 dias atrás, mas não concluíram a compra ou limparam o carrinho.

Os seguintes campos e condições são obrigatórios ao configurar este público-alvo:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

O descritor do cenário de carrinho abandonado aparece como:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Cenário de confirmação de pedido]

Esta jornada não requer a criação de públicos-alvo.

>[!ENDTABS]

### Configuração do Jornada no Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] não abrange tudo o que é mostrado nos diagramas. Todos [anúncios de mídia paga](/help/destinations/catalog/social/overview.md) são criados em [!UICONTROL Destinos].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) O ajuda a fornecer experiências conectadas, contextuais e personalizadas aos clientes. A jornada do cliente envolve todo o processo de interação do cliente com a marca. Cada jornada de caso de uso requer informações específicas. Veja abaixo os dados precisos necessários para cada jornada.

>[!BEGINTABS]

>[!TAB Cenário de pesquisa de produtos abandonada]

O cenário de navegação de produto abandonado segmenta a navegação de produto abandonada no site e no aplicativo móvel.<p>![Visão geral visual de alto nível do cenário de navegação de produto abandonada pelo cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Visão geral visual de alto nível do cenário de navegação de produto abandonada pelo cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

* Evento 1: visualizações do produto
   * Esquema: Transações digitais do cliente
   * Campos:
      * `eventType`
   * Condição:
      * `eventType = commerce.productViews`
      * Campos:
         * `commerce.productViews.id`
         * `commerce.productViews.value`
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
      * `eventType`
   * Condição:
      * `eventType = commerce.productListAdds`
      * Campos:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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
      * `eventType`
   * Condição:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

>[!TAB Cenário de carrinho abandonado]

O cenário de carrinho abandonado segmenta os produtos que foram colocados no carrinho, mas que ainda não foram comprados no site e no aplicativo móvel.<p>![Visão geral visual de alto nível do cenário de carrinho abandonado pelo cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Visão geral visual de alto nível do cenário de carrinho abandonado pelo cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

* Evento 2: Adicionar ao carrinho
   * Esquema: Transações digitais do cliente
   * Campos:
      * `eventType`
   * Condição:
      * `eventType = commerce.productListAdds`
      * Campos:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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
      * `eventType`
   * Condição:
      * `eventType = commerce.purchases`
      * Campos:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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
      * `eventType`
   * Condição:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

>[!TAB Cenário de confirmação de pedido]

O cenário de confirmação de pedido se concentra nas compras de produtos feitas pelo site e pelo aplicativo móvel.<p>![Visão geral visual de alto nível do cenário de confirmação de pedido do cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Visão geral visual de alto nível do cenário de confirmação de pedido do cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

* Evento 4: compras online
   * Esquema: Transações digitais do cliente
   * Campos:
      * `eventType`
   * Condição:
      * `eventType = commerce.purchases`
      * Campos:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

Os destinos de exportação de público-alvo de transmissão (como Facebook, Google Customer Match, Google DV360) são compatíveis com várias identidades de dados do cliente:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

o público do carrinho de abandono é avaliado como um público de streaming e, portanto, pode ser usado pela estrutura de destinos para este caso de uso.

* Fluxo/Acionado
   * [Publicidade](/help/destinations/catalog/advertising/overview.md)/[Mídia paga e redes sociais](/help/destinations/catalog/social/overview.md)
   * [Dispositivo móvel](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destino do streaming](/help/destinations/catalog/streaming/http-destination.md)
   * [Destino personalizado criado por meio do Destination SDK.](/help/destinations/destination-sdk/overview.md). Se você for um cliente do Real-Time CDP Ultimate, também poderá criar uma conta [destino personalizado usando Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)
