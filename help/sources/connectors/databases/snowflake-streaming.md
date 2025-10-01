---
title: Visão geral do Snowflake Streaming Source Connector
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da sua instância do Snowflake para a Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 0d646136da2c508fe7ce99a15787ee15c5921a6c
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 3%

---

# Fonte de transmissão [!DNL Snowflake]

>[!IMPORTANT]
>
>* A fonte de transmissão [!DNL Snowflake] está disponível na API para usuários que compraram o Real-Time CDP Ultimate.
>
>* Agora você pode usar a fonte de streaming [!DNL Snowflake] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para a transmissão de dados de um banco de dados [!DNL Snowflake].

## Compreendendo a fonte de streaming [!DNL Snowflake]

A fonte de transmissão [!DNL Snowflake] funciona com dados carregados executando periodicamente uma consulta SQL e criando um registro de saída para cada linha no conjunto resultante.

Ao usar o [!DNL Kafka Connect], a fonte de streaming [!DNL Snowflake] rastreia o registro mais recente que recebe de cada tabela, para que possa iniciar no local correto para a próxima iteração. A fonte usa essa funcionalidade para filtrar dados e obter apenas as linhas atualizadas de uma tabela em cada iteração.

## Pré-requisitos

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes que você possa transmitir dados do banco de dados do [!DNL Snowflake] para o Experience Platform:

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

A documentação abaixo fornece informações sobre como conectar o [!DNL Amazon Redshift] ao Experience Platform usando APIs ou a interface do usuário:

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Snowflake], você deve fornecer as seguintes propriedades de conexão:

>[!BEGINTABS]

>[!TAB Autenticação básica]

