---
title: Visão geral do Source Talon.One
description: Saiba mais sobre as fontes do Talon.One no Adobe Experience Platform
badge: Beta
last-substantial-update: 2026-04-06T00:00:00Z
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: f3026e0a717c07d95f12e3aeaf380ddc1b87c712
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>As fontes [!DNL Talon.One] estão na versão beta. Leia os [termos e condições](../../home.md#terms-and-conditions) na visão geral das fontes para obter mais informações sobre como usar fontes com rótulo beta.

Com o [!DNL Talon.One], você pode criar, gerenciar e otimizar campanhas de marketing personalizadas de acordo com os seus clientes. Use essa plataforma eficiente para executar descontos, distribuir cupons, iniciar programas de referência, configurar programas de fidelidade e oferecer incentivos gamificados — tudo a partir de um sistema escalável projetado para ajudá-lo a engajar e recompensar seu público.

Você pode usar as [!DNL Talon.One] fontes no catálogo de fontes do Adobe Experience Platform para assimilar dados de fidelidade em lote e de transmissão da sua conta [!DNL Talon.One].

* [Eventos de transmissão Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Conector Talon.One Batch Source](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Os dados de fidelidade se referem às informações do programa de fidelidade dos usuários finais, como pontos de fidelidade, pontos de fidelidade gastos, nível atual, cupons concedidos, indicações e conquistas.

## Pré-requisitos {#prerequisites}

Forneça valores para as credenciais a seguir para autenticar e conectar o [!DNL Talon.One Batch Source Connector].

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Domínio | A URL exclusiva associada ao ambiente de aplicativo [!DNL Talon.One]. Certifique-se de não incluir o protocolo ou caminho ao inserir o domínio. | `acmetalonone.us-east4` |
| [!DNL Talon.One] Chave da API de Gerenciamento | A Chave da API de Gerenciamento é uma credencial usada para autenticar e autorizar o acesso à API de Gerenciamento de [!DNL Talon.One]. Isso lida com operações como: <ul><li>Importação de cupons</li><li>Recuperação de dados da campanha</li><li>Gerenciamento de aplicativos e endpoints</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Mapeamento {#mapping}

Para ajudar a mapear cada objeto de efeito com base em seu valor `effectType` exclusivo, você pode usar a função de preparação de dados `array_to_map`. Isso permite converter facilmente uma matriz desordenada de efeitos em pares de valores chave que correspondam às suas necessidades. Consulte o exemplo abaixo para obter orientação.

Você também pode usar os grupos de campos de fidelidade padronizados que o Adobe fornece para modelar os conceitos do programa de fidelidade de uma maneira consistente.

>[!BEGINTABS]

>[!TAB Detalhes de fidelidade]

Este é um grupo de campos XDM padrão para o Perfil individual XDM, usado para descrever o status de associação de fidelidade de uma pessoa capturando seus atributos de registro, em vez dos dados do evento. Use este grupo de campos em seus esquemas de perfil para capturar:

* **Quem** o membro está no programa (`loyaltyID`, `program`, `status`, `tier`)
* Seus **saldos atuais e de vida útil** (`points`, `lifetimePoints`, `expiredPoints` etc.)
* Chave **datas de associação** (`joinDate`, `upgradeDate`, `tierExpiryDate`)

>[!TAB Detalhes do Evento de Fidelidade]

O grupo de campos Detalhes do Evento de Fidelidade foi criado para capturar a atividade de fidelidade no nível do evento, como pontos ganhos ou resgatados em uma transação específica. Este grupo de campos inclui campos como `xdm:points`, `xdm:pointsRedeemed`, `xdm:pointsAsOfDate` e `xdm:program`. Use este grupo de campos no nível do evento em seus esquemas de evento de experiência para capturar:

* **Movimentos por evento** em pontos (obtidos, resgatados, expirados)
* **Descontos** que foram gerados por cupons de fidelidade ou indicações
* **IDs de programa** e IDs de transação para reconciliação com o provedor de fidelidade.

>[!ENDTABS]

| Fonte | Destino |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Próximas etapas

Leia a documentação a seguir para saber como você pode conectar sua conta do [!DNL Talon.One] à Experience Platform e assimilar dados de fidelidade em lote e de transmissão.

* [Eventos de transmissão Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Conector Talon.One Batch Source](../../tutorials/ui/create/loyalty/talon-one-batch.md)
