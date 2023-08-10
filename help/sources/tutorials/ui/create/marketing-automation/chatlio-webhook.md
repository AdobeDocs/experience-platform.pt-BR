---
title: Criar uma conexão de origem do Chatlio na interface do
description: Saiba como criar uma conexão de origem do Chatlio usando a interface do Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 1%

---

# Criar um [!DNL Chatlio] conexão de origem na interface

>[!NOTE]
>
>A variável [!DNL Chatlio] a fonte está na versão beta. Leia as [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para a criação de um [!DNL Chatlio] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre os pré-requisitos a serem concluídos antes da criação de um [!DNL Chatlio] conexão de origem.

### Amostra de JSON para definir o esquema de origem para [!DNL Chatlio] {#prerequisites-json-schema}

Antes de criar uma [!DNL Chatlio] conexão de origem, será necessário fornecer um esquema de origem. Você pode usar o JSON abaixo.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Criar um esquema da Platform para [!DNL Chatlio] {#create-platform-schema}

Você também deve garantir a criação de um schema da Platform para usar na origem. Leia o tutorial sobre [criação de um schema do Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![A interface do usuário da Platform mostrando um esquema de exemplo para o Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Conecte seu [!DNL Chatlio] account {#connect-account}

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] e veja um catálogo de fontes disponíveis no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a [!UICONTROL Automação de marketing] categoria para ver o [!DNL Chatlio] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo da interface do usuário da Platform com o cartão Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Selecionar dados {#select-data}

A variável **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para que você selecione os dados que deseja trazer para a Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Fazer upload de arquivos]** para carregar um arquivo JSON do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload na [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de visualização do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

A variável **Detalhes do fluxo de dados** A etapa é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa detalhada do fluxo de dados do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mapeamento {#mapping}

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

Os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para a [!UICONTROL Revisão] estágio.

| Campo de destino | Descrição |
| --- | --- |
| `UUID` | A variável [!DNL Chatlio] identificador do evento. |

Depois que os dados de origem forem mapeados com sucesso, selecione **[!UICONTROL Próxima]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Consulte a seção {#review}

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![A etapa de revisão do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Obter o URL do ponto de extremidade de streaming {#get-streaming-endpoint-url}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para construir o URL usado para configurar o webhook no [!DNL Chatlio] você deve recuperar o seguinte:

* **[!UICONTROL ID do fluxo de dados]**
* **[!UICONTROL Endpoint de transmissão]**

Para recuperar o **[!UICONTROL ID do fluxo de dados]** e **[!UICONTROL Endpoint de transmissão]**, vá para a [!UICONTROL Atividade de fluxo de dados] página do fluxo de dados que você acabou de criar e copie os detalhes da parte inferior da [!UICONTROL Propriedades] painel.

![O ponto final de transmissão na atividade de fluxo de dados.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Depois de recuperar o ponto de extremidade de transmissão e a ID do fluxo de dados, crie um URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, um URL de webhook construído pode ser semelhante a: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Configurar webhook no [!DNL Chatlio] {#set-up-webhook}

Com o URL do webhook criado, agora é possível configurar o webhook usando o [!DNL Chatlio] interface do usuário.

Faça logon no [[!DNL Chatlio]](https://chatlio.com/) account e follow [o guia sobre instalação e configuração](https://chatlio.com/docs/setup/) para criar um widget.

Depois que um widget é criado, navegue até a página de configurações do widget para adicionar o URL do webhook a esse widget.

![A página de configurações do webhook no Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Em seguida, selecione o **[!DNL Behavior]** e adicione o URL do webhook à guia *[!DNL Webhook when a new conversation starts]* e quaisquer outros campos de eventos do webhook que você deseja assinar.

![A interface do Chatlio mostrando o campo de ponto de extremidade do webhook.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Você pode assinar uma variedade de eventos diferentes para o seu [!DNL Chatlio] webhook. Para obter mais informações sobre os diferentes eventos, consulte a [[!DNL Chatlio] documentação de eventos](https://chatlio.com/docs/webhooks/).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito um fluxo de dados de transmissão para trazer seus [!DNL Chatlio] dados para Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o manual sobre [monitoramento de fluxos de dados de transmissão usando a interface do usuário da plataforma](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Chatlio] origem.

### Validação {#validation}

Para validar se você configurou corretamente a origem e [!DNL Chatlio] estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar o [!DNL Chatlio] **[!UICONTROL Relatórios]** > **[!UICONTROL Histórico do chat]** página para identificar os eventos que estão sendo capturados pelo [!DNL Chatlio].

![Captura de tela da interface do Chatlio mostrando o histórico do chat](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Na interface do usuário da Platform, selecione **[!UICONTROL Exibir fluxos de dados]** ao lado da variável [!DNL Chatlio] no catálogo de origens. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados pelos webhooks configurados no [!DNL Chatlio].

![Captura de tela da interface do usuário da plataforma mostrando eventos assimilados](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Para obter informações adicionais sobre [!DNL Chatlio], visite o [[!DNL Chatlio] documentação](https://chatlio.com/docs/) e [Perguntas frequentes](https://chatlio.com/pricing/#FAQ).
