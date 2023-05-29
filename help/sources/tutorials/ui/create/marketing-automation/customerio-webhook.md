---
title: Criar uma conexão de origem e um fluxo de dados Customer.io na interface
description: Saiba como criar uma conexão de origem Customer.io usando a interface do Adobe Experience Platform.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Criar um [!DNL Customer.io] conexão de origem e fluxo de dados na interface do

>[!NOTE]
>
>A variável [!DNL Customer.io] a fonte está na versão beta. Leia as [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para a criação de um [!DNL Customer.io] conexão de origem e fluxo de dados usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre os pré-requisitos a serem concluídos antes da criação de um [!DNL Customer.io] conexão de origem.

### Amostra de JSON para definir o esquema de origem para [!DNL Customer.io] {#prerequisites-json-schema}

Antes de criar uma [!DNL Customer.io] conexão de origem, será necessário fornecer um esquema de origem. Você pode usar o JSON abaixo.

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

### Criar um esquema da Platform para [!DNL Customer.io] {#create-platform-schema}

Você também deve garantir a criação de um schema da Platform para usar na origem. Veja o tutorial sobre [criação de um schema do Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![Captura de tela da interface do usuário da plataforma mostrando um esquema de exemplo para Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Conecte seu [!DNL Customer.io] account {#connect-account}

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] e veja um catálogo de fontes disponíveis no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a [!UICONTROL Automação de marketing] categoria para ver o [!DNL Customer.io] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do usuário da plataforma para catálogo com o cartão Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Selecionar dados {#select-data}

A variável **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para que você selecione os dados que deseja trazer para a Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Fazer upload de arquivos]** para carregar um arquivo JSON do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload na [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de visualização do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

A variável **Detalhes do fluxo de dados** A etapa é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa detalhada do fluxo de dados do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Mapeamento {#mapping}

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e campos calculados, consulte o [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

Todos os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para a [!UICONTROL Revisão] estágio.

| Campo de destino | Descrição |
| --- | --- |
| `object_type` | O tipo de objeto, consulte a [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentação dos tipos suportados. |
| `id` | O identificador do objeto. |
| `email` | O endereço de email associado ao objeto. |
| `event_id` | O identificador exclusivo do evento. |
| `cio_id` | A variável [!DNL Customer.io] identificador do evento. |
| `metric` | O tipo de evento. Para obter mais informações, consulte [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentação para os tipos suportados. |
| `timestamp` | O carimbo de data e hora quando o evento ocorreu. |

>[!IMPORTANT]
>
>Não mapear `cio_id` ao executar [!DNL Customer.io] webhook no `test mode` como não haverá campos associados enviados de [!DNL Customer.io].

Depois que os dados de origem forem mapeados com sucesso, selecione **[!UICONTROL Próxima]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Consulte a seção {#review}

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![A etapa de revisão do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Obter o URL do ponto de extremidade de streaming {#get-streaming-endpoint}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para construir o URL usado para configurar o webhook no [!DNL Customer.io] você deve recuperar o seguinte:

* **[!UICONTROL ID do fluxo de dados]**
* **[!UICONTROL Endpoint de transmissão]**

Para recuperar o **[!UICONTROL ID do fluxo de dados]** e **[!UICONTROL Endpoint de transmissão]**, vá para a [!UICONTROL Atividade de fluxo de dados] página do fluxo de dados que você acabou de criar e copie os detalhes da parte inferior da [!UICONTROL Propriedades] painel.

![O ponto final de transmissão na atividade de fluxo de dados.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Depois de recuperar o ponto de extremidade de transmissão e a ID do fluxo de dados, crie um URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, um URL de webhook construído pode ser semelhante a: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configurar webhook de relatórios no [!DNL Customer.io] {#set-up-webhook}

Com o URL do webhook criado, agora é possível configurar o webhook de relatórios usando o [!DNL Customer.io] interface do usuário. Para obter as etapas sobre como configurar webhooks para relatórios, leia o [[!DNL Customer.io] guia](https://customer.io/docs/webhooks/#setup) em configurar webhooks.

No [!DNL Customer.io] interface do usuário, insira seu [URL do webhook](#get-streaming-endpoint-url) no [!DNL WEBHOOK ENDPOINT] campo.

![A interface do usuário Customer.io que mostra o campo de ponto de extremidade do webhook](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Você pode assinar uma variedade de eventos diferentes para seu webhook de relatórios. A mensagem de cada evento será assimilada na Platform quando um [!DNL Customer.io] o critério do acionador de evento de ação foi atendido. Para obter mais informações sobre os diferentes eventos, consulte a seção [[!DNL Customer.io] documentação de eventos](https://customer.io/docs/webhooks/#events).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com êxito um fluxo de dados de transmissão para trazer seus [!DNL Customer.io] dados para Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o manual sobre [monitoramento de fluxos de dados de transmissão usando a interface do usuário da plataforma](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Customer.io] origem.

### Medidas de proteção {#guardrails}

Para obter informações sobre as medidas de proteção, consulte [[!DNL Customer.io] página tempos limite e falhas](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validação {#validation}

Para validar se você configurou corretamente a origem e [!DNL Customer.io] estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar o [!DNL Customer.io] **[!UICONTROL Logs de atividade]** página para identificar os eventos que estão sendo capturados pelo [!DNL Customer.io].

![Captura de tela da interface do usuário Customer.io mostrando os logs de atividades](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Na interface do usuário da Platform, selecione **[!UICONTROL Exibir fluxos de dados]** ao lado da variável [!DNL Customer.io] no catálogo de origens. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados que foram assimilados para os eventos selecionados no [!DNL Customer.io].

![Captura de tela da interface do usuário da plataforma mostrando eventos assimilados](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
