---
title: Visão geral do conector de origem de transmissão Snowflake
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da instância do Snowflake para a Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# [!DNL Snowflake] origem da transmissão

>[!IMPORTANT]
>
>* A variável [!DNL Snowflake] a fonte da transmissão está na versão beta. Leia as [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.
>* A variável [!DNL Snowflake] a fonte de transmissão está disponível no catálogo de fontes para clientes que compraram o Real-Time CDP Ultimate.


O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

Experience Platform fornece suporte para transmissão de dados de um [!DNL Snowflake] banco de dados.

## Compreender o [!DNL Snowflake] origem da transmissão

A variável [!DNL Snowflake] A fonte de transmissão funciona com dados carregados executando periodicamente uma consulta SQL e criando um registro de saída para cada linha no conjunto resultante.

Ao usar [!DNL Kafka Connect], o [!DNL Snowflake] a origem da transmissão rastreia o registro mais recente recebido de cada tabela, para que possa iniciar no local correto da próxima iteração. A fonte usa essa funcionalidade para filtrar dados e obter apenas as linhas atualizadas de uma tabela em cada iteração.

## Pré-requisitos

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes que você possa transmitir dados do seu [!DNL Snowflake] banco de dados para Experience Platform:

### Coletar credenciais necessárias

A fim de [!DNL Flow Service] para se conectar com [!DNL Snowflake], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `account` | O nome completo da conta associado à [!DNL Snowflake] conta. Um [!DNL Snowflake] o nome da conta inclui o nome da conta, a região e a plataforma de nuvem. Por exemplo, `cj12345.east-us-2.azure`. Para obter mais informações sobre nomes de conta, consulte esta [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| `database` | A variável [!DNL Snowflake] contém os dados que você deseja trazer para a Platform. |
| `username` | O nome de usuário para o [!DNL Snowflake] conta. |
| `password` | A senha para o [!DNL Snowflake] conta de usuário. |
| `role` | (Opcional) Uma função definida personalizada que pode ser fornecida para um usuário, para uma determinada conexão. Se não for fornecido, esse valor assumirá como padrão `public`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Snowflake] é `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Para obter mais informações sobre autenticação, consulte esta [[!DNL Snowflake] documento](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Definir configurações de função {#configure-role-settings}

Você deve configurar privilégios para uma função, mesmo que a função pública padrão seja atribuída, para permitir que sua conexão de origem acesse a relevante [!DNL Snowflake] banco de dados, esquema e tabela. Os vários privilégios para diferentes [!DNL Snowflake] é a seguinte:

| [!DNL Snowflake] entidade | Exigir privilégio de função |
| --- | --- |
| Warehouse | OPERAR, USO |
| Banco de dados | USO |
| Esquema | USO |
| Tabela | SELECIONE |

>[!NOTE]
>
>O reinício automático e a suspensão automática devem estar ativados na configuração avançada do seu warehouse.

Para obter mais informações sobre o gerenciamento de funções e privilégios, consulte [[!DNL Snowflake] Referência da API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitações e perguntas frequentes {#limitations-and-frequently-asked-questions}

* A taxa de transferência de dados para o [!DNL Snowflake] a origem é 2000 registros por segundo.
* A precificação pode variar dependendo da quantidade de tempo em que um depósito está ativo e do tamanho do depósito. Para o [!DNL Snowflake] integração de origem, o menor tamanho, x-pequeno armazém é suficiente. Sugere-se ativar a suspensão automática para que o depósito possa suspender por conta própria quando não estiver em uso.
* A variável [!DNL Snowflake] A origem consulta o banco de dados em busca de novos dados a cada 10 segundos.
* Opções de configuração:
   * Você pode ativar um `backfill` sinalizador booleano para o [!DNL Snowflake] origem ao criar uma conexão de origem.
      * Se o preenchimento retroativo for definido como verdadeiro, o valor de timestamp.initial será definido como 0. Isso significa que os dados com uma coluna de carimbo de data e hora maior que 0 época são buscados.
      * Se o preenchimento retroativo for definido como falso, o valor de timestamp.initial será definido como -1. Isso significa que os dados com uma coluna de carimbo de data e hora maior que a hora atual (a hora em que a fonte começa a assimilar) são buscados.
   * A coluna de carimbo de data e hora deve ser formatada como tipo: `TIMESTAMP_LTZ` ou `TIMESTAMP_NTZ`. Se a coluna de carimbo de data e hora estiver definida como `TIMESTAMP_NTZ`, os tipos devem ser armazenados em UTC no banco de dados.

## Próximas etapas

O tutorial a seguir fornece etapas sobre como conectar seus [!DNL Snowflake] origem de transmissão para o Experience Platform usando a API:

* [Transmitir dados de um [!DNL Snowflake] banco de dados para Experience Platform usando a API do Serviço de fluxo](../../tutorials/api/create/databases/snowflake-streaming.md)

