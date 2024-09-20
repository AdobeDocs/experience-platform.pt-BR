---
title: Criar uma conexão do Google Big Query Source na interface
description: Saiba como criar uma conexão de origem do Google Big Query usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Google BigQuery] na interface

>[!IMPORTANT]
>
>A origem [!DNL Google BigQuery] está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Leia este tutorial para saber como conectar sua conta do [!DNL Google BigQuery] ao Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Google BigQuery] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Leia o [[!DNL Google BigQuery] guia de autenticação](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) para obter as etapas detalhadas sobre como coletar as credenciais necessárias.

## Conectar sua conta do Google BigQuery

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Bancos de dados], selecione **[!UICONTROL Google BigQuery]** e **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes com o Google BigQuery selecionado.](../../../../images/tutorials/create/google-big-query/catalog.png)

A página **[!UICONTROL Conectar-se ao Google Big Query]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Google BigQuery] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![A página de conta existente onde uma lista de contas existentes é apresentada.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para sua nova conta [!DNL Google BigQuery].

![A nova interface de conta no fluxo de trabalho de origens.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB Usar autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]** e forneça valores para seu [projeto, ID do cliente, segredo do cliente, token de atualização e ID de conjunto de dados de resultados grandes (opcional)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A nova interface de conta onde a autenticação básica está selecionada.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Usar autenticação de serviço]

Para usar a autenticação de serviço, selecione **[!UICONTROL Autenticação de Serviço]** e forneça valores para sua [ID de projeto, conteúdo de arquivo de chave e ID de conjunto de dados de resultados grandes (opcional)](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A nova interface de conta onde a autenticação de serviço está selecionada.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Google BigQuery]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/databases.md).
