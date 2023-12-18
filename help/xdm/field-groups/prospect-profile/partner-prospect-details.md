---
title: Grupo de Campos de Detalhes de Cliente Potencial do Parceiro (Exemplo)
description: Saiba mais sobre o grupo de campos (XDM) do grupo de campos de detalhes do cliente potencial do parceiro.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Detalhes de Cliente Potencial do Parceiro (Exemplo)] grupo de campos

[!UICONTROL Detalhes de Cliente Potencial do Parceiro (Exemplo)] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). A variável [!UICONTROL Detalhes de Cliente Potencial do Parceiro (Exemplo)] O fornece uma estrutura de exemplo para vários detalhes relacionados ao perfil de um cliente potencial. Essa estrutura simplifica o processo de organização e gerenciamento de diversas informações relacionadas a clientes potenciais.

Este grupo de campos estende a variável [Classe de Perfil de Cliente Potencial Individual](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) no contexto de um parceiro.

![Um diagrama do [!UICONTROL Detalhes de Cliente Potencial do Parceiro (Exemplo)] grupo de campos.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | Faixa etária dentro da família. |
| [!UICONTROL vestuárioAcessórios] | `apparelAccessories` | string | Preferências ou envolvimento em vestuário/acessórios. |
| [!UICONTROL ciclismo] | `bicycling` | string | Interesse ou envolvimento em atividades de ciclismo. |
| [!UICONTROL cableTv] | `cableTv` | string | Indica o engajamento com a televisão a cabo. |
| [!UICONTROL doméstico] | `domestics` | string | Preferências ou envolvimento em atividades domésticas. |
| [!UICONTROL eletrônica] | `electronics` | string | Interesse ou envolvimento em dispositivos eletrônicos. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Preferências ou envolvimento em alimentos/bebidas. |
| [!UICONTROL calçado] | `footwear` | string | Interesse ou envolvimento no calçado. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Preferências ou envolvimento em alimentos saudáveis. |
| [!UICONTROL caminhada] | `hiking` | string | Interesse ou envolvimento em atividades de caminhada. |
| [!UICONTROL householdId] | `householdId` | string | Um identificador exclusivo da família. |
| [!UICONTROL individualId] | `individualId` | string | Um identificador exclusivo do indivíduo. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | A inferência de ser um titular de cartão. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | string | A inferência de ser titular de um cartão premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Um indicador do nível correspondente. |
| [!UICONTROL Classificação do comprador] | `buyerRating` | string | Uma classificação relacionada ao comportamento de compra. |
| [!UICONTROL Classificação do doador] | `donorRating` | string | Uma classificação relacionada ao comportamento do doador. |
| [!UICONTROL Classificação do investimento] | `investmentRating` | string | Uma classificação relacionada ao comportamento de investimento. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Uma classificação relacionada ao comportamento do respondente. |
| [!UICONTROL VelocidadeDeGastos] | `spendingVelocity` | string | A velocidade ou a taxa de gastos. |
| [!UICONTROL Volume de gastos] | `spendingVolume` | string | A quantia ou o volume de gastos. |
| [!UICONTROL recordId] | `recordId` | string | Um identificador exclusivo do registro. |
| [!UICONTROL ResidenceId] | `residenceId` | string | Um identificador exclusivo da residência. |
| [!UICONTROL navegação] | `sailing` | string | Indica o interesse ou envolvimento em atividades de navegação. |
| [!UICONTROL sazonalHolidayProducts] | `seasonalHolidayProducts` | string | Indica as preferências ou o envolvimento em produtos de feriado. |
| [!UICONTROL esqui] | `skiing` | string | Indica o interesse ou envolvimento em atividades de esqui. |
| [!UICONTROL tênis] | `tennis` | string | Indica o interesse ou envolvimento em atividades de tênis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Indica o engajamento com a compra de TV. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) no repositório XDM público.
