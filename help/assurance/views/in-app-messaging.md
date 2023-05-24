---
title: Exibição de mensagens no aplicativo
description: Este guia detalha informações sobre a exibição de Mensagens no aplicativo no Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Exibição de mensagens no aplicativo no Assurance

A exibição de Mensagens no aplicativo no Adobe Experience Platform Assurance permite validar o aplicativo, monitorar as mensagens no aplicativo entregues ao dispositivo e simular mensagens no dispositivo.

## Mensagens no dispositivo

Na parte superior do **[!UICONTROL Mensagens no dispositivo]** é uma **[!UICONTROL Mensagem]** lista suspensa. Isso incluirá todas as mensagens recebidas na sessão de garantia. Se uma mensagem não estiver nessa lista, significa que o aplicativo nunca a recebeu.

![Mensagem](./images/in-app-messaging/message.png)

Selecionar uma mensagem mostrará muitas informações sobre ela, conforme descrito nas seções abaixo.

### Visualização da mensagem

No painel direito, há uma **[!UICONTROL Visualização da mensagem]** que mostra uma pré-visualização da mensagem. Selecionar **[!UICONTROL Simular no dispositivo]** enviará essa mensagem para todos os dispositivos que estão conectados à sessão no momento.

![Visualização](./images/in-app-messaging/preview.png)

### Comportamento da mensagem

Abaixo do **[!UICONTROL Visualização da mensagem]** painel é o **[!UICONTROL Comportamento da mensagem]** guia. Isso tem todos os detalhes sobre como a mensagem é exibida. Essas informações incluem informações de posicionamento, animações, gestos de deslizar e configurações de aparência.

![Comportamento](./images/in-app-messaging/gestures.png)

### Guia Informações

Na seção à esquerda, há quatro guias que mostram detalhes sobre a mensagem. A variável **[!UICONTROL Informações]** A guia mostra informações carregadas do Adobe Journey Optimizer (AJO) sobre a campanha de mensagem.

Também é possível selecionar **[!UICONTROL Exibir campanha]** para abrir a mensagem no AJO para inspeção ou edição.

![Info](./images/in-app-messaging/info.png)

### Guia Regras

A variável **[!UICONTROL Regras]** mostra o que precisa acontecer para que esta mensagem seja exibida. Isso fornece insight sobre exatamente o que acionará a exibição de uma mensagem. Neste exemplo:

![Regras](./images/in-app-messaging/rules.png)

O exemplo mostra três condições diferentes para a regra. Se você selecionar um evento (de uma lista de eventos, da guia Analisar ou na linha do tempo), esse evento será avaliado em relação a essas regras. Se o evento corresponder a uma condição, ele mostrará uma marca de seleção verde:

![Correspondência de regra](./images/in-app-messaging/rule-match.png)

Se o evento não corresponder, ele mostrará um ícone vermelho:

![Incompatibilidade de regras](./images/in-app-messaging/rule-mismatch.png)

Se todas as três condições corresponderem ao evento atual, a mensagem será exibida.

### Guia Analisar

A variável **[!UICONTROL Analisar]** A guia fornece insights adicionais sobre as regras. Aqui, filtramos cada evento na sessão com base na proximidade entre a regra de mensagem e o evento.

![Analisar](./images/in-app-messaging/analyze.png)

No exemplo em **[!UICONTROL Guia Regras]** há três condições na regra. Esta guia mostra a porcentagem de correspondência de cada evento da regra. A maioria dos eventos corresponde a 33% (uma das três condições) e o restante corresponde a 100%.

Como resultado, você pode encontrar eventos que estão próximos de corresponder, mas que não correspondem totalmente à regra.

![Limite](./images/in-app-messaging/threshold.png)

A variável **[!UICONTROL Limite de correspondência]** permite filtrar quais eventos devem ser exibidos. Por exemplo, isso pode ser definido como 50% - 90% para obter uma lista de eventos que correspondem exatamente a duas das três condições.

### Guia Interações

A variável **[!UICONTROL Interações]** A guia mostra uma lista de eventos de interação que foram enviados ao Edge para fins de rastreamento.

![Interações](./images/in-app-messaging/interactions.png)

Geralmente, há quatro eventos de interação sempre que uma mensagem é exibida:

```
trigger > display > interact > dismiss
```

A interação &quot;interagir&quot; tem um valor &quot;action&quot; adicional associado a ela. Os valores possíveis incluem &quot;clicado&quot; ou &quot;cancelar&quot;.

A coluna de validação mostra se o evento de interação foi recebido e processado corretamente pelo Edge.

## Validação

A variável **[!UICONTROL Validação]** A guia executa validações em relação à sessão atual, verificando se o aplicativo foi configurado corretamente para Mensagens no aplicativo:

![Validação](./images/in-app-messaging/validation.png)

Se algum erro for encontrado, os detalhes sobre como corrigi-los serão fornecidos.

## Lista de Eventos

![Validação](./images/in-app-messaging/event-list.png)

A variável **[!UICONTROL Lista de Eventos]** A guia fornece uma olhada rápida em todos os eventos na sessão do Assurance relacionados às Mensagens no aplicativo. Alguns dos eventos que você pode ver aqui são:

* Solicitações e respostas para recuperar mensagens
* Exibir eventos de mensagem
* Eventos de rastreamento de interação

Nesta visualização, você pode usar muitos dos recursos padrão da lista de eventos, incluindo a aplicação de pesquisas, a aplicação de filtros, a adição ou remoção de colunas e a exportação de dados.

Selecione um evento para exibir os detalhes brutos do evento no painel direito.

No painel de detalhes direito, o evento selecionado pode ser sinalizado, o que é útil para marcar algo que deve ser revisado por outra pessoa.
