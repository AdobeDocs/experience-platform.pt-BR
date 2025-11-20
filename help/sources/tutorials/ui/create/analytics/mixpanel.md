---
title: Criar uma conexão do Mixpanel Source na interface
description: Saiba como criar uma conexão de origem do Mixpanel usando a interface do usuário do Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 11%

---

# Criar uma conexão de origem [!DNL Mixpanel] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Mixpanel] usando a interface do usuário do Adobe Experience Platform Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para conectar [!DNL Mixpanel] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Nome de usuário | O nome de usuário da conta de serviço que corresponde à sua conta do [!DNL Mixpanel]. Consulte a [[!DNL Mixpanel] documentação de contas de serviço](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) para obter mais informações. | `Test8.6d4ee7.mp-service-account` |
| Senha | A senha da conta de serviço que corresponde à sua conta do [!DNL Mixpanel]. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID do projeto | A ID do projeto [!DNL Mixpanel]. Essa ID é necessária para criar uma conexão de origem. Consulte a [[!DNL Mixpanel] documentação de configurações do projeto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) e o [[!DNL Mixpanel] manual sobre como criar e gerenciar projetos](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) para obter mais informações. | `2384945` |
| Fuso Horário | O fuso horário que corresponde ao seu projeto [!DNL Mixpanel]. O fuso horário é necessário para criar uma conexão de origem. Consulte a [documentação de configurações do projeto do Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) para obter mais informações. | `Pacific Standard Time` |

Para obter mais informações sobre como autenticar sua origem [!DNL Mixpanel], consulte a [[!DNL Mixpanel] visão geral da origem](../../../../connectors/analytics/mixpanel.md).

## Conectar sua conta do [!DNL Mixpanel]

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Analytics*, selecione [!DNL Mixpanel] e **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

A página **[!UICONTROL Connect Mixpanel account]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Mixpanel] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde algum tempo para a nova conexão ser estabelecida.

![novo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Selecione a ID do projeto e o fuso horário {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Definir um fuso horário para a ingestão do Mixpanel"
>abstract="O fuso horário deve ser o mesmo que o da configuração de fuso horário do perfil do Mixpanel, pois a Experience Platform usa o fuso horário do projeto designado para assimilar dados relevantes do Mixpanel. O Mixpanel ajustará o fuso horário de acordo com o fuso horário do projeto antes de gravar o evento em um armazenamento de dados do Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=pt-BR#project-id-and-timezone" text="Saiba mais na documentação"

Depois que a origem for autenticada, forneça a ID do projeto e o fuso horário e selecione **[!UICONTROL Select]**.

O fuso horário que você designar antes de assimilar seus dados do [!DNL Mixpanel] na Experience Platform deve ser o mesmo que sua configuração de fuso horário do perfil [!DNL Mixpanel]. Quaisquer alterações no fuso horário dos dados serão aplicadas apenas a eventos novos e eventos antigos permanecerão no fuso horário designado anteriormente. O [!DNL Mixpanel] acomoda o horário de verão e ajustará adequadamente o carimbo de data e hora de assimilação. Para obter mais informações sobre como os fusos horários afetam seus dados, consulte o guia [!DNL Mixpanel] em [gerenciando fusos horários de projetos](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Após alguns minutos, a interface correta é atualizada para um painel de visualização, permitindo que você inspecione o esquema antes de criar um fluxo de dados. Quando terminar, selecione **[!UICONTROL Next]**.

![configuração](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Mixpanel]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de análise para o Experience Platform](../../dataflow/analytics.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL Mixpanel].

### Validação {#validation}

As etapas a seguir descrevem as etapas que você pode seguir para validar se conectou com êxito a origem do [!DNL Mixpanel] e se os eventos do [!DNL Mixpanel] estão sendo assimilados para o Experience Platform.

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Datasets]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Datasets]. A tela [!UICONTROL Dataset Activity] exibe os detalhes das execuções.

![atividade-conjunto-de-dados](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Em seguida, selecione a ID de execução do fluxo de dados que deseja exibir para ver detalhes específicos sobre essa execução do fluxo de dados.

![monitoramento de fluxo de dados](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Finalmente, selecione **[!UICONTROL Preview dataset]** para exibir os dados que foram assimilados.

![conjunto de dados de visualização](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Você pode verificar esses dados em relação aos dados na página [!DNL Mixpanel] > [!DNL Events]. Consulte o [[!DNL Mixpanel] documento sobre Eventos](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) para obter mais informações.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Esquema do Mixpanel

A tabela abaixo lista os mapeamentos suportados que devem ser configurados para [!DNL Mixpanel].

>[!TIP]
>
>Consulte [API de exportação de eventos > Baixar](https://developer.mixpanel.com/reference/raw-event-export) para obter mais informações sobre a API.


| Fonte | Tipo |
|---|---|
| `distinct_id` | sequência de caracteres |
| `event_name` | sequência de caracteres |
| `import` | booleano |
| `insert_id` | sequência de caracteres |
| `item_id` | sequência de caracteres |
| `item_name` | sequência de caracteres |
| `item_price` | sequência de caracteres |
| `mp_api_endpoint` | sequência de caracteres |
| `mp_api_timestamp_ms` | inteiro |
| `mp_processing_time_ms` | inteiro |
| `time` | inteiro |

### Limites {#limits}

* Você tem no máximo 100 consultas simultâneas e 60 consultas por hora, conforme indicado em [Exportar limites de taxa de API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
