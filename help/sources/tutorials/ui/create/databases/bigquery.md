---
title: Conectar [!DNL Google BigQuery] Ao Experience Platform Usando A Interface Do Usuário
description: Saiba como criar uma conexão de origem do Google Big Query usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Conectar o [!DNL Google BigQuery] ao Experience Platform usando a interface

>[!IMPORTANT]
>
>A origem [!DNL Google BigQuery] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Leia este tutorial para saber como conectar sua conta do [!DNL Google BigQuery] ao Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Google BigQuery] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Leia o [[!DNL Google BigQuery] guia de autenticação](../../../../connectors/databases/bigquery.md#prerequisites) para obter as etapas detalhadas sobre como coletar as credenciais necessárias.

## Navegar pelo catálogo de origens {#navigate}

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Fontes]*. Você pode selecionar a categoria apropriada no painel *[!UICONTROL Categorias]* Como alternativa, você pode usar a barra de pesquisa para navegar até a fonte específica que deseja usar.

Para usar [!DNL Google BigQuery], selecione o cartão de origem **[!UICONTROL Google BigQuery]** em *[!UICONTROL Bancos de dados]* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Após a criação de uma conta autenticada, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes com o Google BigQuery selecionado.](../../../../images/tutorials/create/google-big-query/catalog.png)

## Usar uma conta existente {#existing}

Para usar uma conta existente, selecione a conta [!DNL Google BigQuery] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![A página de conta existente onde uma lista de contas existentes é apresentada.](../../../../images/tutorials/create/google-big-query/existing.png)

## Criar uma nova conta {#create}

Se você não tiver uma conta existente, deverá criar uma nova conta fornecendo as credenciais de autenticação necessárias que correspondam à sua origem.

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e, opcionalmente, adicione uma descrição para sua conta.

![A nova interface de conta no fluxo de trabalho de origens.](../../../../images/tutorials/create/google-big-query/new.png)

### Conectar-se ao Experience Platform no Azure {#azure}

Você pode conectar sua conta do [!DNL Google BigQuery] ao Experience Platform no Azure usando a autenticação básica ou de serviço.

>[!BEGINTABS]

>[!TAB Usar autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]** e forneça valores para seu [projeto, ID do cliente, segredo do cliente, token de atualização e ID de conjunto de dados de resultados grandes (opcional)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A nova interface de conta onde a autenticação básica está selecionada.](../../../../images/tutorials/create/google-big-query/basic-auth.png)

>[!TAB Usar autenticação de serviço]

Para usar a autenticação de serviço, selecione **[!UICONTROL Autenticação de Serviço]** e forneça valores para sua [ID de projeto, conteúdo de arquivo de chave e ID de conjunto de dados de resultados grandes (opcional)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A nova interface de conta onde a autenticação de serviço está selecionada.](../../../../images/tutorials/create/google-big-query/service-auth.png)

>[!ENDTABS]

### Conectar-se ao Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Para criar uma nova conta do [!DNL Google BigQuery] e conectar-se ao Experience Platform no AWS, verifique se você está em uma sandbox VA6 e forneça as credenciais necessárias para autenticação.

* **ID do Projeto**: a ID do projeto que corresponde à sua conta do [!DNL Google BigQuery].
* **Conteúdo do arquivo de chave**: o arquivo de chave usado para autenticar a conta de serviço. Você pode recuperar este valor do [[!DNL Google Cloud service accounts] painel](https://console.cloud.google.com). O conteúdo principal do arquivo está no formato JSON. Você deve codificar isso em [!DNL Base64] ao autenticar no Experience Platform.
* **ID do conjunto de dados**: a ID do conjunto de dados [!DNL Google BigQuery]. Essa ID representa onde as tabelas de dados estão localizadas e deve ser pré-criada para permitir o suporte a grandes conjuntos de resultados.

![A nova interface de conta para uma conexão AWS.](../../../../images/tutorials/create/google-big-query/aws.png)

## Ignorar pré-visualização de dados de amostra {#skip-preview-of-sample-data}

Durante a etapa de seleção de dados, você pode encontrar um tempo limite ao assimilar tabelas ou arquivos de dados grandes. Você pode ignorar a visualização de dados para contornar o tempo limite e ainda visualizar o esquema, embora sem dados de amostra. Para ignorar a visualização de dados, habilite a opção **[!UICONTROL Ignorar visualização de dados de amostra]**.

O restante do workflow permanecerá o mesmo. O único problema é que ignorar a pré-visualização de dados pode impedir que campos calculados e obrigatórios sejam validados automaticamente durante a etapa de mapeamento e, em seguida, será necessário validar manualmente esses campos durante o mapeamento.

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Google BigQuery]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](../../dataflow/databases.md).
