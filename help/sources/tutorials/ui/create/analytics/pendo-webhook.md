---
title: Criar uma conexão de origem Pendo na interface do usuário
description: Saiba como criar uma conexão de origem Pendo usando a interface do usuário do Adobe Experience Platform.
badge: "Beta"
source-git-commit: 5a199262acd517516b1e5313a25ddff8f1b11959
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 1%

---

# Crie um [!DNL Pendo] fluxo de dados da conexão de origem e na interface do usuário

>[!NOTE]
>
>O [!DNL Pendo] A fonte está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Pendo] conexão de origem e fluxo de dados usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Pré-requisitos {#prerequisites}

A seção a seguir fornece informações sobre pré-requisitos a serem concluídos antes de criar um [!DNL Pendo] conexão de origem.

### Amostra do JSON para definir o schema de origem para [!DNL Pendo] {#prerequisites-json-schema}

Antes de criar um [!DNL Pendo] conexão de origem, será necessário fornecer um schema de origem. Você pode usar o JSON abaixo.

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

Para obter mais informações, leia a [[!DNL Pendo] guia sobre webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Criar um esquema da Platform para [!DNL Pendo] {#create-platform-schema}

Você também deve garantir que primeiro crie um esquema da plataforma para usar na origem. Veja o tutorial em [criação de um schema da plataforma](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![Interface do usuário da plataforma que mostra um schema de exemplo para Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Conecte seu [!DNL Pendo] account {#connect-account}

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] e veja um catálogo de fontes disponível no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica no catálogo.

Vá para o [!UICONTROL Analytics] para ver a [!DNL Pendo] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origem da interface do usuário da plataforma com o cartão Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Selecionar dados {#select-data}

O **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para selecionar os dados que deseja trazer para a plataforma.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Upload de arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload no [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Depois que o arquivo é carregado, a interface de visualização é atualizada para exibir uma pré-visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Também é possível usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Detalhes do fluxo de dados {#dataflow-detail}

O **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo conjunto de dados para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir as configurações para assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mapeamento {#mapping}

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso. Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](../../../../../data-prep/ui/mapping.md).

Os mapeamentos listados abaixo são obrigatórios e devem ser configurados antes de prosseguir para o [!UICONTROL Revisão] palco.

| Campo de destino | Descrição |
| --- | --- |
| `uniqueId` | O [!DNL Pendo] identificador do evento. |

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Consulte a seção {#review}

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Obter o URL do terminal de transmissão {#get-streaming-endpoint-url}

Com o fluxo de dados criado, agora é possível recuperar o URL do terminal de transmissão. Esse terminal será usado para se inscrever no webhook, permitindo que sua fonte de transmissão se comunique com o Experience Platform.

Para criar o URL usado para configurar o webhook em [!DNL Pendo] você deve recuperar o seguinte:

* **[!UICONTROL ID do fluxo de dados]**
* **[!UICONTROL Ponto de extremidade de transmissão]**

Para recuperar o **[!UICONTROL ID do fluxo de dados]** e **[!UICONTROL Ponto de extremidade de transmissão]**, acesse o [!UICONTROL Atividade do fluxo de dados] página do fluxo de dados que você acabou de criar e copiar os detalhes da parte inferior da [!UICONTROL Propriedades] painel.

![O endpoint de transmissão na atividade de fluxo de dados.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Depois de recuperar o terminal de transmissão e a ID do fluxo de dados, crie um URL com base no seguinte padrão: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Por exemplo, um URL de webhook construído pode ter a seguinte aparência: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configurar Webhook em [!DNL Pendo] {#set-up-webhook}

Em seguida, faça logon na sua conta em [[!DNL Pendo]](https://pendo.io/) e criar um webhook. Para obter as etapas sobre como criar um webhook usando o [!DNL Pendo] interface do usuário, consulte [[!DNL Pendo] guia sobre como criar o webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Depois que o webhook for criado, navegue até a página de configurações do seu [!DNL Pendo] webhook e insira seu URL do webhook no [!DNL URL] campo.

![A captura de tela da interface do usuário do Pendo mostrando o campo de ponto de extremidade do webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>É possível assinar uma variedade de diferentes categorias de eventos para determinar o tipo de evento que deseja enviar a partir de [!DNL Pendo] para a Platform. Para obter mais informações sobre os diferentes eventos, consulte o [[!DNL Pendo] documentação](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você configurou com sucesso um fluxo de dados para trazer seu [!DNL Pendo] dados para o Experience Platform. Para monitorar os dados que estão sendo assimilados, consulte o guia em [monitoramento de fluxos de dados de transmissão usando a interface do usuário da plataforma](../../monitor-streaming.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Pendo] fonte.

### Validação {#validation}

Para validar se você configurou a origem corretamente e [!DNL Pendo] As mensagens estão sendo assimiladas, siga as etapas abaixo:

* Você pode verificar o [!DNL Pendo] **[!UICONTROL Relatórios]** > **[!UICONTROL Histórico de bate-papo]** para identificar os eventos capturados por [!DNL Pendo].

![Captura de tela da interface do usuário Pendo mostrando a história do bate-papo](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Na interface do usuário da plataforma, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do [!DNL Pendo] menu cartão no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados para os webhooks que você configurou em [!DNL Pendo].

![Captura de tela da interface do usuário da plataforma que mostra eventos assimilados](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Erros e solução de problemas {#errors-and-troubleshooting}

Ao verificar uma execução de fluxo de dados, você pode encontrar a seguinte mensagem de erro: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Captura de tela da interface do usuário da plataforma que mostra o erro.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Para corrigir esse erro, você deve verificar se a variável *uniqueID* mapeamento configurado. Para obter mais orientações, consulte [Mapeamento](#mapping) seção.

Para obter mais informações, visite [[!DNL Pendo] Central de ajuda](https://www.pendo.io/help-center/).