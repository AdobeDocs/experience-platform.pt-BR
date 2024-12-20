---
title: Grupo de Campos Esquema de Programação
description: Saiba mais sobre o grupo de campos Esquema de agendamento.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# Grupo de campos de esquema [!UICONTROL Agendar]

[!UICONTROL Agenda] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e a [[!DNL Provider class]](../../../classes/provider.md). Ele fornece um único campo de tipo de objeto `healthcareSchedule`, que é um contêiner de espaços de tempo que podem estar disponíveis para compromissos de reserva.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/schedule.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Ator] | `actor` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Os slots que fazem referência a esse cronograma, fornecendo os detalhes de disponibilidade para esses recursos referenciados. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Os identificadores externos do agendamento. |
| [!UICONTROL Horizonte de Planejamento] | `planningHorizon` | [[!UICONTROL Período]](../data-types/period.md) | O período de tempo coberto pelos slots que referenciam esta agenda, mesmo que não exista nenhuma. |
| [!UICONTROL Categoria de Serviço] | `serviceCategory` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Uma categorização ampla do serviço a ser executado durante o compromisso. |
| [!UICONTROL Tipo de serviço] | `serviceType` | Matriz de [[!UICONTROL Referência codificável]](../data-types/codeable-reference.md) | O serviço específico a ser executado durante o compromisso. |
| [!UICONTROL Especialidade] | `specialty` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | A especialidade do profissional que seria necessário para executar o serviço solicitado na nomeação. |
| [!UICONTROL Ativo] | `active` | Booleano | Indica se o registro de agendamento está em uso ativo. |
| [!UICONTROL Comentário] | `comment` | String | Observações sobre a disponibilidade com o objetivo de descrever quaisquer informações alargadas, tais como restrições personalizadas nas faixas horárias. |
| [!UICONTROL Nome] | `name` | String | A descrição da programação como ela seria apresentada a um consumidor durante a pesquisa. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
