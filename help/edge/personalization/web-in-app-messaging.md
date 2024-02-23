---
title: Configurar o suporte a mensagens no aplicativo da Web no SDK da Web
description: Saiba como configurar a extensão de tag do SDK da Web para oferecer suporte a mensagens no aplicativo da Web.
source-git-commit: a020f880be2606024c6a986dc468d70a2fbdc30f
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Configurar o suporte a mensagens no aplicativo da Web no SDK da Web


As mensagens no aplicativo são notificações que podem ser enviadas aos usuários no aplicativo web, guiando-os a pontos de interesse específicos.

É possível usar essas notificações para diferentes propósitos, como promover novos recursos, apresentar ofertas especiais ou facilitar a integração do usuário.

Ao usar mensagens no aplicativo, você pode se envolver efetivamente com seu público-alvo e orientá-los para aspectos importantes de seu aplicativo.

>[!IMPORTANT]
>
>As mensagens no aplicativo da Web são um [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) que usa o SDK da Web para fornecer o conteúdo personalizado.
>
>Para obter instruções detalhadas sobre como configurar a campanha de mensagens no aplicativo da Web, consulte [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Pré-requisitos {#prerequisites}

### Versão da extensão de tag do SDK da Web {#extension-version}

A funcionalidade de mensagens no aplicativo da Web exige a versão mais recente da extensão de tag do SDK da Web.

### Configurar uma CSP para mensagens no aplicativo da Web {#csp}

Ao configurar [Mensagens no aplicativo da Web](../personalization/web-in-app-messaging.md), você deve incluir a seguinte diretiva na CSP:

```
default-src  blob:;
```

Para obter mais informações sobre como configurar uma CSP, consulte [documentação dedicada](../fundamentals/configuring-a-csp.md).

## Configurar mensagens no aplicativo da Web usando a extensão de tag SDK da Web {#tag-extension}

Consulte a [Página de configuração da extensão de tag do SDK da Web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para saber onde encontrar as configurações descritas abaixo.

Depois de ter [instalado](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) Na extensão de tag do SDK da Web, siga as etapas abaixo para configurar a extensão para Mensagens no aplicativo da Web.

No **[!UICONTROL Personalização]** , verifique a **[!UICONTROL Habilitar armazenamento de personalização]** opção. Essa opção permite que o SDK da Web acompanhe quais experiências foram vistas pelo usuário em carregamentos de página.

![Imagem mostrando a opção de armazenamento de personalização na página de configuração da extensão de tag.](assets/web-in-app-messaging/enable-personalization-storage.png)


As mensagens no aplicativo da Web são compatíveis com dois tipos de acionadores:

* [Envio de dados para a Platform](#send-data-platform)
* [Acionamento manual das mensagens](#manual-trigger)

Consulte as seguintes seções para configurar a extensão de tag do SDK da Web de acordo com os acionadores que deseja usar.

### Etapas de configuração para o **[!UICONTROL Enviar dados para a Platform]** acionador {#send-data-platform}

Selecione a propriedade da tag que contém a extensão SDK da Web e [criar uma nova regra](../../tags/ui/managing-resources/rules.md##create-a-rule) com as seguintes configurações:

1. **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
2. **[!UICONTROL Tipo de evento]**: [!UICONTROL Biblioteca carregada (início da página)]

   ![Imagem mostrando a tela de configuração do evento.](assets/web-in-app-messaging/rule-configuration.png)

3. Selecionar **[!UICONTROL Manter alterações]** para salvar a configuração do evento.

Em seguida, você deve adicionar uma ação à regra criada.

1. No [!DNL Actions] , selecione **[!UICONTROL Adicionar]**.
   ![Imagem mostrando a tela de edição de regra.](assets/web-in-app-messaging/add-action.png)

2. Use o seguinte **[!UICONTROL Ação]** configurações:
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Enviar evento]

     ![Imagem mostrando a tela de configuração de ação.](assets/web-in-app-messaging/action-configuration.png)

3. No lado direito da tela, na guia **[!UICONTROL Personalização]** habilite a opção **[!UICONTROL Renderizar decisões de personalização visual]** opção.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/render-visual-personalization.png)

4. No lado direito da tela, na guia **[!UICONTROL Contexto de decisão]** defina o **[!UICONTROL Chave]**/**[!UICONTROL Valor]** pares que você usou na configuração do campaign para se qualificar para a mensagem no aplicativo.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/decision-context.png)

5. Selecionar **[!UICONTROL Manter alterações]** para salvar sua configuração.


Em seguida, você deve adicionar a regra recém-criada à biblioteca de propriedades da tag. Para fazer isso, acesse **[!UICONTROL Fluxo de publicação]** e selecione a regra criada anteriormente.

![Imagem mostrando a tela da biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Após adicionar a regra à biblioteca, selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/publish-flow.png)

O processo de configuração agora está concluído e sua mensagem está pronta para ser exibida aos usuários.

### Etapas de configuração para usar acionadores manuais {#manual-trigger}

Selecione a propriedade da tag que contém a extensão SDK da Web e [criar uma nova regra](../../tags/ui/managing-resources/rules.md##create-a-rule) com as seguintes configurações:

1. **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
2. **[!UICONTROL Tipo de evento]**: [!UICONTROL Clique em]
3. Defina o acionador de um elemento específico na página, identificador por um seletor de CSS de sua escolha.

   ![Imagem mostrando a tela de configuração do evento.](assets/web-in-app-messaging/event-configuration-manual.png)


Em seguida, você deve adicionar uma ação à regra criada.

1. No [!DNL Actions] , selecione **[!UICONTROL Adicionar]**.
   ![Imagem mostrando a tela de edição de regra.](assets/web-in-app-messaging/add-action.png)

2. Use o seguinte **[!UICONTROL Ação]** configurações:
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Avaliar conjuntos de regras]

     ![Imagem mostrando a tela de configuração de ação.](assets/web-in-app-messaging/manual-trigger-action.png)

3. No lado direito da tela, ative a opção **[!UICONTROL Renderizar decisões de personalização visual]** opção.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/manual-trigger-render.png)


4. No lado direito da tela, na guia **[!UICONTROL Contexto de decisão]** defina o **[!UICONTROL Chave]**/**[!UICONTROL Valor]** pares que você usou na configuração do campaign para se qualificar para a mensagem no aplicativo.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Selecionar **[!UICONTROL Manter alterações]** para salvar sua configuração.

Em seguida, você deve adicionar a regra recém-criada à biblioteca de propriedades da tag. Para fazer isso, acesse **[!UICONTROL Fluxo de publicação]** e selecione a regra criada anteriormente.

![Imagem mostrando a tela da biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Após adicionar a regra à biblioteca, selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/publish-flow.png)

O processo de configuração agora está concluído e sua mensagem está pronta para ser exibida aos usuários.

## Configurar mensagens no aplicativo da Web usando a biblioteca JavaScript do SDK da Web {#js-library}

Como alternativa ao uso da extensão de tag SDK da Web, você também pode configurar mensagens no aplicativo da Web diretamente da biblioteca JavaScript do SDK da Web.



Você pode exibir mensagens no aplicativo da Web do Adobe Journey Optimizer de duas maneiras.

### Método 1: buscar automaticamente o conteúdo de personalização {#automatic}

Para que o SDK da Web busque automaticamente o conteúdo de personalização no carregamento da página, use o `sendEvent` conforme mostrado no exemplo abaixo.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Método 2: buscar manualmente o conteúdo de personalização com base na ação do usuário {#manual}

Para mostrar o conteúdo de personalização somente depois que o usuário executar uma ação específica, use o `evaluateRulesets` conforme mostrado no exemplo abaixo.

Neste exemplo, o conteúdo de personalização é exibido quando um usuário clica em **[!UICONTROL Comprar agora]** no seu site.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Configurar armazenamento de personalização {#personalization-storage}

Você pode optar por mostrar mensagens no aplicativo aos usuários por um número definido de vezes, ou sempre que eles visitarem uma página, por meio do `personalizationStorageEnabled` opção de configuração.

No [Configuração do SDK da Web](../fundamentals/configuring-the-sdk.md) defina o `personalizationStorageEnabled` de acordo com suas necessidades:

* `personalizationStorageEnabled: true` aciona a mensagem no aplicativo com a frequência definida na variável [Campanha do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` aciona a mensagem no aplicativo em cada carregamento de página.