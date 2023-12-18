---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;phoneNumber;xdm:phoneNumber;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Número de Telefone
description: Saiba mais sobre o tipo de dados Phone Number XDM.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# [!UICONTROL Número de telefone] tipo de dados

[!UICONTROL Número de telefone] é um tipo de dados XDM padrão que descreve os detalhes de um número de telefone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriedade | Descrição |
| --- | --- |
| `extension` | O número de discagem interna usado para ligar de uma central privada, operadora ou mesa telefônica. |
| `number` | O telefone. Observe que o número de telefone é uma string e pode incluir caracteres significativos, como colchetes `()`, hífens `-`ou caracteres para indicar identificadores de submarcação como extensões `x` por exemplo, `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Um valor booleano que indica se este é o número de telefone principal do indivíduo. Ao contrário do endereço ou endereço de email, pode haver vários números de telefone principais, um por canal de comunicação. O canal de comunicação é definido pelo tipo (indicado pelo nome da propriedade principal): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, e `fax`. |
| `status` | Indica se o número de telefone pode ser usado atualmente. |
| `statusReason` | Uma descrição do status atual. |
| `validity` | Um nível de correção técnica do número de telefone. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados do número de telefone, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
