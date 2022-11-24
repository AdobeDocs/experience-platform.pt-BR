---
title: Extensão de conversões aprimoradas do Google Ads
description: Saiba mais sobre a extensão Conversões aprimoradas do Google Ads para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 1%

---

# [!DNL Google Ads] Extensão de Conversões Avançadas

Usar o [!DNL Google Ads] API, você pode aproveitar [conversões aprimoradas](https://support.google.com/google-ads/answer/9888656) enviando dados primários do cliente na forma de ajustes de conversão. O Google usa esses dados adicionais para melhorar o relatório de suas conversões online orientadas por interações de anúncios.

O [[!DNL Google Ads] Extensão de encaminhamento de eventos de Conversões aprimoradas](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (a seguir designada por [!DNL Enhanced Conversions] extensão) fornece um modelo simples para implementar facilmente conversões aprimoradas para a [!DNL Google Ads] API.

>[!IMPORTANT]
>
>As conversões aprimoradas só funcionam para tipos de conversão em que os dados do cliente estão presentes, como assinaturas, inscrições e compras. Um ou mais dos seguintes dados do cliente devem estar disponíveis, pois são necessários quando [configuração de uma ação de conversão](#conversion-action-event-forwarding) para uma regra de encaminhamento de evento:
>
>* Endereço de email (preferencial)
>* Nome e endereço residencial (endereço, cidade, estado/região e código postal)
>* Número de telefone (deve ser fornecido além de um dos outros dois elementos de informação acima)


## Visão geral da implementação

As conversões aprimoradas aproveitam o [!DNL Google Ads] API para adicionar dados primários a uma conversão que aconteceu em um dispositivo cliente, geralmente um site. Isso significa que há duas etapas para implementar conversões aprimoradas:

1. Envie uma conversão do cliente.
1. Use o encaminhamento de eventos para enviar dados primários adicionais que melhoram os dados de conversão enviados do cliente.

>[!TIP]
>
>Para associar o evento de conversão do lado do cliente aos dados primários enviados do encaminhamento do evento, a variável `transaction_ID` deve ser o mesmo em ambas as chamadas. Para obter mais informações sobre onde esse valor deve ser fornecido para cada serviço, consulte as seções sobre como configurar ações de conversão para [tags](#conversion-action-tags) e [encaminhamento de eventos](#conversion-action-event-forwarding), respectivamente.

Como o envio de eventos de conversão envolve uma implementação do lado do cliente e do lado do servidor, este documento aborda as etapas de pré-requisito para configurar o lado do cliente [[!DNL Google Global Site Tag] extensão (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) além do [!DNL Enhanced Conversions] extensão para encaminhamento de eventos.

O vídeo a seguir apresenta uma introdução ao [!DNL Enhanced Conversions] e analisa as etapas de implementação em um alto nível:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Enviar uma conversão usando tags

Para enviar um evento de conversão de um site, [!DNL Google Global Site Tag] (gtag) deve ser implantada. Você pode fazer isso usando tags configurando e instalando o [!DNL Google Global Site Tag] extensão (gtag).

### Configure e instale o [!DNL Google Global Site Tag] extensão

Navegue até o [!UICONTROL Coleta de dados] Interface do usuário ou Experience Platform e selecione **[!UICONTROL Tags]** no painel de navegação esquerdo. Selecione a propriedade da tag na qual deseja instalar a extensão e selecione **[!UICONTROL Extensões]** no painel de navegação esquerdo. Em **[!UICONTROL Catálogo]** localize a guia [!UICONTROL Tag global do site da Google (gtag)] e selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Tag global do site da Google (gtag)] extensão selecionada na [!UICONTROL Extensões] no [!UICONTROL Coleta de dados] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

A caixa de diálogo de instalação é exibida. Aqui, selecione **[!UICONTROL Adicionar conta]** e forneça os seguintes valores quando solicitado:

| Propriedade da conta | Descrição |
| --- | --- |
| Nome da conta | Um nome exclusivo para a conta. Esse nome é usado somente na interface do usuário de tags. |
| ID da Conta | Seu [!DNL Google Ads] ID da conta. Para localizar esse valor, faça logon em [!DNL Google Ads] e navegue até: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. A string da ID da conta pode ser encontrada na janela do trecho de código que começa com `AW-` ou `d`. |
| Produto | Selecionar **[!UICONTROL Anúncios do Google (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Quando terminar, selecione **[!UICONTROL Adicionar conta]**, em seguida selecione **[!UICONTROL Salvar]**.

### Adicionar uma ação de conversão de envio {#conversion-action-tags}

Depois de instalar a extensão, você pode começar a incluir ações de conversão em suas regras de tags. Ao criar ou editar uma regra que escute a conversão que deseja aprimorar, selecione **[!UICONTROL Adicionar]** under [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Tag global do site da Google (gtag)]** do [!UICONTROL Extensão] lista suspensa e selecione **[!UICONTROL Enviar um evento]** under [!UICONTROL Tipo de ação].

![O [!UICONTROL Enviar um evento] tipo de ação que está sendo selecionado na exibição de configuração de ação do fluxo de trabalho de edição de regras.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Aparecem controles adicionais que permitem configurar a variável [!DNL gtag] evento. No mínimo, os seguintes campos devem ser preenchidos:

1. **[!UICONTROL Nome do evento (Ação)]**: Enter `conversion` como o valor.
1. Adicionar um novo campo onde a chave está `transaction_id` e o valor é um [elemento de dados](../../../ui/managing-resources/data-elements.md) que contém a variável [ID da transação](https://support.google.com/google-ads/answer/6386790) valor.
1. **[!UICONTROL Rótulo de conversão]**: Insira o rótulo de conversão apropriado em seu [!DNL Google Ads] conta. Para encontrar esse valor, faça logon nos Anúncios do Google e navegue até **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. O rótulo de conversão pode ser encontrado em [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Enquanto estiver na área de configuração de tags da [!DNL Google Ads] verifique se as conversões aprimoradas estão ativadas. Para fazer isso, revise e aceite os Termos de serviço e selecione **[!DNL Turn on enhanced conversions]** e **[!DNL API]** como método de implementação.

Após configurar a ação, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique um novo [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Enviar dados primários usando o encaminhamento de eventos

Depois de enviar eventos de conversão do lado do cliente, você pode aprimorar essas conversões usando o [!DNL Enhanced Conversions] extensão de encaminhamento de evento.

### Criar um segredo e um elemento de dados do Google OAuth 2 {#create-secret-data-element}

Antes de configurar a extensão, você deve criar um token de acesso no encaminhamento do evento para autenticar para [!DNL Google Ads] API.

Consulte o guia sobre [criação de segredos de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) para obter etapas detalhadas. Certifique-se de selecionar **[!UICONTROL Google OAuth 2]** como o tipo secreto. Continue a seguir os prompts e, quando solicitado a selecionar um perfil de conta do Google, selecione a conta que tem acesso à ação de conversão que você está configurando.

Depois que o segredo é criado, [criar um novo elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) e selecione **[!UICONTROL Segredo]** para o tipo de elemento de dados. Selecione o segredo Google OAuth 2 apropriado para cada ambiente e selecione **[!UICONTROL Salvar na biblioteca]**.

### Configure e instale o [!DNL Enhanced Conversions] extensão {#install-enhanced-conversions}

Encontre a [!UICONTROL Conversões aprimoradas de anúncios do Google] no catálogo de encaminhamento de eventos e selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Conversões aprimoradas de anúncios do Google] extensão selecionada na [!UICONTROL Extensões] no [!UICONTROL Coleta de dados] IU.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar a extensão, você deve preencher os dois campos obrigatórios:

1. **[!UICONTROL Customer ID]**: A ID que identifica exclusivamente o [!DNL Google Ads] conta. Para localizar esse valor, faça logon em [!DNL Google Ads] e navegue até **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento de dados do token de acesso]**: Selecione o ícone do elemento de dados (![Ícone do elemento de dados](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) e escolha o elemento de dados secreto Google OAuth 2 que você [configurado na etapa anterior](#create-secret-data-element) no menu .

Quando terminar, selecione **[!UICONTROL Salvar]** para instalar a extensão.

### Adicione um [!UICONTROL Enviar conversão] ação para uma regra {#conversion-action-event-forwarding}

Após a instalação da extensão, você pode começar a incluir [!UICONTROL Enviar conversão] nas regras de encaminhamento do evento. Ao criar ou editar uma regra que escute a conversão que você deseja aprimorar, selecione **[!UICONTROL Adicionar]** under [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Conversões aprimoradas de anúncios do Google]** do [!UICONTROL Extensão] lista suspensa e selecione **[!UICONTROL Enviar conversão]** under [!UICONTROL Tipo de ação].

![O [!UICONTROL Enviar conversão] tipo de ação que está sendo selecionado na exibição de configuração de ação do fluxo de trabalho de edição de regras.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Novos controles são exibidos no painel direito, que permite configurar sua conversão. No mínimo, os seguintes campos devem ser preenchidos:

**Informações de conversão**

| Entrada | Descrição |
| --- | --- |
| Customer ID | Seu [!DNL Google Ads] ID do cliente. O padrão é a ID do cliente inserida quando [instalação da extensão](#install-enhanced-conversions). |
| ID de conversão ou rótulo de conversão | Valores de rastreamento obtidos de [!DNL Google Ads] ao configurar o rastreamento de conversão. Os valores começam com `AW-`.<br><br>Para obter detalhes sobre como encontrar esses valores, consulte [[!DNL Google Ads] documentação](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID da transação | Selecione um elemento de dados que tenha o mesmo valor de ID de transação que [enviado do lado do cliente](#conversion-action-tags) usando o [!DNL Google Global Site Tag] extensão. |

**Identificação do usuário**

* Pelo menos um dos três identificadores de usuários deve ser incluído:
   * Email
   * Número de telefone
   * Endereço completo

>[!TIP]
>
>Os dados de identificação do usuário devem ter hash antes de serem enviados ao Google. Se os dados não tiverem hash quando o encaminhamento de eventos os receber, selecione a variável **[!UICONTROL Normalizar &amp; hash]** alterne em um determinado campo para instruir a extensão a hash do valor.
>
>![O [!UICONTROL Normalizar &amp; hash] ativar para a [!UICONTROL Email] entrada dentro do [!UICONTROL Enviar conversão] formulário de configuração de ação.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo encaminhamento de evento [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar eventos de conversão para o [!DNL Google Ads] usando o [!DNL Enhanced Conversions] extensão de encaminhamento de evento. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
