---
title: Notas de versão da Adobe Experience Platform de novembro de 2022
description: As notas de versão de novembro de 2022 da Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 55%

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
| Extensão [!DNL AWS] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Amazon Web Services] ([!DNL AWS]) usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL AWS] Visão geral de extensões](../../tags/extensions/server/aws/overview.md) para obter mais informações. |
| Extensão [!DNL Google Ads Enhanced Conversions] para encaminhamento de eventos | Agora você pode enviar dados de conversão para [!DNL Google Ads] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Google Ads Enhanced Conversions] Visão geral de extensões](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para obter mais informações. |
| Extensão [!DNL Microsoft Azure] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Microsoft Azure] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Microsoft Azure] Visão geral de extensões](../../tags/extensions/server/azure/overview.md) para obter mais informações. |

Para obter mais informações sobre os recursos de coleta de dados da Experience Platform, consulte a [visão geral da coleta de dados](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Atribuir campos a classes personalizadas ao adicionar diretamente a um esquema | Ao [adicionar um campo individual diretamente a um esquema](../../xdm/ui/resources/schemas.md#add-individual-fields), anteriormente você só podia atribuir o campo a um grupo de campos como seu recurso pai. Agora, além dos grupos de campos, você pode [atribuir o campo a uma classe personalizada](../../xdm/ui/resources/schemas.md#add-to-class) como seu recurso pai. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, consulte a [visão geral do sistema XDM](../../xdm/home.md).
