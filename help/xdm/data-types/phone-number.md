---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do número de telefone
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do número de telefone.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# [!UICONTROL Tipo de dados de número] de telefone

[!UICONTROL O número] de telefone é um tipo de dados XDM padrão que descreve os detalhes de um número de telefone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriedade | Descrição |
| --- | --- |
| `extension` | O número de discagem interno usado para chamar de um intercâmbio privado, operador ou central telefônica. |
| `number` | O número de telefone. Observe que o número de telefone é uma string e pode incluir caracteres significativos, como colchetes `()`, hífens `-`ou caracteres, para indicar identificadores de subdiscagem, como extensões `x` por exemplo, `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Um valor booliano que indica se este é o número de telefone principal do indivíduo. Diferentemente do endereço ou endereço de email, pode haver vários números de telefone primários; um por canal de comunicação. O canal de comunicação é definido pelo tipo (indicado pelo nome da propriedade pai): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, e `fax`. |
| `status` | Indica se o número de telefone pode ser usado no momento. |
| `statusReason` | Uma descrição do status atual. |
| `validity` | Um nível de correção técnica do número de telefone. |

Para obter mais detalhes sobre o tipo de dados do número de telefone, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)