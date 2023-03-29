---
title: Criar uma conexão de fonte Customer.io e um fluxo de dados na interface do usuário
description: Saiba como criar uma conexão de origem Customer.io usando a interface do usuário do Adobe Experience Platform.
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Crie um [!DNL Customer.io] conexão de origem e fluxo de dados na interface do usuário

>[!NOTE]
>
>O [!DNL Customer.io] A fonte está em beta. Leia o [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Customer.io] conexão de origem e fluxo de dados usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre pré-requisitos a serem concluídos antes de criar um [!DNL Customer.io] conexão de origem.

### Amostra do JSON para definir o schema de origem para [!DNL Customer.io] {#prerequisites-json-schema}

Antes de criar um [!DNL Customer.io] conexão de origem, será necessário fornecer um schema de origem. Você pode usar o JSON abaixo.

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

Você também deve garantir que crie um esquema da plataforma para usar na origem. Veja o tutorial em [criação de um schema da plataforma](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![Captura de tela da interface do usuário da plataforma mostrando um esquema de exemplo para Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)

## Conecte seu [!DNL Customer.io] account {#connect-account}

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] e veja um catálogo de fontes disponível no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica no catálogo.

Vá para o [!UICONTROL Automação de marketing] para ver a [!DNL Customer.io] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do usuário da plataforma para catálogo com o cartão Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## Selecionar dados {#select-data}

O **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para selecionar os dados que deseja trazer para a plataforma.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Upload de arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload no [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Depois que o arquivo é carregado, a interface de visualização é atualizada para exibir uma pré-visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Também é possível usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

O **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo conjunto de dados para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir as configurações para assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Mapeamento {#mapping}

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso. Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](../../../../../data-prep/ui/mapping.md).

Todos os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para a [!UICONTROL Revisão] palco.

| Campo de destino | Descrição |
| --- | --- |
| `object_type` | O tipo de objeto , consulte a [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentação dos tipos suportados. |
| `id` | O identificador do objeto. |
| `email` | O endereço de email associado ao objeto. |
| `event_id` | O identificador exclusivo do evento. |
| `cio_id` | O [!DNL Customer.io] identificador do evento. |
| `metric` | O tipo de evento. Para obter mais informações, consulte [!DNL Customer.io] [events](https://customer.io/docs/webhooks/#events) documentação para tipos suportados. |
| `timestamp` | O carimbo de data e hora em que o evento ocorreu. |

>[!IMPORTANT]
>
>Não mapear `cio_id` ao executar [!DNL Customer.io] webhook na `test mode` como não haverá campos associados enviados de [!DNL Customer.io].

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Consulte a seção {#review}

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Obter o URL do terminal de transmissão {#get-streaming-endpoint}

Com o fluxo de dados criado, agora é possível recuperar o URL do terminal de transmissão. Esse terminal será usado para se inscrever no webhook, permitindo que sua fonte de transmissão se comunique com o Experience Platform.

Para criar o URL usado para configurar o webhook em [!DNL Customer.io] você deve recuperar o seguinte:

* **[!UICONTROL ID do fluxo de dados]**
* **[!UICONTROL Ponto de extremidade de transmissão]**

Para recuperar o **[!UICONTROL ID do fluxo de dados]** e **[!UICONTROL Ponto de extremidade de transmissão]**, acesse o [!UICONTROL Atividade do fluxo de dados] página do fluxo de dados que você acabou de criar e copiar os detalhes da parte inferior da [!UICONTROL Propriedades] painel.

![O endpoint de transmissão na atividade de fluxo de dados.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Depois de recuperar o terminal de transmissão e a ID do fluxo de dados, crie um URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, um URL de webhook construído pode ter a seguinte aparência: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Configurar o webhook de relatórios em [!DNL Customer.io] {#set-up-webhook}

Com o URL do webhook criado, você pode configurar o webhook de relatórios usando o [!DNL Customer.io] interface do usuário. Para obter as etapas sobre como configurar webhooks de relatórios, leia o [[!DNL Customer.io] guia](https://customer.io/docs/webhooks/#setup) ao configurar webhooks.

No [!DNL Customer.io] interface do usuário, insira [URL do webhook](#get-streaming-endpoint-url) no [!DNL WEBHOOK ENDPOINT] campo.

![A interface do usuário do Customer.io que mostra o campo de ponto de extremidade do webhook](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>Você pode assinar uma variedade de eventos diferentes para o seu webhook de relatórios. A mensagem de cada evento será assimilada na plataforma quando uma [!DNL Customer.io] os critérios do acionador do evento de ação são atendidos. Para obter mais informações sobre os diferentes eventos, consulte o [[!DNL Customer.io] documentação de eventos](https://customer.io/docs/webhooks/#events).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com sucesso um fluxo de dados para trazer seu [!DNL Customer.io] dados para o Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o guia em [monitoramento de fluxos de dados de transmissão usando a interface do usuário da plataforma](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Customer.io] fonte.

### Medidas de proteção {#guardrails}

Para obter informações sobre medidas de proteção, consulte [[!DNL Customer.io] página de tempos limite e falhas](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validação {#validation}

Para validar se você configurou a origem corretamente e [!DNL Customer.io] As mensagens estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar o [!DNL Customer.io] **[!UICONTROL Logs de atividade]** para identificar os eventos capturados por [!DNL Customer.io].

![Captura de tela da interface do usuário do Customer.io mostrando logs de atividades](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* Na interface do usuário da plataforma, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do [!DNL Customer.io] menu cartão no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados para os eventos selecionados no [!DNL Customer.io].

![Captura de tela da interface do usuário da plataforma que mostra eventos assimilados](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
