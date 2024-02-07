---
title: Criar uma conexão de origem do Mixpanel na interface
description: Saiba como criar uma conexão de origem do Mixpanel usando a interface do usuário do Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 10%

---

# Criar um [!DNL Mixpanel] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Mixpanel] conexão de origem usando a interface da Adobe Experience Platform Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para se conectar [!DNL Mixpanel] Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Nome de usuário | O nome de usuário da conta de serviço que corresponde ao seu [!DNL Mixpanel] conta. Consulte a [[!DNL Mixpanel] documentação de contas de serviço](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) para obter mais informações. | `Test8.6d4ee7.mp-service-account` |
| Senha | A senha da conta de serviço que corresponde ao seu [!DNL Mixpanel] conta. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID do projeto | Seu [!DNL Mixpanel] ID do projeto. Essa ID é necessária para criar uma conexão de origem. Consulte a [[!DNL Mixpanel] documentação das configurações do projeto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) e a variável [[!DNL Mixpanel] guia sobre criação e gerenciamento de projetos](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) para obter mais informações. | `2384945` |
| Fuso horário | O fuso horário que corresponde ao seu [!DNL Mixpanel] projeto. O fuso horário é necessário para criar uma conexão de origem. Consulte a [Documentação de configurações de projeto do Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) para obter mais informações. | `Pacific Standard Time` |

Para obter mais informações sobre a autenticação do [!DNL Mixpanel] fonte, consulte o [[!DNL Mixpanel] visão geral da origem](../../../../connectors/analytics/mixpanel.md).

## Conecte seu [!DNL Mixpanel] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *Analytics* categoria, selecione [!DNL Mixpanel]e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

A variável **[!UICONTROL Conectar conta do Mixpanel]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Mixpanel] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Selecione a ID do projeto e o fuso horário {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Definir um fuso horário para a ingestão do Mixpanel"
>abstract="O fuso horário deve ser o mesmo que a configuração de fuso horário do perfil do Mixpanel, pois a Platform usa o fuso horário designado do projeto para assimilar dados relevantes do Mixpanel. O Mixpanel ajustará o fuso horário para coordenar com o fuso horário do projeto antes de gravar o evento em um armazenamento de dados do Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=pt-BR#project-id-and-timezone" text="Saiba mais na documentação"

Depois que a origem for autenticada, forneça a ID do projeto e o fuso horário e selecione **[!UICONTROL Selecionar]**.

O fuso horário que você designar antes de assimilar sua [!DNL Mixpanel] Os dados para a Platform devem ser iguais aos [!DNL Mixpanel] configuração de fuso horário do perfil. Quaisquer alterações no fuso horário dos dados serão aplicadas apenas a eventos novos e eventos antigos permanecerão no fuso horário designado anteriormente. [!DNL Mixpanel] O acomoda o Horário de verão e ajustará adequadamente o carimbo de data e hora de assimilação. Para obter mais informações sobre como os fusos horários afetam seus dados, consulte a [!DNL Mixpanel] guia sobre [gerenciamento de fusos horários de projetos](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Após alguns minutos, a interface correta é atualizada para um painel de visualização, permitindo que você inspecione o esquema antes de criar um fluxo de dados. Quando terminar, selecione **[!UICONTROL Próxima]**.

![configuração](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Mixpanel] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de análise para a Platform](../../dataflow/analytics.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Mixpanel] origem.

### Validação {#validation}

As etapas a seguir descrevem as etapas que você pode seguir para validar se conectou com êxito o [!DNL Mixpanel] fonte e que [!DNL Mixpanel] Os eventos estão sendo assimilados na Platform.

Na interface do usuário da Platform, selecione **[!UICONTROL Conjuntos de dados]** na barra de navegação esquerda, para acessar a [!UICONTROL Conjuntos de dados] espaço de trabalho. A variável [!UICONTROL Atividade do conjunto de dados] exibe os detalhes das execuções.

![atividade do conjunto de dados](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Em seguida, selecione a ID de execução do fluxo de dados que deseja exibir para ver detalhes específicos sobre essa execução do fluxo de dados.

![monitoramento de fluxo de dados](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Finalmente, selecione **[!UICONTROL Visualizar conjunto de dados]** para exibir os dados assimilados.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Você pode verificar esses dados em relação aos dados no [!DNL Mixpanel] > [!DNL Events] página. Consulte a [[!DNL Mixpanel] documento sobre eventos](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) para obter mais informações.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Esquema do Mixpanel

A tabela abaixo lista os mapeamentos compatíveis que devem ser configurados para [!DNL Mixpanel].

>[!TIP]
>
>Consulte [API de exportação de eventos > Baixar](https://developer.mixpanel.com/reference/raw-event-export) para obter mais informações sobre a API.


| Fonte | Tipo |
|---|---|
| `distinct_id` | string |
| `event_name` | string |
| `import` | booleano |
| `insert_id` | string |
| `item_id` | string |
| `item_name` | string |
| `item_price` | string |
| `mp_api_endpoint` | string |
| `mp_api_timestamp_ms` | inteiro |
| `mp_processing_time_ms` | inteiro |
| `time` | inteiro |

### Limites {#limits}

* Você tem no máximo 100 consultas simultâneas e 60 consultas por hora, conforme indicado em [Exportar limites de taxa de API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
