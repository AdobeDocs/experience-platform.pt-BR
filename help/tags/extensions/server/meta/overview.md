---
title: Visão geral da extensão da API de meta conversões
description: Saiba mais sobre a extensão da API de meta conversões para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 3cd937f49f27006e3cab60df1692d33138944ce2
workflow-type: tm+mt
source-wordcount: '2583'
ht-degree: 0%

---

# Visão geral da extensão do [!DNL Meta Conversions API]

O [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) permite conectar seus dados de marketing do lado do servidor às tecnologias do [!DNL Meta] para otimizar o direcionamento de seus anúncios, reduzir o custo por ação e medir os resultados. Eventos estão vinculados a uma ID do [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) e são processados de maneira semelhante aos eventos do lado do cliente.

Usando a extensão [!DNL Meta Conversions API], você pode aproveitar os recursos da API em suas regras [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) para enviar dados para [!DNL Meta] do Edge Network Adobe Experience Platform. Este documento aborda como instalar a extensão e usar seus recursos em uma [regra](../../../ui/managing-resources/rules.md) de encaminhamento de eventos.

## Demonstração

O vídeo a seguir tem como objetivo ajudá-lo a entender o [!DNL Meta Conversions API].

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Pré-requisitos

É altamente recomendável usar [!DNL Meta Pixel] e [!DNL Conversions API] para compartilhar e enviar os mesmos eventos do lado do cliente e do lado do servidor, respectivamente, pois isso pode ajudar a recuperar eventos que não foram selecionados por [!DNL Meta Pixel]. Antes de instalar a extensão [!DNL Conversions API], consulte o guia na [[!DNL Meta Pixel] extensão](../../client/meta/overview.md) para obter etapas sobre como integrá-la nas implementações de tags do lado do cliente.

>[!NOTE]
>
>A seção sobre [desduplicação de eventos](#deduplication), apresentada posteriormente neste documento, aborda as etapas para garantir que o mesmo evento não seja usado duas vezes, pois pode ser recebido do navegador e do servidor.

Para usar a extensão [!DNL Conversions API], você deve ter acesso ao encaminhamento de eventos e ter uma conta [!DNL Meta] válida com acesso a [!DNL Ad Manager] e [!DNL Event Manager]. Especificamente, você deve copiar a ID de um [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) existente (ou [criar um novo [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755)) para que a extensão possa ser configurada para sua conta.

>[!INFO]
>
>Se você estiver planejando usar esta extensão com dados de aplicativo móvel ou se também trabalhar com dados de evento offline em suas campanhas do [!DNL Meta], será necessário criar seu conjunto de dados por meio de um aplicativo existente e selecionar **Criar a partir de uma ID de pixel** quando solicitado. Consulte o artigo [Decida qual opção de criação de conjunto de dados é adequada para sua empresa](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) para obter detalhes. Consulte o documento [API de Conversões para Eventos de Aplicativo](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) para obter todos os parâmetros de rastreamento de aplicativo obrigatórios e opcionais.

## Instalar a extensão

Para instalar a extensão [!DNL Meta Conversions API], navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Encaminhamento de eventos]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Catálogo]**. Procure o cartão [!UICONTROL APIs de MetaConversões] e selecione **[!UICONTROL Instalar]**.

![A opção [!UICONTROL Instalar] está sendo selecionada para a extensão [!UICONTROL API de Metaconversões] na interface da Coleção de Dados.](../../../images/extensions/server/meta/install.png)

Na exibição de configuração exibida, você deve fornecer a ID do [!DNL Pixel] copiada anteriormente para vincular a extensão à sua conta. Você pode colar a ID diretamente na entrada ou usar um elemento de dados.

Você também precisa fornecer um token de acesso para usar o [!DNL Conversions API] especificamente. Consulte a documentação [!DNL Conversions API] em [gerando um token de acesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) para obter etapas sobre como obter esse valor.

Quando terminar, selecione **[!UICONTROL Salvar]**

![A ID [!DNL Pixel] fornecida como um elemento de dados na exibição de configuração de extensão.](../../../images/extensions/server/meta/configure.png)

A extensão é instalada e agora você pode empregar seus recursos nas regras de encaminhamento de eventos.

## Integração com a extensão do Facebook e do Instagram {#facebook}

