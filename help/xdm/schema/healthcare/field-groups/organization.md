---
title: Grupo de Campos de Esquema da Organização
description: Saiba mais sobre o grupo de campos Esquema da organização.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 6%

---

# Grupo de campos de esquema de [!UICONTROL Organização]

[!UICONTROL Organização] é um grupo de campos de esquema padrão para [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e [[!DNL Provider class]](../../../classes/provider.md). Ele fornece um único campo de tipo de objeto `healthcareOrganization` que contém informações sobre agrupamentos de pessoas ou organizações com uma finalidade comum.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/organization/organization.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| ---| --- | --- | --- |
| [!UICONTROL Detalhes de contato] | `contact` | Matriz de [[!UICONTROL Detalhes de Contato Estendidos]](../data-types/extended-contact-detail.md) | Os dados de contato dos dispositivos de comunicação disponíveis para a organização específica. Isso pode incluir endereços, números de telefone, números de fax, números de celular, endereços de email e sites. |
| [!UICONTROL Ponto de Extremidade] | `endpoint` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Terminais técnicos que fornecem acesso aos serviços operados pela organização. |
| [!UICONTROL Identificador] | `indentifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | O identificador usado para identificar a organização em vários sistemas diferentes. |
| [!UICONTROL Parte Da Organização] | `partOf` | [[!UICONTROL Referência]](../data-types/reference.md) | A organização da qual esta organização faz parte. |
| [!UICONTROL Qualificação] | `qualification` | Matriz de objetos | As certificações, acreditações, treinamento, designações e licenças oficiais que autorizam e/ou aprovam de outra forma a prestação de cuidados pela organização. Consulte a [seção abaixo](#qualification) para obter mais informações. |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | O tipo de organização que é. |
| [!UICONTROL Ativo] | `active` | Booleano | Se o registro da organização ainda está em uso ativo. |
| [!UICONTROL Alias] | `alias` | Matriz de cadeias de caracteres | Uma lista de nomes alternativos com os quais a organização é conhecida ou era conhecida no passado. |
| [!UICONTROL Descrição] | `description` | String | A descrição da organização que ajuda a fornecer o contexto geral para garantir que a organização correta seja selecionada. |
| [!UICONTROL Nome] | `name` | String | O nome associado à organização. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![estrutura de qualificação](../../../images/healthcare/field-groups/organization/qualification.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | Representação codificada da qualificação. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | Um identificador alocado para essa qualificação para essa organização. |
| [!UICONTROL Emissor] | `issuer` | [[!UICONTROL Referência]](../data-types/reference.md) | Organização que regulamenta e emite a qualificação. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Período durante o qual a qualificação é válida. |
