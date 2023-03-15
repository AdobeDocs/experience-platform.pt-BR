---
title: Visão geral da extensão da API de meta conversões
description: Saiba mais sobre a extensão da API de meta conversões para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# [!DNL Meta Conversions API] visão geral da extensão

A variável [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) permite conectar seus dados de marketing do lado do servidor ao [!DNL Meta] para otimizar o direcionamento de seus anúncios, reduzir o custo por ação e medir os resultados. Os eventos estão vinculados a um [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) e são processados de maneira semelhante aos eventos do lado do cliente.

Usar o [!DNL Meta Conversions API] você pode aproveitar os recursos da API em sua [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) regras para enviar dados para [!DNL Meta] da Rede de borda da Adobe Experience Platform. Este documento aborda como instalar a extensão e usar seus recursos em um encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md).

## Pré-requisitos

É altamente recomendável usar [!DNL Meta Pixel] e a variável [!DNL Conversions API] para compartilhar e enviar os mesmos eventos do lado do cliente e do lado do servidor, respectivamente, pois isso pode ajudar a recuperar eventos que não foram coletados pelo [!DNL Meta Pixel]. Antes de instalar o [!DNL Conversions API] consulte o guia na seção [[!DNL Meta Pixel] extensão](../../client/meta/overview.md) para obter etapas sobre como integrá-la às implementações de tags do lado do cliente.

