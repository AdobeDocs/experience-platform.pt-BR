---
title: Notas de versão da Adobe Experience Platform de setembro de 2019
description: As notas de versão de setembro de 2019 para Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 10 de setembro de 2019**

Atualizações dos recursos existentes na Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. Adobe Experience Platform [!DNL Data Ingestion] O fornece várias alternativas para assimilação de dados, incluindo APIs de lote, APIs de streaming, conectores de Adobe nativos, parceiros de integração de dados ou a interface do usuário do Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
| ----------- | ---------- |
| Novo domínio para assimilação por transmissão | A variável `dcs.data.adobe.net` domínio foi movido para o novo domínio comum de coleta de dados `dcs.adobedc.net`. Os usuários devem atualizar suas implementações de acordo com a documentação revisada de assimilação de streaming do Adobe Experience Platform. Toda a documentação relacionada à assimilação por transmissão do Adobe Experience Platform foi atualizada para usar o novo domínio. |

Para obter mais informações, visite o [Documentação de assimilação de dados](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] O é um serviço totalmente gerenciado no [!DNL Experience Platform] que permite que os cientistas de dados gerem insights de dados e conteúdo em soluções Adobe e sistemas de terceiros criando e operacionalizando modelos de aprendizado de máquina. [!DNL Data Science Workspace] O é totalmente integrado ao [!DNL Platform] e possibilita o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguido do desenvolvimento e da operacionalização de modelos para enriquecer automaticamente [!DNL Real-Time Customer Profile] com os Insights de aprendizado de máquina.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Agendamento de serviços por meio da interface | Integrado ao [!DNL Platform] Serviço de orquestração para automatizar o treinamento e a pontuação do modelo com programações definidas pelo usuário usando a interface do usuário. |
| [!DNL Service Gallery] | Navegue, monitore e acesse os serviços de aprendizado de máquina com a capacidade de programar treinamentos automatizados e tarefas de pontuação, tudo dentro do projeto reprojetado [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Melhorias na interface. |

**Problemas conhecidos**

* Atualmente, não há nenhum modo acessível no [!DNL Service Gallery] para excluir um Serviço existente. Enquanto isso, consulte o [Referência da API do Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para excluir um Serviço existente por meio de chamadas de API.
* A variável [!DNL Service Gallery] não tem suporte à paginação para filtrar o treinamento de um Serviço e as execuções de pontuação.
* Ao configurar o treinamento programado ou a pontuação, o passa pelo [!DNL Service Gallery], definir a frequência como hora impede que o agendamento seja aplicado.

Para obter mais informações, visite o [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] O fornece a capacidade de usar o SQL padrão para consultar dados no Adobe Experience Platform para oferecer suporte a uma variedade de casos de uso de análise e gerenciamento de dados. É uma ferramenta sem servidor que permite que você participe de conjuntos de dados do [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, [!DNL Data Science Workspace]ou para assimilação em [!DNL Real-Time Customer Profile].

Você pode usar [!DNL Query Service] para criar ecossistemas de análise de dados, criando uma imagem dos clientes em seus vários canais de interação. Esses canais podem incluir sistemas de ponto de venda, Web, móvel ou CRM.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias no [!DNL Query Editor] | Adição de uma função para salvar que permite salvar uma consulta e trabalhar nela posteriormente. Adição da guia &quot;Navegar&quot; à [!DNL Query Service] interface do usuário na Adobe Experience Platform que mostra consultas salvas por usuários em sua organização. Implementação de um painel &quot;Detalhes da consulta&quot; que exibe metadados úteis sobre a consulta que está sendo visualizada. |
| Novas funções de atribuição | funções definidas pelo Adobe no [!DNL Query Service] para consultar a atribuição de canal com parâmetros de expiração. |
| Melhorias na sintaxe SQL | Suporte para sintaxe iLike. |
| Gerar conjuntos de dados com um esquema XDM definido | Adição de uma nova cláusula em consultas Criar Tabela como Seleção (CTAS) que permite especificar um schema de destino. |

Para obter mais informações, consulte [Documentação do Serviço de consulta](../../query-service/home.md).
