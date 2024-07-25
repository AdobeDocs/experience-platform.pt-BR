---
title: Extensão de conversões aprimoradas do Google Ads
description: Saiba mais sobre a extensão de conversões aprimoradas do Google Ads para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads] Extensão de conversões aprimoradas

Usando a API [!DNL Google Ads], você pode aproveitar [conversões aprimoradas](https://support.google.com/google-ads/answer/9888656) enviando dados de clientes primários na forma de ajustes de conversão. O Google usa esses dados adicionais para melhorar os relatórios de suas conversões online orientadas por interações de anúncio.

A [[!DNL Google Ads] extensão de encaminhamento de eventos de Conversões Aprimoradas](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (até então referida como a [!DNL Enhanced Conversions] extensão) fornece um modelo amigável para implementar facilmente conversões aprimoradas na API [!DNL Google Ads].

>[!IMPORTANT]
>
>As conversões aprimoradas só funcionam para tipos de conversão nos quais há dados do cliente, como assinaturas, inscrições e compras. Um ou mais dos seguintes dados do cliente devem estar disponíveis, pois são necessários ao [configurar uma ação de conversão](#conversion-action-event-forwarding) para uma regra de encaminhamento de eventos:
>
>* Endereço de email (preferencial)
>* Nome e endereço residencial (rua, cidade, estado/região e CEP)
>* Número de telefone (deve ser fornecido juntamente com uma das outras duas informações acima)

## Visão geral da implementação

As conversões aprimoradas usam a API [!DNL Google Ads] para adicionar dados primários a uma conversão que ocorreu em um dispositivo cliente, geralmente um site. Isso significa que há duas etapas para implementar conversões aprimoradas:

1. Envie uma conversão do cliente.
1. Use o encaminhamento de eventos para enviar dados primários adicionais que aprimoram os dados de conversão enviados do cliente.

>[!TIP]
>
>Para associar o evento de conversão do lado do cliente aos dados primários enviados do encaminhamento de eventos, o `transaction_ID` deve ser o mesmo em ambas as chamadas. Para obter mais informações sobre onde esse valor deve ser fornecido para cada serviço, consulte as seções sobre configuração de ações de conversão para [tags](#conversion-action-tags) e [encaminhamento de eventos](#conversion-action-event-forwarding), respectivamente.

Como o envio de eventos de conversão envolve uma implementação no lado do cliente e no lado do servidor, este documento aborda as etapas de pré-requisito para a configuração da extensão [[!DNL Google Global Site Tag] (gtag) do lado do cliente](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag), além da extensão [!DNL Enhanced Conversions] para encaminhamento de eventos.

O vídeo a seguir fornece uma introdução à extensão [!DNL Enhanced Conversions] e aborda as etapas de implementação em alto nível:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Enviar uma conversão usando tags

Para enviar um evento de conversão de em um site, [!DNL Google Global Site Tag] (gtag) deve ser implantado. Você pode fazer isso usando tags, configurando e instalando a extensão [!DNL Google Global Site Tag] (gtag).

### Configurar e instalar a extensão [!DNL Google Global Site Tag]

Navegue até a [!UICONTROL Interface da Coleção de Dados] ou a interface do Experience Platform e selecione **[!UICONTROL Tags]** na navegação à esquerda. Selecione a propriedade da tag na qual você deseja instalar a extensão e selecione **[!UICONTROL Extensões]** na navegação à esquerda. Na guia **[!UICONTROL Catálogo]**, localize a extensão [!UICONTROL Marca de Site Global da Google (gtag)] e selecione **[!UICONTROL Instalar]**.

![A extensão [!UICONTROL Marca de Site Global (gtag)] da Google sendo selecionada na exibição [!UICONTROL Extensões] da interface de usuário da [!UICONTROL Coleção de Dados].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

A caixa de diálogo de instalação é exibida. Aqui, selecione **[!UICONTROL Adicionar conta]** e forneça os seguintes valores quando solicitado:

| Propriedade da conta | Descrição |
| --- | --- |
| Nome da conta | Nome exclusivo da conta. Esse nome só é usado na interface do usuário de tags. |
| ID da Conta | Sua ID de conta do [!DNL Google Ads]. Para localizar este valor, faça logon em [!DNL Google Ads] e navegue até: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. A cadeia de caracteres da ID da conta pode ser encontrada na janela de trecho de código que começa com `AW-` ou `d`. |
| Produto | Selecione **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Adicionar conta]** e **[!UICONTROL Salvar]**.

### Adicionar uma ação de conversão de envio {#conversion-action-tags}

Depois de instalar a extensão, você pode começar a incluir ações de conversão nas regras de tag. Ao criar ou editar uma regra que escute a conversão que você deseja aprimorar, selecione **[!UICONTROL Adicionar]** em [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Marca de Site Global da Google (gtag)]** na lista suspensa [!UICONTROL Extensão] e **[!UICONTROL Enviar um evento]** em [!UICONTROL Tipo de Ação].

![O tipo de ação [!UICONTROL Enviar um evento] que está sendo selecionado na exibição de configuração de ação do fluxo de trabalho de edição de regras.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

São exibidos controles adicionais que permitem configurar o evento [!DNL gtag]. No mínimo, os seguintes campos devem ser preenchidos:

1. **[!UICONTROL Nome do evento (Ação)]**: insira `conversion` como o valor.
1. Adicione um novo campo onde a chave seja `transaction_id` e o valor seja um [elemento de dados](../../../ui/managing-resources/data-elements.md) que contenha o valor [ID da transação](https://support.google.com/google-ads/answer/6386790).
1. **[!UICONTROL Rótulo de conversão]**: insira o rótulo de conversão apropriado de sua conta [!DNL Google Ads]. Para encontrar esse valor, faça logon no Google Ads e navegue até **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. O rótulo de conversão pode ser encontrado em [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Enquanto estiver na área de configuração de tag da sua conta do [!DNL Google Ads], verifique se as conversões avançadas estão habilitadas. Para fazer isso, revise e aceite os Termos de Serviço e selecione **[!DNL Turn on enhanced conversions]** e **[!DNL API]** como o método de implementação.

Depois de configurar a ação, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Enviar dados primários usando o encaminhamento de eventos

Depois de enviar eventos de conversão pelo lado do cliente, você poderá aprimorar essas conversões usando a extensão de encaminhamento de eventos do [!DNL Enhanced Conversions].

### Criar um segredo e um elemento de dados OAuth 2 do Google {#create-secret-data-element}

Antes de configurar a extensão, você deve criar um token de acesso no encaminhamento de eventos para autenticar na API [!DNL Google Ads].

Consulte o manual sobre [criação de segredos de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) para obter etapas detalhadas. Certifique-se de selecionar **[!UICONTROL Google OAuth 2]** como o tipo secreto. Continue a seguir as instruções e, quando solicitado a selecionar um perfil de conta do Google, selecione a conta que tem acesso à ação de conversão que você está configurando.

Depois que o segredo for criado, [crie um novo elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) e selecione **[!UICONTROL Segredo]** para o tipo de elemento de dados. Selecione o segredo OAuth 2 do Google apropriado para cada ambiente e selecione **[!UICONTROL Salvar na biblioteca]**.

### Configurar e instalar a extensão [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Localize a extensão [!UICONTROL Conversões Aprimoradas do Google Ads] no catálogo de encaminhamento de eventos e selecione **[!UICONTROL Instalar]**.

![A extensão [!UICONTROL Conversões Aprimoradas do Google Ads] sendo selecionada na exibição [!UICONTROL Extensões] da interface [!UICONTROL Coleção de Dados].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Para configurar a extensão, você deve preencher os dois campos obrigatórios:

1. **[!UICONTROL ID do cliente]**: a ID que identifica exclusivamente a conta do [!DNL Google Ads]. Para localizar este valor, faça logon em [!DNL Google Ads] e navegue até **[!DNL Help]** > **[!DNL Customer ID]**.
2. **[!UICONTROL Elemento de Dados do Token de Acesso]**: selecione o ícone do elemento de dados (![ícone do elemento de dados](/help/images/icons/database.png)) e escolha no menu o elemento de dados secreto OAuth 2 do Google que você [configurou na etapa anterior](#create-secret-data-element).

Quando terminar, selecione **[!UICONTROL Salvar]** para instalar a extensão.

### Adicionar uma ação [!UICONTROL Enviar Conversão] a uma regra {#conversion-action-event-forwarding}

Após a extensão ser instalada, você pode começar a incluir as ações [!UICONTROL Enviar conversão] nas regras de encaminhamento de eventos. Ao criar ou editar uma regra que ouça a conversão que você deseja aprimorar, selecione **[!UICONTROL Adicionar]** em [!UICONTROL Ações]. Na próxima caixa de diálogo, selecione **[!UICONTROL Conversões Aprimoradas do Google Ads]** na lista suspensa [!UICONTROL Extensão] e selecione **[!UICONTROL Enviar Conversão]** em [!UICONTROL Tipo de Ação].

![O tipo de ação [!UICONTROL Enviar Conversão] que está sendo selecionado na exibição de configuração de ação do fluxo de trabalho de edição da regra.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Novos controles são exibidos no painel direito que permitem configurar a conversão. No mínimo, os seguintes campos devem ser preenchidos:

**Informações de conversão**

| Entrada | Descrição |
| --- | --- |
| ID do cliente | Sua ID de cliente do [!DNL Google Ads]. O padrão é a ID de cliente inserida ao [instalar a extensão](#install-enhanced-conversions). |
| ID de conversão ou rótulo de conversão | Valores de rastreamento obtidos de [!DNL Google Ads] ao configurar o rastreamento de conversão. Valores iniciam com `AW-`.<br><br>Para obter detalhes sobre como encontrar esses valores, consulte a [[!DNL Google Ads] documentação](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID da transação | Selecione um elemento de dados que tenha o mesmo valor de ID de transação [enviado do lado do cliente](#conversion-action-tags) usando a extensão [!DNL Google Global Site Tag]. |

**Identificação de usuário**

* Pelo menos um dos três identificadores de usuário deve ser incluído:
   * Email
   * Número de telefone
   * Endereço completo

>[!TIP]
>
>Os dados de identificação do usuário devem ser transformados em hash antes de serem enviados para o Google. Se os dados não tiverem hash quando o encaminhamento de eventos os receber, selecione a opção **[!UICONTROL Normalizar e hash]** em um determinado campo para instruir a extensão a ter o valor hash.
>
>![A opção [!UICONTROL Normalizar e Hash] habilitada para a entrada de [!UICONTROL Email] no formulário de configuração da ação [!UICONTROL Enviar Conversão].](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar eventos de conversão para [!DNL Google Ads] usando a extensão de encaminhamento de eventos [!DNL Enhanced Conversions]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