>[!NOTE]
>
>A seção sobre [desduplicação de eventos](#deduplication) mais adiante neste documento aborda as etapas para garantir que o mesmo evento não seja usado duas vezes, pois pode ser recebido tanto do navegador quanto do servidor.

Para utilizar a variável [!DNL Conversions API] extensão, você deve ter acesso ao encaminhamento de eventos e ter uma [!DNL Meta] conta com acesso a [!DNL Ad Manager] e [!DNL Event Manager]. Você deve copiar a ID de uma ID existente [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (ou [criar um novo [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) em vez disso), para que a extensão possa ser configurada para sua conta.

## Instalar a extensão

Para instalar o [!DNL Meta Conversions API] , navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia. Procure por [!UICONTROL API de meta conversões] e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL API de meta conversões] na interface da Coleção de dados.](../../../images/extensions/server/meta/install.png)

Na visualização de configuração exibida, você deve fornecer a [!DNL Pixel] ID que você copiou anteriormente para vincular a extensão à sua conta. Você pode colar a ID diretamente na entrada ou usar um elemento de dados.

Também é necessário fornecer um token de acesso para usar o [!DNL Conversions API] especificamente. Consulte a [!DNL Conversions API] documentação sobre [geração de um token de acesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) para obter etapas sobre como obter esse valor.

Quando terminar, selecione **[!UICONTROL Salvar]**

![A variável [!DNL Pixel] A ID fornecida como um elemento de dados na visualização de configuração de extensão.](../../../images/extensions/server/meta/configure.png)

A extensão é instalada e agora você pode empregar seus recursos nas regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Esta seção aborda como usar o [!DNL Conversions API] em uma regra de encaminhamento de eventos genérica. Na prática, você deve configurar várias regras para enviar todas as mensagens aceitas [eventos padrão](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] e [!DNL Conversions API].

>[!NOTE]
>
>Os eventos devem ser [enviado em tempo real](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou o mais próximo possível do tempo real para uma melhor otimização da campanha publicitária.

Comece a criar uma nova regra de encaminhamento de eventos e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Extensão da API de meta conversões]** para a extensão e selecione **[!UICONTROL Enviar evento de API de conversões]** para o tipo de ação.

![A variável [!UICONTROL Enviar Exibição de Página] tipo de ação que está sendo selecionado para uma regra na interface da Coleção de dados.](../../../images/extensions/server/meta/select-action.png)

São exibidos controles que permitem configurar os dados do evento que serão enviados para [!DNL Meta] por meio da [!DNL Conversions API]. Essas opções podem ser inseridas diretamente nas entradas fornecidas ou você pode selecionar elementos de dados existentes para representar os valores. As opções de configuração são divididas em quatro seções principais, conforme descrito abaixo.

| Seção de configuração | Descrição |
| --- | --- |
| [!UICONTROL Parâmetros de evento do servidor] | Informações gerais sobre o evento, incluindo o momento em que ocorreu e a ação de origem que o acionou. Consulte a [!DNL Meta] para obter mais informações sobre o [parâmetros de evento padrão](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) aceito pelo [!DNL Conversions API].<br><br>Se você estiver usando ambos [!DNL Meta Pixel] e a variável [!DNL Conversions API] para enviar eventos, inclua um **[!UICONTROL Nome do evento]** (`event_name`) e **[!UICONTROL ID de evento]** (`event_id`) com cada evento, já que esses valores são usados para [desduplicação de eventos](#deduplication).<br><br>Você também tem a opção de **[!UICONTROL Habilitar Uso Limitado De Dados]** para ajudar a estar em conformidade com as opções de não participação do cliente. Consulte a [!DNL Conversions API] documentação sobre [opções de processamento de dados](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) para obter detalhes sobre esse recurso. |
| [!UICONTROL Parâmetros de Informações do Cliente] | Dados de identidade do usuário usados para atribuir o evento a um cliente. Alguns desses valores devem ser transformados em hash antes de serem enviados para a API.<br><br>Para garantir uma boa conexão de API comum e alta qualidade de correspondência de evento (EMQ), é recomendável enviar todos [parâmetros de informações de clientes aceitos](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) juntamente com eventos do servidor. Estes parâmetros devem também ser [priorizados com base em sua importância e impacto na EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Dados personalizados] | Dados adicionais a serem usados para otimização de entrega de anúncios, fornecidos no formato de um objeto JSON. Consulte a [[!DNL Conversions API] documentação](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) para obter mais informações sobre as propriedades aceitas para este objeto.<br><br>Se estiver enviando um evento de compra, você deve usar esta seção para fornecer os atributos necessários `currency` e `value`. |
| [!UICONTROL Evento de teste] | Esta opção é usada para verificar se sua configuração está fazendo com que os eventos do servidor sejam recebidos por [!DNL Meta] conforme esperado. Para usar esse recurso, selecione a variável **[!UICONTROL Enviar como evento de teste]** e forneça um código de evento de teste de sua escolha na entrada abaixo. Depois que a regra de encaminhamento de eventos for implantada, se você tiver configurado a extensão e a ação corretamente, verá as atividades que aparecem na **[!DNL Test Events]** exibir em [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra.

![[!UICONTROL Manter alterações] selecionada para a configuração da ação.](../../../images/extensions/server/meta/keep-changes.png)

Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**. Por fim, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para ativar as alterações feitas na biblioteca.

## Desduplicação de eventos {#deduplication}

Tal como mencionado no [seção de pré-requisitos](#prerequisites), é recomendável usar as opções [!DNL Meta Pixel] extensão de tag e o [!DNL Conversions API] extensão de encaminhamento de eventos para enviar os mesmos eventos do cliente e do servidor em uma configuração redundante. Isso pode ajudar a recuperar eventos que não foram coletados por uma extensão ou outra.

Se você estiver enviando tipos de evento diferentes do cliente e do servidor sem sobreposição entre os dois, a desduplicação não será necessária. No entanto, se algum evento for compartilhado por ambos [!DNL Meta Pixel] e a variável [!DNL Conversions API], você deve garantir que esses eventos redundantes sejam desduplicados para que seus relatórios não sejam afetados negativamente.

Ao enviar eventos compartilhados, verifique se você está incluindo uma ID e um nome de evento em cada evento enviado do cliente e do servidor. Quando vários eventos com a mesma ID e o mesmo nome forem recebidos, [!DNL Meta] O emprega automaticamente várias estratégias para desduplicá-las e manter os dados mais relevantes. Consulte a [!DNL Meta] documentação sobre [desduplicação para [!DNL Meta Pixel] e [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) para obter detalhes sobre esse processo.

## Próximas etapas

Este guia abordou como enviar dados do evento do lado do servidor para o [!DNL Meta] usando o [!DNL Meta Conversions API] extensão. A partir daqui, é recomendável expandir sua integração conectando mais [!DNL Pixels] e compartilhamento de mais eventos, quando aplicável. Siga qualquer um dos procedimentos a seguir para melhorar ainda mais o desempenho dos seus anúncios:

* Conectar qualquer outro [!DNL Pixels] que ainda não estão conectados a um [!DNL Conversions API] integração.
* Se você estiver enviando determinados eventos exclusivamente por meio do [!DNL Meta Pixel] no lado do cliente, envie esses mesmos eventos para o [!DNL Conversions API] do lado do servidor também.

Consulte a [!DNL Meta] documentação sobre [práticas recomendadas para o [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obter mais orientações sobre como implementar efetivamente sua integração. Para obter mais informações sobre tags e encaminhamento de eventos no Adobe Experience Cloud, consulte o [visão geral das tags](../../../home.md).
