---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;aplicativo;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Aplicativo
description: Saiba mais sobre o tipo de dados do Application Experience Data Model (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Tipo de dados [!UICONTROL Aplicativo]

[!UICONTROL Aplicativo] é um tipo de dados padrão do Experience Data Model (XDM) que descreve detalhes relacionados às interações geradas por um aplicativo. Um aplicativo se refere a uma experiência de software, como um aplicativo móvel ou desktop que pode ser instalado, executado, fechado ou desinstalado por um usuário final. As propriedades desse tipo de dados não têm como objetivo descrever agentes como chatbots, plug-ins baseados em navegador ou outras experiências que não se aplicam a aplicativos.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Medida]](./measure.md) | Descreve detalhes sobre o encerramento de um aplicativo. |
| `crashes` | [[!UICONTROL Medida]](./measure.md) | Essa propriedade é acionada quando o aplicativo não sai conforme esperado. |
| `featureUsages` | [[!UICONTROL Medida]](./measure.md) | Descreve quaisquer dados da ativação de um recurso de aplicativo que está sendo medido. |
| `firstLaunches` | [[!UICONTROL Medida]](./measure.md) | Contém dados sobre a primeira inicialização. Essa propriedade é acionada na primeira inicialização após uma instalação. |
| `installs` | [[!UICONTROL Medida]](./measure.md) | Registra a instalação de um aplicativo em um dispositivo quando um evento de instalação específico está disponível. |
| `launches` | [[!UICONTROL Medida]](./measure.md) | Descreve um valor associado à inicialização de um aplicativo. Isso é acionado a cada execução, incluindo travamentos, instalações e retomada de segundo plano quando o tempo limite da sessão é excedido. |
| `upgrades` | [[!UICONTROL Medida]](./measure.md) | Contém dados sobre a atualização de um aplicativo previamente instalado. Isso é acionado na primeira inicialização após uma atualização. |
| `id` | String | Um identificador exclusivo do aplicativo. |
| `name` | String | O nome do aplicativo. |
| `userPerspective` | String | A perspectiva ou o relacionamento físico entre o usuário e o aplicativo ou marca no momento em que um evento aconteceu. Compreender a perspectiva do usuário em relação ao aplicativo ajuda a gerar sessões com precisão, pois na maioria das vezes você não desejará incluir eventos do `background` e do `detached` como parte de uma sessão &quot;ativa&quot;. O valor dessa propriedade deve ser igual a um dos valores de enumeração listados abaixo. <li> `foreground`: o usuário e o aplicativo estão interagindo diretamente um com o outro. </li> <li> `background`: o aplicativo e o usuário estão interagindo indiretamente. Por exemplo, o aplicativo pode medir um valor e atualizar enquanto a tela está bloqueada ou outro aplicativo está sendo usado em primeiro plano.  </li> <li> `detached`: Desanexado significa que o evento estava relacionado ao aplicativo, mas não veio diretamente do aplicativo, como o envio de um email ou notificação por push de um sistema externo. |
| `version` | String | A versão do aplicativo. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
