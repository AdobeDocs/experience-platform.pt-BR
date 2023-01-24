---
title: Visão geral da Distiller de dados
description: Um resumo dos limites de uso do Data Distiller para dados do Serviço de query em relação ao seu direito de licenciamento.
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Visão geral do Data Distiller

O Data Distiller é uma oferta de pacote que inclui um subconjunto das funcionalidades do Adobe Experience Platform. Com o Data Distiller, você pode executar a preparação de dados pós-ingestão (como limpeza, modelagem e manipulação) para o perfil do cliente em tempo real ou casos de uso analítico executando consultas em lote no Serviço de query. O uso do Data Distiller depende da licença atual e contínua de pelo menos um dos seguintes: Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer.

## Uso da licença {#license-usage}

Consulte a [Documento de uso da licença do Data Distiller](./license-usage.md) para exibir informações importantes sobre o uso da licença do Serviço de query de sua organização.

## Parâmetros de escopo {#scoping-parameters}

Os parâmetros de escopo são limites de uso relacionados ao escopo do caso de uso proposto, conforme definido pela capacidade da licença. Sem complementos, os parâmetros de escopo do Data Distiller são os seguintes:

* **Computar Horas**: Você pode usar o PSQL ou a API do Serviço de Consulta para executar consultas em lote executadas em qualquer sandbox (programada ou não) para verificar e gravar dados. Ele usa as Horas de computação atribuídas por ano, conforme determinado no processo de escopo do seu contrato de licença. O total de horas de computação é acumulado em todas as sandboxes.
* **Dados assimilados**: Os dados assimilados no Adobe Experience Platform que podem ser consultados usando o Data Distiller estão sujeitos às limitações descritas na licença atual para Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer.
* **Armazenamento do Data Lake**: O armazenamento do data lake fornecido em sua licença atual para Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer também pode ser usado com o Data Distiller. O Data Lake Storage é um recurso compartilhado.
* **Usuários do Serviço de Consulta**: O número de usuários do Serviço de query detalhado em sua licença atual para Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer também pode ser usado com o Data Distiller. Usuários do Serviço de query é um recurso compartilhado.

## Medidas de proteção

Consulte a [Medidas de proteção do serviço de consulta](../guardrails.md) documento sobre limites de uso padrão para dados do Serviço de query em relação ao seu direito de licenciamento.

## Limites estáticos

Um limite estático é o limite de uso que está relacionado aos limites funcionais do Adobe Experience Platform Ativation. [Mais informações sobre o Adobe Experience Platform Ativation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) pode ser encontrada nos documentos de ajuda do Adobe. Um resumo dos limites estáticos do Data Distiller está listado abaixo. Para obter informações mais completas, consulte o documento de garantia do Serviço de query.

* **Consultas em lote**: As consultas em lote programadas atingem o tempo limite após 24 horas.
* **Serviço de query**: Você pode usar o Serviço de query para os seguintes fins:
   * Para executar consultas SQL para análise de dados e preparação de dados de assimilação de postagens (limpeza, modelagem e manipulação).
   * Para executar queries SQL para criar métricas de roll-up diretamente em uma ferramenta BI.
   * Para inspecionar rapidamente os dados no Adobe Experience Platform.
* **Chamada da API de relatórios**: Para garantir que as consultas executadas em dados agregados usando a API de relatórios tenham recursos suficientes para serem executadas com eficiência. Isso inclui queries que aprimoram os modelos de dados existentes, como os fornecidos pela Real-time Customer Data Platform. A API de relatórios rastreia a utilização de recursos ao atribuir slots de simultaneidade a cada query. No máximo 4 chamadas de API de relatórios estão disponíveis simultaneamente. Se você acessar a API de relatórios por meio de uma ferramenta de BI e precisar de mais slots de simultaneidade, será necessário um servidor de BI.


