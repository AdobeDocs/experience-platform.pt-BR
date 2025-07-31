---
title: Configurar o suporte a mensagens no aplicativo da Web no Web SDK
description: Saiba como configurar a extensão de tag do Web SDK para oferecer suporte a mensagens no aplicativo da Web.
exl-id: 90a19ef4-e94c-4f16-a26a-8919ad2dbd6f
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# Configurar o suporte a mensagens no aplicativo da Web no Web SDK

As mensagens no aplicativo são notificações que podem ser enviadas aos usuários no aplicativo web, guiando-os a pontos de interesse específicos.

É possível usar essas notificações para diferentes propósitos, como promover novos recursos, apresentar ofertas especiais ou facilitar a integração do usuário.

Ao usar mensagens no aplicativo, você pode se envolver efetivamente com seu público-alvo e orientá-los para aspectos importantes de seu aplicativo.

>[!IMPORTANT]
>
>As Mensagens no Aplicativo Web são um recurso do [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR), que usa o Web SDK para fornecer o conteúdo personalizado.
>
>Para obter instruções detalhadas sobre como configurar a campanha de Mensagens no Aplicativo da Web, consulte a [documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html?lang=pt-BR).


## Pré-requisitos {#prerequisites}

### Versão da extensão de tag do Web SDK {#extension-version}

A funcionalidade de mensagens no aplicativo da Web exige a versão mais recente da extensão de tag do Web SDK.

### Configurar uma CSP para mensagens no aplicativo da Web {#csp}

Ao configurar [Mensagens no aplicativo da Web](../personalization/web-in-app-messaging.md), você deve incluir a seguinte diretiva na CSP:

```
default-src  blob:;
```

Para obter mais informações sobre como configurar uma CSP, consulte a [documentação dedicada](../use-cases/configuring-a-csp.md).

## Configurar mensagens no aplicativo da Web usando a extensão de tag da Web SDK {#tag-extension}

