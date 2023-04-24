---
title: Notas de versão da Adobe Experience Platform, abril de 2023
description: As notas de versão de abril de 2023 para o Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de abril de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Preparação de dados](#data-prep)
- [Fontes](#sources)

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações do período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção | O período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção foi reduzido para três meses. O preenchimento retroativo de sandboxes de produção permanece o mesmo em 13 meses. Essa alteração se aplica somente a novos fluxos e não afetará os fluxos existentes. Para obter mais informações, leia a [Visão geral do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nova função mapeadora para converter strings FPID em ECID | Use o `fpid_to_ecid` para converter strings FPID em ECID para uso em aplicativos Experience Platform e Experience Cloud. Para obter mais informações, leia a [Guia de funções de Preparação de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre Preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte a API para filtrar dados em nível de linha para Microsoft Dynamics, Salesforce CRM e Salesforce Marketing Cloud | Use operadores lógicos e de comparação para filtrar dados no nível da linha para as fontes de Marketing Cloud do Microsoft Dynamics, Salesforce CRM e Salesforce. Leia o guia em [filtragem de dados de uma fonte usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |
| Disponibilidade beta do Shopify Streaming | O [Comprar fonte de transmissão](../../sources/connectors/ecommerce/shopify-streaming.md) O agora está disponível em beta. Use a fonte de transmissão Shopify para transmitir dados da sua conta de parceiros Shopify para o Experience Platform. |
| Disponibilidade geral da integração do OneTrust | O [Origem de Integração do OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) agora está pronta. Use a fonte de integração do OneTrust para trazer os dados de consentimento e preferências da sua conta de Integração do OneTrust para o Experience Platform. |
| Disponibilidade geral da Oracle Service Cloud | O [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) agora está pronta. Use a fonte da nuvem do Oracle Service para trazer seus dados da nuvem do Oracle Service para o Experience Platform. |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
