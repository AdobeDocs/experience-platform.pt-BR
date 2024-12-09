---
title: Tipo de Dados de Detalhes do Serviço Virtual
description: Saiba mais sobre o tipo de dados do Virtual Service Detail Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# Tipo de dados [!UICONTROL Detalhes do Serviço Virtual]

[!UICONTROL Detalhes do Serviço Virtual] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes do contato do serviço virtual. Esse tipo de dados é criado de acordo com as especificações do HL7 FHIR versão 5.

![Estrutura de tipo de dados de Detalhes do Serviço Virtual](../../images/data-types/healthcare/virtual-service-detail.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Ponto de Contato de Endereço] | `addressContactPoint` | [[!UICONTROL Ponto de contato]](../healthcare/contact-point.md) | Os detalhes de um ponto de contato mediado por tecnologia, como telefone, fax ou email. |
| [!UICONTROL Detalhes do Contato Estendido do Endereço] | `addressExtendedContactDetail` | [[!UICONTROL Detalhes do Contato Estendido]](../healthcare/extended-contact-detail.md) | Informações de contato estendidas. |
| [!UICONTROL Tipo de canal] | `channelType` | [[!UICONTROL Codificação]](../healthcare/coding.md) | O tipo de serviço virtual ao qual se conectar, como Teams, Zoom ou WhatsApp. |
| [!UICONTROL Informações adicionais] | `additionalInfo` | Matriz de cadeias de caracteres | O endereço para ver detalhes de conexão alternativos, representado como um URI. |
| [!UICONTROL Cadeia de Caracteres de Endereço] | `addressString` | String | O endereço a ser usado para se conectar ao serviço virtual. |
| [!UICONTROL Url Do Endereço] | `addressUrl` | String | O URL a ser usado para se conectar ao serviço virtual, representado como um URI. |
| [!UICONTROL Número Máximo de Participantes] | `maxParticipants` | Número inteiro | O número máximo de participantes aceito, com um valor mínimo de `0`. |
| [!UICONTROL Chave de sessão] | `sessionKey` | String | A chave de sessão exigida pelo serviço virtual. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
