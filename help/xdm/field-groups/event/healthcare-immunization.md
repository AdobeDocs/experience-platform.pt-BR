---
title: Grupo de Campos de Esquema de Imunização
description: Saiba mais sobre o grupo de campos Esquema de imunização.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 8%

---

# Grupo de campos de esquema [!UICONTROL Imunização]

[!UICONTROL Imunização] é um grupo de campos de esquema padrão para a [[!DNL XDM Experience Event] classe](../../classes/experienceevent.md). Ele fornece um único campo de tipo de objeto `healthcareImmunization` que captura informações de evento de imunização.

![Estrutura do grupo de campos](../../images/field-groups/healthcare-immunization/immunization.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Produto Administrado] | `administeredProduct` | [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | O produto administrado. |
| [!UICONTROL Com Base Em] | `basedOn` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A autoridade na qual se baseia o evento de imunização. |
| [!UICONTROL Quantidade da Dose] | `doseQuantity` | [[!UICONTROL Quantidade Simples]](../../data-types/healthcare/simple-quantity.md) | A quantidade de vacina administrada. |
| [!UICONTROL Encontrado] | `encounter` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O encontro do qual a imunização fez parte. |
| [!UICONTROL Source de Financiamento] | `fundingSource` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | A fonte de financiamento da vacina. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | O identificador comercial. |
| [!UICONTROL Source de Informações] | `informationSource` | [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | Indica a origem do registro relatado. |
| [!UICONTROL Localização] | `location` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O local onde ocorreu a imunização. |
| [!UICONTROL Fabricante] | `manufacturer` | [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | O fabricante da vacina. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL Anotação]](../../data-types/healthcare/annotation.md) | Notas adicionais de imunização. |
| [!UICONTROL Paciente] | `patient` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Que foi imunizado. |
| [!UICONTROL Lote] | `performer` | Matriz de objetos | Que realizaram o evento de imunização. Consulte a [seção abaixo](#performer) para obter mais informações. |
| [!UICONTROL Qualificação de programa] | `programEligibility` | Matriz de objetos | A elegibilidade do paciente para um programa de vacinação específico. Consulte a [seção abaixo](#program-eligibility) para obter mais informações. |
| [!UICONTROL Protocolo aplicado] | `protocolApplied` | Matriz de objetos | O protocolo fornecido pelo provedor. Consulte a [seção abaixo](#protocol-applied) para obter mais informações. |
| [!UICONTROL Reação] | `reaction` | Matriz de objetos | Os detalhes de uma reação após a imunização. Consulte a [seção abaixo](#reaction) para obter mais informações. |
| [!UICONTROL Motivo] | `reason` | Matriz de [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | O motivo da imunização. |
| [!UICONTROL Rota] | `route` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | Como a vacina entrou no corpo. |
| [!UICONTROL Site] | `site` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O local do corpo onde a vacina foi administrada |
| [!UICONTROL Motivo do status] | `statusReason` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O motivo do status atual. |
| [!UICONTROL Motivo Subpotente] | `subpotentReason` | Matriz de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) | A razão da vacina ser subpotente. |
| [!UICONTROL Informações de suporte] | `supportingInformation` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Informações adicionais de apoio à imunização. |
| [!UICONTROL Código de vacina] | `vaccineCode` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O código da vacina administrada. |
| [!UICONTROL Data de vencimento] | `expirationDate` | Data | A data de validade da vacina. |
| [!UICONTROL É Subpotente] | `isSubpotent` | Booleano | O indicador de que a vacina é subpotente. |
| [!UICONTROL Número do Lote] | `lotNumber` | String | O número de lote da vacina. |
| [!UICONTROL DateTime da Ocorrência] | `occurenceDateTime` | DateTime | A data de administração da vacina. |
| [!UICONTROL Cadeia de Caracteres de Ocorrência] | `occurenceString` | String | A data de administração da vacina. |
| [!UICONTROL Source Primário] | `primarySource` | Booleano | Indica se os dados foram capturados de uma fonte primária. |
| [!UICONTROL Status] | `status` | String | O status da imunização. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `completed` </li> <li> `entered-in-error` </li> <li> `not-done` </li> |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.schema.json)

## `performer` {#performer}

`performer` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura do executor](../../images/field-groups/healthcare-immunization/performer.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Ator] | `actor` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O indivíduo ou a organização que estava se apresentando. |
| [!UICONTROL Função] | `function` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | Que tipo de desempenho foi feito. |

## `programEligibility` {#program-eligibility}

`programEligibility` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura programEligibility](../../images/field-groups/healthcare-immunization/program-eligibility.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Programa] | `program` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O programa para o qual a qualificação é declarada. |
| [!UICONTROL Status do programa] | `programStatus` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O status de elegibilidade do paciente para o programa. |

## `protocolApplied` {#protocol-applied}

`protocolApplied` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![protocolApplied estrutura](../../images/field-groups/healthcare-immunization/protocol-applied.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Autoridade] | `authority` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Quem é responsável pela publicação das recomendações. |
| [!UICONTROL Doença do Target] | `targetDisease` | Matriz de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) | A doença que a vacina visa prevenir. |
| [!UICONTROL Número da Dose] | `doseNumber` | String | O número da dose na série. |
| [!UICONTROL Série] | `series` | String | O nome da série de vacinas. |
| [!UICONTROL Doses da Série] | `seriesDoses` | String | Número recomendado de doses para imunidade. |

## `reaction` {#reaction}

`reaction` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de reação](../../images/field-groups/healthcare-immunization/reaction.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Manifestação] | `manifestation` | [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-concept.md) | Informações adicionais sobre a reação. |
| [!UICONTROL Data] | `date` | DateTime | Quando a reação começou. |
| [!UICONTROL Relatado] | `reported` | String | Indica se a reação foi relatada automaticamente. |