Consulte a [página de configuração da extensão de tag do Web SDK](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para entender onde você pode encontrar as configurações descritas abaixo.

Depois de [instalar](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) a extensão de tag do Web SDK, siga as etapas abaixo para configurar a extensão para Mensagens no Aplicativo Web.

Na seção **[!UICONTROL Personalization]**, marque a opção **[!UICONTROL Habilitar armazenamento de personalização]**. Essa opção permite que o Web SDK acompanhe quais experiências foram vistas pelo usuário em carregamentos de página.

![Imagem mostrando a opção de armazenamento de personalização na página de configuração de extensão de marca.](assets/web-in-app-messaging/enable-personalization-storage.png)


As mensagens no aplicativo da Web são compatíveis com dois tipos de acionadores:

* [Envio de dados para o Experience Platform](#send-data-platform)
* [Acionamento manual das mensagens](#manual-trigger)

Consulte as seções a seguir para configurar a extensão de tag do Web SDK de acordo com os acionadores que deseja usar.

### Etapas de configuração para o gatilho **[!UICONTROL Enviar dados para a Experience Platform]** {#send-data-platform}

Selecione a propriedade da marca que contém sua extensão do Web SDK e [crie uma nova regra](../../tags/ui/managing-resources/rules.md##create-a-rule) com as seguintes configurações:

1. **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
2. **[!UICONTROL Tipo de Evento]**: [!UICONTROL Biblioteca Carregada (Início da Página)]

   ![Imagem mostrando a tela de configuração do evento.](assets/web-in-app-messaging/rule-configuration.png)

3. Selecione **[!UICONTROL Manter alterações]** para salvar a configuração do evento.

Em seguida, você deve adicionar uma ação à regra criada.

1. Na seção [!DNL Actions], selecione **[!UICONTROL Adicionar]**.
   ![Imagem mostrando a tela editar regra.](assets/web-in-app-messaging/add-action.png)

2. Usar as seguintes configurações de **[!UICONTROL Ação]**:
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Enviar evento]

     ![Imagem mostrando a tela de configuração da ação.](assets/web-in-app-messaging/action-configuration.png)

3. No lado direito da tela, na seção **[!UICONTROL Personalization]**, habilite a opção **[!UICONTROL Renderizar decisões de personalização visual]**.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/render-visual-personalization.png)

4. No lado direito da tela, na seção **[!UICONTROL Contexto de decisão]**, defina os pares de **[!UICONTROL Chave]**/**[!UICONTROL Valor]** que você usou na configuração da campanha para se qualificar para a mensagem no aplicativo.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/decision-context.png)

5. Selecione **[!UICONTROL Manter alterações]** para salvar sua configuração.


Em seguida, você deve adicionar a regra recém-criada à biblioteca de propriedades da tag. Para fazer isso, vá para **[!UICONTROL Fluxo de publicação]** e selecione a regra criada anteriormente.

![Imagem mostrando a tela da biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Depois de adicionar a regra à biblioteca, selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/publish-flow.png)

O processo de configuração agora está concluído e sua mensagem está pronta para ser exibida aos usuários.

### Etapas de configuração para usar acionadores manuais {#manual-trigger}

Selecione a propriedade da marca que contém sua extensão do Web SDK e [crie uma nova regra](../../tags/ui/managing-resources/rules.md##create-a-rule) com as seguintes configurações:

1. **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
2. **[!UICONTROL Tipo de Evento]**: [!UICONTROL Clique]
3. Defina o acionador de um elemento específico na página, identificado por um seletor de CSS de sua escolha.

   ![Imagem mostrando a tela de configuração do evento.](assets/web-in-app-messaging/event-configuration-manual.png)


Em seguida, você deve adicionar uma ação à regra criada.

1. Na seção [!DNL Actions], selecione **[!UICONTROL Adicionar]**.
   ![Imagem mostrando a tela editar regra.](assets/web-in-app-messaging/add-action.png)

2. Usar as seguintes configurações de **[!UICONTROL Ação]**:
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Avaliar conjuntos de regras]

     ![Imagem mostrando a tela de configuração da ação.](assets/web-in-app-messaging/manual-trigger-action.png)

3. No lado direito da tela, habilite a opção **[!UICONTROL Renderizar decisões de personalização visual]**.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/manual-trigger-render.png)


4. No lado direito da tela, na seção **[!UICONTROL Contexto de decisão]**, defina os pares de **[!UICONTROL Chave]**/**[!UICONTROL Valor]** que você usou na configuração da campanha para se qualificar para a mensagem no aplicativo.
   ![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Selecione **[!UICONTROL Manter alterações]** para salvar sua configuração.

Em seguida, você deve adicionar a regra recém-criada à biblioteca de propriedades da tag. Para fazer isso, vá para **[!UICONTROL Fluxo de publicação]** e selecione a regra criada anteriormente.

![Imagem mostrando a tela da biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Depois de adicionar a regra à biblioteca, selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

![Imagem mostrando a tela de configuração de personalização.](assets/web-in-app-messaging/publish-flow.png)

O processo de configuração agora está concluído e sua mensagem está pronta para ser exibida aos usuários.

## Configurar mensagens no aplicativo da Web usando a biblioteca JavaScript do Web SDK {#js-library}

Como alternativa ao uso da extensão de tag do Web SDK, você também pode configurar Mensagens no aplicativo Web diretamente da biblioteca JavaScript do Web SDK.



Você pode exibir mensagens no aplicativo da Web do Adobe Journey Optimizer de duas maneiras.

### Método 1: buscar automaticamente o conteúdo de personalização {#automatic}

Para que o Web SDK busque automaticamente o conteúdo de personalização no carregamento da página, use o comando `sendEvent`, conforme mostrado no exemplo abaixo.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Método 2: buscar manualmente o conteúdo de personalização com base na ação do usuário {#manual}

Para mostrar o conteúdo de personalização somente depois que o usuário executar uma ação específica, use o comando `evaluateRulesets` como mostrado no exemplo abaixo.

Neste exemplo, o conteúdo de personalização é exibido quando um usuário clica no botão **[!UICONTROL Comprar agora]** no seu site.

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

Você pode optar por mostrar mensagens no aplicativo aos usuários por um número definido de vezes, ou sempre que eles visitarem uma página, por meio da opção de configuração `personalizationStorageEnabled`.

Na [configuração do Web SDK](../commands/configure/overview.md), defina a opção `personalizationStorageEnabled` de acordo com suas necessidades:

* `personalizationStorageEnabled: true` aciona a mensagem no aplicativo com a frequência que você definiu na [campanha do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html?lang=pt-BR#configure-inapp).
* `personalizationStorageEnabled: false` aciona a mensagem no aplicativo em cada carregamento de página.
