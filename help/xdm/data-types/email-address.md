---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;Schemas;emailAddress;xdm:email;email;email address;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados de endereço de email
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Endereço de Email.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# [!UICONTROL Tipo de ] dados de endereços de email

[!UICONTROL O ] endereço de email é um tipo de dados XDM padrão que descreve os detalhes de um endereço de email.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `address` | O endereço técnico do email, como geralmente é definido no RFC2822 e nos padrões subsequentes (por exemplo, `name@domain.com`). |
| `label` | Informações de exibição adicionais que podem estar disponíveis. Por exemplo, se um email tiver uma exibição de endereço avançado do Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` será colocado nesse campo. |
| `primary` | Indica se este é o endereço de email principal do indivíduo. Um perfil pode ter apenas um `primary` endereço de email em um determinado momento. |
| `status` | Indica se o endereço de email pode ser usado no momento |
| `statusReason` | Uma descrição do `status` atual. |
| `type` | A forma como a conta se relaciona à pessoa (como `work` ou `personal`). |


Para obter mais detalhes sobre o tipo de dados de endereço de email, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)