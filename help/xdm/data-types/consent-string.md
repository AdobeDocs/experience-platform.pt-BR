---
solution: Experience Platform
title: Tipo de dados da string de consentimento
description: Saiba mais sobre o tipo de dados XDM da string de consentimento.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL String de consentimento] tipo de dados

[!UICONTROL String de consentimento] é um tipo de dados XDM padrão que descreve um valor de sequência de caracteres que representa o consentimento de um cliente. Inclui informações contextuais, como o padrão para a cadeia de consentimento (por exemplo, o [Estrutura de transparência e consentimento (TCF) do IAB 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `consentStandard` | String | O padrão para a cadeia de consentimento. Isso ajuda a determinar o formato da cadeia de consentimento conforme definido pelos serviços de gerenciamento de consentimento. |
| `consentStandardVersion` | String | A versão do padrão de consentimento, usada para definir com precisão o formato da cadeia de caracteres de consentimento conforme definido pelos serviços de gerenciamento de consentimento. |
| `consentStringValue` | String | A string de consentimento completa fornecida pelo serviço de gerenciamento de consentimento. `consentStandard` e `consentStandardVersion` ajuda a definir como analisar esta cadeia de caracteres. |
| `containsPersonalData` | Booleano | Quando esse campo é true, significa que essa cadeia de consentimento precisa ser processada para aplicar o consentimento. |
| `gdprApplies` | Booleano | Quando esse campo é verdadeiro, significa que o consentimento está vindo com dados pessoais. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
