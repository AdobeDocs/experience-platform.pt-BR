---
title: Configuração de extensão
description: Saiba como configurar uma extensão de tag para coletar configurações globais de um usuário na interface do usuário da Coleta de dados do Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 70%

---

# Configuração de extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A configuração de extensão é a maneira pela qual uma extensão coleta configurações globais de um usuário. Por exemplo, considere uma extensão que permita ao usuário enviar um beacon usando uma ação Enviar beacon, e o beacon sempre deva conter uma ID de conta. Não queremos causar problemas aos usuários solicitando-lhes a ID da conta sempre que configurarem uma ação Enviar beacon. Em vez disso, a extensão deve solicitar a ID da conta uma vez na visualização de configuração da extensão. Sempre que um beacon é enviado, o módulo da biblioteca de ação Enviar beacon pode obter a ID da conta por meio da configuração de extensão e adicioná-la ao beacon.

Quando os usuários instalam uma extensão em uma propriedade de tag no Adobe Experience Platform, eles são mostrados na exibição de configuração de extensão que sua extensão fornecerá. Não é possível concluir a instalação da extensão sem concluir a configuração dela. Consulte o documento sobre [visualizações](./web/views.md) para saber como criar uma visualização para configuração de extensão.

Depois que as configurações forem salvas de uma visualização de configuração de extensão, elas serão emitidas na biblioteca de tempo de execução de tags. Em seguida, você pode acessar essas configurações dos módulos de biblioteca de extensão chamando [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

A configuração de extensão é um recurso opcional que você pode não utilizar.
