---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 10 de setembro de 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 10 de setembro de 2019**

Atualizações dos recursos existentes no Adobe Experience Platform:

* [!DNL Data Ingestion](#ingestion)
* [!DNL Data Science Workspace](#dsw)
* [!DNL Query Service](#query)

## [!DNL Data Ingestion] {#ingestion}

O Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. O Adobe Experience Platform [!DNL Data Ingestion] oferece várias alternativas para assimilar dados, incluindo APIs em lote, APIs de transmissão, conectores nativos de Adobe, parceiros de integração de dados ou a interface do usuário do Adobe Experience Platform.

**Novos recursos**

| Recurso | Descrição |
| ----------- | ---------- |
| Novo domínio para ingestão de streaming | O `dcs.data.adobe.net` domínio foi movido para o novo domínio comum de coleta de dados `dcs.adobedc.net`. Os usuários devem atualizar suas implementações de acordo com a documentação de ingestão de streaming de Adobe Experience Platform revista. Toda a documentação relacionada à ingestão de streaming de Adobe Experience Platform foi atualizada para usar o novo domínio. |

Para obter mais informações, visite a documentação [de ingestão de](../../ingestion/home.md)dados.

## [!DNL Data Science Workspace] {#dsw}

O Adobe Experience Platform [!DNL Data Science Workspace] é um serviço totalmente gerenciado dentro do [!DNL Experience Platform] qual os cientistas de dados podem gerar insights de dados e conteúdo através de soluções de Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizagem de Máquinas. [!DNL Data Science Workspace] é totalmente integrada com [!DNL Platform] e potencializa o ciclo de vida completo da ciência de dados, incluindo a exploração e preparação de dados XDM, seguido pelo desenvolvimento e operacionalização de Modelos para enriquecer automaticamente [!DNL Real-time Customer Profile] com os Insights de Aprendizagem de Máquinas.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Agendamento de serviços por meio da interface do usuário | Integrado ao [!DNL Platform] Orchestration Service para automatizar o treinamento e a pontuação do Modelo com agendamentos definidos pelo usuário usando a interface do usuário. |
| [!DNL Service Gallery] | Navegue, monitore e acesse os serviços de aprendizado de máquina com a capacidade de programar trabalhos automatizados de treinamento e pontuação, tudo isso dentro do novo design [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Melhorias na interface do usuário. |

**Problemas conhecidos**

* Atualmente, não há uma maneira acessível de excluir um Serviço existente [!DNL Service Gallery] . Enquanto isso, consulte a referência [da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning para excluir um serviço existente por meio de chamadas de API.
* O [!DNL Service Gallery] não tem suporte de paginação para filtrar as execuções de treinamento e pontuação de um Serviço.
* Ao configurar o treinamento agendado ou a pontuação é executada pelo [!DNL Service Gallery], definir a frequência como horária impede que o agendamento seja aplicado.

Para obter mais informações, visite a Visão geral [da área de trabalho da](../../data-science-workspace/home.md)Data Science.

## [!DNL Query Service] {#query}

[!DNL Query Service] fornece a capacidade de usar SQL padrão para dados de query no Adobe Experience Platform para suportar uma variedade de casos de uso de análise e gestão de dados. It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. Esses canais podem incluir sistemas de ponto de venda, sistemas web, móveis ou CRM.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias para [!DNL Query Editor] | Adicionada uma função de gravação que permite salvar um query e trabalhar nele posteriormente. Adicionada uma guia &quot;Procurar&quot; à interface do [!DNL Query Service] usuário no Adobe Experience Platform que mostra query salvos pelos usuários em sua organização. Implementado um painel &quot;Detalhes do Query&quot; que exibe metadados úteis sobre o query que está sendo visualizado. |
| Novas funções de atribuição | funções definidas pelo Adobe em [!DNL Query Service] ao query para atribuição do canal com parâmetros de expiração. |
| Aprimoramentos à sintaxe SQL | Suporte para sintaxe iLike. |
| Gerar conjuntos de dados com um Schema XDM definido | Adicionada uma nova cláusula nos query Criar tabela como seleção (CTAS) que permite especificar um schema de público alvo. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).