A integração usando a extensão Facebook e Instagram permite que você se autentique rapidamente em sua conta Meta Business. Em seguida, o [!UICONTROL Pixel ID] e o [!UICONTROL Token de acesso] da API de metaconversões são preenchidos automaticamente, facilitando a instalação e a configuração da API de metaconversões.

Um prompt de caixa de diálogo para autenticar no Facebook e no Instagram é exibido ao instalar a extensão [!UICONTROL API de Meta Conversões].

![A [!UICONTROL Extensão da API de Meta Conversões] destacando a página de instalação [!UICONTROL Conectar-se a Meta].](../../../images/extensions/server/meta/mbe-extension-install.png)

Um prompt da caixa de diálogo para autenticar no Facebook e no Instagram também é exibido na interface do fluxo de trabalho de início rápido no encaminhamento de eventos.

![A interface de início rápido do fluxo de trabalho destacando [!UICONTROL Conectar-se a Meta].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Integração com a Pontuação de correspondência de qualidade do evento (EMQ) {#emq}

A integração com a Pontuação de correspondência de qualidade do evento (EMQ) permite visualizar facilmente a eficácia da implementação ao mostrar pontuações da EMQ. Essa integração minimiza a alternância de contexto e ajuda a melhorar o sucesso das implementações da API de Meta Conversões. Essas pontuações de eventos aparecem na tela de configuração da [!UICONTROL Extensão de API de metaconversões].

![A [!UICONTROL Extensão da API de Metaconversões] destacando a página de configuração [!UICONTROL Exibir Pontuação EMQ].](../../../images/extensions/server/meta/emq-score.png)

## Integração com o LiveRamp (Alpha) {#alpha}

[!DNL LiveRamp] clientes que têm a solução de tráfego autenticado (ATS) do [!DNL LiveRamp] implantada em seus sites podem optar por compartilhar RampIDs como um parâmetro de informações do cliente. Trabalhe com a equipe de conta do [!DNL Meta] para participar do programa Alpha para este recurso.

![A página de configuração da [!UICONTROL Regra] do encaminhamento de Metaeventos, destacando [!UICONTROL Nome do Parceiro (alfa)] e [!UICONTROL ID do Parceiro (alfa)].](../../../images/extensions/server/meta/live-ramp.png)

## Configurar uma regra de encaminhamento de eventos {#rule}

Esta seção aborda como usar a extensão [!DNL Conversions API] em uma regra de encaminhamento de eventos genérica. Na prática, você deve configurar várias regras para enviar todos os [eventos padrão](https://developers.facebook.com/docs/meta-pixel/reference) aceitos via [!DNL Meta Pixel] e [!DNL Conversions API]. Para dados de aplicativos móveis, consulte os campos obrigatórios, os campos de dados de aplicativos, os parâmetros de informações do cliente e os detalhes de dados personalizados [aqui](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Os eventos devem ser [enviados em tempo real](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou o mais próximo possível do tempo real para uma melhor otimização da campanha publicitária.

Comece a criar uma nova regra de encaminhamento de eventos e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Extensão da API de Metaconversões]** para a extensão e selecione **[!UICONTROL Enviar evento da API de conversões]** para o tipo de ação.

![O tipo de ação [!UICONTROL Enviar Exibição de Página] que está sendo selecionado para uma regra na Interface da Coleção de Dados.](../../../images/extensions/server/meta/select-action.png)

São exibidos controles que permitem configurar os dados do evento que serão enviados para [!DNL Meta] por meio de [!DNL Conversions API]. Essas opções podem ser inseridas diretamente nas entradas fornecidas ou você pode selecionar elementos de dados existentes para representar os valores. As opções de configuração são divididas em quatro seções principais, conforme descrito abaixo.

| Seção de configuração | Descrição |
| --- | --- |
| [!UICONTROL Parâmetros de Evento do Servidor] | Informações gerais sobre o evento, incluindo o momento em que ocorreu e a ação de origem que o acionou. Consulte a documentação do desenvolvedor [!DNL Meta] para obter mais informações sobre os [parâmetros de evento padrão](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) aceitos pelo [!DNL Conversions API].<br><br>Se você estiver usando [!DNL Meta Pixel] e [!DNL Conversions API] para enviar eventos, certifique-se de incluir um **[!UICONTROL Nome do Evento]** (`event_name`) e uma **[!UICONTROL ID do Evento]** (`event_id`) com cada evento, uma vez que esses valores são usados para a [eliminação de duplicação de eventos](#deduplication).<br><br>Você também tem a opção de **[!UICONTROL Habilitar o Uso Limitado de Dados]** para ajudar a estar em conformidade com as opções de não participação do cliente. Consulte a documentação [!DNL Conversions API] em [opções de processamento de dados](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) para obter detalhes sobre este recurso. |
| [!UICONTROL Parâmetros de informações do cliente] | Dados de identidade do usuário usados para atribuir o evento a um cliente. Alguns desses valores devem ser transformados em hash antes de serem enviados para a API.<br><br>Para garantir uma boa conexão de API comum e uma alta qualidade de correspondência de eventos (EMQ), é recomendável enviar todos os [parâmetros de informações de clientes aceitos](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) juntamente com eventos de servidor. Esses parâmetros também devem ser [priorizados com base em sua importância e impacto no EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Dados personalizados] | Dados adicionais a serem usados para otimização de entrega de anúncios, fornecidos no formato de um objeto JSON. Consulte a [[!DNL Conversions API] documentação](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) para obter mais informações sobre as propriedades aceitas para este objeto.<br><br>Se estiver enviando um evento de compra, você deve usar esta seção para fornecer os atributos necessários `currency` e `value`. |
| [!UICONTROL Evento de teste] | Esta opção é usada para verificar se sua configuração está fazendo com que os eventos de servidor sejam recebidos por [!DNL Meta] conforme esperado. Para usar este recurso, marque a caixa de seleção **[!UICONTROL Enviar como Evento de Teste]** e forneça um código de evento de teste de sua escolha na entrada abaixo. Depois que a regra de encaminhamento de eventos for implantada, se você tiver configurado a extensão e a ação corretamente, deverá ver as atividades que aparecem na exibição **[!DNL Test Events]** em [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra.

![[!UICONTROL Manter alterações] sendo selecionadas para a configuração da ação.](../../../images/extensions/server/meta/keep-changes.png)

Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**. Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações feitas na biblioteca.

## Desduplicação de eventos {#deduplication}

Conforme mencionado na [seção de pré-requisitos](#prerequisites), é recomendável usar a extensão de tag [!DNL Meta Pixel] e a extensão de encaminhamento de eventos [!DNL Conversions API] para enviar os mesmos eventos do cliente e do servidor em uma configuração redundante. Isso pode ajudar a recuperar eventos que não foram coletados por uma extensão ou outra.

Se você estiver enviando tipos de evento diferentes do cliente e do servidor sem sobreposição entre os dois, a desduplicação não será necessária. No entanto, se qualquer evento for compartilhado por [!DNL Meta Pixel] e [!DNL Conversions API], você deve garantir que esses eventos redundantes sejam desduplicados para que seus relatórios não sejam afetados negativamente.

Ao enviar eventos compartilhados, verifique se você está incluindo uma ID e um nome de evento em cada evento enviado do cliente e do servidor. Quando vários eventos com a mesma ID e o mesmo nome são recebidos, o [!DNL Meta] emprega automaticamente várias estratégias para desduplicá-los e manter os dados mais relevantes. Consulte a documentação do [!DNL Meta] sobre a [desduplicação para [!DNL Meta Pixel] e [!DNL Conversions API] eventos](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) para obter detalhes sobre esse processo.

## Fluxo de trabalho de início rápido: Extensão da API de meta conversões (Beta) {#quick-start}

>[!IMPORTANT]
>
>* O recurso de início rápido está disponível para clientes que compraram o pacote Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.
>* Esse recurso é para novas implementações e atualmente não é compatível com a instalação automática de extensões e configurações em tags existentes e propriedades de encaminhamento de eventos.

>[!NOTE]
>
>Qualquer cliente existente pode usar os workflows de início rápido para criar uma implementação de referência que pode ser usada para o seguinte:
>* Use-a como o início de uma implementação totalmente nova.
>* Aproveite-a como uma implementação de referência que pode ser examinada para ver como ela foi configurada e replicar em suas implementações de produção atuais.

O recurso de início rápido ajuda a configurar com facilidade e eficiência a API de Meta Conversões e as extensões Meta Pixel. Essa ferramenta automatiza várias etapas executadas em tags de Adobe e no encaminhamento de eventos, reduzindo significativamente o tempo de configuração.

Esse recurso instala e configura automaticamente a API de metaconversões e as extensões de metapixels em uma propriedade de tags recém-gerada automaticamente e encaminhamento de eventos com as regras e os elementos de dados necessários. Além disso, ele também instala e configura automaticamente o SDK da Web do Experience Platform e o Datastream. Por fim, o recurso de início rápido publica automaticamente a biblioteca no URL designado em um ambiente de desenvolvimento, o que permite a coleta de dados do lado do cliente e o encaminhamento de eventos do lado do servidor em tempo real por meio do encaminhamento de eventos e do Edge Network Experience Platform.

O vídeo a seguir fornece uma introdução ao recurso de início rápido.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Instalar o recurso de início rápido

>[!NOTE]
>
>Esse recurso foi projetado para ajudar você a começar a implementar o encaminhamento de eventos. Ele não fornecerá uma implementação completa e totalmente funcional que acomode todos os casos de uso.

Esta configuração instala automaticamente as extensões Meta Conversions API e Meta Pixel. Essa implementação híbrida é recomendada pelo Meta para coletar e encaminhar conversões de eventos no lado do servidor.
O recurso de configuração rápida foi projetado para ajudar os clientes a começar a usar uma implementação de encaminhamento de eventos, e não tem como objetivo fornecer uma implementação completa e totalmente funcional que acomode todos os casos de uso.

Para instalar o recurso, selecione **[!UICONTROL Introdução]** para **[!DNL Send Conversions Data to Meta]** na página **[!UICONTROL Página inicial]** da Coleção de dados da Adobe Experience Platform.

![Página inicial da coleção de dados mostrando dados de conversões para meta](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Insira seu **[!UICONTROL Domínio]** e selecione **[!UICONTROL Próximo]**. Esse domínio será usado como uma convenção de nomenclatura para suas propriedades geradas automaticamente de Tags e Encaminhamento de eventos, regras, elementos de dados, sequências de dados e assim por diante.

![Tela de boas-vindas solicitando o nome de domínio](../../../images/extensions/server/meta/welcome.png)

Na caixa de diálogo **[!UICONTROL Configuração Inicial]**, insira o **[!UICONTROL ID de Meta Pixel]**, o **[!UICONTROL Token de Acesso da API de Meta Conversão]** e o **[!UICONTROL Caminho da Camada de Dados]** e selecione **[!UICONTROL Avançar]**.

![Caixa de diálogo de configuração inicial](../../../images/extensions/server/meta/initial-setup.png)

Aguarde alguns minutos para que o processo de instalação inicial seja concluído e selecione **[!UICONTROL Avançar]**.

![Tela de confirmação de conclusão da instalação inicial](../../../images/extensions/server/meta/setup-complete.png)

Na caixa de diálogo **[!UICONTROL Adicionar código ao seu site]**, copie o código fornecido usando a função de cópia ![Copiar](../../../images/extensions/server/meta/copy-icon.png) e cole-o no `<head>` do site de origem. Depois de implementado, selecione **[!UICONTROL Iniciar Validação]**

![Adicionar código na caixa de diálogo do site](../../../images/extensions/server/meta/add-code-on-your-site.png)

A caixa de diálogo [!UICONTROL Resultados da Validação] exibe os resultados da implementação da Extensão Meta. Selecione **[!UICONTROL Próximo]**. Você também pode ver resultados de validação adicionais selecionando o link **[!UICONTROL Garantia]**.

![Caixa de diálogo de resultados de teste exibindo resultados da implementação](../../../images/extensions/server/meta/test-results.png)

A exibição da tela **[!UICONTROL Próximas Etapas]** confirma a conclusão da instalação. Aqui, você tem a opção de otimizar sua implementação adicionando novos eventos, que são mostrados na próxima seção.

Se não quiser adicionar mais eventos, selecione **[!UICONTROL Fechar]**.

![Caixa de diálogo Próximas etapas](../../../images/extensions/server/meta/next-steps.png)

#### Adição de eventos adicionais

Para adicionar novos eventos, selecione **[!UICONTROL Editar Propriedade da Web de Marcas]**.

![Caixa de diálogo de próximas etapas mostrando como editar a propriedade da Web de suas marcas](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Selecione a regra que corresponde ao metaevento que você deseja editar. Por exemplo, **MetaConversion_AddToCart**.

>[!NOTE]
>
>Se não houver nenhum evento, essa regra não será executada. Isso é verdadeiro para todas as regras, com a regra **MetaConversion_PageView** sendo a exceção.

Para adicionar um evento, selecione **[!UICONTROL Adicionar]** sob o cabeçalho [!UICONTROL Eventos].

![A página de propriedades da marca não mostra eventos](../../../images/extensions/server/meta/edit-rule.png)

Selecione o [!UICONTROL Tipo de Evento]. Neste exemplo, selecionamos o evento [!UICONTROL Clique] e o configuramos para disparar quando o **.botão adicionar ao carrinho** estiver selecionado. Selecione **[!UICONTROL Manter alterações]**.

![Tela de configuração de evento mostrando o evento de clique](../../../images/extensions/server/meta/event-configuration.png)

O novo evento foi salvo. Selecione **[!UICONTROL Selecionar uma biblioteca de trabalho]** e selecione a biblioteca para a qual você deseja compilar.

![Selecione uma lista suspensa de biblioteca de trabalho](../../../images/extensions/server/meta/working-library.png)

Em seguida, selecione a lista suspensa ao lado de **[!UICONTROL Salvar na biblioteca]** e selecione **[!UICONTROL Salvar na biblioteca e na build]**. Isso publicará a alteração na biblioteca.

![Selecione Salvar na biblioteca e compilar](../../../images/extensions/server/meta/save-and-build.png)

Repita essas etapas para qualquer outro evento de meta conversão que deseje configurar.

#### Configuração da camada de dados {#configuration}

>[!IMPORTANT]
>
>A maneira como você atualiza essa camada de dados global depende da arquitetura do site. Um aplicativo de página única será diferente de um aplicativo de renderização do lado do servidor. Também há a possibilidade de que você seja totalmente responsável pela criação e atualização desses dados dentro do produto de Tags. Em todas as instâncias, a camada de dados precisará ser atualizada entre a execução de cada `MetaConversion_* rules`. Se você não atualizar os dados entre regras, também poderá se deparar com um caso em que esteja enviando dados obsoletos do último `MetaConversion_* rule` no `MetaConversion_* rule` atual.

Durante a configuração, você foi perguntado onde está a camada de dados. Por padrão, seria `window.dataLayer.meta` e, dentro do objeto `meta`, seus dados seriam esperados, como mostrado abaixo.

![Metainformações da camada de dados](../../../images/extensions/server/meta/data-layer-meta.png)

É importante entender isso, pois cada regra `MetaConversion_*` usa essa estrutura de dados para transmitir os dados relevantes à extensão [!DNL Meta Pixel] e ao [!DNL Meta Conversions API]. Consulte a documentação em [eventos padrão](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) para obter mais informações sobre quais dados são necessários para os diferentes metaeventos.

Por exemplo, se você quiser usar a regra `MetaConversion_Subscribe`, será necessário atualizar `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv` e `window.dataLayer.meta.value` de acordo com as propriedades de objeto descritas na documentação em [eventos padrão](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Veja abaixo um exemplo do que precisaria ser executado em um site para atualizar a camada de dados antes da execução da regra.

![Atualizar informações meta da camada de dados](../../../images/extensions/server/meta/update-data-layer-meta.png)

Por padrão, o `<datalayerpath>.conversionData.eventId` será gerado aleatoriamente pela ação &quot;Gerar nova ID de evento&quot; em qualquer um dos `MetaConversion_* rules`.

Para obter uma referência local de como a camada de dados deve ser exibida, você pode abrir o editor de código personalizado no elemento de dados `MetaConversion_DataLayer` na propriedade.

## Próximas etapas

Este guia abordou como enviar dados de eventos do lado do servidor para o [!DNL Meta] usando a extensão [!DNL Meta Conversions API]. A partir daqui, é recomendável expandir sua integração conectando mais [!DNL Pixels] e compartilhando mais eventos, quando aplicável. Siga qualquer um dos procedimentos a seguir para melhorar ainda mais o desempenho dos seus anúncios:

* Conecte qualquer outro [!DNL Pixels] que ainda não esteja conectado a uma integração [!DNL Conversions API].
* Se você estiver enviando determinados eventos exclusivamente por meio do [!DNL Meta Pixel] no lado do cliente, envie esses mesmos eventos para o [!DNL Conversions API] também no lado do servidor.

Consulte a documentação do [!DNL Meta] sobre [práticas recomendadas para o [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obter mais orientações sobre como implementar efetivamente sua integração. Para obter mais informações sobre tags e encaminhamento de eventos no Adobe Experience Cloud, consulte a [visão geral das tags](../../../home.md).
