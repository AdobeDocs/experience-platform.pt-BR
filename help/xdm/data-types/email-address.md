---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;endereçoEmail;xdm:endereçoEmail;email;endereço de email;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Endereço de Email
description: Este documento fornece uma visão geral do tipo de dados XDM de endereço de email.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!UICONTROL Endereço de email] tipo de dados

[!UICONTROL Endereço de email] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes de um endereço de email.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propriedade | Descrição |
| --- | --- |
| `address` | O endereço técnico do email conforme geralmente definido no RFC2822 e padrões subsequentes (por exemplo, `name@domain.com`).<br><br>No XDM, os endereços de email devem conter um domínio de nível superior válido para passar na validação. Consulte o seguinte [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) para obter uma lista completa de domínios de nível superior válidos, conforme definido pela IANA (Internet Assigned Numbers Authority). |
| `label` | Informações adicionais de exibição que podem estar disponíveis. Por exemplo, se um email tiver uma exibição de endereço avançado do Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` será colocado nesse campo. |
| `primary` | Indica se é o endereço de email principal do indivíduo. Um perfil pode ter apenas um `primary` endereço de email em um determinado momento. |
| `status` | Indica se o endereço de email pode ser usado atualmente |
| `statusReason` | Uma descrição do atual `status`. |
| `type` | A forma como a conta se relaciona com a pessoa (como `work` ou `personal`). |

{style="table-layout:auto"}


Para obter mais detalhes sobre o tipo de dados do endereço de email, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
