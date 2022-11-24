---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 9100597c94c21beb9d967f67061e18a9421c6674
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 8%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 23 de novembro de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [!DNL AWS] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Amazon Web Services] ([!DNL AWS]) usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL AWS] visão geral da extensão](../../tags/extensions/web/aws/overview.md) para obter mais informações. |
| [!DNL Google Ads Enhanced Conversions] extensão para encaminhamento de eventos | Agora é possível enviar dados de conversão para [!DNL Google Ads] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Google Ads Enhanced Conversions] visão geral da extensão](../../tags/extensions/web/google-ads-enhanced-conversions/overview.md) para obter mais informações. |
| [!DNL Microsoft Azure] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Microsoft Azure] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Microsoft Azure] visão geral da extensão](../../tags/extensions/web/azure/overview.md) para obter mais informações. |

Para obter mais informações sobre os recursos de coleta de dados da Platform, consulte o [visão geral da coleta de dados](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Atribuir campos a classes personalizadas ao adicionar diretamente a um schema | When [adição de um campo individual diretamente a um schema](../../xdm/ui/resources/schemas.md#add-individual-fields), anteriormente era possível atribuir o campo somente a um grupo de campos como seu recurso pai. Agora, além dos grupos de campos, você pode [atribuir o campo a uma classe personalizada](../../xdm/ui/resources/schemas.md#add-to-class) como seu recurso principal. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- | 
| Disponibilidade beta da origem da nuvem do Oracle Service | Use a fonte da nuvem do Oracle Service para assimilar dados da sua conta da Oracle Service Cloud para o Experience Platform. Para obter mais informações, leia a documentação sobre o [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).