---
title: Aplicar resposta
description: Execute uma ação com base em uma resposta do Edge Network.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Aplicar resposta

O tipo de ação **[!UICONTROL Apply response]** permite executar várias ações com base em uma resposta da Edge Network. Normalmente, esse tipo de ação é usado em implantações híbridas em que o servidor faz uma chamada inicial para o Edge Network. Em seguida, esse tipo de ação recebe a resposta dessa chamada e inicializa a Web SDK no navegador. O uso desse tipo de ação pode reduzir os tempos de carregamento do cliente para casos de uso de personalização híbrida.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Apply response]**.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação Aplicar resposta.](../assets/apply-response.png)

## Casos de uso

* **Divisão manual entre coleta e personalização de dados**: você pode acionar uma ação [Enviar evento](send-event.md) com decisões de renderização definidas como `false` e, em seguida, fazer com que uma regra &quot;Enviar evento concluído&quot; capture a promessa. A primeira ação dentro dessa regra pode ser &quot;Aplicar resposta&quot;. Esse fluxo de trabalho permite atrasar a manipulação de DOM até que o código da própria organização conclua outro trabalho.
* **Resposta do Edge recebida de fora da Web SDK**: se você usar outra biblioteca para se comunicar com a Edge Network, poderá permitir que a Web SDK ainda manipule a resposta da Edge Network usando esta ação.

## Campos disponíveis

Esse tipo de ação oferece suporte às seguintes opções de configuração:

* **[!UICONTROL Instance]**: a instância do SDK à qual a ação se aplica. Esse menu suspenso estará desativado se sua implementação usar uma única instância do SDK.
* **[!UICONTROL Response headers]**: Selecione o elemento de dados que retorna um objeto contendo as chaves e os valores do cabeçalho retornados pela chamada de servidor do Edge Network.
* **[!UICONTROL Response body]**: Selecione o elemento de dados que retorna o objeto contendo a carga JSON fornecida pela resposta do Edge Network.
* **[!UICONTROL Render visual personalization decisions]**: Habilite esta opção para renderizar automaticamente o conteúdo de personalização fornecido pelo Edge Network e pré-ocultar o conteúdo para evitar cintilação.
