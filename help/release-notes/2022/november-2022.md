---
title: Notas de versão da Adobe Experience Platform de novembro de 2022
description: As notas de versão de novembro de 2022 do Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 52%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 23 de novembro de 2022**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Coleção de dados](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Fontes](#sources)

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Extensão [!DNL AWS] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Amazon Web Services] ([!DNL AWS]) usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL AWS] visão geral da extensão](../../tags/extensions/server/aws/overview.md) para obter mais informações. |
| Extensão [!DNL Google Ads Enhanced Conversions] para encaminhamento de eventos | Agora você pode enviar dados de conversão para [!DNL Google Ads] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Google Ads Enhanced Conversions] visão geral da extensão](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações. |
| Extensão [!DNL Microsoft Azure] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Microsoft Azure] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Microsoft Azure] visão geral da extensão](../../tags/extensions/server/azure/overview.md) para obter mais informações. |

Para obter mais informações sobre os recursos de coleção de dados da Platform, consulte a [visão geral da coleção de dados](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Atribuir campos a classes personalizadas ao adicionar diretamente a um esquema | Ao [adicionar um campo individual diretamente a um esquema](../../xdm/ui/resources/schemas.md#add-individual-fields), anteriormente você só podia atribuir o campo a um grupo de campos como seu recurso pai. Agora, além dos grupos de campos, você pode [atribuir o campo a uma classe personalizada](../../xdm/ui/resources/schemas.md#add-to-class) como seu recurso pai. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema de XDM](../../xdm/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- | 
| Disponibilidade do Beta para a origem na nuvem do Oracle Service | Use a fonte da Oracle Service Cloud para assimilar dados da sua conta da Oracle Service Cloud para o Experience Platform. Para obter mais informações, leia a documentação na [fonte da Nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
