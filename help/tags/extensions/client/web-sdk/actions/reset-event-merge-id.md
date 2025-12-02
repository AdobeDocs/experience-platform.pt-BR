---
title: Redefinir ID de mesclagem
description: Ação obsoleta que permite separar eventos chamados na mesma página.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Redefinir ID de mesclagem

>[!IMPORTANT]
>
>Esta ação está obsoleta. Em vez disso, use as configurações [Coletar cliques internos em links](../configure/data-collection.md#collect-internal-link-clicks).

O tipo de ação **[!UICONTROL Reset merge ID]** permite separar eventos chamados na mesma página. Normalmente, ela é usada em cenários de links internos, nos quais você pode ter várias cargas que deseja enviar para o Adobe. Essa ação permite redefinir a ID de mesclagem de um evento para que ele não seja considerado parte do mesmo evento depois de chegar à Edge Network.

Se quiser controlar como vários eventos na mesma página são separados ou mesclados, use a opção [Coletar cliques internos em links](../configure/data-collection.md#collect-internal-link-clicks) ao configurar a extensão de tag.
