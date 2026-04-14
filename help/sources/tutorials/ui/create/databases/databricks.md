---
title: Conectar databricks ao Experience Platform usando a interface do
description: Saiba como conectar Databricks ao Experience Platform usando a interface do usuário do.
exl-id: 877e22c0-cb77-45bb-88c9-54fdde2d6905
source-git-commit: 23b8d5d49e217d587dfe3d68631e6056c61b2cb8
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 4%

---

# Conectar o [!DNL Databricks] ao Experience Platform na interface

>[!AVAILABILITY]
>
>A origem [!DNL Databricks] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.

Leia este guia para saber como conectar sua conta do [!DNL Databricks] à Adobe Experience Platform usando o espaço de trabalho de fontes na interface do usuário.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Forneça valores para as credenciais a seguir para conectar [!DNL Databricks] ao Experience Platform.

| Credencial | Descrição |
| --- | --- |
| Domínio | A URL do espaço de trabalho [!DNL Databricks]. Por exemplo, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| ID do cluster | A ID do cluster em [!DNL Databricks]. Este cluster já deve ser um cluster existente e deve ser um cluster interativo. |
| Token de acesso | O token de acesso que autentica a conta do [!DNL Databricks]. Você pode gerar seu token de acesso usando o espaço de trabalho [!DNL Databricks]. |
| Banco de dados | O nome do banco de dados no lago delta. |

Para obter mais informações, leia a visão geral[&#128279;](../../../../connectors/databases/databricks.md) do [!DNL Databricks] .

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Sources]*. Escolha uma categoria ou use a barra de pesquisa para localizar sua fonte.

Para se conectar a [!DNL Databricks], vá para a categoria *[!UICONTROL Databases]*, selecione o cartão de origem **[!UICONTROL Azure Databricks]** e selecione **[!UICONTROL Set up]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Set up]** quando uma determinada origem ainda não tem uma conta autenticada. Depois que uma conta autenticada é criada, esta opção muda para **[!UICONTROL Add data]**.

![O catálogo de origens com o cartão de origem Azure Databricks selecionado.](../../../../images/tutorials/create/databricks/catalog.png)

### Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e depois selecione a conta [!DNL Azure Databricks] que deseja usar.

![A interface de contas existentes no fluxo de trabalho de origem com a opção &quot;Conta existente&quot; selecionada.](../../../../images/tutorials/create/databricks/existing.png)

### Criar uma nova conta

Para criar uma nova conta, selecione **[!UICONTROL New account]**, forneça um nome e, opcionalmente, adicione uma descrição para sua conta. Em seguida, forneça valores para as seguintes credenciais de autenticação:

* Domínio
* ID do cluster
* Token de acesso
* Banco de dados
* Catálogo

![A nova interface de conta no fluxo de trabalho de origem com um nome de conta e uma descrição opcional fornecidos.](../../../../images/tutorials/create/databricks/new.png)

Além disso, você deve copiar e colar suas credenciais do [!UICONTROL Staging SAS URI] no ambiente do [!DNL Azure Databricks]. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde alguns momentos para a conexão ser estabelecida.

![As credenciais de preparo do URI SAS.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Criar um fluxo de dados para dados de [!DNL Azure Databricks]

Agora que a conta do [!DNL Azure Databricks] foi conectada com êxito, você pode [criar um fluxo de dados e assimilar dados do banco de dados na Experience Platform](../../dataflow/databases.md).
