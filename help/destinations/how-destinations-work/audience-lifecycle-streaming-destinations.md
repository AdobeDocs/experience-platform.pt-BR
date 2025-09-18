---
title: Ciclo de vida do público-alvo no Experience Platform e destinos de transmissão
description: Saiba como os nomes e mapeamentos de público-alvo do Experience Platform são refletidos nas plataformas de destino de transmissão.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# Ciclo de vida do público-alvo em destinos de transmissão

Esta página descreve como as atualizações de nome de público-alvo e os mapeamentos no Experience Platform são sincronizados com as plataformas de destino de transmissão. Ao modificar nomes de público ou remover mapeamentos de público no Experience Platform, o comportamento varia dependendo dos recursos da plataforma de destino.

Entender essas diferenças é importante para gerenciar as operações do ciclo de vida do público e garantir que as plataformas de destino reflitam o estado atual dos públicos no Experience Platform.

## Comportamento de propagação do nome do público {#audience-name-propagation}

Quando você ativa um público para um destino de transmissão, o nome do público é enviado para o destino durante a ativação inicial. No entanto, o comportamento de atualização do nome do público-alvo varia de acordo com o destino:

* **[Destinos que oferecem suporte a atualizações de nome de público-alvo](#name-update-supported)**: se você alterar um nome de público-alvo no Experience Platform, o nome atualizado será propagado automaticamente para esses destinos.
* **[Destinos que não oferecem suporte a atualizações de nome de público-alvo](#name-update-not-supported)**: se você alterar um nome de público-alvo no Experience Platform, o destino continuará a usar o nome original a partir da ativação inicial.

### Destinos que oferecem suporte a atualizações de nome de público-alvo {#name-update-supported}

Os seguintes destinos de transmissão oferecem suporte a atualizações automáticas de nome de público-alvo quando você modifica nomes de público-alvo no Experience Platform:

* [Acxiom Audience Connection](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Critério](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Pessoas do Demandbase](../catalog/advertising/demandbase-people.md)
* [Públicos-alvo da Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Público-alvo personalizado do Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(Empresas) Público-alvo correspondente do LinkedIn](../catalog/social/linkedin-b2b.md)
* [Público-alvo correspondente do LinkedIn](../catalog/social/linkedin.md)
* [(Herdado) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Públicos-alvo personalizados do Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinos que não oferecem suporte a atualizações de nome de público-alvo {#name-update-not-supported}

Para destinos não listados acima, os nomes de público-alvo permanecem estáticos após a ativação inicial. Se precisar atualizar um nome de público-alvo para esses destinos, você deverá:

1. Crie um novo público no Experience Platform com o nome desejado
2. Ativar o novo público para o destino

>[!TIP]
>
>Para evitar confusão, use nomes descritivos de público-alvo da primeira ativação, especialmente ao ativar para destinos que não oferecem suporte a atualizações de nomes de público-alvo.

## Destinos que oferecem suporte à remoção de público {#support-removal}

Ao remover (desmapear) um público-alvo de um destino de transmissão, o Experience Platform tenta remover o público-alvo correspondente da plataforma de destino. No entanto, nem todos os destinos oferecem suporte a essa funcionalidade.

Os seguintes destinos de transmissão oferecem suporte à remoção automática de público-alvo quando você desmapeia um público-alvo do destino:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Empresas) Público-alvo correspondente do LinkedIn](../catalog/social/linkedin-b2b.md)
* [(Herdado) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Públicos da conta Bombora](../catalog/advertising/bombora.md)
* [Critério](../catalog/advertising/criteo.md)
* [Públicos-alvo da Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [Públicos correspondentes do LinkedIn](../catalog/social/linkedin.md)
* [LiveRamp - Distribuição](../catalog/advertising/liveramp-distribution.md)
* [Categorias de interesse do Mailchimp](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Engajamento com a conta do Salesforce Marketing Cloud](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Públicos-alvo personalizados do Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinos que não oferecem suporte à remoção de públicos

Para destinos não listados acima, ao desmapear um público-alvo do destino, o Experience Platform remove apenas o mapeamento. O público-alvo na plataforma de destino permanece ativo até que você o exclua manualmente na plataforma do parceiro.
