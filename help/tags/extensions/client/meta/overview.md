---
title: Visão geral da extensão do Meta Pixel
description: Saiba mais sobre a extensão de tag Meta Pixel no Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Visão geral da extensão do [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) é uma ferramenta de análise baseada no JavaScript que permite rastrear a atividade do visitante em seu site. As ações de visitante que você rastreia (chamadas de conversões) são enviadas para [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager), onde podem ser usadas para medir a eficácia de seus anúncios, campanhas, funis de conversão e muito mais.

A extensão de tag [!DNL Meta Pixel] permite aproveitar as funcionalidades do [!DNL Pixel] nas bibliotecas de tags do lado do cliente. Este documento aborda como instalar a extensão e usar seus recursos em uma [regra](../../../ui/managing-resources/rules.md).

## Pré-requisitos

Para usar a extensão, você deve ter uma conta válida do [!DNL Meta] com acesso ao [!DNL Ads Manager]. Você deve [criar um novo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copiar seu [!DNL Pixel ID] para que a extensão possa ser configurada em sua conta. Se você já tiver um [!DNL Meta Pixel] existente, poderá usar a respectiva ID.

É altamente recomendável usar [!DNL Meta Pixel] em combinação com [!DNL Meta Conversions API] para compartilhar e enviar os mesmos eventos do lado do cliente e do lado do servidor, respectivamente, pois isso pode ajudar a recuperar eventos que não foram selecionados por [!DNL Meta Pixel]. Consulte o guia na [[!DNL Meta Conversions API] extensão para encaminhamento de eventos](../../client/meta/overview.md) para obter etapas sobre como integrá-la às implementações do lado do servidor. Observe que sua organização deve ter acesso ao [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) para usar a extensão do lado do servidor.

## Instalar a extensão

Para instalar a extensão [!DNL Meta Pixel], navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Tags]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Catálogo]**. Procure o cartão [!UICONTROL Meta Pixel] e selecione **[!UICONTROL Instalar]**.

![O botão [!UICONTROL Instalar] está sendo selecionado para a extensão [!UICONTROL Meta Pixel] na interface da Coleção de Dados.](../../../images/extensions/client/meta/install.png)

Na exibição de configuração exibida, você deve fornecer a ID do [!DNL Pixel] copiada anteriormente para vincular a extensão à sua conta. Você pode colar a ID diretamente na entrada ou selecionar um elemento de dados existente.

>[!TIP]
>
>O uso de um elemento de dados oferece a opção de alterar dinamicamente a ID [!DNL Pixel] usada, dependendo de outros fatores, como o ambiente de compilação. Consulte a seção do apêndice em [usando diferentes [!DNL Pixel] IDs para diferentes ambientes](#id-data-element) para obter mais informações.

Opcionalmente, também é possível fornecer uma ID de evento para associar à extensão. Isso é usado para desduplicar eventos idênticos entre [!DNL Meta Pixel] e [!DNL Meta Conversions API]. Para obter detalhes, consulte a seção sobre [desduplicação de eventos](../../server/meta/overview.md#event-deduplication) na visão geral da extensão [!DNL Conversions API].

Quando terminar, selecione **[!UICONTROL Salvar]**

![A ID [!DNL Pixel] fornecida como um elemento de dados na exibição de configuração de extensão.](../../../images/extensions/client/meta/configure.png)

A extensão é instalada e agora você pode empregar suas várias ações nas regras de tag.

## Configurar uma regra de tag {#rule}

[!DNL Meta Pixel] aceita um conjunto de [eventos padrão](https://www.facebook.com/business/help/402791146561655) predefinidos, cada um com seus próprios contextos e propriedades aceitas. As ações de regra fornecidas pela extensão [!DNL Pixel] estão correlacionadas a esses tipos de evento, permitindo categorizar e configurar facilmente o evento que está sendo enviado para [!DNL Meta] de acordo com seu tipo.

Para fins de demonstração, esta seção mostra como criar uma regra que envia um evento de exibição de página para [!DNL Meta].

Comece a criar uma nova regra de tag e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Meta Pixel]** para a extensão e selecione **[!UICONTROL Enviar Exibição de Página]** para o tipo de ação.

![O tipo de ação [!UICONTROL Enviar Exibição de Página] que está sendo selecionado para uma regra na Interface da Coleção de Dados.](../../../images/extensions/client/meta/select-action.png)

Não é necessária mais nenhuma configuração para a ação [!UICONTROL Enviar Exibição de Página]. Selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique uma nova tag [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Confirmar se [!DNL Meta] está recebendo dados

Depois que a compilação atualizada for implantada no seu site, você poderá confirmar se os dados estão sendo enviados como esperado gerando alguns eventos de conversão no seu navegador e verificando se esses eventos aparecem em [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Próximas etapas

Este guia abordou como enviar dados para [!DNL Meta] usando a extensão de tag [!DNL Meta Pixel]. Se você pretende enviar eventos do lado do servidor para o [!DNL Meta], agora é possível prosseguir para instalar e configurar a [[!DNL Conversions API] extensão de encaminhamento de eventos](../../server/meta/overview.md).

Para obter mais informações sobre tags no Experience Platform, consulte a [visão geral das tags](../../../home.md).

## Apêndice: Usar diferentes IDs do [!DNL Pixel] para diferentes ambientes {#id-data-element}

Se você quiser testar sua implementação em ambientes de desenvolvimento ou de preparo enquanto mantém as análises da produção [!DNL Meta Pixel] intactas, poderá usar um elemento de dados para escolher dinamicamente uma ID [!DNL Pixel] apropriada, dependendo do ambiente que está sendo usado.

Você pode fazer isso usando um elemento de dados [!UICONTROL Código personalizado] (fornecido pela extensão [[!UICONTROL Core]](../core/overview.md)) em combinação com a variável livre [`turbine`](../../../extension-dev/turbine.md). No código JavaScript do elemento de dados, use o objeto `turbine` para localizar o estágio de ambiente atual e retorne uma ID [!DNL Pixel] apropriada com base no resultado.

O exemplo a seguir retorna uma ID de produção falsa `exampleProductionKey` quando usada no ambiente de produção, e uma ID diferente `exampleTestKey` quando qualquer outro ambiente é usado. Ao implementar esse código, substitua cada valor pela produção real e teste [!DNL Pixel] IDs.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
