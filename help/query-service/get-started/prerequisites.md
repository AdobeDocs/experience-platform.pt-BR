---
keywords: Experience Platform;serviço de consulta;serviço de consulta;consulta;;query service;Query service;query
title: Introdução ao Serviço de consulta do Adobe Experience Platform
description: Um detalhamento das etapas necessárias para utilizar totalmente o Serviço de consulta do Adobe Experience Platform
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Introdução ao Adobe Experience Platform [!DNL Query Service] {#getting-started}

Use o Serviço de consulta da Adobe Experience Platform para executar consultas SQL em conjuntos de dados assimilados, unir dados de várias fontes e gerar conjuntos de dados derivados para análise, fluxos de trabalho de aprendizado de máquina ou Perfil do cliente em tempo real. Depois de assimilar dados, acesse o Serviço de consulta por meio da interface do usuário para análise e colaboração interativas ou por meio da API para execução de consulta automatizada e programática.

## Pré-requisitos {#prerequisites}

Antes de começar a consultar dados, verifique se você tem:

- **Permissões necessárias**: sua conta de usuário tem acesso ao Serviço de consulta na Experience Platform. Se o serviço não estiver disponível na interface, revise a [documentação de permissões](../../access-control/home.md#permissions) e contate o administrador do sistema.
- **Assimilação de dados**: você tem dados assimilados na Experience Platform.

Se você precisar assimilar dados, reveja o [vídeo tutorial sobre assimilação de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) para obter uma visão geral sobre a criação de conjuntos de dados, mapeamento de esquemas, assimilação e validação. Leia a [documentação de visão geral de assimilação](../../ingestion/home.md) para obter informações mais detalhadas e links para outros recursos de aprendizado.

## Caminhos de início rápido

Após assimilar seus dados na Experience Platform, você pode começar a trabalhar com o Serviço de consulta usando o [!DNL Query Editor] na Experience Platform ou na API do Serviço de consulta.

### [!DNL Query Editor]

Use o [!DNL Query Editor] para análise, exploração de dados e desenvolvimento de consulta colaborativa. Para obter uma visão geral da funcionalidade da interface, consulte a [documentação da interface do usuário do Serviço de Consulta](../ui/overview.md). Para saber mais sobre como gravar e executar consultas na interface do usuário, leia o [[!DNL Query Editor user guide]](../ui/user-guide.md).

### API do serviço de consulta

Use a API do Serviço de consulta para fluxos de trabalho automatizados, gerenciamento de modelos de consulta e integrações programáticas. Consulte o [Guia do desenvolvedor do Serviço de Consulta](../api/getting-started.md) para obter instruções detalhadas sobre como usar a API do Serviço de Consulta.

## Próximas etapas

Este documento abordou os pré-requisitos necessários para usar os recursos do [!DNL Query Service] no Experience Platform. Para começar rapidamente a usar os recursos do Serviço de consulta, é recomendável ler os seguintes documentos:

- [Orientação geral para execução de consulta](../best-practices/writing-queries.md)
- [Sintaxe SQL no Serviço de consulta](../sql/syntax.md)
- [Criar conjuntos de dados derivados com SQL](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

Como alternativa, para saber mais sobre como o Serviço de consulta beneficia o processamento de dados no Experience Platform, assista à [apresentação do caso de uso de navegação abandonada](../use-cases/abandoned-browse.md#video-example).

Os recursos a seguir são úteis para melhorar sua compreensão do [!DNL Query Service]:

- [Visão geral da interface do [!DNL Query Service]](../ui/overview.md)
- [[!DNL Query Service] credenciais](../ui/credentials.md)
- [A visão geral das conexões de clientes](../clients/overview.md)
