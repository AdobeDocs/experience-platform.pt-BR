---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;aplicativo;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;applications;application;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados do aplicativo
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Application Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de dados de aplicativo

[!UICONTROL O ] aplicativo é um tipo de dados padrão do Modelo de Dados de Experiência (XDM) que descreve detalhes relacionados às interações geradas pelo aplicativo. Um aplicativo se refere a uma experiência de software, como um aplicativo móvel ou desktop que pode ser instalado, executado, fechado ou desinstalado por um usuário final. As propriedades desse tipo de dados não se destinam a descrever agentes como chatbots, plug-ins baseados em navegador ou outras experiências que não se aplicam aos aplicativos.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Medição]](./measure.md) | Descreve detalhes sobre o término de um aplicativo. |
| `crashes` | [[!UICONTROL Medição]](./measure.md) | Essa propriedade é acionada quando o aplicativo não sai conforme esperado. |
| `featureUsages` | [[!UICONTROL Medição]](./measure.md) | Descreve todos os dados da ativação de um recurso de aplicativo que está sendo medido. |
| `firstLaunches` | [[!UICONTROL Medição]](./measure.md) | Contém dados na primeira inicialização. Essa propriedade é acionada na primeira inicialização após uma instalação. |
| `installs` | [[!UICONTROL Medição]](./measure.md) | Registra a instalação de um aplicativo em um dispositivo quando um evento de instalação específico está disponível. |
| `launches` | [[!UICONTROL Medição]](./measure.md) | Descreve um valor associado à inicialização de um aplicativo. Isso é acionado a cada execução, incluindo falhas, instalações e retomada do plano de fundo quando o tempo limite da sessão é excedido. |
| `upgrades` | [[!UICONTROL Medição]](./measure.md) | Contém dados sobre a atualização de um aplicativo que foi instalado anteriormente. Isso é acionado na primeira inicialização após uma atualização. |
| `id` | String | Um identificador exclusivo para o aplicativo. |
| `name` | String | O nome do aplicativo  |
| `userPerspective` | String | A perspectiva ou a relação física entre o usuário e o aplicativo ou marca no momento em que um evento aconteceu. Compreender a perspectiva do usuário em relação ao aplicativo ajuda a gerar sessões com precisão como a maioria das vezes que você não deseja incluir os eventos `background` e `detached` como parte de uma sessão &quot;ativa&quot;. O valor dessa propriedade deve ser igual a um dos valores de enumeração listados abaixo. <li> `foreground`: O usuário e o aplicativo estão interagindo diretamente entre si. </li> <li> `background`: O aplicativo e o usuário estão interagindo indiretamente. Por exemplo, o aplicativo pode medir um valor e atualizar enquanto a tela está bloqueada ou outro aplicativo está sendo usado em primeiro plano.  </li> <li> `detached`: Desanexado significa que o evento foi relacionado ao aplicativo, mas não veio diretamente do aplicativo, como o envio de um email ou notificação por push de um sistema externo. |
| `version` | String | A versão do aplicativo. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)