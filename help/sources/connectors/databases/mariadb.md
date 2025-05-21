---
title: Visão geral do MariaDB Source Connector
description: Saiba como conectar o MariaDB ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL MariaDB]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de um banco de dados de terceiros. [!DNL Experience Platform] pode se conectar a diferentes tipos de bancos de dados, como bancos relacionais, NoSQL ou data warehouses. O suporte para provedores de banco de dados inclui [!DNL MariaDB].

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar sua conta do [!DNL MariaDB] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar no Experience Platform

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL MariaDB] ao Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, forneça os valores apropriados para as credenciais a seguir.

| Credencial | Descrição |
| --- | --- |
| `connectionString` | A cadeia de conexão associada à sua autenticação [!DNL MariaDB]. O padrão da cadeia de conexão [!DNL MariaDB] é: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL MariaDB] é `3000eb99-cd47-43f3-827c-43caf170f015`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

Para obter mais informações sobre como obter uma cadeia de conexão, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Autenticação básica]

Para usar a autenticação básica, forneça os valores apropriados para as credenciais a seguir.

| Credencial | Descrição |
| --- | --- |
| `server` | O nome ou IP do banco de dados [!DNL MariaDB]. |
| `username` | O nome do banco de dados. |
| `port` | O número da porta do ponto de extremidade de comunicação ao qual você está se conectando. |
| `password` | O nome de usuário que corresponde ao banco de dados. |
| `database` | A senha que corresponde ao banco de dados. |
| `sslMode` | O método pelo qual os dados são criptografados durante a transferência. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL MariaDB] é `3000eb99-cd47-43f3-827c-43caf170f015`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

Para obter mais informações sobre como obter uma cadeia de conexão, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

## Conectar o [!DNL MariaDB] ao Experience Platform usando APIs

- [Criar uma conexão base MariaDB usando a API Serviço de fluxo](../../tutorials/api/create/databases/mariadb.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar o [!DNL MariaDB] ao Experience Platform usando a interface

- [Criar uma conexão de origem MariaDB na interface](../../tutorials/ui/create/databases/mariadb.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
