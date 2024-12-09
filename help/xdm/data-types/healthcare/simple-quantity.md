---
title: Tipo de Dados de Quantidade Simples
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de quantidade simples (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# Tipo de dados [!UICONTROL Quantidade Simples]

[!UICONTROL Quantidade Simples] é um tipo de dados padrão do Experience Data Model (XDM) que fornece uma quantidade medida ou mensurável. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de Quantidade Simples](../../images/data-types/healthcare/simple-quantity.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | String | A forma codificada da unidade. |
| [!UICONTROL Sistema] | `system` | String | O sistema que define o formulário de unidade codificado, representado como um URI. |
| [!UICONTROL Unidade] | `unit` | String | A representação da unidade. |
| [!UICONTROL Valor] | `value` | Duplo | O valor numérico. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
