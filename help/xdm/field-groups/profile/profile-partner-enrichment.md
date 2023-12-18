---
title: Grupo de campos Enriquecimento do parceiro de perfil (amostra)
description: Saiba mais sobre o grupo de campos do esquema Enriquecimento do parceiro de perfil (Amostra).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 13%

---


# [!UICONTROL Enriquecimento do parceiro de perfil (amostra)] grupo de campos de esquema

[!UICONTROL Enriquecimento do parceiro de perfil (amostra)] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Use este grupo de campos para fornecer dados adicionais relacionados a enriquecimentos orientados por parceiros para perfis de clientes.

![Um diagrama do [!UICONTROL Enriquecimento do parceiro de perfil (amostra)] grupo de campos.](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | A faixa etária dentro da família. |
| [!UICONTROL vestuárioAcessórios] | `apparelAccessories` | string | Dados de vestuário e acessórios. |
| [!UICONTROL ciclismo] | `bicycling` | string | Informações relacionadas ao ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | string | Informações relacionadas à TV a cabo. |
| [!UICONTROL doméstico] | `domestics` | string | Dados nacionais. |
| [!UICONTROL eletrônica] | `electronics` | string | Informações relacionadas a eletrônicos. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Dados sobre alimentos e bebidas. |
| [!UICONTROL calçado] | `footwear` | string | Informações relativas ao calçado. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Dados sobre alimentos saudáveis. |
| [!UICONTROL caminhada] | `hiking` | string | Informações relacionadas à caminhada. |
| [!UICONTROL householdId] | `householdId` | string | O identificador exclusivo de uma família. |
| [!UICONTROL individualId] | `individualId` | string | O identificador exclusivo de um indivíduo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | Informações sobre o titular do cartão inferido. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | string | Detalhes do titular do cartão premium inferido. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Corresponder dados de sinalizador de nível. |
| [!UICONTROL Classificação do comprador] | `buyerRating` | string | Informações de classificação do comprador. |
| [!UICONTROL Classificação do doador] | `donorRating` | string | Detalhes da classificação do doador. |
| [!UICONTROL Classificação do investimento] | `investmentRating` | string | Dados de notação de investimento. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Informações de classificação do respondente. |
| [!UICONTROL VelocidadeDeGastos] | `spendingVelocity` | string | Detalhes da velocidade de gasto. |
| [!UICONTROL Volume de gastos] | `spendingVolume` | string | Informações do volume de gastos. |
| [!UICONTROL recordId] | `recordId` | string | Identificador de registro exclusivo. |
| [!UICONTROL ResidenceId] | `residenceId` | string | Identificador exclusivo da residência. |
| [!UICONTROL navegação] | `sailing` | string | Dados relativos à navegação. |
| [!UICONTROL sazonalHolidayProducts] | `seasonalHolidayProducts` | string | Informações sobre o produto de feriados sazonais. |
| [!UICONTROL esqui] | `skiing` | string | Dados relativos ao esqui. |
| [!UICONTROL tênis] | `tennis` | string | Informação relativa ao tênis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Informações dos compradores de TV. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) no repositório XDM público.
