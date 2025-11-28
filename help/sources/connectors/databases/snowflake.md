---
title: Visão geral do Snowflake Source Connector
description: Saiba como conectar o Snowflake ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 1%

---

# [!DNL Snowflake] origem

>[!IMPORTANT]
>
>* A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.
>* Por padrão, a origem [!DNL Snowflake] interpreta `null` como uma cadeia de caracteres vazia. Entre em contato com o representante da Adobe para garantir que os valores de `null` sejam gravados corretamente como `null` no Adobe Experience Platform.
>* Para que o Experience Platform assimile dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para a origem [!DNL Snowflake] é TIMESTAMP_NTZ com a hora UTC.

[!DNL Snowflake] é uma plataforma de data warehouse baseada em nuvem projetada para permitir que as organizações armazenem, processem e analisem grandes volumes de dados com eficiência. Criado para aproveitar a escalabilidade e a flexibilidade da nuvem, o [!DNL Snowflake] oferece suporte à integração de dados, à análise avançada e ao compartilhamento contínuo entre equipes. Como um serviço totalmente gerenciado, o [!DNL Snowflake] elimina as complexidades de manutenção comuns aos bancos de dados tradicionais, permitindo que você se concentre em obter insights e valor de seus dados.

Você pode usar a origem [!DNL Snowflake] para se conectar e trazer seus dados do [!DNL Snowflake] para a Adobe Experience Platform. Leia a documentação abaixo para saber como configurar sua origem do [!DNL Snowflake] e se conectar ao Experience Platform.

## Pré-requisitos {#prerequisites}

Esta seção descreve as tarefas de instalação que devem ser concluídas para que você possa conectar sua origem do [!DNL Snowflake] à Experience Platform.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes propriedades de credencial para autenticar sua origem [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Autenticação de chave de conta (Azure)]

Forneça valores para as credenciais a seguir para conectar [!DNL Snowflake] ao Experience Platform no Azure usando a autenticação de chave de conta.

