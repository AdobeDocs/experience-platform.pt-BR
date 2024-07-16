---
title: Exibição de mensagens no aplicativo
description: Este manual detalha informações sobre a exibição de mensagens no aplicativo no Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 100%

---

# Exibição de mensagens no aplicativo no Assurance

A exibição de mensagens no aplicativo no Adobe Experience Platform Assurance permite validar o aplicativo, monitorar as mensagens no aplicativo entregues ao seu dispositivo e simular mensagens nele.

## Mensagens no dispositivo

Na parte superior da guia **[!UICONTROL Mensagens no dispositivo]** há uma lista suspensa **[!UICONTROL Mensagem]**. Ela incluirá todas as mensagens recebidas na sessão do Assurance. Se uma mensagem não estiver nessa lista, significa que o aplicativo nunca a recebeu.

![Mensagem](./images/in-app-messaging/message.png)

Selecionar uma mensagem mostrará muitas informações sobre ela, conforme descrito nas seções abaixo.

### Visualização da mensagem

No painel direito, há a janela **[!UICONTROL Visualização da mensagem]** que mostra uma visualização da mensagem. Selecionar **[!UICONTROL Simular no dispositivo]** enviará essa mensagem para todos os dispositivos que estão conectados à sessão no momento.

![Visualização](./images/in-app-messaging/preview.png)

### Comportamento da mensagem

Abaixo da janela **[!UICONTROL Visualização da mensagem]** fica a guia **[!UICONTROL Comportamento da mensagem]**. Aqui estão todos os detalhes sobre como a mensagem é exibida. Essas informações incluem informações de posicionamento, animações, gestos de deslizar na tela e configurações de aparência.

![Comportamento](./images/in-app-messaging/gestures.png)

### Guia Informações

Na seção à esquerda, há quatro guias que mostram detalhes sobre a mensagem. A guia **[!UICONTROL Informações]** mostra informações carregadas do Adobe Journey Optimizer (AJO) sobre a campanha da mensagem.

Também é possível selecionar **[!UICONTROL Exibir campanha]** para abrir a mensagem no AJO para inspeção ou edição.

![Informações](./images/in-app-messaging/info.png)

### Guia Regras

A guia **[!UICONTROL Regras]** mostra o que é necessário para que essa mensagem seja exibida. Ela fornece insight sobre exatamente o que acionará a exibição de uma mensagem. Neste exemplo:

![Regras](./images/in-app-messaging/rules.png)

O exemplo mostra três condições diferentes para a regra. Se você selecionar um evento (de uma lista de eventos, da guia Analisar ou na linha do tempo), ele será avaliado em relação a essas regras. Se o evento corresponder a uma condição, ela mostrará uma marca de seleção verde:

![Regra corresponde](./images/in-app-messaging/rule-match.png)

Se o evento não corresponder, ela mostrará um ícone vermelho:

![Regra não corresponde](./images/in-app-messaging/rule-mismatch.png)

Se todas as três condições corresponderem ao evento atual, a mensagem será exibida.

### Guia Analisar

A guia **[!UICONTROL Analisar]** fornece insights adicionais sobre as regras. Aqui, filtramos cada evento na sessão com base na proximidade entre a regra da mensagem e o evento.

![Analisar](./images/in-app-messaging/analyze.png)

No exemplo da seção da **[!UICONTROL Guia Regras]**, há três condições na regra. Esta guia mostra a porcentagem de correspondência de cada evento com a regra. A maioria dos eventos têm 33% de correspondência (uma das três condições) e o restante têm 100% de correspondência.

Como resultado, é possível encontrar eventos que estão próximos de corresponder, mas que não correspondem totalmente à regra.

![Limite](./images/in-app-messaging/threshold.png)

O controle deslizante **[!UICONTROL Limite de correspondência]** permite filtrar quais eventos devem ser exibidos. Por exemplo, ele pode ser definido para 50% - 90% para obter uma lista de eventos que correspondem exatamente a duas das três condições.

### Guia Interações

A guia **[!UICONTROL Interações]** mostra uma lista de eventos de interação que foram enviados ao Edge para fins de rastreamento.

![Interações](./images/in-app-messaging/interactions.png)

Geralmente, há quatro eventos de interação sempre que uma mensagem é exibida:

```
trigger > display > interact > dismiss
```

A interação “interagir” tem um valor “ação” adicional associado a ela. Os valores possíveis incluem “clicado” ou “cancelar”.

A coluna de validação mostra se o evento de interação foi recebido e processado corretamente pelo Edge.

## Validação

A guia **[!UICONTROL Validação]** executa validações em relação à sessão atual, verificando se o aplicativo foi configurado corretamente para Mensagens no aplicativo:

![Validação](./images/in-app-messaging/validation.png)

Se algum erro for encontrado, os detalhes sobre como corrigi-lo serão fornecidos.

## Lista de eventos

![Validação](./images/in-app-messaging/event-list.png)

A guia **[!UICONTROL Lista de eventos]** fornece uma olhada rápida em todos os eventos na sessão do Assurance relacionados às Mensagens no aplicativo. Alguns dos eventos que podem estar aqui incluem:

* Solicitações para recuperar mensagens e respostas
* Exibir eventos de mensagem
* Eventos de rastreamento de interação

Neste visualização, é possível usar muitos dos recursos padrão da lista de eventos, incluindo pesquisa, a aplicação de filtros, a adição ou remoção de colunas e a exportação de dados.

Selecione um evento para exibir os detalhes brutos do evento no painel direito.

No painel de detalhes direito, o evento selecionado pode ser sinalizado, o que é útil para marcar algo que deve ser revisado por outra pessoa.
