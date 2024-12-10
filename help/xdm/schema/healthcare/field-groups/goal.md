---
title: Grupo de Campos de Esquema de Meta
description: Saiba mais sobre o grupo de campos Esquema de meta.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# Grupo de campos de esquema [!UICONTROL Meta]

[!UICONTROL Meta] é um grupo de campos de esquema padrão para [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e [[!DNL Provider class]](../../../classes/provider.md). Ele fornece um único campo do tipo objeto `healthcareGoal` que descreve o(s) objetivo(s) pretendido(s) para um paciente, grupo ou atendimento da organização.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/goal/goal.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Status da Conquista] | `achievementStatus` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Descreve a progressão, ou falta dela, em direção à meta em relação à meta. |
| [!UICONTROL Endereços] | `addresses` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | As condições e outros elementos do registro de integridade que devem ser abordados pela meta. |
| [!UICONTROL Categoria] | `category` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Indica uma categoria na qual a meta se enquadra, como dieta ou comportamental. |
| [!UICONTROL Descrição] | `description` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O código ou texto que descreve a meta. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Os identificadores de negócios atribuídos a essa meta pelo executor ou outros sistemas que permanecem constantes à medida que o recurso é atualizado e propagado de servidor para servidor. |
| [!UICONTROL Nota] | `note` | Matriz de [[!UICONTROL Anotação]](../data-types/annotation.md) | Comentários sobre a meta. |
| [!UICONTROL Resultado] | `outcome` | Matriz de [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | Identifica a alteração (ou falta de alteração) quando o status da meta é avaliado. |
| [!UICONTROL Prioridade] | `priority` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Identifica o nível de importância acordado mutuamente associado à obtenção ou sustentação da meta. |
| [!UICONTROL Source] | `source` | [[!UICONTROL Referência]](../data-types/reference.md) | Indica a fonte da meta, como o paciente ou o profissional. |
| [!UICONTROL Iniciar Conceito Codificável] | `startCodeableConcept` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O evento após o qual o objetivo deve ser persuadido. |
| [!UICONTROL Assunto |]`subject` | [[!UICONTROL Referência]](../data-types/reference.md) | Identifica o paciente, grupo ou organização para quem a meta está sendo estabelecida. |
| [!UICONTROL Target] | `target` | Matriz de objetos | Indica a linha do tempo de etapas específicas da meta. Consulte a [seção abaixo](#target) para obter mais informações. |
| [!UICONTROL Contínuo] | `continous` | Booleano | Indica se, após atingir a meta, é necessária uma atividade em andamento para sustentar o objetivo da meta. |
| [!UICONTROL Status do ciclo de vida] | `lifecycleStatus` | String | O status do ciclo de vida da meta. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Data de Início] | `startDate` | Data | A data após a qual a meta deve começar a ser perseguida. |
| [!UICONTROL Data do status] | `statusDate` | Data | Identifica quando o status foi criado. |
| [!UICONTROL Motivo do status] | `statusReason` | String | Registra o motivo do status atual. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de destino](../../../images/healthcare/field-groups/goal/target.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Detalhar Conceito Codificável] | `detailCodeableConcept` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O código de público alvo a ser alcançado para indicar o cumprimento da meta. |
| [!UICONTROL Quantidade Detalhada] | `detailQuantity` | [[!UICONTROL Quantidade]](../data-types/quantity.md) | A quantidade de destino a ser atingida para indicar o cumprimento da meta. |
| [!UICONTROL Intervalo de detalhes] | `detailRange` | [[!UICONTROL Intervalo]](../data-types/range.md) | O intervalo alvo a ser alcançado para indicar o cumprimento da meta. |
| [!UICONTROL Taxa de Detalhes] | `detailRatio` | [[!UICONTROL Taxa]](../data-types/ratio.md) | A taxa de meta a ser atingida para indicar o cumprimento da meta. |
| [!UICONTROL Medida] | `measure` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O parâmetro do valor está sendo rastreado. |
| [!UICONTROL Booleano de detalhe] | `detailBoolean` | Booleano | Indica o cumprimento da meta. |
| [!UICONTROL Inteiro Detalhado] | `detailInteger` | Número inteiro | O número alvo a ser alcançado para indicar o cumprimento da meta. |
| [!UICONTROL Cadeia de Caracteres de Detalhes] | `detailString` | String | O valor de destino a ser alcançado para indicar o cumprimento da meta. |
| [!UICONTROL Data de vencimento] | `dueDate` | Data | A data até a qual o público alvo deve ser alcançado. |
