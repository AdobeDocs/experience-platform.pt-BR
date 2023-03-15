---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;ambiente;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados do ambiente
description: Este documento fornece uma visão geral do tipo de dados XDM do ambiente.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---

# [!UICONTROL Ambiente] tipo de dados

[!UICONTROL Ambiente] é um tipo de dados XDM padrão que descreve o ambiente ao redor de um evento observado, detalhando especificamente informações transitórias, como versões de rede e software.

>[!IMPORTANT]
>
>Todos os valores devem estar alinhados com o [DeviceAtlas](https://deviceatlas.com) banco de dados, licenciado pelo Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc` | Objeto | Um objeto que contém um único campo, `language`, que indica o idioma do ambiente para representar as preferências linguísticas, geográficas ou culturais do usuário para a apresentação de dados. Os idiomas são especificados no código de idioma conforme definido em [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Detalhes do navegador](./browser-details.md) | Descreve os detalhes específicos do navegador do ambiente, como nome do navegador, versão, versão do JavaScript, sequência de agente do usuário e linguagem de aceitação. |
| `ISP` | String | O nome do provedor de serviços de Internet do usuário. |
| `carrier` | String | O nome da operadora de rede móvel ou MNO (também conhecido como provedor de serviços sem fio, operadora sem fio, empresa de celular ou operadora de rede móvel) que vende e fornece serviços de comunicação ao usuário. |
| `colorDepth` | Número inteiro | O número de bits usados para cada componente de cor de um único pixel. |
| `connectionType` | String | O tipo de conexão com a Internet. Os valores aceitos incluem: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | String | O domínio do ISP do usuário. |
| `ipV4` | String | O rótulo numérico atribuído a um dispositivo que participa de uma rede de computadores que usa o Internet Protocol para comunicação (32 bits). |
| `ipV6` | String | O rótulo numérico atribuído a um dispositivo que participa de uma rede de computadores que usa o protocolo da Internet para comunicação (128 bits). |
| `operatingSystem` | String | O nome do sistema operacional usado quando a observação foi feita. O atributo não deve conter informações de versão, como `10.5.3`, mas contêm designações de &quot;edição&quot;, como `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | String | O nome do fornecedor do sistema operacional usado quando a observação foi feita. |
| `operatingSystemVersion` | String | O identificador de versão completa do sistema operacional usado quando a observação foi feita. As versões geralmente são compostas numericamente, mas podem estar em um formato definido pelo fornecedor. |
| `type` | String | O tipo de ambiente de aplicativo. Consulte a [apêndice](#type) para obter os valores aceitos. |
| `viewportHeight` | Número inteiro | O tamanho vertical em pixels da janela em que a experiência foi exibida. Para um evento de visualização da Web, essa é a altura da janela de visualização do navegador. |
| `viewPortWidth` | Número inteiro | O tamanho horizontal em pixels da janela em que a experiência foi exibida. Para um evento de visualização da Web, essa é a largura da janela de visualização do navegador. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o [!UICONTROL Dispositivo] tipo de dados.

## Valores aceitos para o tipo {#type}

A tabela a seguir descreve os valores aceitos para `type` e significados associados:

| Valor | Descrição |
| --- | --- |
| `browser` | Navegador |
| `application` | Aplicativo |
| `iot` | Internet das coisas |
| `external` | Sistema externo |
| `widget` | Extensão do aplicativo |
