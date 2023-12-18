---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;assinatura;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Assinatura
description: Saiba mais sobre o tipo de dados Subscription Experience Data Model (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 6%

---

# [!UICONTROL Inscrição] tipo de dados

[!UICONTROL Inscrição] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os direitos licenciados para software, serviços ou bens utilizados com base no tempo ou no uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Descreve detalhes sobre o dispositivo vinculado à assinatura. |
| `environment` | [[!UICONTROL Ambiente]](./environment.md) | Contém informações sobre a situação circundante em que ocorreu a observação do evento, detalhando especificamente informações transitórias, como a rede ou versões de software. |
| `subscriber` | [[!UICONTROL Pessoa]](./person.md) | Descreve uma pessoa individual. Também pode representar uma pessoa que atua em várias funções, como cliente, contato ou proprietário. |
| `SKU` | String | A unidade de manutenção de estoque (SKU), um identificador exclusivo de um produto. |
| `billingPeriod` | String | A duração entre os faturamentos. |
| `billingStartDate` | Data | A data de vencimento da primeira fatura. O formato de data (sem hora) deve seguir o [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) padrão. |
| `category` | String | A categorização de nível superior principal desse tipo de assinatura. |
| `chargeMethod` | String | A forma como o faturamento é configurado para cobrar do cliente. |
| `contractID` | String | O identificador exclusivo do contrato que rege esta assinatura. |
| `country` | String | O país em que os termos do contrato e do acordo de assinatura estão enraizados. |
| `endDate` | Data | A data em que termina o período de assinatura atual. O formato de data (sem hora) deve seguir o [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) padrão. |
| `paymentMethod` | String | O método de pagamento para pagamentos recorrentes. |
| `paymentStatus` | String | A posição de pagamento da conta. |
| `planName` | String | O nome legível da assinatura. |
| `reason` | String | A intenção geral que o membro tem para o uso da assinatura. |
| `renew` | String | A forma acordada para que a assinatura continue após a data de término. |
| `revision` | String | A identificação entre assinaturas de mesmo nome e hierarquia de categoria. |
| `startDate` | Data | A data em que a assinatura começa. O formato de data (sem hora) deve seguir o [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) padrão. |
| `status` | String | O status atual da assinatura. |
| `subCategory` | String | A subcategorização específica da assinatura. |
| `term` | Número inteiro | O valor numérico do termo de assinatura. |
| `termUnitOfTime` | String | A unidade de tempo para o período do prazo. |
| `topUp` | String | Descreve os termos acordados sobre como os aspectos consumíveis de uma assinatura são recomprados durante um período de faturamento. |
| `type` | String | O escopo do direito em relação a quantas pessoas estão cobertas pela assinatura. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
