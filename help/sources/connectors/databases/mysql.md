---
title: Visão geral do MySQL Source Connector
description: Saiba como conectar o MySQL ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: 16fe5340582dcea0ff40000fb516c1b72d5f150e
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL] é um sistema de gerenciamento de banco de dados relacional de código aberto usado para armazenar e gerenciar dados estruturados. Ele organiza os dados em tabelas e usa SQL (Structured Query Language) para consultar e atualizar informações. O [!DNL MySQL] é amplamente usado em aplicativos Web, oferece suporte a várias plataformas e é conhecido por sua velocidade, confiabilidade e facilidade de uso.

Você pode usar a origem [!DNL MySQL] para conectar sua conta e assimilar dados do banco de dados [!DNL MySQL] com a Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar sua conta do [!DNL MySQl] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure ou no Amazon Web Services (AWS). Leia o manual sobre [Como Experience Platform endereços IP da incluir na lista de permissões no Azure e no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar para o Experience Platform no Azure {#azure}

Você pode usar a autenticação de chave de conta ou a autenticação básica para conectar seu banco de dados do [!DNL MySQL] ao Experience Platform no Azure.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL MySQL] à Experience Platform usando a autenticação de chave de conta.

| Credencial | Descrição |
| --- | --- |
| `connectionString` | A cadeia de conexão [!DNL MySQL] associada à sua conta. O padrão da cadeia de conexão [!DNL MySQL] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL MySQL] é `26d738e0-8963-47ea-aadf-c60de735468a`. |

Para obter mais informações, leia a [[!DNL MySQL] documentação sobre cadeias de conexão](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB Autenticação básica]

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL MySQL] à Experience Platform usando a autenticação básica.

| Credencial | Descrição |
| --- | --- |
| `server` | O nome ou endereço IP do banco de dados [!DNL MySQL]. |
| `username` | O nome de usuário associado à autenticação do banco de dados do [!DNL MySQL]. |
| `password` | A senha associada à autenticação do banco de dados do [!DNL MySQL]. |
| `database` | O nome do banco de dados [!DNL MySQL] ao qual você deseja se conectar. |
| `sslMode` | O método [!DNL Secure Sockets Layer] (SSL) a ser aplicado à sua conexão. Os valores disponíveis são: <ul><li>`DISABLED`: Use esta opção para desabilitar o SSL. Se o servidor exigir uma configuração SSL, a conexão falhará</li><li>`PREFERRED`: use esta opção para preferir conexões SSL, pois o servidor oferece suporte a elas. Essa opção também permite conexões não SSL.</li><li>`REQUIRED`: use esta opção para tornar as conexões SSL obrigatórias. Se o servidor não suportar SSL, as conexões falharão.</li><li>`Verify-Ca`: Use esta opção para verificar certificados de servidor durante falha de conexão se o servidor não oferecer suporte a SSL.</li><li>`Verify Identity`: Use esta opção para verificar os certificados do servidor com o nome do host ao falhar as conexões se o servidor não oferecer suporte a SSL.</li></ul> |

>[!ENDTABS]

### Autenticar para o Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL MySQL] ao Experience Platform no AWS.

| Credencial | Descrição |
| --- | --- |
| `server` | O nome ou IP do banco de dados [!DNL MySQL]. |
| `username` | O nome do banco de dados. |
| `password` | O nome de usuário que corresponde ao banco de dados. |
| `database` | A senha que corresponde ao banco de dados. |
| `sslMode` | Um valor booleano que controla se o SSL é imposto ou não, dependendo do suporte do servidor. O padrão dessa configuração é `false`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL MySQL] é `26d738e0-8963-47ea-aadf-c60de735468a`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

## Conectar o [!DNL MySQL] ao Experience Platform usando APIs

- [Conectar o banco de dados  [!DNL MySQL]  usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/mysql.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o MySQL ao Experience Platform usando a interface

- [Conectar o banco de dados  [!DNL MySQL]  ao Experience Platform usando a interface](../../tutorials/ui/create/databases/mysql.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
