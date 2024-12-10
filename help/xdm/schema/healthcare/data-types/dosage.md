---
title: Tipo de dados de dosagem
description: Saiba mais sobre o tipo de dados Dosage Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Dosagem]

[!UICONTROL Dosagem] é um tipo de dados padrão do Experience Data Model (XDM) que descreve como o medicamento é/foi tomado ou deve ser tomado. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de dosagem](../../../images/healthcare/data-types/dosage/dosage.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Instruções adicionais] | `additionalInstruction` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Instruções complementares ou advertências ao paciente. |
| [!UICONTROL Conforme Necessário Para] | `asNeededFor` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Descreve qual problema a medicação deve ser tomada conforme necessário. |
| [!UICONTROL Dose E Taxa] | `doseAndRate` | Matriz de objetos | A quantidade de medicamento administrada ou a quantidade típica a ser administrada. Consulte a [seção abaixo](#dose-and-rate) para obter mais informações |
| [!UICONTROL Dose Máxima Por Administração] | `maxDosePerAdministration` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | O limite máximo de medicação por administração. |
| [!UICONTROL Dose Máxima Por Vida] | `maxDosePerLifetime` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | O limite máximo de medicação por vida útil do paciente. |
| [!UICONTROL Dose Máxima Por Período] | `maxDosePerPeriod` | Matriz de [[!UICONTROL Taxa]](../data-types/ratio.md) | O limite máximo de medicação por unidade de tempo. |
| [!UICONTROL Método] | `method` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | A técnica para administrar a medicação. |
| [!UICONTROL Rota] | `route` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Como o medicamento deve entrar no corpo. |
| [!UICONTROL Site do Corpo] | `site` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O local do corpo para administrar o medicamento. |
| [!UICONTROL Horário] | `timing` | [[!UICONTROL Horário]](../data-types/timing.md) | Quando a medicação deve ser administrada. |
| [!UICONTROL Conforme Necessário] | `asNeeded` | Booleano | Um indicador para saber se a medicação deve ser tomada conforme necessário. |
| [!UICONTROL Instruções para o paciente] | `patientInstruction` | String | Instruções em termos a serem entendidos pelo paciente ou consumidor. |
| [!UICONTROL Sequência] | `Integer` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | A ordem das instruções de dosagem. |
| [!UICONTROL Texto] | `text` | String | Instruções de dosagem do texto do plano. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de dose e taxa](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Quantidade da Dose] | `doseQuantity` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | A quantidade de medicação por dose. |
| [!UICONTROL Intervalo de Doses] | `doseRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | A quantidade de medicação por dose. |
| [!UICONTROL Quantidade de Taxa] | `rateQuantity` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | A quantidade de medicação por unidade de tempo. |
| [!UICONTROL Intervalo de taxas] | `rateRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | A quantidade de medicação por unidade de tempo. |
| [!UICONTROL Taxa Proporção] | `rateRatio` | [[!UICONTROL Taxa]](../data-types/ratio.md) | A quantidade de medicação por unidade de tempo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O tipo de dose ou taxa especificada. |
