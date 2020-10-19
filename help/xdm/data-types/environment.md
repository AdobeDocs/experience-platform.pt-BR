---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;environment;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do ambiente
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do Ambiente.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---


# [!UICONTROL Tipo de dados do ambiente]

[!UICONTROL Ambiente] é um tipo de dados XDM padrão que descreve o ambiente ao redor de um evento observado, detalhando especificamente informações transitórias, como versões de rede e software.

>[!IMPORTANT]
>
>Todos os valores devem ser alinhados com o banco de dados [DeviceAtlas](https://deviceatlas.com) , licenciado pelo Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc` | Objeto | Um objeto que contém um único campo, `language`, que indica o idioma do ambiente para representar as preferências linguísticas, geográficas ou culturais do usuário para a apresentação de dados. Os idiomas são especificados no código de idioma, conforme definido em [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Detalhes do navegador](./browser-details.md) | Descreve os detalhes específicos do navegador do ambiente, como nome do navegador, versão, versão do JavaScript, string do agente do usuário e linguagem de aceitação. |
| `ISP` | String | O nome do provedor de serviço da Internet do usuário. |
| `carrier` | String | O nome da operadora de rede móvel ou MNO (também conhecido como provedor de serviço sem fio, operadora de rede sem fio, empresa celular ou operadora de rede móvel) que vende e entrega serviços de comunicação ao usuário. |
| `colorDepth` | Número inteiro | O número de bits usados para cada componente de cor de um único pixel. |
| `connectionType` | String | O tipo de conexão com a Internet. Os valores aceitos incluem: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | String | O domínio do ISP do usuário. |
| `ipV4` | String | O rótulo numérico atribuído a um dispositivo participante em uma rede de computadores que usa o Internet Protocol para comunicação (32 bits). |
| `ipV6` | String | O rótulo numérico atribuído a um dispositivo participante em uma rede de computadores que usa o Internet Protocol para comunicação (128 bits). |
| `operatingSystem` | String | O nome do sistema operacional usado quando a observação foi feita. O atributo não deve conter nenhuma informação de versão, como `10.5.3`, mas conter designações de &quot;edição&quot;, como `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | String | O nome do fornecedor do sistema operacional usado quando a observação foi feita. |
| `operatingSystemVersion` | String | Identificador da versão completa do sistema operacional utilizado quando a observação foi feita. As versões geralmente são compostas numericamente, mas podem estar em um formato definido pelo fornecedor. |
| `type` | String | O tipo do ambiente do aplicativo. Consulte o [apêndice](#type) para obter os valores aceitos. |
| `viewportHeight` | Número inteiro | O tamanho vertical em pixels da janela em que a experiência foi exibida. Para um evento de visualização da Web, esta é a altura do visor do navegador. |
| `viewPortWidth` | Número inteiro | O tamanho horizontal em pixels da janela em que a experiência foi exibida. Para um evento de visualização da Web, esta é a largura da janela do navegador. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados do [!UICONTROL Dispositivo] .

## Valores aceitos para tipo {#type}

A tabela a seguir descreve os valores aceitos para `type` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `browser` | Browser |
| `application` | aplicação |
| `iot` | Internet das coisas |
| `external` | Sistema externo |
| `widget` | Extensão do aplicativo |