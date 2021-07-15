---
solution: Experience Platform
title: Tipo de dados da string de consentimento
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM da cadeia de consentimento.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# [!UICONTROL Tipo ] de dados de consentimento

[!UICONTROL A ] Sequência de caracteres de consentimento é um tipo de dados XDM padrão que descreve um valor de string que representa o consentimento de um cliente. Inclui informações contextuais, como o padrão para a cadeia de consentimento (por exemplo, o [Estrutura de transparência e consentimento (TCF) 2.0](../field-groups/profile/iab.md) do IAB).

![](../images/data-types/consent-string.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `consentStandard` | String | O padrão para a cadeia de consentimento. Isso ajuda a determinar o formato da cadeia de consentimento, conforme definido pelos serviços de gerenciamento de consentimento. |
| `consentStandardVersion` | String | A versão do padrão de consentimento, usada para definir com precisão o formato da cadeia de consentimento conforme definido pelos serviços de gerenciamento de consentimento. |
| `consentStringValue` | String | A cadeia de consentimento completo, conforme fornecido pelo serviço de gerenciamento de consentimento. `consentStandard` e  `consentStandardVersion` ajuda a definir como analisar essa string. |
| `containsPersonalData` | Booleano | Quando esse campo é verdadeiro, significa que essa cadeia de consentimento precisa ser processada para imposição de consentimento. |
| `gdprApplies` | Booleano | Quando esse campo é verdadeiro, significa que o consentimento vem com dados pessoais. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
