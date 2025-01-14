---
title: Notas de versão da Adobe Experience Platform de setembro de 2019
description: As notas de versão de setembro de 2019 da Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 10 de setembro de 2019**

Atualizações dos recursos já existentes na Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. O Adobe Experience Platform [!DNL Data Ingestion] fornece várias alternativas para assimilação de dados, incluindo APIs de Lote, APIs de Streaming, conectores de Adobe nativos, parceiros de integração de dados ou a interface do usuário do Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
| ----------- | ---------- |
| Novo domínio para assimilação por transmissão | O domínio `dcs.data.adobe.net` foi movido para o novo domínio de coleta de dados comum `dcs.adobedc.net`. Os usuários devem atualizar suas implementações de acordo com a documentação revisada de assimilação de streaming do Adobe Experience Platform. Toda a documentação relacionada à assimilação por transmissão do Adobe Experience Platform foi atualizada para usar o novo domínio. |

Para obter mais informações, visite a [documentação de Assimilação de dados](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

O Adobe Experience Platform [!DNL Data Science Workspace] é um serviço totalmente gerenciado no [!DNL Experience Platform], que permite que cientistas de dados gerem insights de dados e conteúdo em soluções de Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizado de Máquina. O [!DNL Data Science Workspace] é totalmente integrado ao [!DNL Platform] e capacita o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguidos pelo desenvolvimento e a operacionalização de Modelos para enriquecer automaticamente o [!DNL Real-Time Customer Profile] com Machine Learning Insights.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Agendamento de serviços por meio da interface | Integrado ao Serviço de Orquestração do [!DNL Platform] para automatizar o treinamento e a pontuação do modelo com agendamentos definidos pelo usuário usando a interface do usuário. |
| [!DNL Service Gallery] | Navegue, monitore e acesse os Serviços de aprendizado de máquina com a capacidade de agendar treinamentos automatizados e trabalhos de pontuação, tudo dentro do [!DNL Service Gallery] reprojetado. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] melhorias na interface. |

**Problemas conhecidos**

* No momento, não há nenhum modo acessível no [!DNL Service Gallery] para excluir um Serviço existente. Enquanto isso, consulte a [Referência da API do Sensei Machine Learning](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) para excluir um Serviço existente por meio de chamadas de API.
* O [!DNL Service Gallery] não tem suporte à paginação para filtrar o treinamento de um Serviço e as execuções de pontuação.
* Ao configurar o treinamento ou a pontuação agendados, o [!DNL Service Gallery] é executado, definir a frequência como horária impede que a programação seja aplicada.

Para obter mais informações, visite a [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

O [!DNL Query Service] fornece a capacidade de usar o SQL padrão para consultar dados no Adobe Experience Platform para oferecer suporte a uma variedade de casos de uso de análise e gerenciamento de dados. É uma ferramenta sem servidor que permite que você ingresse conjuntos de dados do [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, [!DNL Data Science Workspace], ou para assimilação no [!DNL Real-Time Customer Profile].

Você pode usar o [!DNL Query Service] para criar ecossistemas de análise de dados, criando uma imagem dos clientes em seus vários canais de interação. Esses canais podem incluir sistemas de ponto de venda, Web, móvel ou CRM.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias no [!DNL Query Editor] | Adição de uma função para salvar que permite salvar uma consulta e trabalhar nela posteriormente. Adicionada a guia &quot;Procurar&quot; à interface de usuário do [!DNL Query Service] no Adobe Experience Platform, que mostra consultas salvas por usuários em sua organização. Implementação de um painel &quot;Detalhes da consulta&quot; que exibe metadados úteis sobre a consulta que está sendo visualizada. |
| Novas funções de atribuição | Funções definidas por Adobe em [!DNL Query Service] para consultar atribuição de canal com parâmetros de expiração. |
| Melhorias na sintaxe SQL | Suporte para sintaxe iLike. |
| Gerar conjuntos de dados com um esquema XDM definido | Adição de uma nova cláusula em consultas Criar Tabela como Seleção (CTAS) que permite especificar um schema de destino. |

Para obter mais informações, consulte a [documentação do Serviço de consulta](../../query-service/home.md).
