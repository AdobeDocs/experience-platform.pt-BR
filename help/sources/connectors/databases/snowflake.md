---
title: Visão geral do Snowflake Source Connector
description: Saiba como conectar o Snowflake ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# [!DNL Snowflake] origem

>[!IMPORTANT]
>
>* A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.
>* Por padrão, a origem [!DNL Snowflake] interpreta `null` como uma cadeia de caracteres vazia. Entre em contato com o representante da Adobe para garantir que os valores de `null` sejam gravados corretamente como `null` no Adobe Experience Platform.
>* Para que o Experience Platform assimile dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para a origem [!DNL Snowflake] é TIMESTAMP_NTZ com a hora UTC.

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. O Experience Platform pode se conectar a diferentes tipos de bancos de dados, como bancos de dados relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL Snowflake].

## Pré-requisitos {#prerequisites}

Esta seção descreve as tarefas de instalação que devem ser concluídas para que você possa conectar sua origem do [!DNL Snowflake] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes propriedades de credencial para autenticar sua origem [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Autenticação de chave de conta (Azure)]

Forneça valores para as credenciais a seguir para conectar [!DNL Snowflake] ao Experience Platform no Azure usando a autenticação de chave de conta.

| Credencial | Descrição |
| ---------- | ----------- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia a seção sobre [recuperação do [!DNL Snowflake] identificador de conta](#retrieve-your-account-identifier) para obter orientações adicionais. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |
| `database` | O banco de dados [!DNL Snowflake] contém os dados que você deseja trazer para a Experience Platform. |
| `username` | O nome de usuário da conta [!DNL Snowflake]. |
| `password` | A senha da conta de usuário [!DNL Snowflake]. |
| `role` | A função de controle de acesso padrão a ser usada na sessão [!DNL Snowflake]. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| `connectionString` | A cadeia de conexão usada para se conectar à sua instância do [!DNL Snowflake]. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Autenticação de par de chaves (Azure)]

Para usar a autenticação de par de chaves, gere primeiro um par de chaves RSA de 2048 bits. Em seguida, forneça valores para as credenciais a seguir para se conectar ao Experience Platform no Azure usando a autenticação de par de chaves.

| Credencial | Descrição |
| --- | --- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia a seção sobre [recuperação do [!DNL Snowflake] identificador de conta](#retrieve-your-account-identifier) para obter orientações adicionais. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | O nome de usuário da sua conta [!DNL Snowflake]. |
| `privateKey` | A chave privada [!DNL Base64-]codificada da sua conta [!DNL Snowflake]. Você pode gerar chaves privadas criptografadas ou não. Se você estiver usando uma chave privada criptografada, também deverá fornecer uma senha de chave privada ao autenticar no Experience Platform. Leia a seção sobre [recuperando sua chave privada](#retrieve-your-private-key) para obter mais informações. |
| `privateKeyPassphrase` | A senha da chave privada é uma camada adicional de segurança que deve ser usada ao autenticar com uma chave privada criptografada. Não é necessário fornecer a senha se você estiver usando uma chave privada não criptografada. |
| `port` | O número da porta usada por [!DNL Snowflake] ao se conectar a um servidor pela Internet. |
| `database` | O banco de dados [!DNL Snowflake] que contém os dados que você deseja assimilar na Experience Platform. |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |

Para obter mais informações sobre esses valores, consulte o [[!DNL Snowflake] guia de autenticação de par de chaves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Autenticação básica (AWS)]

Forneça valores para as credenciais a seguir para conectar [!DNL Snowflake] ao Experience Platform no AWS usando a autenticação básica.

>[!WARNING]
>
>A autenticação básica (ou autenticação de chave de conta) para a origem [!DNL Snowflake] será substituída em novembro de 2025. Você deve migrar para a autenticação baseada em par de chaves para continuar usando a origem e assimilando dados do banco de dados para o Experience Platform. Para obter mais informações sobre a descontinuação, leia o [[!DNL Snowflake] manual de práticas recomendadas sobre como mitigar os riscos de comprometimento de credenciais](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Credencial | Descrição |
| --- | --- |
| `host` | A URL de host à qual sua conta do [!DNL Snowflake] se conecta. |
| `port` | O número da porta usada por [!DNL Snowflake] ao se conectar a um servidor pela Internet. |
| `username` | O nome de usuário associado à sua conta [!DNL Snowflake]. |
| `password` | A senha associada à sua conta [!DNL Snowflake]. |
| `database` | O banco de dados [!DNL Snowflake] de onde os dados serão extraídos. |
| `schema` | O nome do esquema associado ao banco de dados [!DNL Snowflake]. Você deve garantir que o usuário ao qual deseja conceder acesso ao banco de dados também tenha acesso a esse esquema. |
| `warehouse` | O warehouse [!DNL Snowflake] que você está usando. |

>[!TAB Autenticação de par de chaves (AWS)]

Para usar a autenticação de par de chaves, gere primeiro um par de chaves RSA de 2048 bits. Em seguida, forneça valores para as credenciais a seguir para se conectar ao Experience Platform no AWS usando a autenticação de par de chaves.

| Credencial | Descrição |
| --- | --- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia o guia em [recuperando seu [!DNL Snowflake] identificador de conta](#etrieve-your-account-identifier) para obter orientação adicional. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | O nome de usuário da sua conta [!DNL Snowflake]. |
| `privateKey` | A chave privada do usuário [!DNL Snowflake], codificada em base64 como uma linha única sem cabeçalhos ou quebras de linha. Para prepará-lo, copie o conteúdo do arquivo PEM, remova as linhas `BEGIN`/`END` e todas as quebras de linha e, em seguida, codifique o resultado em base64. Leia a seção sobre [recuperando sua chave privada](#retrieve-your-private-key) para obter mais informações. **Observação:** chaves privadas criptografadas não têm suporte no momento para uma conexão AWS. |
| `port` | O número da porta usada por [!DNL Snowflake] ao se conectar a um servidor pela Internet. |
| `database` | O banco de dados [!DNL Snowflake] que contém os dados que você deseja assimilar na Experience Platform. |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |

Para obter mais informações sobre esses valores, consulte o [[!DNL Snowflake] guia de autenticação de par de chaves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

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

A documentação abaixo fornece informações sobre como conectar o [!DNL Snowflake] ao Experience Platform usando APIs ou a interface do usuário:

## Conectar o [!DNL Snowflake] ao Experience Platform usando APIs

* [Criar uma conexão básica do Snowflake usando a API do serviço de fluxo](../../tutorials/api/create/databases/snowflake.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL Snowflake] ao Experience Platform usando a interface

* [Criar uma conexão de origem do Snowflake na interface](../../tutorials/ui/create/databases/snowflake.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
