---
title: Grupo de Campos de Esquema de Solicitação de Medicamento
description: Saiba mais sobre o grupo de campos do esquema Solicitação de medicação.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# Grupo de campos de esquema [!UICONTROL Solicitação de medicação]

[!UICONTROL Solicitação de Medicação] é um grupo de campos de esquema padrão para a [[!DNL Medication] classe](../../classes/location.md), a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) e a [[!DNL Provider class]](../../classes/provider.md). Ele fornece um único campo de tipo de objeto `healthcareMedicationDispense` que captura uma ordem ou solicitação para o fornecimento do medicamento e as instruções para a administração do medicamento a um paciente.

![Estrutura do grupo de campos](../../images/field-groups/healthcare-medication-request/medication-request.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Com Base Em] | `basedOn` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O plano ou solicitação preenchido por esta solicitação de medicação. |
| [!UICONTROL Categoria] | `category` | Matriz de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) | A categorização ou agrupamento da solicitação de medicação. |
| [!UICONTROL Tipo De Curso De Terapia] | `courseOfTherapyType` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | A descrição do padrão geral de administração do medicamento ao paciente. |
| [!UICONTROL Dispositivo] | `device` | Matriz de [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | O tipo de dispositivo a ser usado para a administração do medicamento. |
| [!UICONTROL Solicitação de dispensa] | `dispenseRequest` | Objeto | Indica os detalhes específicos da solicitação de dispensa, geralmente conhecida como pedido de medicação. Consulte a [seção abaixo](#dispense-request) para obter mais informações. |
| [!UICONTROL Instrução de Dosagem] | `dosageInstructions` | Matriz de [[!UICONTROL Dosagem]](../../data-types/healthcare/dosage.md) | Instruções específicas sobre como o medicamento deve ser usado pelo paciente. |
| [!UICONTROL Período de Dose Efetiva] | `effectiveDosePeriod` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | O período durante o qual a medicação deve ser tomada. Quando existem várias linhas `dosageInstruction` (por exemplo, quando doses reduzidas), esta é a data mais antiga e a data mais recente das instruções de dosagem. |
| [!UICONTROL Encontrado] | `encounter` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O encontro durante o qual a solicitação foi criada. |
| [!UICONTROL Histórico de Eventos] | `eventHistory` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Link para registros de eventos relacionados à solicitação de medicação, como atender à solicitação, momentos de transições de estado principais ou atualizações relevantes. |
| [!UICONTROL Identificador do Grupo] | `groupIdentifier` | [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | Um identificador compartilhado em várias instâncias de solicitação independentes que foram ativadas por um único autor. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | Identificadores associados à solicitação de medicamento que são definidos por processos comerciais e/ou são usados para fazer referência a ela quando uma referência direta de URL para o próprio recurso não é apropriada. |
| [!UICONTROL Source de Informações] | `informationSource` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A pessoa ou organização que forneceu as informações para a solicitação se a origem for outra que não `requester`. |
| [!UICONTROL Seguros] | `insurance` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Planos de seguro, extensões de cobertura, pré-autorizações e/ou pré-determinações que podem ser necessários para a entrega do serviço solicitado. |
| [!UICONTROL Medicação] | `medication` | [[!UICONTROL Referência codificável]](../../data-types/healthcare/codeable-reference.md) | Identifica o medicamento que está sendo solicitado. Deve ser um link para um recurso que representa detalhes do medicamento ou um código que identifica o medicamento. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL Anotação]](../../data-types/healthcare/annotation.md) | Informações adicionais sobre a receita que não puderam ser transmitidas pelos outros atributos. |
| [!UICONTROL Executor] | `performer` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O executor especificado do tratamento/administração do medicamento. Para dispositivos, este é o dispositivo que se destina a realizar a administração do medicamento. |
| [!UICONTROL Tipo de Executor] | `performerType` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | Indica o tipo de executor para a administração do medicamento. |
| [!UICONTROL Receita médica prévia] | `priorPrescription` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A referência a um pedido ou uma receita médica que está sendo substituída por esta solicitação. |
| [!UICONTROL Motivo] | `reason` | Matriz de [[!UICONTROL Referência codificável]](../../data-types/healthcare/reference.md) | O motivo ou indicação para pedir ou não o medicamento. |
| [!UICONTROL Gravador] | `recorder` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A pessoa que inseriu o pedido em nome de outro indivíduo. |
| [!UICONTROL Solicitante] | `requester` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O indivíduo, a organização ou o dispositivo que iniciou a solicitação e é responsável por sua ativação. |
| [!UICONTROL Motivo do status] | `statusReason` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O motivo para o estado atual da solicitação. |
| [!UICONTROL Assunto] | `subject` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O indivíduo ou grupo para o qual a medicação foi solicitada. |
| [!UICONTROL Substituição] | `substitution` | Objeto | Indica se uma substituição pode ou deve fazer parte da dispensa. Contém três propriedades: <li>`allowedBoolean`: Um valor booleano que é verdadeiro se o prescritor permite uma substituição.</li> <li>`allowedCodeableConcept`: Um valor de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) que fornece um código se o prescritor permite uma substituição.</li> <li>`reason`: Um valor de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) que indica um motivo para a substituição.</li> |
| [!UICONTROL Informações de suporte] | `supportingInformation` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Informações para apoiar o cumprimento da medicação, como a altura e o peso do paciente. |
| [!UICONTROL Criado Em] | `authoredOn` | DateTime | A data (e, opcionalmente, a hora) em que a receita foi escrita. |
| [!UICONTROL Não Executar] | `doNotPerform` | Booleano | Um indicador booleano que é verdadeiro é que o paciente deve parar (ou não começar) a tomar o medicamento. |
| [!UICONTROL Propósito] | `intent` | String | A intenção da solicitação. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Prioridade] | `priority` | String | A prioridade da solicitação. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Instrução de Dosagem Renderizada] | `renderedDosageInstruction` | String | A representação completa da dose incluída em todas as instruções de dosagem. A utilizar quando forem incluídas instruções de dose múltiplas para representar doses complexas, tais como doses crescentes ou reduzidas. |
| [!UICONTROL Relatado] | `reported` | Booleano | Indica se esse registro foi capturado como um registro secundário relatado, e não como um registro original de fonte da verdade primária. |
| [!UICONTROL Status] | `status` | String | O status da distribuição. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status alterado] | `statusChanged` | DateTime | A data (e, opcionalmente, a hora) em que o status foi alterado. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura de solicitação de dispensa](../../images/field-groups/healthcare-medication-request/dispense-request.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Intervalo de dispensa] | `dispenseInterval` | [[!UICONTROL Duração]](../../data-types/healthcare/duration.md) | O período mínimo de tempo que deve ocorrer entre dispensas da medicação. |
| [!UICONTROL Dispensador] | `dispenser` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A organização pretendida que irá dispensar o medicamento conforme especificado pelo prescritor. |
| [!UICONTROL Instrução do Dispensador] | `dispenserInstruction` | Matriz de [[!UICONTROL Anotação]](../../data-types/healthcare/annotation.md) | Informações adicionais para o dispensador, como aconselhamento a ser fornecido ao paciente |
| [!UICONTROL Ajuda de administração de dose] | `doseAdministrationAid` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | Informações sobre o tipo de embalagem de adesão a ser fornecida para a dispensa do medicamento. |
| [!UICONTROL Duração de Fornecimento Esperada] | `expectedSupplyDuration` | [[!UICONTROL Duração]](../../data-types/healthcare/duration.md) | O período de tempo durante o qual se espera que o produto fornecido seja usado, ou o período de tempo durante o qual se espera que o dispêndio dure. |
| [!UICONTROL Preenchimento Inicial] | `initialFill` | Objeto | Informações para o preenchimento inicial. Contém duas propriedades: <li>`quantity`: Um valor de [[!UICONTROL Quantidade Simples]](../../data-types/healthcare/simple-quantity.md) que fornece o valor a ser fornecido durante a primeira dispensa.</li> <li>`duration`: Um valor de [[!UICONTROL Duration]](../../data-types/healthcare/duration.md) que fornece a duração esperada da primeira dispensação.</li> |
| [!UICONTROL Quantidade] | `quantity` | [[!UICONTROL Quantidade Simples]](../../data-types/healthcare/simple-quantity.md) | A quantidade a ser dispensada para um preenchimento. |
| [!UICONTROL Período de Validade] | `validityPeriod` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | O período de validade da receita. |
| [!UICONTROL Número De Repetições Permitidas] | `numberOfRepeatsAllowed` | Número inteiro | O número de recargas autorizadas, com um valor mínimo de 0. |
