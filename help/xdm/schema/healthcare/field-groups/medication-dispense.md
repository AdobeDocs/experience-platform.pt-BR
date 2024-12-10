---
title: Grupo de Campos de Esquema de Dispensa de Medicação
description: Saiba mais sobre o grupo de campos do esquema Dispensa de medicação.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Grupo de campos de esquema [!UICONTROL Dispensa de Medicação]

[!UICONTROL Dispensa de Medicação] é um grupo de campos de esquema padrão para a [[!DNL Medication] classe](../../../classes/medication.md), a [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e a [[!DNL Provider class]](../../../classes/provider.md). Ele fornece um único campo de tipo de objeto `healthcareMedicationDispense` que captura informações sobre um medicamento que deve ser ou foi dispensado para uma pessoa/paciente nomeado.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Autorizando a Receita Médica] | `authorizingPrescription` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | A ordem que permite a dispensa da receita. |
| [!UICONTROL Com Base Em] | `basedOn` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | O plano em que a administração do medicamento se baseia. |
| [!UICONTROL Categoria] | `category` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | A categoria em que o medicamento que está sendo dispensado se enquadra, como a categoria legal do medicamento ou a classificação do medicamento. |
| [!UICONTROL Suprimento dos Dias] | `daysSupply` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | O número de dias que o medicamento fornecerá ao paciente. |
| [!UICONTROL Destino] | `destination` | [[!UICONTROL Referência]](../data-types/reference.md) | A instalação ou local para onde o medicamento foi ou será enviado como parte do evento de dispensa. |
| [!UICONTROL Instrução de Dosagem] | `dosageInstruction` | Matriz de [[!UICONTROL Dosagem]](../data-types/dosage.md) | Descreve como o medicamento deve ser usado pelo paciente. |
| [!UICONTROL Encontrado] | `encounter` | [[!UICONTROL Referência]](../data-types/reference.md) | O encontro que estabelece o contexto para este evento. |
| [!UICONTROL Histórico de Eventos] | `eventHistory` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Um resumo dos eventos que ocorreram em torno da dispensação. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Identificadores associados à distribuição. Os identificadores devem ser definidos por processos comerciais e/ou usados para fazer referência a eles quando uma referência direta ao URL não for apropriada. |
| [!UICONTROL Localização] | `location` | [[!UICONTROL Referência]](../data-types/reference.md) | O principal local físico onde a medicação foi dispensada. |
| [!UICONTROL Medicação] | `medication` | [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | Identifica o medicamento que está sendo solicitado. Deve ser um link para um recurso que representa detalhes do medicamento ou um código que identifica o medicamento. |
| [!UICONTROL Motivo Não Executado] | `notPerformedReason` | [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | A razão pela qual a medicação não foi dispensada. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL Anotação]](../data-types/annotation.md) | Informações adicionais sobre a distribuição. |
| [!UICONTROL Parte De] | `partOf` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | O procedimento ou solicitação de medicação que acionou a dispensa. |
| [!UICONTROL Executor] | `performer` | Matriz de objetos | Indica quem ou o que executou o evento de dispensação. Consulte a [seção abaixo](#performer) para obter mais informações. |
| [!UICONTROL Quantidade] | `quantity` | [[!UICONTROL Quantidade Simples]](../data-types/simple-quantity.md) | A quantidade de medicação que foi dispensada, incluindo a unidade de medida. |
| [!UICONTROL Destinatário] | `receiver` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Identifica a pessoa que pegou o medicamento ou o local onde o medicamento foi entregue. |
| [!UICONTROL Assunto] | `subject` | [[!UICONTROL Referência]](../data-types/reference.md) | Um link para um recurso que representa a pessoa ou grupo a quem o medicamento será dado. |
| [!UICONTROL Substituição] | `substitution` | Objeto | Indica se a substituição foi ou não feita como parte da dispensa. Contém quatro propriedades: <li>`wasSubstituted`: um valor booleano que é verdadeiro se o dispensador solicitou uma substituição.</li> <li>`type`: Um valor de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) que fornece um código que significa se uma substituição foi feita.</li> <li>`reason`: Uma matriz de valores de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) que contém o(s) motivo(s) da substituição.</li> <li>`responsibleParty`: Um valor de [[!UICONTROL Reference]](../data-types/reference.md) que fornece a pessoa ou o responsável pela substituição. </li> |
| [!UICONTROL Informações de suporte] | `supportingInformation` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Informações adicionais que apoiam a administração do medicamento. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Descreve o tipo de evento de dispensação executado, como um preenchimento de emergência ou preenchimento parcial. |
| [!UICONTROL Gravado] | `recorded` | DateTime | A data e a hora em que a atividade de despesa começou se `whenPrepared` ou `whenHandedOver` não estiver preenchida. |
| [!UICONTROL Instrução de Dosagem Renderizada] | `renderedDosageInstruction` | String | A representação completa da dose incluída em todas as instruções de dosagem. A utilizar quando forem incluídas instruções de dose múltiplas para representar doses complexas, tais como doses crescentes ou reduzidas. |
| [!UICONTROL Status] | `status` | String | O status da distribuição. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status alterado] | `statusChanged` | DateTime | A data e hora em que o status do registro de despesa foi alterado. |
| [!UICONTROL Ao Entregar] | `whenHandedOver` | DateTime | A data e hora em que o medicamento foi fornecido ao paciente. |
| [!UICONTROL Quando preparado] | `whenPrepared` | DateTime | A data e a hora em que o medicamento fornecido foi embalado e revisto. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura do executor](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Ator] | `actor` | [[!UICONTROL Referência]](../data-types/reference.md) | O profissional (ou similar) que executou a ação. Deve-se assumir que o ator é o distribuidor do medicamento. |
| [!UICONTROL Função] | `function` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O tipo de executor na distribuição, como o operador de data, embalador ou verificador final. |
