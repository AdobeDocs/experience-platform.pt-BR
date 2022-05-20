---
title: Notas de versão da Adobe Experience Platform de setembro de 2019
description: As notas de versão de setembro de 2019 para o Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
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

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. Adobe Experience Platform [!DNL Data Ingestion] O fornece várias alternativas para assimilar dados, incluindo APIs em lote, APIs de streaming, conectores nativos do Adobe, parceiros de integração de dados ou a interface do usuário da Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
| ----------- | ---------- |
| Novo domínio para assimilação de streaming | O `dcs.data.adobe.net` O domínio foi movido para o novo domínio comum de coleta de dados `dcs.adobedc.net`. Os usuários devem atualizar suas implementações de acordo com a documentação revisada de assimilação de streaming do Adobe Experience Platform. Toda a documentação relacionada à assimilação de streaming do Adobe Experience Platform foi atualizada para usar o novo domínio. |

Para obter mais informações, visite o [Documentação da assimilação de dados](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] é um serviço totalmente gerenciado no [!DNL Experience Platform] que permite que os cientistas de dados gerem insights de dados e conteúdo de forma contínua em soluções de Adobe e sistemas de terceiros, criando e operacionalizando Modelos de aprendizado de máquina. [!DNL Data Science Workspace] é totalmente integrado ao [!DNL Platform] e potencializa o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguido do desenvolvimento e da operacionalização de Modelos para enriquecer automaticamente [!DNL Real-time Customer Profile] com Insights de aprendizado de máquina.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Agendamento de serviços por meio da interface do usuário | Integrado com [!DNL Platform] Serviço de orquestração para automatizar o treinamento e a pontuação do Modelo com agendamentos definidos pelo usuário usando a interface do usuário. |
| [!DNL Service Gallery] | Navegue, monitore e acesse os serviços de aprendizado de máquina com a capacidade de agendar trabalhos de treinamento automatizados e de pontuação, tudo isso dentro do novo design [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Melhorias na interface do usuário. |

**Problemas conhecidos**

* No momento, não há maneira acessível na variável [!DNL Service Gallery] para excluir um Serviço existente. Enquanto isso, consulte o [Referência da API do Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para excluir um serviço existente por meio de chamadas de API.
* O [!DNL Service Gallery] não tem suporte de paginação para filtrar as execuções de treinamento e pontuação de um Serviço.
* Ao configurar o treinamento programado ou a pontuação é executada pelo [!DNL Service Gallery], definir a frequência como por hora impede que a programação seja aplicada.

Para obter mais informações, visite o [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] O oferece a capacidade de usar o SQL padrão para consultar dados no Adobe Experience Platform para oferecer suporte a uma variedade de casos de uso de análise e gerenciamento de dados. É uma ferramenta sem servidor que permite unir conjuntos de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, [!DNL Data Science Workspace]ou para ingestão em [!DNL Real-time Customer Profile].

Você pode usar [!DNL Query Service] para criar ecossistemas de análise de dados, criando uma imagem dos clientes em seus vários canais de interação. Esses canais podem incluir sistemas de ponto de venda, Web, dispositivos móveis ou sistemas CRM.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias no [!DNL Query Editor] | Adição de uma função de salvamento que permite salvar uma consulta e trabalhar nela posteriormente. Adição de uma guia &quot;Procurar&quot; ao [!DNL Query Service] interface do usuário no Adobe Experience Platform que mostra consultas salvas pelos usuários em sua organização. Implementação de um painel &quot;Detalhes da consulta&quot; que exibe metadados úteis sobre a consulta que está sendo visualizada. |
| Novas funções de atribuição | funções definidas pelo Adobe em [!DNL Query Service] para consultar a atribuição de canal com parâmetros de expiração. |
| Aprimoramentos na sintaxe SQL | Suporte para sintaxe iLike . |
| Gerar conjuntos de dados com um esquema XDM definido | Adição de uma nova cláusula nas consultas Criar tabela como seleção (CTAS), que permite especificar um esquema de destino. |

Para obter mais informações, consulte [Documentação do Serviço de query](../../query-service/home.md).
