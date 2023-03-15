---
title: Visão geral da extensão do Meta Pixel
description: Saiba mais sobre a extensão de tag Meta Pixel no Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] visão geral da extensão

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) O é uma ferramenta de análise baseada em JavaScript que permite rastrear a atividade do visitante no seu site. As ações do visitante que você rastreia (chamadas de conversões) são enviadas para [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) onde eles podem ser usados para medir a eficácia de seus anúncios, campanhas, funis de conversão e muito mais.

A variável [!DNL Meta Pixel] a extensão de tag permite aproveitar [!DNL Pixel] nas bibliotecas de tags do lado do cliente. Este documento aborda como instalar a extensão e usar seus recursos em uma [regra](../../../ui/managing-resources/rules.md).

## Pré-requisitos

Para usar a extensão, você deve ter uma [!DNL Meta] conta com acesso a [!DNL Ads Manager]. Especificamente, você deve [criar um novo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copie seu [!DNL Pixel ID] para que a extensão possa ser configurada para sua conta. Se você já tiver um [!DNL Meta Pixel], você pode usar a ID dele no lugar.

É altamente recomendável usar [!DNL Meta Pixel] em combinação com a [!DNL Meta Conversions API] para compartilhar e enviar os mesmos eventos do lado do cliente e do lado do servidor, respectivamente, pois isso pode ajudar a recuperar eventos que não foram coletados pelo [!DNL Meta Pixel]. Consulte o guia no [[!DNL Meta Conversions API] extensão para encaminhamento de eventos](../../client/meta/overview.md) para obter etapas sobre como integrá-lo nas implementações do lado do servidor. Observe que sua organização deve ter acesso a [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) para usar a extensão do lado do servidor.

## Instalar a extensão

Para instalar o [!DNL Meta Pixel] , navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Tags]** no painel de navegação esquerdo. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia. Procure por [!UICONTROL Meta Pixel] e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL Meta Pixel] na interface da Coleção de dados.](../../../images/extensions/client/meta/install.png)

Na visualização de configuração exibida, você deve fornecer a [!DNL Pixel] ID que você copiou anteriormente para vincular a extensão à sua conta. Você pode colar a ID diretamente na entrada ou selecionar um elemento de dados existente.

>[!TIP]
>
>O uso de um elemento de dados oferece a opção de alterar dinamicamente a [!DNL Pixel] ID usada dependendo de outros fatores, como o ambiente de compilação. Consulte a seção do apêndice sobre [usar diferentes [!DNL Pixel] IDs para diferentes ambientes](#id-data-element) para obter mais informações.

Opcionalmente, também é possível fornecer uma ID de evento para associar à extensão. Isso é usado para desduplicar eventos idênticos entre [!DNL Meta Pixel] e a variável [!DNL Meta Conversions API]. Para obter detalhes, consulte a seção sobre [desduplicação de eventos](../../server/meta/overview.md#event-deduplication) em visão geral para o [!DNL Conversions API] extensão.

Quando terminar, selecione **[!UICONTROL Salvar]**

![A variável [!DNL Pixel] A ID fornecida como um elemento de dados na visualização de configuração de extensão.](../../../images/extensions/client/meta/configure.png)

A extensão é instalada e agora você pode empregar suas várias ações nas regras de tag.

## Configurar uma regra de tag {#rule}

[!DNL Meta Pixel] aceita um conjunto de valores predefinidos [eventos padrão](https://www.facebook.com/business/help/402791146561655), cada um com seus próprios contextos e propriedades aceitas. As ações de regra fornecidas pelo [!DNL Pixel] A extensão do está correlacionada a esses tipos de evento, permitindo categorizar e configurar facilmente o evento que está sendo enviado para o [!DNL Meta] de acordo com o seu tipo.

Para fins de demonstração, esta seção mostra como criar uma regra que envia um evento de exibição de página para o [!DNL Meta].

Comece a criar uma nova regra de tag e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Meta Pixel]** para a extensão e selecione **[!UICONTROL Enviar Exibição de Página]** para o tipo de ação.

![A variável [!UICONTROL Enviar Exibição de Página] tipo de ação que está sendo selecionado para uma regra na interface da Coleção de dados.](../../../images/extensions/client/meta/select-action.png)

Não é necessária mais nenhuma configuração para o [!UICONTROL Enviar Exibição de Página] ação. Selecionar **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique uma nova tag [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Confirme que [!DNL Meta] está recebendo dados

Depois que a build atualizada for implantada em seu site, você poderá confirmar se os dados estão sendo enviados conforme esperado, gerando alguns eventos de conversão em seu navegador e verificando se esses eventos aparecem em [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Próximas etapas

Este guia abordou como enviar dados para o [!DNL Meta] usando o [!DNL Meta Pixel] extensão de tag. Se você estiver planejando enviar eventos do lado do servidor para o [!DNL Meta], agora você pode prosseguir para instalar e configurar o [[!DNL Conversions API] extensão de encaminhamento de eventos](../../server/meta/overview.md).

Para obter mais informações sobre tags no Experience Platform, consulte a [visão geral das tags](../../../home.md).

## Apêndice: Usar diferentes [!DNL Pixel] IDs para diferentes ambientes {#id-data-element}

Se você quiser testar a implementação em ambientes de desenvolvimento ou de preparo enquanto mantém a produção [!DNL Meta Pixel] do analytics intactas, você pode usar um elemento de dados para escolher dinamicamente um [!DNL Pixel] ID dependendo do ambiente que está sendo usado.

Você pode fazer isso usando um [!UICONTROL Custom Code] elemento de dados (fornecido pelo [[!UICONTROL Núcleo] extensão](../core/overview.md)em combinação com a [`turbine` variável livre](../../../extension-dev/turbine.md). No código JavaScript do elemento de dados, use a variável `turbine` para encontrar o estágio de ambiente atual, em seguida, retorne um [!DNL Pixel] ID com base no resultado.

O exemplo a seguir retorna uma ID de produção falsa `exampleProductionKey` quando usado no ambiente de produção, e uma ID diferente `exampleTestKey` quando qualquer outro ambiente é usado. Ao implementar esse código, substitua cada valor pela produção e pelo teste reais [!DNL Pixel] IDs.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
