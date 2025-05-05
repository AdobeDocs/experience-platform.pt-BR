---
title: Grupo de Campos de Detalhes de Cliente Potencial do Parceiro (Exemplo)
description: Saiba mais sobre o grupo de campos (XDM) do grupo de campos de detalhes do cliente potencial do parceiro.
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL Detalhes de Cliente Potencial Parceiro (Amostra)] grupo de campos

[!UICONTROL Detalhes de Cliente Potencial do Parceiro (Amostra)] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Os [!UICONTROL Detalhes de Cliente Potencial do Parceiro (Amostra)] fornecem uma estrutura de exemplo para vários detalhes relacionados ao perfil de um cliente potencial. Essa estrutura simplifica o processo de organização e gerenciamento de diversas informações relacionadas a clientes potenciais.

Este grupo de campos estende a [classe de Perfil de Cliente Potencial Individual](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html?lang=pt-BR) no contexto de um parceiro.

![Um diagrama do grupo de campos [!UICONTROL Detalhes de Cliente Potencial do Parceiro (Amostra)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | sequência de caracteres | Faixa etária dentro da família. |
| [!UICONTROL acessóriosDeVestuário] | `apparelAccessories` | sequência de caracteres | Preferências ou envolvimento em vestuário/acessórios. |
| [!UICONTROL ciclismo] | `bicycling` | sequência de caracteres | Interesse ou envolvimento em atividades de ciclismo. |
| [!UICONTROL tvcabo] | `cableTv` | sequência de caracteres | Indica o engajamento com a televisão a cabo. |
| [!UICONTROL domínios] | `domestics` | sequência de caracteres | Preferências ou envolvimento em atividades domésticas. |
| [!UICONTROL eletrônicos] | `electronics` | sequência de caracteres | Interesse ou envolvimento em dispositivos eletrônicos. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | sequência de caracteres | Preferências ou envolvimento em alimentos/bebidas. |
| [!UICONTROL calçados] | `footwear` | sequência de caracteres | Interesse ou envolvimento no calçado. |
| [!UICONTROL healthFoods] | `healthFoods` | sequência de caracteres | Preferências ou envolvimento em alimentos saudáveis. |
| [!UICONTROL caminhada] | `hiking` | sequência de caracteres | Interesse ou envolvimento em atividades de caminhada. |
| [!UICONTROL IDdoDomicílio] | `householdId` | sequência de caracteres | Um identificador exclusivo da família. |
| [!UICONTROL individualId] | `individualId` | sequência de caracteres | Um identificador exclusivo do indivíduo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | sequência de caracteres | A inferência de ser um titular de cartão. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | sequência de caracteres | A inferência de ser titular de um cartão premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | sequência de caracteres | Um indicador do nível correspondente. |
| [!UICONTROL ClassificaçãoCompradora] | `buyerRating` | sequência de caracteres | Uma classificação relacionada ao comportamento de compra. |
| [!UICONTROL ClassificaçãoDoDoador] | `donorRating` | sequência de caracteres | Uma classificação relacionada ao comportamento do doador. |
| [!UICONTROL ClassificaçãoInvestimento] | `investmentRating` | sequência de caracteres | Uma classificação relacionada ao comportamento de investimento. |
| [!UICONTROL ClassificaçãoDoRespondente] | `responderRating` | sequência de caracteres | Uma classificação relacionada ao comportamento do respondente. |
| [!UICONTROL VelocidadeDaDespesa] | `spendingVelocity` | sequência de caracteres | A velocidade ou a taxa de gastos. |
| [!UICONTROL VolumeDeGastos] | `spendingVolume` | sequência de caracteres | A quantia ou o volume de gastos. |
| [!UICONTROL recordId] | `recordId` | sequência de caracteres | Um identificador exclusivo do registro. |
| [!UICONTROL IDdaResidência] | `residenceId` | sequência de caracteres | Um identificador exclusivo da residência. |
| [!UICONTROL navegação] | `sailing` | sequência de caracteres | Indica o interesse ou envolvimento em atividades de navegação. |
| [!UICONTROL ProdutosDeFeriadoSazonais] | `seasonalHolidayProducts` | sequência de caracteres | Indica as preferências ou o envolvimento em produtos de feriado. |
| [!UICONTROL esquiando] | `skiing` | sequência de caracteres | Indica o interesse ou envolvimento em atividades de esqui. |
| [!UICONTROL tênis] | `tennis` | sequência de caracteres | Indica o interesse ou envolvimento em atividades de tênis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | sequência de caracteres | Indica o engajamento com a compra de TV. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) no repositório XDM público.
