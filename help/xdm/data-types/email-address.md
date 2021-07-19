---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, emailAddress, xdm:emailAddress, email, endereço de email, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do endereço de email
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de endereço de email.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 2%

---

# [!UICONTROL Tipo de dados de ] endereços de email

[!UICONTROL O ] endereço de email é um tipo de dados XDM padrão que descreve os detalhes de um endereço de email.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `address` | O endereço técnico do email, como geralmente definido no RFC2822 e nos padrões subsequentes (por exemplo, `name@domain.com`). |
| `label` | Informações adicionais de exibição que podem estar disponíveis. Por exemplo, se um email tiver uma exibição de endereço avançado do Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` seria colocado nesse campo. |
| `primary` | Indica se este é o endereço de email principal do indivíduo. Um perfil pode ter somente um endereço de email `primary` em um determinado momento. |
| `status` | Indica se o endereço de email pode ser usado no momento |
| `statusReason` | Uma descrição do `status` atual. |
| `type` | A maneira como a conta se relaciona à pessoa (como `work` ou `personal`). |

{style=&quot;table-layout:auto&quot;}


Para obter mais detalhes sobre o tipo de dados de endereço de email, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
