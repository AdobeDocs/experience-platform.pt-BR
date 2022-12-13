---
title: Visão geral da extensão da API MetaConversions
description: Saiba mais sobre a extensão da API Meta conversões para encaminhamento de eventos no Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# [!DNL Meta Conversions API] visão geral da extensão

O [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) permite conectar seus dados de marketing do lado do servidor ao [!DNL Meta] para otimizar o direcionamento de anúncios, diminuir o custo por ação e medir os resultados. Os eventos estão vinculados a um [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID e são processados de maneira semelhante aos eventos do lado do cliente.

Usar o [!DNL Meta Conversions API] , você pode aproveitar os recursos da API em sua [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) regras para enviar dados para [!DNL Meta] da rede de borda Adobe Experience Platform. Este documento aborda como instalar a extensão e usar seus recursos em um encaminhamento de evento [regra](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Se você estiver tentando enviar eventos para o [!DNL Meta] no lado do cliente, em vez de no lado do servidor, use o [[!DNL Meta Pixiel] extensão de tag](../../client/meta/overview.md) em vez disso.

## Pré-requisitos

Para usar a extensão do , você deve acessar o encaminhamento de eventos e ter um [!DNL Meta] com acesso a [!DNL Ad Manager] e [!DNL Event Manager]. Especificamente, você deve copiar a ID de um [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) ou [criar um novo [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) em vez disso), para que a extensão possa ser configurada para sua conta.

## Instalar a extensão

Para instalar o [!DNL Meta Conversions API] , navegue até a interface do usuário da coleta de dados ou a interface do usuário do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade para adicionar a extensão ou crie uma nova propriedade.

Após selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia . Procure a variável [!UICONTROL API Meta conversões] cartão e, em seguida, selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL API Meta conversões] na interface do usuário da Coleta de dados.](../../../images/extensions/server/meta/install.png)

Na exibição de configuração que aparece, você deve fornecer a variável [!DNL Pixel] ID copiada anteriormente para vincular a extensão à conta. Você pode colar a ID diretamente na entrada ou pode usar um elemento de dados.

Também é necessário fornecer um token de acesso para usar o [!DNL Conversions API] especificamente. Consulte a [!DNL Conversions API] documentação sobre [geração de um token de acesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) para obter as etapas sobre como obter esse valor.

Quando terminar, selecione **[!UICONTROL Salvar]**

![O [!DNL Pixel] ID fornecida como um elemento de dados na exibição de configuração da extensão.](../../../images/extensions/server/meta/configure.png)

A extensão do está instalada e agora você pode empregar seus recursos nas regras de tags.

## Configurar uma regra de encaminhamento de eventos {#rule}

Comece criando uma nova regra de encaminhamento de eventos e configure suas condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Extensão da API de Meta Conversões]** para a extensão e selecione **[!UICONTROL Enviar evento da API de conversões]** para o tipo de ação.

![O [!UICONTROL Enviar visualização de página] tipo de ação sendo selecionado para uma regra na interface do usuário da Coleta de dados.](../../../images/extensions/server/meta/select-action.png)

Aparecem controles que permitem configurar os dados do evento que serão enviados para [!DNL Meta] através da [!DNL Conversions API]. Essas opções podem ser inseridas diretamente nas entradas fornecidas ou você pode selecionar elementos de dados existentes para representar os valores. As opções de configuração são divididas em quatro seções principais, conforme descrito abaixo.

| Seção de configuração | Descrição |
| --- | --- |
| [!UICONTROL Parâmetros de evento do servidor] | Informações gerais sobre o evento, incluindo a hora em que ele ocorreu e a ação de origem que o acionou. Consulte a [[!DNL Conversions API] documentação](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) para obter mais informações sobre esses parâmetros.<br><br>Você também tem a opção de **[!UICONTROL Habilitar uso limitado de dados]** para ajudar a estar em conformidade com as opções de não participação do cliente. Consulte a [!DNL Conversions API] documentação sobre [opções de processamento de dados](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) para obter detalhes sobre este recurso. |
| [!UICONTROL Parâmetros de informações do cliente] | Dados de identidade do usuário usados para atribuir o evento a um cliente. Alguns desses valores devem ter hash antes de serem enviados à API. Consulte a [[!DNL Conversions API] documentação](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) para obter mais informações sobre esses parâmetros. |
| [!UICONTROL Dados personalizados] | Dados adicionais a serem usados para otimização de entrega de anúncios, fornecidos no formato de um objeto JSON. Consulte a [[!DNL Conversions API] documentação](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) para obter mais informações sobre as propriedades aceitas para este objeto.<br><br>Se estiver enviando um evento de compra, você deve usar esta seção para fornecer os atributos necessários `currency` e `value`. |
| [!UICONTROL Evento de teste] | Essa opção é usada para verificar se a configuração está fazendo com que os eventos do servidor sejam recebidos por [!DNL Meta] conforme esperado. Para usar esse recurso, selecione o **[!UICONTROL Enviar como evento de teste]** e forneça um código de evento de teste de sua escolha na entrada abaixo. Depois que a regra de encaminhamento de eventos é implantada, se você configurou a extensão e a ação corretamente, é necessário ver as atividades que aparecem no **[!DNL Test Events]** exibir em [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra.

![[!UICONTROL Manter alterações] sendo selecionado para a configuração da ação.](../../../images/extensions/server/meta/keep-changes.png)

Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**. Finalmente, publique um novo encaminhamento de evento [build](../../../ui/publishing/builds.md) para ativar as alterações feitas na biblioteca.

## Próximas etapas

Este guia cobriu como enviar dados de evento do lado do servidor para o [!DNL Meta] usando o [!DNL Meta Conversions API] extensão. Para obter mais informações sobre tags e encaminhamento de eventos, consulte o [visão geral das tags](../../../home.md).
