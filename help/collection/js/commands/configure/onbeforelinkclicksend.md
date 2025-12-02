---
title: onBeforeLinkClickSend
description: Retorno de chamada que é executado antes do envio dos dados de rastreamento do link.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Esse retorno de chamada está obsoleto. Em vez disso, use [`clickCollection.filterClickDetails`](clickcollection.md).

O retorno de chamada `onBeforeLinkClickSend` permite registrar uma função JavaScript que pode alterar os dados de rastreamento de link enviados antes que esses dados sejam enviados para a Adobe. Permite manipular o objeto `xdm` ou `data`, incluindo a capacidade de adicionar, editar ou remover elementos. Você também pode cancelar condicionalmente o envio de dados, como com o tráfego de bot do lado do cliente detectado.

Esse retorno de chamada só será executado se [`clickCollectionEnabled`](clickcollectionenabled.md) estiver habilitado e `filterClickDetails` não contiver uma função registrada.

Se [`onBeforeEventSend`](onbeforeeventsend.md) e `onBeforeLinkClickSend` contêm funções registradas, `onBeforeLinkClickSend` é executado primeiro.

>[!WARNING]
>
>Esse retorno de chamada permite o uso do código personalizado. Se qualquer código incluído no retorno de chamada acionar uma exceção não capturada, o processamento do evento será interrompido. Os dados não são enviados para a Adobe.

## `onBeforeLinkClickSend` e `filterClickDetails`

O retorno de chamada [`clickCollection.filterClickDetails`](clickcollection.md) foi criado para substituir `onBeforeLinkClickSend`. A Adobe recomenda não atribuir funções de retorno de chamada a ambos simultaneamente. Se você atribuir uma função de retorno de chamada a `filterClickDetails` e `onBeforeLinkClickSend`, a biblioteca usará a seguinte lógica:

* Apenas `filterClickDetails` é executado; `onBeforeLinkClickSend` não.
* O agrupamento de eventos `clickCollection.eventGroupingEnabled` não funciona.
