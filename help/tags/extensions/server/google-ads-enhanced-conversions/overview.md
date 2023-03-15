---
title: Extensão de conversões aprimoradas do Google Ads
description: Saiba mais sobre a extensão de conversões aprimoradas do Google Ads para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] Extensão de conversões aprimoradas

Usar o [!DNL Google Ads] , você pode aproveitar [conversões aprimoradas](https://support.google.com/google-ads/answer/9888656) enviando dados de clientes primários na forma de ajustes de conversão. O Google usa esses dados adicionais para melhorar os relatórios de suas conversões online orientadas por interações de anúncio.

A variável [[!DNL Google Ads] Extensão de encaminhamento de eventos de conversões aprimoradas](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (a seguir designada por [!DNL Enhanced Conversions] extensão) fornece um modelo amigável para implementar facilmente conversões aprimoradas no [!DNL Google Ads] API.

>[!IMPORTANT]
>
>As conversões aprimoradas só funcionam para tipos de conversão nos quais há dados do cliente, como assinaturas, inscrições e compras. Um ou mais dos seguintes dados do cliente devem estar disponíveis, pois são necessários quando [configurar uma ação de conversão](#conversion-action-event-forwarding) para uma regra de encaminhamento de eventos:
>
>* Endereço de email (preferencial)
>* Nome e endereço residencial (rua, cidade, estado/região e CEP)
>* Número de telefone (deve ser fornecido juntamente com uma das outras duas informações acima)


## Visão geral da implementação

As conversões aprimoradas usam o [!DNL Google Ads] API para adicionar dados primários a uma conversão que ocorreu em um dispositivo cliente, geralmente um site. Isso significa que há duas etapas para implementar conversões aprimoradas:

1. Envie uma conversão do cliente.
1. Use o encaminhamento de eventos para enviar dados primários adicionais que aprimoram os dados de conversão enviados do cliente.

>[!TIP]
>
>Para associar o evento de conversão do lado do cliente aos dados primários enviados do encaminhamento de eventos, a variável `transaction_ID` deve ser o mesmo em ambas as chamadas. Para obter mais informações sobre onde esse valor deve ser fornecido para cada serviço, consulte as seções sobre configuração de ações de conversão para [tags](#conversion-action-tags) e [encaminhamento de eventos](#conversion-action-event-forwarding), respectivamente.

Como o envio de eventos de conversão envolve uma implementação no lado do cliente e no lado do servidor, este documento aborda as etapas de pré-requisito para a configuração do lado do cliente [[!DNL Google Global Site Tag] Extensão (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) além do [!DNL Enhanced Conversions] extensão para encaminhamento de eventos.

O vídeo a seguir apresenta uma introdução à [!DNL Enhanced Conversions] extensão e aborda as etapas de implementação em alto nível:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Enviar uma conversão usando tags

Para enviar um evento de conversão do em um site, [!DNL Google Global Site Tag] (gtag) deve ser implantado. Você pode fazer isso usando tags, configurando e instalando o [!DNL Google Global Site Tag] extensão (gtag).

### Configure e instale o [!DNL Google Global Site Tag] extensão

Navegue até a [!UICONTROL Coleta de dados] ou Experience Platform e selecione **[!UICONTROL Tags]** no painel de navegação esquerdo. Selecione a propriedade da tag na qual você deseja instalar a extensão e selecione **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** localize o [!UICONTROL Tag do site global da Google (gtag)] e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Tag do site global da Google (gtag)] extensão que está sendo selecionada no [!UICONTROL Extensões] exibir no [!UICONTROL Coleta de dados] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

A caixa de diálogo de instalação é exibida. Aqui, selecione **[!UICONTROL Adicionar conta]** e forneça os seguintes valores quando solicitado:

| Propriedade da conta | Descrição |
| --- | --- |
| Nome da conta | Nome exclusivo da conta. Esse nome só é usado na interface do usuário de tags. |
| ID da Conta | Seu [!DNL Google Ads] ID da conta. Para encontrar esse valor, faça logon no [!DNL Google Ads] e navegue até: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. A cadeia de caracteres da ID da conta pode ser encontrada na janela de trecho de código que começa com `AW-` ou `d`. |
| Produto | Selecionar **[!UICONTROL Anúncios do Google (AdWords)]**. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Adicionar conta]** e selecione **[!UICONTROL Salvar]**.

### Adicionar uma ação de conversão de envio {#conversion-action-tags}

Depois de instalar a extensão, você pode começar a incluir ações de conversão nas regras de tag. Ao criar ou editar uma regra que ouça a conversão que você deseja aprimorar, selecione **[!UICONTROL Adicionar]** em [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Tag do site global da Google (gtag)]** do [!UICONTROL Extensão] e selecione **[!UICONTROL Enviar um evento]** em [!UICONTROL Tipo de ação].

![A variável [!UICONTROL Enviar um evento] tipo de ação que está sendo selecionado na visualização configuração de ação do fluxo de trabalho de edição de regras.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Controles adicionais são exibidos para permitir a configuração do [!DNL gtag] evento. No mínimo, os seguintes campos devem ser preenchidos:

1. **[!UICONTROL Nome do evento (Ação)]**: Enter `conversion` como o valor.
1. Adicionar um novo campo onde a chave está `transaction_id` e o valor é um [elemento de dados](../../../ui/managing-resources/data-elements.md) que contém o [ID da transação](https://support.google.com/google-ads/answer/6386790) valor.
1. **[!UICONTROL Rótulo de conversão]**: insira o rótulo de conversão apropriado em [!DNL Google Ads] conta. Para encontrar esse valor, faça logon no Google Ads e navegue até **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. O rótulo da conversão pode ser encontrado em [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Enquanto estiver na área de configuração de tag do seu [!DNL Google Ads] conta, verifique se as conversões aprimoradas estão ativadas. Para fazer isso, revise e aceite os Termos de serviço e selecione **[!DNL Turn on enhanced conversions]** e **[!DNL API]** como o método de implementação.

Depois de configurar a ação, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique uma nova [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Enviar dados primários usando o encaminhamento de eventos

Depois de enviar eventos de conversão pelo lado do cliente, você pode aprimorar essas conversões usando o [!DNL Enhanced Conversions] extensão de encaminhamento de eventos.

### Criar um segredo e um elemento de dados OAuth 2 do Google {#create-secret-data-element}

Antes de configurar a extensão, você deve criar um token de acesso no encaminhamento de eventos para autenticar no [!DNL Google Ads] API.

Consulte o guia sobre [criação de segredos do encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) para obter etapas detalhadas. Certifique-se de selecionar **[!UICONTROL Google OAuth 2]** como o tipo secreto. Continue a seguir as instruções e, quando solicitado a selecionar um perfil de conta do Google, selecione a conta que tem acesso à ação de conversão que você está configurando.

Depois que o segredo é criado, [criar um novo elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) e selecione **[!UICONTROL Segredo]** para o tipo de elemento de dados. Selecione o segredo do Google OAuth 2 apropriado para cada ambiente e selecione **[!UICONTROL Salvar na biblioteca]**.

### Configure e instale o [!DNL Enhanced Conversions] extensão {#install-enhanced-conversions}

Localize o [!UICONTROL Conversões aprimoradas do Google Ads] no catálogo de encaminhamento de eventos e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Conversões aprimoradas do Google Ads] extensão que está sendo selecionada no [!UICONTROL Extensões] exibir no [!UICONTROL Coleta de dados] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar a extensão, você deve preencher os dois campos obrigatórios:

1. **[!UICONTROL ID do cliente]**: a ID que identifica exclusivamente o [!DNL Google Ads] conta. Para encontrar esse valor, faça logon no [!DNL Google Ads] e navegue até **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento de dados do token de acesso]**: Selecione o ícone do elemento de dados (![Ícone do elemento de dados](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) e escolha o elemento de dados secreto do Google OAuth 2 que você [configurado na etapa anterior](#create-secret-data-element) no menu.

Quando terminar, selecione **[!UICONTROL Salvar]** para instalar a extensão.

### Adicionar um [!UICONTROL Enviar conversão] ação para uma regra {#conversion-action-event-forwarding}

Depois que a extensão for instalada, você poderá começar a incluir [!UICONTROL Enviar conversão] nas regras de encaminhamento de eventos. Ao criar ou editar uma regra que ouça a conversão que você deseja aprimorar, selecione **[!UICONTROL Adicionar]** em [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Conversões aprimoradas do Google Ads]** do [!UICONTROL Extensão] e selecione **[!UICONTROL Enviar conversão]** em [!UICONTROL Tipo de ação].

![A variável [!UICONTROL Enviar conversão] tipo de ação que está sendo selecionado na visualização configuração de ação do fluxo de trabalho de edição de regras.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Novos controles são exibidos no painel direito que permitem configurar a conversão. No mínimo, os seguintes campos devem ser preenchidos:

**Informações de conversão**

| Entrada | Descrição |
| --- | --- |
| Customer ID | Seu [!DNL Google Ads] ID do cliente. Assume como padrão a ID do cliente que você informou quando [instalação da extensão](#install-enhanced-conversions). |
| ID de conversão ou rótulo de conversão | Valores de rastreamento obtidos de [!DNL Google Ads] ao configurar o rastreamento de conversão. Valores que começam com `AW-`.<br><br>Para obter detalhes sobre como encontrar esses valores, consulte o [[!DNL Google Ads] documentação](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID da transação | Selecione um elemento de dados que tenha o mesmo valor de ID de transação que seja [enviado do lado do cliente](#conversion-action-tags) usando o [!DNL Google Global Site Tag] extensão. |

**Identificação do usuário**

* Pelo menos um dos três identificadores de usuário deve ser incluído:
   * Email
   * Número de telefone
   * Endereço completo

>[!TIP]
>
>Os dados de identificação do usuário devem ser transformados em hash antes de serem enviados para o Google. Se os dados não tiverem hash quando o encaminhamento de eventos os receber, selecione a variável **[!UICONTROL Normalizar &amp; hash]** alterne em um determinado campo para instruir a extensão a emitir o hash do valor.
>
>![A variável [!UICONTROL Normalizar &amp; hash] alternância ativada para o [!UICONTROL E-mail] entrada dentro do [!UICONTROL Enviar conversão] formulário de configuração de ação.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar eventos de conversão para o [!DNL Google Ads] usando o [!DNL Enhanced Conversions] extensão de encaminhamento de eventos. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
