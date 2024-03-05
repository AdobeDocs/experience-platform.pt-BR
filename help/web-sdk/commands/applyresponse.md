---
title: applyResponse
description: Use uma resposta da Rede de borda para inicializar o SDK da Web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

A variável `applyResponse` permite executar várias ações com base em uma resposta da Edge Network. Normalmente, ele é usado em implantações híbridas, nas quais o servidor faz uma chamada inicial para a Rede de borda. Esse comando recebe a resposta dessa chamada e inicializa o SDK da Web no navegador.

## Aplicar resposta usando a extensão de tag do SDK da Web

A aplicação de respostas é executada como uma ação em uma regra na interface das tags da Coleção de dados da Adobe Experience Platform.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Aplicar resposta]**.
1. Defina os campos desejados à direita.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Aplicar resposta usando a biblioteca JavaScript do SDK da Web

Execute o `applyResponse` ao chamar a instância configurada do SDK da Web. O objeto que contém opções de configuração é compatível com os seguintes campos:

* **`renderDecisions`**: um booleano que força o SDK da Web a renderizar qualquer conteúdo personalizado que esteja qualificado para renderização automática. Idêntico a [`renderDecisions`](sendevent/renderdecisions.md) no [`sendEvent`](sendevent/overview.md) comando.
* **`responseHeaders`**: um mapa de nomes de cabeçalho de string para valores de cabeçalho de string.
* **`responseBody`**: Obrigatório. Um corpo de resposta JSON da chamada do servidor para a Rede de borda.
* **`personalization.sendDisplayEvent`**: um booleano que opera de forma idêntica a [`personalization.sendDisplayEvent`](sendevent/personalization.md) no `sendEvent` comando.

```js
allow("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objeto de resposta

Se você decidir [lidar com respostas](command-responses.md) com esse comando, as seguintes propriedades estão disponíveis no objeto de resposta:

* **`propositions`**: uma matriz de propostas retornadas pela Rede de borda. As apresentações renderizadas automaticamente incluem o sinalizador `renderAttempted` definir como `true`.
* **`inferences`**: uma matriz de objetos de inferência, que contém informações de aprendizado de máquina sobre este usuário.
* **`destinations`**: uma matriz de objetos de destino retornados pela Rede de borda.