| Credencial | Descrição |
| ---------- | ----------- |
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `myorg-myaccount.snowflakecomputing.com`. Leia a seção sobre [recuperação do [!DNL Snowflake] identificador de conta](#retrieve-your-account-identifier) para obter orientações adicionais. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `myorg-myaccount.snowflakecomputing.com`. Leia a seção sobre [recuperação do [!DNL Snowflake] identificador de conta](#retrieve-your-account-identifier) para obter orientações adicionais. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `http://myorg-myaccount.snowflakecomputing.com/`. Leia o guia em [recuperando seu [!DNL Snowflake] identificador de conta](#etrieve-your-account-identifier) para obter orientação adicional. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | O nome de usuário da sua conta [!DNL Snowflake]. |
| `privateKey` | A chave privada do usuário [!DNL Snowflake], codificada em base64 como uma linha única sem cabeçalhos ou quebras de linha. Para prepará-lo, copie o conteúdo do arquivo PEM, remova as linhas `BEGIN`/`END` e todas as quebras de linha e, em seguida, codifique o resultado em base64. Leia a seção sobre [recuperando sua chave privada](#retrieve-your-private-key) para obter mais informações. **Observação:** chaves privadas criptografadas não têm suporte no momento para uma conexão AWS. |
| `port` | O número da porta usada por [!DNL Snowflake] ao se conectar a um servidor pela Internet. |
| `database` | O banco de dados [!DNL Snowflake] que contém os dados que você deseja assimilar na Experience Platform. |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a Experience Platform. |

Para obter mais informações sobre esses valores, consulte o [[!DNL Snowflake] guia de autenticação de par de chaves](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recupere o identificador da sua conta {#retrieve-your-account-identifier}

Você deve recuperar o identificador da conta no painel da interface do usuário do [!DNL Snowflake], pois você o usará para autenticar sua instância do [!DNL Snowflake] no Experience Platform.

Para recuperar o identificador da conta:

* Use o [[!DNL Snowflake] painel da interface do usuário do aplicativo](https://app.snowflake.com/) para acessar sua conta.
* Na navegação à esquerda, selecione **[!DNL Accounts]** e, em seguida, selecione **[!DNL Active Accounts]** no cabeçalho.
* Em seguida, selecione o ícone de informações e selecione e copie o nome de domínio do URL atual.

![O painel da interface do usuário do Snowflake com o nome de domínio selecionado.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Gerar seu par de chaves RSA

Use o OpenSSL na interface de linha de comando para gerar um par de chaves RSA de 2048 bits no formato PKCS#8. É uma prática recomendada criar uma chave privada criptografada para segurança, o que exigirá uma senha.

>[!BEGINTABS]

>[!TAB Gerar uma chave privada criptografada]

Para gerar sua chave privada [!DNL Snowflake] criptografada, execute o seguinte comando no terminal:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Gerar uma chave privada não criptografada]

Para gerar sua chave privada [!DNL Snowflake] não criptografada, execute o seguinte comando no terminal:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Gerar uma chave pública a partir de sua chave privada

Em seguida, execute o seguinte comando na interface da linha de comando para criar uma chave pública com base na sua chave privada.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Atribuir a chave pública ao usuário [!DNL Snowflake]

Você precisa usar uma função de administrador [!DNL Snowflake] (como **SECURITYADMIN**) para associar a chave pública gerada ao usuário de serviço [!DNL Snowflake] que a Experience Platform usará. Para recuperar o conteúdo da chave pública, abra o arquivo `rsa_key.pub` e copie o conteúdo inteiro, excluindo as linhas `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`. Em seguida, execute o seguinte SQL em [!DNL Snowflake]:

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Codificar a chave privada em [!DNL Base64]

O Experience Platform exige que a chave privada seja codificada em [!DNL Base64] e fornecida como uma cadeia de caracteres durante a configuração da conexão. Use uma ferramenta ou um script adequado para codificar o conteúdo do arquivo `rsa_key.p8` em uma única cadeia de caracteres [!DNL Base64].

>[!TIP]
>
>Verifique se não há espaços extras ou quebras de linha, incluindo as linhas de cabeçalho/rodapé `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`, antes ou depois do processo de codificação, pois isso pode causar erros de autenticação.

### Verificar configurações

Antes de criar a conexão de origem [!DNL Snowflake] no Experience Platform, verifique se o **[!DNL Default Role]** e o **[!DNL Default Warehouse]** do usuário correspondem aos valores fornecidos no Experience Platform. Você pode verificar essas configurações na interface do usuário [!DNL Snowflake] usando o comando SQL `DESCRIBE USER {USERNAME}`.

Como alternativa, siga as etapas abaixo para verificar suas configurações:

* Selecione **[!DNL Admin]** na navegação à esquerda e **[!DNL Users & Roles]**.
* Selecione o usuário apropriado e, em seguida, selecione as reticências (`...`) no canto superior direito.
* Na janela [!DNL Edit user] que aparece, navegue até [!DNL Default Role] para exibir a função associada ao usuário fornecido.
* Na mesma janela, navegue até [!DNL Default Warehouse] para exibir o depósito associado ao usuário especificado.

![A interface do usuário do Snowflake na qual você pode verificar sua função e seu depósito.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Próximas etapas

Com a configuração concluída, você pode prosseguir para conectar a conta do [!DNL Snowflake] à Experience Platform. Leia a documentação a seguir para obter mais informações:

### Conectar o [!DNL Snowflake] ao Experience Platform usando APIs

* [Conectar  [!DNL Snowflake]  ao Experience Platform usando a API](../../tutorials/api/create/databases/snowflake.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

### Conectar o [!DNL Snowflake] ao Experience Platform usando a interface

* [Conectar [!DNL Snowflake] ao Experience Platform usando a interface](../../tutorials/ui/create/databases/snowflake.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
