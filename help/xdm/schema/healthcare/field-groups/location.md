---
title: Grupo de campos de esquema de localização
description: Saiba mais sobre o grupo de campos Esquema de localização.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# Grupo de campos de esquema [!UICONTROL Local]

[!UICONTROL O local] é um grupo de campos de esquema padrão para a [[!DNL Location] classe](../classes/location.md). Ele fornece um único campo de tipo de objeto `healthcareLocation` que captura detalhes e informações de posição para um local.

![Estrutura do grupo de campos](../../../images/healthcare/field-groups/location.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Endereço] | `address` | [[!UICONTROL Endereço]](../data-types/address.md) | O endereço do local físico. |
| [!UICONTROL Característica] | `characteristic` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | Uma coleção das características do local. |
| [!UICONTROL Contato] | `contact` | Matriz de [[!UICONTROL Detalhes de Contato Estendidos]](../data-types/extended-contact-detail.md) | Os detalhes de contato da localização. |
| [!UICONTROL Ponto de extremidade] | `endpoint` | Matriz de [[!UICONTROL Referência]](../data-types/reference.md) | Os endpoints técnicos que fornecem acesso aos serviços operacionais da localização. |
| [!UICONTROL Formulário] | `form` | [[!UICONTROL Conceito codificável]](../data-types/codeable-concept.md) | O formato físico do local. |
| [!UICONTROL Horas de Operação] | `hoursOfOperation` | Matriz de [[!UICONTROL Disponibilidade]](../data-types/availability.md) | Que dias e horários esse local normalmente está aberto (incluindo exceções). |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../data-types/identifier.md) | O código ou número exclusivo que identifica o local. |
| [!UICONTROL Gerenciando a Organização] | `managingOrganization` | [[!UICONTROL Referência]](../data-types/reference.md) | A organização responsável pelo provisionamento e manutenção. |
| [!UICONTROL Status operacional] | `operationalStatus` | [[!UICONTROL Codificação]](../data-types/coding.md) | O status operacional da localização. |
| [!UICONTROL Parte Do Local] | `partOf` | [[!UICONTROL Referência]](../data-types/reference.md) | A localização da qual esta localização faz parte. |
| [!UICONTROL Posição] | `position` | Objeto | A localização geográfica absoluta. Contém três propriedades no formato Double: <li>`longitude`: Longitude com datum WGS84</li> <li>`latitude`: Latitude com referência WGS84.</li> <li>`altitude`: altitude com datum WGS84.</li> |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL Conceito Codificável]](../data-types/codeable-concept.md) | O tipo de função executada no local. |
| [!UICONTROL Serviço Virtual] | `virtualService` | Matriz de [[!UICONTROL Detalhes de Serviço Virtual]](../data-types/virtual-service-detail.md) | Os detalhes de conexão de um serviço virtual. |
| [!UICONTROL Alias] | `alias` | Matriz de cadeias de caracteres | Uma lista de nomes alternativos com os quais o local é ou era conhecido. |
| [!UICONTROL Descrição] | `description` | String | Informações adicionais para identificar o local além de seu nome. |
| [!UICONTROL Modo] | `mode` | String | O modo do local. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Nome] | `name` | String | O nome do local. |
| [!UICONTROL Status] | `status` | String | O status da localização. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
