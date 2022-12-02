---
title: Visão geral da extensão Meta Pixel
description: Saiba mais sobre a extensão de tag Meta Pixel no Adobe Experience Platform.
source-git-commit: 644941b4d95f986bb37219be59424e41c7442511
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# [!DNL Meta Pixel] visão geral da extensão

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) O é uma ferramenta de análise baseada em JavaScript que permite rastrear a atividade do visitante no seu site. As ações de visitante rastreadas (chamadas de conversões) são enviadas para o [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) onde podem ser usados para medir a eficácia de seus anúncios, campanhas, funis de conversão e muito mais.

O [!DNL Meta Pixel] a extensão de tag permite aproveitar [!DNL Pixel] funcionalidades nas bibliotecas de tags do lado do cliente. Este documento aborda como instalar a extensão e usar seus recursos em um [regra](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## Pré-requisitos

Para usar a extensão do , você deve ter um [!DNL Facebook] com acesso a [!DNL Ads Manager]. Especificamente, você deve [criar um novo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copie [!DNL Pixel ID] para que a extensão possa ser configurada para sua conta. Se você já tiver um [!DNL Meta Pixel], você pode usar a ID em vez disso.

## Instalar a extensão

Para instalar o [!DNL Meta Pixel] , navegue até a interface do usuário da coleta de dados ou a interface do usuário do Experience Platform e selecione **[!UICONTROL Tags]** no painel de navegação esquerdo. Aqui, selecione uma propriedade para adicionar a extensão ou crie uma nova propriedade.

Após selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia . Procure a variável [!UICONTROL Meta Pixel] cartão e, em seguida, selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL Meta Pixel] na interface do usuário da Coleta de dados.](../../../images/extensions/client/meta/install.png)

Na exibição de configuração que aparece, você deve fornecer a variável [!DNL Pixel] ID copiada anteriormente para vincular a extensão à conta. Você pode colar a ID diretamente na entrada ou pode selecionar um elemento de dados existente.

>[!TIP]
>
>O uso de um elemento de dados oferece a opção de alterar dinamicamente a variável [!DNL Pixel] ID usada, dependendo de outros fatores, como o ambiente de criação. Consulte a seção do apêndice em [usando diferentes [!DNL Pixel] IDs para ambientes diferentes](#id-data-element) para obter mais informações.

Quando terminar, selecione **[!UICONTROL Salvar]**

![O [!DNL Pixel] ID fornecida como um elemento de dados na exibição de configuração da extensão.](../../../images/extensions/client/meta/configure.png)

A extensão do está instalada e agora você pode empregar suas várias ações nas regras de tags.

## Configurar uma regra de tag {#rule}

[!DNL Meta Pixel] aceita um conjunto de [eventos padrão](https://www.facebook.com/business/help/402791146561655), cada um com seus próprios contextos e propriedades aceitas. As ações de regra fornecidas pela [!DNL Pixel] extensão correlacionada a esses tipos de evento, permitindo categorizar e configurar facilmente o evento enviado para [!DNL Meta] de acordo com seu tipo.

Para fins de demonstração, esta seção mostra como criar uma regra que envia um evento de exibição de página para o [!DNL Meta].

Comece criando uma nova regra de tag e configure suas condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Meta Pixel]** para a extensão e selecione **[!UICONTROL Enviar visualização de página]** para o tipo de ação.

![O [!UICONTROL Enviar visualização de página] tipo de ação sendo selecionado para uma regra na interface do usuário da Coleta de dados.](../../../images/extensions/client/meta/select-action.png)

Não é necessária mais configuração para a variável [!UICONTROL Enviar visualização de página] ação. Selecionar **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique uma nova tag [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Confirme que [!DNL Meta] está recebendo dados

Depois que sua build atualizada tiver sido implantada em seu site, você poderá confirmar se os dados estão sendo enviados como esperado, gerando alguns eventos de conversão em seu navegador e verificando se esses eventos aparecem em [Gerenciador de Meta Eventos](https://www.facebook.com/business/help/898185560232180).

## Próximas etapas

Este guia cobriu como enviar dados para o [!DNL Meta] usando o [!DNL Meta Pixel] extensão da tag. Para obter mais informações sobre tags no Experience Platform, consulte [visão geral das tags](../../../home.md).

## Apêndice: Usar diferentes [!DNL Pixel] IDs para ambientes diferentes {#id-data-element}

Caso queira testar a implementação em ambientes de desenvolvimento ou de preparo, mantendo a produção [!DNL Meta Pixel] do analytics intacto, é possível usar um elemento de dados para escolher dinamicamente um [!DNL Pixel] ID dependendo do ambiente que está sendo usado.

Você pode fazer isso usando um [!UICONTROL Código personalizado] elemento de dados (fornecido pelo [[!UICONTROL Núcleo] extensão](../core/overview.md)) em combinação com [`turbine` variável gratuita](../../../extension-dev/turbine.md). No código JavaScript do elemento de dados, use a variável `turbine` para localizar o estágio de ambiente atual e, em seguida, retornar um [!DNL Pixel] ID com base no resultado.

O exemplo a seguir retorna uma ID de produção falsa `exampleProductionKey` quando usado no ambiente de produção e uma ID diferente `exampleTestKey` quando qualquer outro ambiente for usado. Ao implementar esse código, substitua cada valor por sua produção e teste reais [!DNL Pixel] IDs.

```js
if (turbine.environment.stage === "production") {
  return 'exampleProductionKey';
} else {
  return 'exampleTestKey';
}
```
