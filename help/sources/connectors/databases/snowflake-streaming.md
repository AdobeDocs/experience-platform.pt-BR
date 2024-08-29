---
title: Visão geral do conector Source de transmissão Snowflake
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da instância do Snowflake para a Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: e8ab39ce085a95eac898f65667706b71bdadd350
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# Fonte de transmissão [!DNL Snowflake]

>[!IMPORTANT]
>
>* A fonte de streaming [!DNL Snowflake] está na versão beta. Leia a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.
>* A fonte de transmissão [!DNL Snowflake] está disponível na API para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para streaming de dados de um banco de dados [!DNL Snowflake].

## Compreendendo a fonte de streaming [!DNL Snowflake]

A fonte de transmissão [!DNL Snowflake] funciona com dados carregados executando periodicamente uma consulta SQL e criando um registro de saída para cada linha no conjunto resultante.

Ao usar o [!DNL Kafka Connect], a fonte de streaming [!DNL Snowflake] rastreia o registro mais recente que recebe de cada tabela, para que possa iniciar no local correto para a próxima iteração. A fonte usa essa funcionalidade para filtrar dados e obter apenas as linhas atualizadas de uma tabela em cada iteração.

## Pré-requisitos

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes que você possa transmitir dados do banco de dados do [!DNL Snowflake] para o Experience Platform:

### Atualizar sua lista de permissões de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources) para obter mais informações.

A documentação abaixo fornece informações sobre como conectar o [!DNL Amazon Redshift] à Plataforma usando APIs ou a interface do usuário:

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Snowflake], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `account` | O identificador de conta completo (nome da conta ou localizador de conta) da sua conta do [!DNL Snowflake] foi acrescentado com o sufixo `snowflakecomputing.com`. O identificador da conta pode ter diferentes formatos: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (por exemplo, `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (por exemplo, `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (por exemplo, `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Para obter mais informações, leia o [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a plataforma. |
| `database` | O banco de dados [!DNL Snowflake] contém os dados que você deseja trazer para a Plataforma. |
| `username` | O nome de usuário da conta [!DNL Snowflake]. |
| `password` | A senha da conta de usuário [!DNL Snowflake]. |
| `role` | (Opcional) Uma função definida personalizada que pode ser fornecida para um usuário, para uma determinada conexão. Se não for fornecido, o padrão será `public`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Snowflake] é `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

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

O tutorial a seguir fornece etapas sobre como conectar sua fonte de transmissão do [!DNL Snowflake] ao Experience Platform usando a API:

* [Transmitir dados de um banco de dados  [!DNL Snowflake]  para o Experience Platform usando a API do Serviço de Fluxo](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Transmitir dados de um banco de dados  [!DNL Snowflake]  para o Experience Platform usando o espaço de trabalho de origens na interface de usuário do Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
