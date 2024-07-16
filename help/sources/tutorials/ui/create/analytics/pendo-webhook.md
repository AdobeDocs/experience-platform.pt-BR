---
title: Criar uma conexão do Pendo Source na interface
description: Saiba como criar uma conexão de origem do Pendo usando a interface do Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# Criar um fluxo de dados de conexão de origem [!DNL Pendo] e na interface do usuário

>[!NOTE]
>
>A origem [!DNL Pendo] está na versão beta. Leia a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar uma conexão de origem e um fluxo de dados do [!DNL Pendo] usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre os pré-requisitos a serem concluídos antes da criação de uma conexão de origem do [!DNL Pendo].

### Amostra de JSON para definir o esquema de origem para [!DNL Pendo] {#prerequisites-json-schema}

Antes de criar uma conexão de origem [!DNL Pendo], você precisará de um esquema de origem a ser fornecido. Você pode usar o JSON abaixo.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Para obter mais informações, leia o [[!DNL Pendo] guia sobre webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Criar um esquema da plataforma para [!DNL Pendo] {#create-platform-schema}

Você também deve garantir que primeiro crie um esquema da Platform para usar na origem. Consulte o tutorial sobre [criação de um esquema da Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

![Interface do usuário da plataforma mostrando um exemplo de esquema para Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Conectar sua conta do [!DNL Pendo] {#connect-account}

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes] e ver um catálogo de fontes disponíveis no Experience Platform.

Use o menu *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a categoria [!UICONTROL Analytics] para ver o cartão de origem [!DNL Pendo]. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origem da interface do usuário da Platform com o cartão Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Selecionar dados {#select-data}

A etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para que você selecione os dados que deseja trazer para a Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecione **[!UICONTROL Carregar arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja carregar no painel [!UICONTROL Arrastar e soltar arquivos].

![A etapa para adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário [!UICONTROL Campo de pesquisa] para acessar itens específicos de dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

A etapa **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mapeamento {#mapping}

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../../data-prep/ui/mapping.md).

Os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para o estágio [!UICONTROL Revisão].

| Campo de público alvo | Descrição |
| --- | --- |
| `uniqueId` | O identificador [!DNL Pendo] do evento. |

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Revisar {#review}

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos de conjunto de dados e mapa]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Obter o URL do ponto de extremidade de streaming {#get-streaming-endpoint-url}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para construir a URL usada para configurar o webhook em [!DNL Pendo], você deve recuperar o seguinte:

* **[!UICONTROL ID do Fluxo de Dados]**
* **[!UICONTROL Ponto de extremidade de streaming]**

Para recuperar sua **[!UICONTROL ID de Fluxo de Dados]** e o **[!UICONTROL Ponto de extremidade de streaming]**, vá para a página [!UICONTROL Atividade de Fluxo de Dados] do fluxo de dados que você acabou de criar e copie os detalhes da parte inferior do painel [!UICONTROL Propriedades].

![A extremidade de streaming na atividade de fluxo de dados.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Depois de recuperar o ponto de extremidade de streaming e a ID de fluxo de dados, crie uma URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, uma URL de webhook construída pode ser semelhante a: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configurar Webhook em [!DNL Pendo] {#set-up-webhook}

Em seguida, faça logon em sua conta no [[!DNL Pendo]](https://pendo.io/) e crie um webhook. Para obter etapas sobre como criar um webhook usando a interface do usuário [!DNL Pendo], consulte o [[!DNL Pendo] guia sobre criação de webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Depois que o webhook for criado, navegue até a página de configurações do webhook [!DNL Pendo] e insira a URL do webhook no campo [!DNL URL].

![A captura de tela da interface do usuário do Pendo mostrando o campo de ponto de extremidade do webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Você pode assinar várias categorias de eventos diferentes para determinar o tipo de evento que deseja enviar da instância [!DNL Pendo] para a Platform. Para obter mais informações sobre eventos diferentes, consulte a [[!DNL Pendo] documentação](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito um fluxo de dados de transmissão para trazer seus dados do [!DNL Pendo] para o Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o manual sobre [monitoramento de fluxos de dados de transmissão usando a interface do usuário da plataforma](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL Pendo].

### Validação {#validation}

Para validar se você configurou corretamente a origem e se [!DNL Pendo] mensagens estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar a página [!DNL Pendo] **[!UICONTROL Relatórios]** > **[!UICONTROL Histórico do Chat]** para identificar os eventos que estão sendo capturados por [!DNL Pendo].

![Captura de tela da interface do usuário do Pendo mostrando o histórico do chat](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Na interface da Platform, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do menu de cartão [!DNL Pendo] no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados pelos webhooks configurados no [!DNL Pendo].

![Captura de tela da interface do usuário da plataforma mostrando eventos assimilados](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Erros e solução de problemas {#errors-and-troubleshooting}

Ao verificar uma execução de fluxo de dados, você pode encontrar a seguinte mensagem de erro: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Captura de tela da Interface do Usuário da Plataforma mostrando erro.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Para corrigir esse erro, verifique se o mapeamento *uniqueID* foi configurado. Para obter orientação adicional, consulte a seção [Mapeamento](#mapping).

Para obter mais informações, visite a [[!DNL Pendo] Central de ajuda](https://www.pendo.io/help-center/).
