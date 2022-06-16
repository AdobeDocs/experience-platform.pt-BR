---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: (Beta) Crie uma conexão de origem do Mixpanel na interface do usuário
description: Saiba como criar uma conexão de origem do Mixpanel usando a interface do usuário do Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 8092829c95c9bc43894b73db104fdbb22363e460
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# (Beta) Criar um [!DNL Mixpanel] conexão de origem na interface do usuário

>[!NOTE]
>
>O [!DNL Mixpanel] A fonte está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Mixpanel] conexão de origem usando a interface do usuário da Adobe Experience Platform Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

### Obter credenciais necessárias

Para se conectar [!DNL Mixpanel] para Plataforma, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Host | O [!DNL Mixpanel] endpoint da API de exportação de dados brutos. Consulte a [!DNL Raw Data Export API] na seção [Documentação de referência da API do Mixpanel](https://developer.mixpanel.com/reference/overview) para obter mais informações. | `https://data.mixpanel.com` |
| Nome do usuário | O nome de usuário da conta de serviço que corresponde a sua [!DNL Mixpanel] conta. Consulte a [[!DNL Mixpanel] documentação das contas de serviço](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) para obter mais informações. | `Test8.6d4ee7.mp-service-account` |
| Senha | A senha da conta de serviço que corresponde ao seu [!DNL Mixpanel] conta. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID do projeto | Seu [!DNL Mixpanel] ID do projeto. Essa ID é necessária para criar uma conexão de origem. Consulte a [[!DNL Mixpanel] documentação de configurações do projeto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) e [[!DNL Mixpanel] guia sobre criação e gestão de projetos](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) para obter mais informações. | `2384945` |
| Fuso horário | O fuso horário que corresponde a [!DNL Mixpanel] projeto. O fuso horário é necessário para criar uma conexão de origem. Consulte a [Documentação de configurações do projeto Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) para obter mais informações. | `Pacific Standard Time` |

Para obter mais informações sobre como autenticar seu [!DNL Mixpanel] na fonte, consulte o [[!DNL Mixpanel] visão geral da fonte](../../../../connectors/analytics/mixpanel.md).

## Conecte seu [!DNL Mixpanel] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em *Analytics* categoria , selecione [!DNL Mixpanel]e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

O **[!UICONTROL Conexão da conta do Mixpanel]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Mixpanel] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Selecione a ID do projeto e o fuso horário {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Definir um fuso horário para a assimilação do Mixpanel"
>abstract="O fuso horário deve ser o mesmo que a configuração de fuso horário do perfil do Mixpanel, pois o Platform usa o fuso horário designado do projeto para assimilar dados relevantes do Mixpanel. O Mixpanel ajustará o fuso horário para coordenar com o fuso horário do projeto antes de gravar o evento em um armazenamento de dados do Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=en#project-id-and-timezone" text="Saiba mais na documentação"

Depois que a fonte for autenticada, forneça a ID do projeto e o fuso horário e selecione **[!UICONTROL Selecionar]**.

O fuso horário que você designar antes de assimilar seu [!DNL Mixpanel] os dados para a plataforma devem ser iguais aos seus [!DNL Mixpanel] configuração de fuso horário do perfil. Todas as alterações no fuso horário dos dados serão aplicadas apenas a novos eventos e os eventos antigos permanecerão no fuso horário designado anteriormente. [!DNL Mixpanel] O acomoda o Horário de verão e ajustará seu carimbo de data e hora de assimilação apropriadamente. Para obter mais informações sobre como os fusos horários afetam seus dados, consulte o [!DNL Mixpanel] guia em [gerenciamento de fusos horários para projetos](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Após alguns minutos, a interface correta é atualizada para um painel de visualização, permitindo inspecionar seu esquema antes de criar um fluxo de dados. Quando terminar, selecione **[!UICONTROL Próximo]**.

![configuração](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Mixpanel] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de análise para a plataforma](../../dataflow/analytics.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Mixpanel] fonte.

### Validação {#validation}

As linhas gerais a seguir podem ser usadas para validar que você conectou seu [!DNL Mixpanel] e que [!DNL Mixpanel] eventos estão sendo assimilados na Platform.

Na interface do usuário da plataforma, selecione **[!UICONTROL Conjuntos de dados]** na barra de navegação esquerda para acessar o [!UICONTROL Conjuntos de dados] espaço de trabalho. O [!UICONTROL Atividade do conjunto de dados] exibe os detalhes das execuções.

![atividade do conjunto de dados](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Em seguida, selecione a ID de execução do fluxo de dados que deseja visualizar para ver detalhes específicos sobre a execução do fluxo de dados.

![monitoramento de fluxo de dados](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Finalmente, selecione **[!UICONTROL Visualizar conjunto de dados]** para exibir os dados que foram assimilados.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Você pode verificar esses dados em relação aos dados no [!DNL Mixpanel] > [!DNL Events] página. Consulte a [[!DNL Mixpanel] documento sobre eventos](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) para obter mais informações.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Schema Mixpanel

A tabela abaixo lista os mapeamentos suportados que devem ser configurados para [!DNL Mixpanel].

>[!TIP]
>
>Consulte [API de exportação de evento > Download](https://developer.mixpanel.com/reference/raw-event-export) para obter mais informações sobre a API.


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
| `mp_api_timestamp_ms` | integer |
| `mp_processing_time_ms` | integer |
| `time` | integer |

### Limites {#limits}

* Você tem no máximo 100 queries simultâneos e 60 queries por hora, conforme indicado em [Exportar limites de taxa de API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).