---
title: Visão geral das configurações
description: Saiba mais sobre as opções disponíveis ao configurar a extensão de tag do Web SDK.
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Visão geral das configurações

A extensão de tag do Adobe Experience Platform Web SDK fornece várias opções que podem ser personalizadas. Essas definições de configuração são o equivalente ao uso do comando [`configure`](/help/collection/js/commands/configure/overview.md) na biblioteca do JavaScript.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].

## Componentes de build personalizados

Se a otimização do tamanho da build for uma prioridade para sua organização, você poderá desativar determinados recursos que não são usados para diminuir o tamanho da build da extensão. Consulte [Componentes de compilação personalizados](custom-build-components.md) para obter mais informações.

## Instâncias do SDK

A maioria das implementações geralmente precisa de uma única instância do SDK. No entanto, se sua organização exigir várias instâncias de rastreamento do Web SDK, você poderá usar o botão **[!UICONTROL Add instance]**. As seguintes seções abrangentes estão disponíveis ao configurar cada instância de tag do Web SDK:

* [**[!UICONTROL SDK instance]**](general.md): configurações gerais da instância. Todos os campos desta seção são obrigatórios.
* [**[!UICONTROL Datastreams]**](datastreams.md): Onde você deseja que os dados sejam colocados para cada ambiente de marcas.
* [**[!UICONTROL Consent]**](consent.md): Configurações de consentimento padrão para a extensão.
* [**[!UICONTROL Identity]**](identity.md): configurações de migração de cookies e visitantes.
* [**[!UICONTROL Personalization]**](personalization.md): Personalizar a experiência do visitante individualmente.
* [**[!UICONTROL Data collection]**](data-collection.md): Incluir ou omitir o que é coletado automaticamente.
* [**[!UICONTROL Streaming media]**](streaming-media.md): configurações específicas para coleção de streaming de mídia.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): Modifique as definições de configuração quando determinadas condições forem atendidas.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): especifique o caminho base para o Edge Network.
