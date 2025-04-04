---
title: Visão geral do Snowflake Source Connector
description: Saiba como conectar o Snowflake ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Snowflake] origem

>[!IMPORTANT]
>
>* A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.
>* Por padrão, a origem [!DNL Snowflake] interpreta `null` como uma cadeia de caracteres vazia. Entre em contato com o representante da Adobe para garantir que os valores de `null` sejam gravados corretamente como `null` no Adobe Experience Platform.
>* Para que o Experience Platform assimile dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para a origem [!DNL Snowflake] é TIMESTAMP_NTZ com a hora UTC.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. O Experience Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Snowflake].

## Pré-requisitos {#prerequisites}

Esta seção descreve as tarefas de instalação que devem ser concluídas para que você possa conectar sua origem do [!DNL Snowflake] à Experience Platform.

### Recupere o identificador da sua conta {#retrieve-your-account-identifier}

Você deve recuperar o identificador de conta do painel da interface do usuário do [!DNL Snowflake] porque você usará o identificador de conta para autenticar sua instância do [!DNL Snowflake] no Experience Platform.

Para recuperar o identificador da conta:

* Navegue até sua conta no [[!DNL Snowflake] painel da interface do usuário do aplicativo](https://app.snowflake.com/).
* Na navegação à esquerda, selecione **[!DNL Accounts]**, seguido por **[!DNL Active Accounts]** no cabeçalho.
* Em seguida, selecione o ícone de informações e selecione e copie o nome de domínio do URL atual.

![O painel da interface do usuário do Snowflake com o nome de domínio selecionado.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Recuperar sua chave privada {#retrieve-your-private-key}

Se você estiver usando a autenticação de par de chaves para a conexão do [!DNL Snowflake], também deverá gerar sua chave privada antes de se conectar ao Experience Platform.

>[!BEGINTABS]

>[!TAB Criar uma chave privada criptografada]

Para gerar sua chave privada [!DNL Snowflake] criptografada, execute o seguinte comando no terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Se tiver êxito, você deverá receber sua chave privada no formato PEM.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Criar uma chave privada não criptografada]

Para gerar sua chave privada [!DNL Snowflake] não criptografada, execute o seguinte comando no terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Se tiver êxito, você deverá receber sua chave privada no formato PEM.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Em seguida, pegue sua chave privada e codifique-a em [!DNL Base64]. Certifique-se de não fazer transformações ou conversões de formato na chave privada do [!DNL Snowflake]. Além disso, você deve garantir que não haja caracteres de nova linha no final da chave privada, antes de codificá-la em [!DNL Base64].

### Verificar configurações

Antes de criar uma conexão de origem para seus dados do [!DNL Snowflake], você também deve garantir que as seguintes configurações sejam atendidas:

* O depósito padrão atribuído a um determinado usuário deve ser igual ao depósito inserido ao autenticar no Experience Platform.
* A função padrão atribuída a um determinado usuário deve ter acesso ao mesmo banco de dados inserido ao autenticar no Experience Platform.

Para verificar sua função e depósito:

* Selecione **[!DNL Admin]** na navegação à esquerda e **[!DNL Users & Roles]**.
* Selecione o usuário apropriado e, em seguida, selecione as reticências (`...`) no canto superior direito.
* Na janela [!DNL Edit user] que aparece, navegue até [!DNL Default Role] para exibir a função associada ao usuário fornecido.
* Na mesma janela, navegue até [!DNL Default Warehouse] para exibir o depósito associado ao usuário especificado.

![A interface do usuário do Snowflake na qual você pode verificar sua função e seu depósito.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Depois de codificada com êxito, você pode usar essa chave privada codificada em [!DNL Base64] no Experience Platform para autenticar sua conta do [!DNL Snowflake].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

A documentação abaixo fornece informações sobre como conectar o [!DNL Snowflake] ao Experience Platform usando APIs ou a interface do usuário:

## Conectar o [!DNL Snowflake] ao Experience Platform usando APIs

* [Criar uma conexão básica do Snowflake usando a API do serviço de fluxo](../../tutorials/api/create/databases/snowflake.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL Snowflake] ao Experience Platform usando a interface

* [Criar uma conexão de origem do Snowflake na interface](../../tutorials/ui/create/databases/snowflake.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