| Credencial | Descrição |
| --- | --- |
| `account` | O identificador de conta completo (nome da conta ou localizador de conta) da sua conta do [!DNL Snowflake] foi acrescentado com o sufixo `snowflakecomputing.com`. O identificador da conta pode ter diferentes formatos: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (por exemplo, `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (por exemplo, `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (por exemplo, `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Para obter mais informações, leia o [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |
| `database` | O banco de dados [!DNL Snowflake] contém os dados que você deseja trazer para a Experience Platform. |
| `username` | O nome de usuário da conta [!DNL Snowflake]. |
| `password` | A senha da conta de usuário [!DNL Snowflake]. |
| `role` | (Opcional) Uma função definida personalizada que pode ser fornecida para um usuário, para uma determinada conexão. Se não for fornecido, o padrão será `public`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Snowflake] é `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, você deve gerar um par de chaves RSA de 2048 bits e fornecer os seguintes valores ao criar uma conta para sua origem [!DNL Snowflake].

| Credencial | Descrição |
| --- | --- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia o guia em [recuperando seu [!DNL Snowflake] identificador de conta](./snowflake.md#retrieve-your-account-identifier) para obter orientação adicional. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | O nome de usuário da sua conta [!DNL Snowflake]. |
| `privateKey` | A chave privada [!DNL Base64-]codificada da sua conta [!DNL Snowflake]. Você pode gerar chaves privadas criptografadas ou não. Se você estiver usando uma chave privada criptografada, também deverá fornecer uma senha de chave privada ao autenticar no Experience Platform. Leia o guia em [recuperando sua [!DNL Snowflake] chave privada](./snowflake.md) para obter mais informações. |
| `passphrase` | A senha é uma camada adicional de segurança que você deve usar ao autenticar com uma chave privada criptografada. Não é necessário fornecer a senha se você estiver usando uma chave privada não criptografada. |
| `database` | O banco de dados [!DNL Snowflake] que contém os dados que você deseja assimilar na Experience Platform. |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |

Para obter mais informações sobre esses valores, consulte o [[!DNL Snowflake] guia de autenticação de par de chaves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recupere o identificador da sua conta {#retrieve-your-account-identifier}

Para autenticar sua instância do [!DNL Snowflake] com o Experience Platform, obtenha o identificador de conta no painel da interface do usuário do [!DNL Snowflake].

Siga estas etapas para encontrar o identificador da conta:

* Navegue até sua conta no [[!DNL Snowflake] painel da interface do usuário do aplicativo](https://app.snowflake.com/).
* Na navegação à esquerda, selecione **[!DNL Accounts]**, seguido por **[!DNL Active Accounts]** no cabeçalho.
* Em seguida, selecione o ícone de informações e selecione e copie o nome de domínio do URL atual.

### Recuperar sua chave privada {#retrieve-your-private-key}

Se você planeja usar a autenticação de par de chaves para sua conexão do [!DNL Snowflake], é necessário gerar uma chave privada antes de se conectar ao Experience Platform.

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

Depois de gerar sua chave privada, codifique-a diretamente no [!DNL Base64] sem fazer alterações no formato ou conteúdo. Antes de codificar, verifique se não há espaços extras ou linhas em branco (incluindo novas linhas à direita) no final da chave privada.

### Verificar configurações

Antes de criar uma conexão de origem para seus dados do [!DNL Snowflake], você também deve garantir que as seguintes configurações sejam atendidas:

* O depósito padrão atribuído a um determinado usuário deve ser igual ao depósito inserido ao autenticar no Experience Platform.
* A função padrão atribuída a um determinado usuário deve ter acesso ao mesmo banco de dados inserido ao autenticar no Experience Platform.

Para verificar sua função e depósito:

* Selecione **[!DNL Admin]** na navegação à esquerda e **[!DNL Users & Roles]**.
* Selecione o usuário apropriado e, em seguida, selecione as reticências (`...`) no canto superior direito.
* Na janela [!DNL Edit user] que aparece, navegue até [!DNL Default Role] para exibir a função associada ao usuário fornecido.
* Na mesma janela, navegue até [!DNL Default Warehouse] para exibir o depósito associado ao usuário especificado.

Depois de codificada com êxito, você pode usar essa chave privada codificada em [!DNL Base64] no Experience Platform para autenticar sua conta do [!DNL Snowflake].

### Definir configurações de função {#configure-role-settings}

Você deve configurar privilégios para uma função, mesmo que a função pública padrão seja atribuída, para permitir que sua conexão de origem acesse o banco de dados, o esquema e a tabela [!DNL Snowflake] relevantes. Os vários privilégios para diferentes entidades [!DNL Snowflake] são os seguintes:

| Entidade [!DNL Snowflake] | Exigir privilégio de função |
| --- | --- |
| Warehouse | OPERAR, USO |
| Banco de dados | USO |
| Esquema | USO |
| Tabela | SELECIONE |

>[!NOTE]
>
>O reinício automático e a suspensão automática devem estar ativados na configuração avançada do seu warehouse.

Para obter mais informações sobre o gerenciamento de funções e privilégios, consulte a [[!DNL Snowflake] Referência da API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitações e perguntas frequentes {#limitations-and-frequently-asked-questions}

* A taxa de transferência de dados para a origem [!DNL Snowflake] é de 2000 registros por segundo.
* A precificação pode variar dependendo da quantidade de tempo em que um depósito está ativo e do tamanho do depósito. Para a integração de origem [!DNL Snowflake], o menor warehouse, de tamanho x-pequeno, é suficiente. Sugere-se ativar a suspensão automática para que o depósito possa suspender por conta própria quando não estiver em uso.
* A origem [!DNL Snowflake] pesquisa o banco de dados em busca de novos dados a cada 10 segundos.
* Opções de configuração:
   * Você pode habilitar um sinalizador booleano `backfill` para sua origem [!DNL Snowflake] ao criar uma conexão de origem.
      * Se o preenchimento retroativo for definido como verdadeiro, o valor de timestamp.initial será definido como 0. Isso significa que os dados com uma coluna de carimbo de data e hora maior que 0 época são buscados.
      * Se o preenchimento retroativo for definido como falso, o valor de timestamp.initial será definido como -1. Isso significa que os dados com uma coluna de carimbo de data e hora maior que a hora atual (a hora em que a fonte começa a assimilar) são buscados.
   * A coluna de carimbo de data/hora deve ser formatada como tipo: `TIMESTAMP_LTZ` ou `TIMESTAMP_NTZ`. Se a coluna de carimbo de data/hora estiver definida como `TIMESTAMP_NTZ`, o fuso horário correspondente no qual os valores são armazenados deverá ser passado por meio do parâmetro `timezoneValue`. Se não fornecido, o valor padrão será UTC.
      * `TIMESTAMP_TZ` não pode ser usada uma coluna de carimbo de data/hora ou em um mapeamento.

## Próximas etapas

>[!NOTE]
>
>Depois de criar ou atualizar um fluxo de dados de transmissão, é necessária uma breve pausa de 5 minutos na assimilação de dados para evitar possíveis instâncias de perda ou perda de dados.

O tutorial a seguir fornece etapas sobre como conectar sua fonte de streaming do [!DNL Snowflake] ao Experience Platform usando a API:

* [Transmitir dados de um banco de dados  [!DNL Snowflake]  para o Experience Platform usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Transmitir dados de um banco de dados  [!DNL Snowflake]  para o Experience Platform usando o espaço de trabalho de origens na interface do usuário do Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
