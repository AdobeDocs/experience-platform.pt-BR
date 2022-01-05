---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, emailAddress, xdm:emailAddress, email, endereço de email, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do endereço de email
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de endereço de email.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: fe6abe468025ab3373f802954aedceeb1af625fe
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL Endereço de email] tipo de dados

[!UICONTROL Endereço de email] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes de um endereço de email.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `address` | O endereço técnico do email, como geralmente definido no RFC2822 e nos padrões subsequentes (por exemplo, `name@domain.com`).<br><br>No XDM, os endereços de email devem conter um domínio de nível superior válido para passarem a validação. Consulte o seguinte [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) para obter uma lista completa de domínios de nível superior válidos, conforme definido pela IANA (Internet Assigned Numbers Authority). |
| `label` | Informações adicionais de exibição que podem estar disponíveis. Por exemplo, se um email tiver uma exibição de endereço avançado do Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` seria colocado nesse campo. |
| `primary` | Indica se este é o endereço de email principal do indivíduo. Um perfil pode ter apenas um `primary` endereço de email em um determinado momento. |
| `status` | Indica se o endereço de email pode ser usado no momento |
| `statusReason` | Uma descrição do atual `status`. |
| `type` | A forma como a conta se relaciona com a pessoa (como `work` ou `personal`). |

{style=&quot;table-layout:auto&quot;}


Para obter mais detalhes sobre o tipo de dados de endereço de email, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
