---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;subscrição;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de subscrição
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM (Subscrição Experience Data Model).
translation-type: tm+mt
source-git-commit: 8ccf0a53f231c9f59cd87735126b180c6b678e51
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 9%

---


# [!UICONTROL Tipo ] de dados de assinatura

[!UICONTROL A ] assinatura é um tipo de dados padrão do Experience Data Model (XDM) que descreve os direitos licenciados a software, serviços ou bens que são utilizados com base no tempo ou no uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Descreve detalhes sobre o dispositivo vinculado à subscrição. |
| `environment` | [[!UICONTROL Ambiente]](./environment.md) | Contém informações sobre a situação ao redor da qual ocorreu a observação do evento, detalhando especificamente informações transitórias como, por exemplo, as versões de rede ou de software. |
| `subscriber` | [[!UICONTROL Pessoa]](./person.md) | Descreve uma pessoa individual. Isso também pode representar uma pessoa agindo em várias funções, como cliente, contato ou proprietário. |
| `SKU` | String | A unidade de manutenção de estoque (SKU), um identificador exclusivo para um produto. |
| `billingPeriod` | String | A duração entre as cobranças. |
| `billingStartDate` | Data | A data em que a primeira fatura é devida. O formato de data (sem tempo) deve seguir o padrão [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | String | A principal categorização de nível superior desse tipo de subscrição. |
| `chargeMethod` | String | A forma como a cobrança é configurada para cobrar o cliente. |
| `contractID` | String | A ID exclusiva do contrato que rege essa subscrição. |
| `country` | String | O país em que os termos do contrato subscrição e do acordo estão enraizados. |
| `endDate` | Data | A data em que o termo de subscrição atual termina. O formato de data (sem tempo) deve seguir o padrão [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | String | O método de pagamento para pagamentos recorrentes. |
| `paymentStatus` | String | A posição de pagamento da conta. |
| `planName` | String | O nome legível para a subscrição. |
| `reason` | String | A intenção geral do membro de usar a subscrição. |
| `renew` | String | A forma acordada de a subscrição continuar após a data de término. |
| `revision` | String | A identificação entre subscrições com o mesmo nome e a hierarquia de categorias. |
| `startDate` | Data | A data de início da subscrição. O formato de data (sem tempo) deve seguir o padrão [RFC 3339, seção 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | String | O status atual da subscrição. |
| `subCategory` | String | A subcategorização específica da subscrição. |
| `term` | Número inteiro | O valor numérico do termo de subscrição. |
| `termUnitOfTime` | String | A unidade de tempo para o período do termo. |
| `topUp` | String | Descreve os termos acordados para o quão consumíveis os aspectos de uma subscrição são recomprados durante um período de faturamento. |
| `type` | String | O âmbito do direito em relação ao número de pessoas abrangidas pela subscrição. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)