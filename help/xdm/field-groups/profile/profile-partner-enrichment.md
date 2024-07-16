---
title: Grupo de campos Enriquecimento do parceiro de perfil (amostra)
description: Saiba mais sobre o grupo de campos do esquema Enriquecimento do parceiro de perfil (Amostra).
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# [!UICONTROL Enriquecimento do Parceiro de Perfil (Amostra)] grupo de campos de esquema

[!UICONTROL Enriquecimento do Parceiro de Perfil (Amostra)] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Use este grupo de campos para fornecer dados adicionais relacionados a enriquecimentos orientados por parceiros para perfis de clientes.

![Um diagrama do [!UICONTROL Grupo de campos Enriquecimento do Parceiro de Perfil (Amostra)].](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | sequência de caracteres | A faixa etária dentro da família. |
| [!UICONTROL acessóriosDeVestuário] | `apparelAccessories` | sequência de caracteres | Dados de vestuário e acessórios. |
| [!UICONTROL ciclismo] | `bicycling` | sequência de caracteres | Informações relacionadas ao ciclismo. |
| [!UICONTROL tvcabo] | `cableTv` | sequência de caracteres | Informações relacionadas à TV a cabo. |
| [!UICONTROL domínios] | `domestics` | sequência de caracteres | Dados nacionais. |
| [!UICONTROL eletrônicos] | `electronics` | sequência de caracteres | Informações relacionadas a eletrônicos. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | sequência de caracteres | Dados sobre alimentos e bebidas. |
| [!UICONTROL calçados] | `footwear` | sequência de caracteres | Informações relativas ao calçado. |
| [!UICONTROL healthFoods] | `healthFoods` | sequência de caracteres | Dados sobre alimentos saudáveis. |
| [!UICONTROL caminhada] | `hiking` | sequência de caracteres | Informações relacionadas à caminhada. |
| [!UICONTROL IDdoDomicílio] | `householdId` | sequência de caracteres | O identificador exclusivo de uma família. |
| [!UICONTROL individualId] | `individualId` | sequência de caracteres | O identificador exclusivo de um indivíduo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | sequência de caracteres | Informações sobre o titular do cartão inferido. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | sequência de caracteres | Detalhes do titular do cartão premium inferido. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | sequência de caracteres | Corresponder dados de sinalizador de nível. |
| [!UICONTROL ClassificaçãoCompradora] | `buyerRating` | sequência de caracteres | Informações de classificação do comprador. |
| [!UICONTROL ClassificaçãoDoDoador] | `donorRating` | sequência de caracteres | Detalhes da classificação do doador. |
| [!UICONTROL ClassificaçãoInvestimento] | `investmentRating` | sequência de caracteres | Dados de notação de investimento. |
| [!UICONTROL ClassificaçãoDoRespondente] | `responderRating` | sequência de caracteres | Informações de classificação do respondente. |
| [!UICONTROL VelocidadeDaDespesa] | `spendingVelocity` | sequência de caracteres | Detalhes da velocidade de gasto. |
| [!UICONTROL VolumeDeGastos] | `spendingVolume` | sequência de caracteres | Informações do volume de gastos. |
| [!UICONTROL recordId] | `recordId` | sequência de caracteres | Identificador de registro exclusivo. |
| [!UICONTROL IDdaResidência] | `residenceId` | sequência de caracteres | Identificador exclusivo da residência. |
| [!UICONTROL navegação] | `sailing` | sequência de caracteres | Dados relativos à navegação. |
| [!UICONTROL ProdutosDeFeriadoSazonais] | `seasonalHolidayProducts` | sequência de caracteres | Informações sobre o produto de feriados sazonais. |
| [!UICONTROL esquiando] | `skiing` | sequência de caracteres | Dados relativos ao esqui. |
| [!UICONTROL tênis] | `tennis` | sequência de caracteres | Informação relativa ao tênis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | sequência de caracteres | Informações dos compradores de TV. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) no repositório XDM público.
