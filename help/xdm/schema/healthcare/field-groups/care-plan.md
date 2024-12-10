---
title: Grupo de Campos de Esquema de Plano de Assistência Médica
description: Saiba mais sobre o grupo de campos Plano de atendimento.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# Grupo de campos de esquema [!UICONTROL Plano de atendimento]

O [!UICONTROL Plano de Atendimento] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md). Ele fornece um único campo de tipo de objeto `healthcareCarePlan` que captura um plano de saúde para um paciente ou grupo.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Atividade] | `activity` | Matriz de objetos | Identifica uma ação que ocorreu ou está planejada para ocorrer como parte do plano. Consulte a [seção abaixo](#activity) para obter mais informações. |
| [!UICONTROL Endereços] | `addresses` | Matriz de [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | Identifica as condições ou preocupações que o plano de atendimento trata. |
| [!UICONTROL Com Base Em] | `basedOn` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Um recurso de solicitação de nível superior que é preenchido no todo ou em parte por este plano de assistência. |
| [!UICONTROL Equipe de atendimento] | `careTeam` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Identifica todas as pessoas e organizações que devem estar envolvidas no tratamento previsto por este plano. |
| [!UICONTROL Categoria] | `category` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Identifica que tipo de plano é para dar suporte à diferenciação entre vários planos coexistentes. |
| [!UICONTROL Colaborador] | `contributor` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Identifica a(s) pessoa(s), organização ou dispositivo(s) que forneceu o conteúdo do plano de cuidado. |
| [!UICONTROL Responsável] | `custodian` | [[!UICONTROL Referência]](../data-types/reference.md) | Quando preenchido, o custodiante é responsável e atribuído ao plano de cuidado. |
| [!UICONTROL Encontrado] | `encounter` | [[!UICONTROL Referência]](../data-types/reference.md) | O encontro durante o qual o plano de cuidado foi criado. |
| [!UICONTROL Meta] | `goal` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | O(s) objetivo(s) pretendido(s) da execução do plano. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Os identificadores de negócios atribuídos a esse plano de atendimento pelo executor ou outros sistemas que permanecem constantes à medida que o recurso é atualizado e propagado de servidor para servidor. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL Anotação]](../data-types/annotation.md) | Observações gerais sobre o plano de cuidado não abordado em outros atributos. |
| [!UICONTROL Parte De] | `partOf` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | O plano de cuidados mais amplo no qual esse plano de cuidados específico é um componente ou etapa. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Indica quando o plano entrou (ou deve entrar em vigor) e quando terminou. |
| [!UICONTROL Substitui] | `replaces` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | O plano de cuidados concluído ou encerrado cuja função é assumida por este plano de cuidados. |
| [!UICONTROL Assunto] | `subject` | [[!UICONTROL Referência]](../data-types/reference.md) | Identifica o paciente ou grupo cujo tratamento pretendido está descrito no plano. |
| [!UICONTROL Informações de suporte] | `supportingInfo` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Identifica partes do registro do paciente que influenciaram a formação do plano. Isso pode incluir comorbidades, procedimentos recentes, limitações ou avaliações recentes. |
| [!UICONTROL Criado] | `created` | DateTime | Representa quando esse plano de atendimento foi criado no sistema, que geralmente é uma data gerada pelo sistema. |
| [!UICONTROL Descrição] | `description` | String | Uma descrição do escopo e da natureza do plano. |
| [!UICONTROL Instancia Canônico] | `instantiatesCanonical` | Matriz de cadeias de caracteres | O URL que aponta para um protocolo, diretriz, questionário ou outra definição definida pelo FHIR que é atendido no todo ou em parte por esse plano. |
| [!UICONTROL Instancia Uri] | `instantiatesUri` | Matriz de cadeias de caracteres | O URL que aponta para um protocolo, diretriz, questionário ou outra definição mantida externamente e que é atendido no todo ou em parte por esse plano, representado como um URI. |
| [!UICONTROL Propósito] | `intent` | String | A intenção do plano de cuidado. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Status] | `status` | String | O status do plano de cuidado. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Title] | `title` | String | O nome do plano de cuidado. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de atividade](../../../images/healthcare/field-groups/care-plan/activity.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Atividade realizada] | `performedActivity` | Matriz de [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | Os resultados da atividade, como um compromisso ou um procedimento. |
| [!UICONTROL Referência da atividade planejada] | `plannedActivityReference` | [[!UICONTROL Referência]](../data-types/reference.md) | Os detalhes da atividade proposta. |
| [!UICONTROL Progresso] | `progress` | Matriz de [[!UICONTROL Anotação]](../data-types/annotation.md) | Observações sobre a aderência, o status ou o progresso da atividade. |
