---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, phoneNumber, xdm:phoneNumber, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do número de telefone
description: Este documento fornece uma visão geral do tipo de dados XDM do número de telefone.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# [!UICONTROL Número de telefone] tipo de dados

[!UICONTROL Número de telefone] é um tipo de dados XDM padrão que descreve os detalhes de um número de telefone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriedade | Descrição |
| --- | --- |
| `extension` | O número de discagem interno usado para chamar de um intercâmbio privado, operador ou quadro de distribuição. |
| `number` | O número de telefone. Observe que o número de telefone é uma string e pode incluir caracteres significativos, como colchetes `()`, hífens `-`ou caracteres para indicar identificadores de submarcação como extensões `x` por exemplo, `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Um valor booleano que indica se esse é o número de telefone principal do indivíduo. Ao contrário do endereço ou endereço de email, pode haver vários números de telefone primários; um por canal de comunicação. O canal de comunicação é definido pelo tipo (indicado pelo nome da propriedade pai): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`e `fax`. |
| `status` | Indica se o número de telefone pode ser usado no momento. |
| `statusReason` | Uma descrição do status atual. |
| `validity` | Um nível de correção técnica do número de telefone. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados do número de telefone, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
