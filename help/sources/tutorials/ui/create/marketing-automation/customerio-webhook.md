---
title: Criar uma conexão e um fluxo de dados do Source Customer.io na interface
description: Saiba como criar uma conexão de origem Customer.io usando a interface do Adobe Experience Platform.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 1%

---

# Criar uma conexão de origem e um fluxo de dados de [!DNL Customer.io] na interface do usuário

>[!NOTE]
>
>A origem [!DNL Customer.io] está na versão beta. Leia a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar uma conexão de origem e um fluxo de dados do [!DNL Customer.io] usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre os pré-requisitos a serem concluídos antes da criação de uma conexão de origem do [!DNL Customer.io].

### Amostra de JSON para definir o esquema de origem para [!DNL Customer.io] {#prerequisites-json-schema}

Antes de criar uma conexão de origem [!DNL Customer.io], você precisará de um esquema de origem a ser fornecido. Você pode usar o JSON abaixo.

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### Criar um esquema do Experience Platform para [!DNL Customer.io] {#create-platform-schema}

Você também deve garantir a criação de um esquema do Experience Platform para usar na origem. Consulte o tutorial sobre [criação de um esquema do Experience Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

![Captura de tela da interface do Experience Platform mostrando um exemplo de esquema para Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Conectar sua conta do [!DNL Customer.io] {#connect-account}

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes] e ver um catálogo de fontes disponíveis no Experience Platform.

Use o menu *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a categoria [!UICONTROL Automação de marketing] para ver o cartão de origem [!DNL Customer.io]. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do Experience Platform para catálogo com o cartão Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Selecionar dados {#select-data}

A etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para que você selecione os dados que deseja trazer para a Experience Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecione **[!UICONTROL Carregar arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja carregar no painel [!UICONTROL Arrastar e soltar arquivos].

![A etapa para adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário [!UICONTROL Campo de pesquisa] para acessar itens específicos de dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

A etapa **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Mapeamento {#mapping}

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../../data-prep/ui/mapping.md).

Todos os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para o estágio [!UICONTROL Revisão].

| Campo de público alvo | Descrição |
| --- | --- |
| `object_type` | O tipo de objeto, consulte a documentação de [!DNL Customer.io] [eventos](https://customer.io/docs/webhooks/#events) para obter os tipos suportados. |
| `id` | O identificador do objeto. |
| `email` | O endereço de email associado ao objeto. |
| `event_id` | O identificador exclusivo do evento. |
| `cio_id` | O identificador [!DNL Customer.io] do evento. |
| `metric` | O tipo de evento. Para obter mais informações, consulte a documentação de [!DNL Customer.io] [eventos](https://customer.io/docs/webhooks/#events) para conhecer os tipos com suporte. |
| `timestamp` | O carimbo de data e hora quando o evento ocorreu. |

>[!IMPORTANT]
>
>Não mapeie `cio_id` ao executar o webhook [!DNL Customer.io] em `test mode`, pois nenhum campo associado será enviado de [!DNL Customer.io].

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Revisar {#review}

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos de conjunto de dados e mapa]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Obter o URL do ponto de extremidade de streaming {#get-streaming-endpoint}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para construir a URL usada para configurar o webhook em [!DNL Customer.io], você deve recuperar o seguinte:

* **[!UICONTROL ID do Fluxo de Dados]**
* **[!UICONTROL Ponto de extremidade de streaming]**

Para recuperar sua **[!UICONTROL ID de Fluxo de Dados]** e o **[!UICONTROL Ponto de extremidade de streaming]**, vá para a página [!UICONTROL Atividade de Fluxo de Dados] do fluxo de dados que você acabou de criar e copie os detalhes da parte inferior do painel [!UICONTROL Propriedades].

![A extremidade de streaming na atividade de fluxo de dados.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Depois de recuperar o ponto de extremidade de streaming e a ID de fluxo de dados, crie uma URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, uma URL de webhook construída pode ser semelhante a: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configurar webhook de relatórios em [!DNL Customer.io] {#set-up-webhook}

Com a URL do webhook criada, agora você pode configurar o webhook de relatórios usando a interface do usuário [!DNL Customer.io]. Para obter as etapas de configuração de webhooks de relatórios, leia o [[!DNL Customer.io] guia](https://customer.io/docs/webhooks/#setup) sobre a configuração de webhooks.

Na interface de usuário do [!DNL Customer.io], insira sua [URL do webhook](#get-streaming-endpoint-url) no campo [!DNL WEBHOOK ENDPOINT].

![A interface do usuário Customer.io mostrando o campo de ponto de extremidade do webhook](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Você pode assinar uma variedade de eventos diferentes para seu webhook de relatórios. A mensagem de cada evento será assimilada para a Experience Platform quando um critério de gatilho de evento de ação [!DNL Customer.io] for atendido. Para obter mais informações sobre os diferentes eventos, consulte a [[!DNL Customer.io] documentação sobre eventos](https://customer.io/docs/webhooks/#events).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito um fluxo de dados de transmissão para trazer seus dados do [!DNL Customer.io] para a Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o manual sobre [monitoramento de fluxos de dados de transmissão usando a interface do Experience Platform](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL Customer.io].

### Medidas de proteção {#guardrails}

Para obter informações sobre medidas de proteção, consulte a [[!DNL Customer.io] página de tempos limite e falhas](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validação {#validation}

Para validar se você configurou corretamente a origem e se [!DNL Customer.io] mensagens estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar a página [!DNL Customer.io] **[!UICONTROL Logs de atividade]** para identificar os eventos que estão sendo capturados por [!DNL Customer.io].

![Captura de tela da interface do usuário Customer.io mostrando os logs de atividades](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Na interface do usuário do Experience Platform, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do menu de cartão [!DNL Customer.io] no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados que foram assimilados para os eventos selecionados em [!DNL Customer.io].

![Captura de tela da interface do Experience Platform mostrando eventos assimilados](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
