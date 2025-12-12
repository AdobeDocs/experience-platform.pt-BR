---
title: Configuração de extensão
description: Saiba como configurar uma extensão de tag para coletar configurações globais de um usuário na interface do usuário do Adobe Experience Platform ou na interface da coleção de dados.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 89%

---

# Configuração de extensão

A configuração de extensão é a maneira pela qual uma extensão coleta configurações globais de um usuário. Por exemplo, considere uma extensão que permita ao usuário enviar um beacon usando uma ação Enviar beacon, e o beacon sempre deva conter uma ID de conta. Não queremos causar problemas aos usuários solicitando-lhes a ID da conta sempre que configurarem uma ação Enviar beacon. Em vez disso, a extensão deve solicitar a ID da conta uma vez na visualização de configuração da extensão. Sempre que um beacon é enviado, o módulo da biblioteca de ação Enviar beacon pode obter a ID da conta por meio da configuração de extensão e adicioná-la ao beacon.

Quando os usuários instalarem uma extensão para uma propriedade de tag na Adobe Experience Platform, será exibida a visualização de configuração de extensão fornecida pela sua extensão. Não é possível concluir a instalação da extensão sem concluir a configuração dela. Consulte o documento sobre [visualizações](./web/views.md) para saber como criar uma visualização para configuração de extensão.

Depois que as configurações de uma visualização de configuração de extensão forem salvas, elas serão emitidas na biblioteca de tempo de execução de tag. Em seguida, você pode acessar essas configurações dos módulos de biblioteca de extensão chamando [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

A configuração de extensão é um recurso opcional que você pode não utilizar.
