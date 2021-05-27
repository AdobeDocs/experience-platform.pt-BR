---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, aplicativo, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados do aplicativo
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Application Experience Data Model (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

#  Tipo de dados da aplicação

 Aplicativo é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes relacionados às interações geradas pelo aplicativo. Um aplicativo se refere a uma experiência de software, como um aplicativo móvel ou de desktop que pode ser instalado, executado, fechado ou desinstalado por um usuário final. As propriedades desse tipo de dados não se destinam a descrever agentes como chatbots, plug-ins baseados em navegador ou outras experiências que não se aplicam a aplicativos.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Medição]](./measure.md) | Descreve detalhes sobre o término de um aplicativo. |
| `crashes` | [[!UICONTROL Medição]](./measure.md) | Essa propriedade é acionada quando o aplicativo não sai conforme esperado. |
| `featureUsages` | [[!UICONTROL Medição]](./measure.md) | Descreve todos os dados da ativação de um recurso de aplicativo que está sendo medido. |
| `firstLaunches` | [[!UICONTROL Medição]](./measure.md) | Contém dados sobre a primeira inicialização. Essa propriedade é acionada na primeira inicialização após uma instalação. |
| `installs` | [[!UICONTROL Medição]](./measure.md) | Registra a instalação de um aplicativo em um dispositivo quando um evento de instalação específico está disponível. |
| `launches` | [[!UICONTROL Medição]](./measure.md) | Descreve um valor associado à inicialização de um aplicativo. Isso é acionado a cada execução, incluindo falhas, instalações e retomada do segundo plano quando o tempo limite da sessão foi excedido. |
| `upgrades` | [[!UICONTROL Medição]](./measure.md) | Contém dados sobre a atualização de um aplicativo que foi instalado anteriormente. Isso é acionado na primeira inicialização após uma atualização. |
| `id` | String | Um identificador exclusivo para o aplicativo. |
| `name` | String | O nome do aplicativo  |
| `userPerspective` | String | A perspectiva ou relação física entre o usuário e o aplicativo ou marca no momento em que um evento aconteceu. Entender a perspectiva do usuário em relação ao aplicativo ajuda a gerar sessões com precisão, pois na maioria das vezes você não desejará incluir eventos `background` e `detached` como parte de uma sessão &quot;ativa&quot;. O valor dessa propriedade deve ser igual a um dos valores de enumeração listados abaixo. <li> `foreground`: O usuário e o aplicativo estão interagindo diretamente um com o outro. </li> <li> `background`: O aplicativo e o usuário interagem indiretamente. Por exemplo, o aplicativo pode medir um valor e atualizar enquanto a tela está bloqueada ou outro aplicativo está sendo usado em primeiro plano.  </li> <li> `detached`: Desconectado significa que o evento foi relacionado ao aplicativo, mas não veio diretamente dele, como o envio de uma notificação por email ou por push de um sistema externo. |
| `version` | String | A versão do aplicativo. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
