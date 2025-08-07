---
title: Visão geral do Oracle DB Source Connector
description: Saiba como conectar o Oracle ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] é um poderoso sistema de gerenciamento de banco de dados relacional desenvolvido por [!DNL Oracle Corporation]. Você pode usar o [!DNL Oracle DB] para armazenar, gerenciar e recuperar grandes volumes de dados estruturados com eficiência e segurança.

Use a origem [!DNL Oracle DB] no catálogo de origens do Adobe Experience Platform para conectar seu banco de dados e assimilar dados na Experience Platform.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para concluir a configuração de pré-requisito antes de conectar sua conta do [!DNL Oracle DB] à Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform no Azure ou no Amazon Web Services (AWS). Para obter mais informações, leia o manual sobre [sobre como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform no Azure e no AWS](../../ip-address-allow-list.md) para obter mais informações.

### Autenticar para o Experience Platform no Azure {#azure}

Forneça uma cadeia de conexão para autenticar e conectar sua conta do [!DNL Oracle DB] ao Experience Platform no Azure.

| Credencial | Descrição |
| --- | --- |
| String de conexão | Uma string de conexão é uma string de texto usada pelas aplicações para estabelecer conexão com um banco de dados. O padrão da cadeia de conexão [!DNL Oracle DB] é: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| ID de especificação da conexão | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL Oracle] é `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |

### Autenticar para o Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

Forneça valores para as credenciais a seguir para autenticar e conectar sua conta do [!DNL Oracle DB] ao Experience Platform no AWS.

| Credencial | Descrição |
| --- | --- |
| Servidor | O endereço IP ou o nome do host do seu servidor [!DNL Oracle DB]. |
| Porta | O número da porta do servidor de banco de dados. O número de porta padrão é `1521`. |
| Nome de usuário | A conta de usuário [!DNL Oracle DB] usada para autenticar e acessar o banco de dados. |
| Senha | A chave secreta associada ao seu nome de usuário, usada para autenticação. |
| Banco de dados | A instância de banco de dados [!DNL Oracle] específica à qual você deseja se conectar. |
| Esquema | O container para objetos de banco de dados, como tabelas, exibições ou procedimentos. |
| Modo SSL | Um valor booleano que controla se o SSL é imposto ou não. Essa configuração depende do suporte do servidor e o padrão é `false`. |
| ID de especificação da conexão | A ID de especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID de especificação da conexão para [!DNL Oracle] é `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Observação**: esta credencial é necessária somente ao conectar-se por meio da API [!DNL Flow Service]. |


## Conectar [!DNL Oracle] a [!DNL Experience Platform] usando APIs

- [Conectar o Oracle DB usando a API do Serviço de fluxo](../../tutorials/api/create/databases/oracle.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma fonte de banco de dados usando a API do Serviço de fluxo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Oracle] a [!DNL Experience Platform] usando a interface

- [Conecte o Oracle DB usando o espaço de trabalho da interface do usuário do Experience Platform.](../../tutorials/ui/create/databases/oracle.md)
- [Criar um fluxo de dados para uma conexão de origem de banco de dados na interface](../../tutorials/ui/dataflow/databases.md)
