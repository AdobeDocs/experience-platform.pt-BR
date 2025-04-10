---
title: Visão geral do PostgreSQL Source Connector
description: Saiba mais sobre a fonte PostgreSQL no Adobe Experience Platform.
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 98d1bec3cd453f3a20b8871b891b5464ddd44a09
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

Leia este documento para saber mais sobre as etapas de pré-requisito que você precisa concluir antes de poder conectar seu banco de dados do [!DNL PostgreSQL] ao Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar o banco de dados do [!DNL PostgreSQL] ao Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure ou no Amazon Web Services (AWS). Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no Azure e no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar para o Experience Platform no Azure {#azure}

Você deve fornecer valores para as credenciais de autenticação a seguir para conectar [!DNL PostgreSQL] ao Experience Platform no Azure.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL PostgreSQL] ao Experience Platform no Azure usando a autenticação de chave de conta.

| Credencial | Descrição |
| --- | --- |
| `connectionString` | A cadeia de conexão associada à sua conta [!DNL PostgreSQL]. O padrão da cadeia de conexão [!DNL PostgreSQL] é: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL PostgreSQL] é `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Leia a [[!DNL PostgreSQL] documentação](https://www.postgresql.org/docs/current/) para obter mais informações.

>[!TAB Autenticação básica]

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL PostgreSQL] ao Experience Platform no Azure usando a autenticação básica.

| Credencial | Descrição |
| --- | --- |
| `server` | O nome ou endereço IP do banco de dados [!DNL PostgreSQL]. |
| `port` | A porta TCP do servidor [!DNL PostgreSQL]. |
| `username` | O nome de usuário associado à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `password` | A senha associada à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `database` | O nome do banco de dados [!DNL PostgreSQL] ao qual você deseja se conectar. |
| `sslMode` | O método [!DNL Secure Sockets Layer] (SSL) a ser aplicado à sua conexão. Os valores disponíveis são: <ul><li>`Disable`: Use esta opção para desabilitar o SSL. Se o servidor exigir uma configuração SSL, a conexão falhará.</li><li>`Allow`: Use esta opção para permitir conexões SSL. As conexões não SSL ainda poderão ser usadas se o servidor oferecer suporte a elas.</li><li>`Prefer`: use esta opção para preferir conexões SSL, pois o servidor oferece suporte a elas. Essa opção também permite conexões não SSL.</li><li>`Require`: use esta opção para tornar as conexões SSL obrigatórias. Se o servidor não suportar SSL, as conexões falharão.</li><li>`Verify-Ca`: Use esta opção para verificar certificados de servidor durante falha de conexão se o servidor não oferecer suporte a SSL.</li><li>`Verify-Full`: Use esta opção para verificar os certificados do servidor com o nome do host ao falhar as conexões se o servidor não oferecer suporte a SSL.</li></ul> |

Leia a [[!DNL PostgreSQL] documentação](https://www.postgresql.org/docs/current/) para obter mais informações.

>[!ENDTABS]

### Autenticar para o Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

Forneça valores para as credenciais a seguir para conectar o banco de dados do [!DNL PostgreSQL] ao Experience Platform no AWS usando a autenticação básica.

| Credencial | Descrição |
| --- | --- |
| `server` | O nome ou endereço IP do banco de dados [!DNL PostgreSQL]. |
| `port` | A porta TCP do servidor [!DNL PostgreSQL]. |
| `username` | O nome de usuário associado à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `password` | A senha associada à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `database` | O nome do banco de dados [!DNL PostgreSQL] ao qual você deseja se conectar. |
| `sslMode` | O método [!DNL Secure Sockets Layer] (SSL) a ser aplicado à sua conexão. Os valores disponíveis são: <ul><li>`Disable`: Use esta opção para desabilitar o SSL. Se o servidor exigir uma configuração SSL, a conexão falhará.</li><li>`Allow`: Use esta opção para permitir conexões SSL. As conexões não SSL ainda poderão ser usadas se o servidor oferecer suporte a elas.</li><li>`Prefer`: use esta opção para preferir conexões SSL, pois o servidor oferece suporte a elas. Essa opção também permite conexões não SSL.</li><li>`Require`: use esta opção para tornar as conexões SSL obrigatórias. Se o servidor não suportar SSL, as conexões falharão.</li><li>`Verify-Ca`: Use esta opção para verificar certificados de servidor durante falha de conexão se o servidor não oferecer suporte a SSL.</li><li>`Verify-Full`: Use esta opção para verificar os certificados do servidor com o nome do host ao falhar as conexões se o servidor não oferecer suporte a SSL.</li></ul> |

Leia a [[!DNL PostgreSQL] documentação](https://www.postgresql.org/docs/current/) para obter mais informações.

## Conectar o [!DNL PostgreSQL] ao Experience Platform usando APIs

* [Criar uma conexão base  [!DNL PostgreSQL]  usando a API de Serviço de Fluxo](../../tutorials/api/create/databases/postgres.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL PostgreSQL] ao Experience Platform usando a interface

* [Criar uma conexão de origem  [!DNL PostgreSQL]  na interface](../../tutorials/ui/create/databases/postgres.md)
* [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
