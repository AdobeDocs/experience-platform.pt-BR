---
title: Visão geral da extensão Encaixar pixel
description: Saiba como você pode usar a extensão de tag Encaixar Pixel para capturar valiosas interações de usuário no Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Visão geral da extensão do [!DNL Snap Pixel]

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) é uma ferramenta de análise baseada no JavaScript que capacita você a capturar interações de usuário valiosas em seu site. Ações de visitantes importantes, como compras, inscrições ou outras conversões, são automaticamente enviadas ao seu [Gerenciador de Anúncios](http://ads.snapchat.com/), permitindo medir e otimizar o desempenho de seus anúncios, campanhas, caminhos de conversão e muito mais.

A extensão de tags do [!DNL Snap Pixel] permite integrar a funcionalidade do [!DNL Snap Pixel] diretamente às bibliotecas de tags do lado do cliente. Esta documentação descreve como instalar a extensão e implementar seus recursos nas regras de gerenciamento de tags.

A extensão de tag [!DNL Snap Pixel] simplifica a integração da funcionalidade [!DNL Snap Pixel] nas bibliotecas de tags do lado do cliente existentes. Esta documentação descreve como instalar a extensão e configurar seus recursos nas [regras](../../../ui/managing-resources/rules.md) do gerenciamento de tags.

## Pré-requisitos {#prerequisites}

Para usar a extensão, você precisará de uma conta válida do [!DNL Snap] com acesso ao [!DNL Ads Manager]. Você deve [criar um novo [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) e copiar sua ID de Pixel para configurar a extensão para sua conta. Se você tiver um [!DNL Snap Pixel] existente, poderá simplesmente usar sua ID.

É recomendável usar [!DNL Snap Pixel] junto com [!DNL Snap Conversions API] para enviar os mesmos eventos do lado do cliente e do lado do servidor. Esta abordagem pode ajudar a recuperar eventos que podem não ser capturados somente pelo [!DNL Snap Pixel]. Consulte a [[!DNL Snap] Extensão de API de conversões para encaminhamento de eventos](../../server/snap/overview.md) para obter etapas sobre como integrá-la às implementações do lado do servidor. Observe que sua organização deve ter acesso a [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) para usar a extensão do lado do servidor.

## Instalar a extensão {#install}

Para instalar a extensão [!DNL Snap Pixel], navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Tags]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Catálogo]**. Procure a placa [!UICONTROL Encaixar Pixel] e selecione **[!UICONTROL Instalar]**.

![O botão [!UICONTROL Instalar] sendo selecionado para a extensão [!UICONTROL Pixel de Instantâneo] na interface da Coleção de Dados.](./images/install.png)

Na visualização de configuração exibida, você deve fornecer a ID do Pixel copiada anteriormente para vincular a extensão à sua conta. Você pode colar a ID diretamente na entrada ou selecionar um elemento de dados existente.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![A ID [!DNL Pixel] fornecida como um elemento de dados na exibição de configuração de extensão.](./images/configure.png)

A extensão é instalada e agora você pode empregar suas várias ações nas regras de tag.

## Configurar uma regra de tag {#rule}

O [!DNL Snap Pixel] oferece suporte a um conjunto de eventos padrão predefinidos, cada um com contextos específicos e parâmetros aceitos. As ações de regra disponíveis na extensão [!DNL Snap Pixel] estão alinhadas a esses tipos de evento, tornando simples categorizar e configurar eventos que estão sendo enviados para [!DNL Snap] de acordo com seus tipos.

Para fins de demonstração, esta seção mostra como criar uma regra que envia eventos de compra para [!DNL Snap].

Para começar, crie uma nova regra de tag e defina as condições conforme necessário. Ao configurar as ações da regra, escolha [!DNL Snap Pixel] como extensão e selecione **[!UICONTROL Enviar evento de compra]** como tipo de ação.

Depois de concluir a configuração da ação [!UICONTROL Enviar Evento de Compra], selecione **[!UICONTROL Manter Alterações]** para adicioná-lo à configuração de regras.

![O tipo de ação [!UICONTROL Enviar Evento de Compra] selecionado para uma regra na Interface da Coleção de Dados.](./images/action-type.png)

Quando estiver satisfeito com a configuração geral da regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Para aplicar suas atualizações, publique uma nova tag [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Confirmar se [!DNL Snap] está recebendo dados {#confirm}

Depois que a compilação atualizada for implantada no seu site, você poderá verificar se os dados estão sendo enviados conforme esperado acionando eventos de conversão no seu navegador e verificando se eles aparecem em [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Próximas etapas {#next-steps}

Este guia aborda como enviar dados para [!DNL Snap] usando a extensão de tag [!DNL Snap Pixel]. Se você também planeja enviar eventos do lado do servidor para o [!DNL Snap], continue com a instalação e configure o [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
