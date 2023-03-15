---
title: Visão geral do Data Distiller
description: Um resumo dos limites de uso do Data Distiller para dados do Serviço de consulta em relação ao seu direito de licenciamento.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Visão geral do Data Distiller

O Data Distiller é uma oferta de pacote que inclui um subconjunto das funcionalidades do Adobe Experience Platform. Com o Data Distiller, você pode executar a preparação de dados após a assimilação (como limpeza, modelagem e manipulação) para o perfil do cliente em tempo real ou casos de uso analíticos, executando consultas em lote no Serviço de consulta. Seu uso do Data Distiller depende de seus direitos para aplicativos baseados em plataforma.

## Uso da licença {#license-usage}

A variável  [Painel de uso de licença do Data Distiller](./license-usage.md) estará disponível após comprar as horas de computação do Data Distiller. O painel de uso da licença ajuda a monitorar o consumo de horas de computação qualificadas. Consulte a [Documento de uso de licença do Data Distiller](./license-usage.md) para exibir informações importantes sobre o uso da licença do Serviço de consulta da sua organização.

## Parâmetros de escopo {#scoping-parameters}

Os parâmetros de escopo são limites de uso relacionados ao escopo da sua configuração necessária e são definidos pela capacidade da licença. Sem complementos, os parâmetros de escopo do Data Distiller são os seguintes:

* **Computar horas**: Você pode usar o PSQL ou a API do Serviço de consulta para executar consultas em lote executadas em qualquer sandbox (programada ou não) para verificar e gravar dados. Ele usa as horas de computação por ano atribuídas, conforme determinado no processo de definição do escopo do contrato de licença. O total de horas de computação é acumulado em todas as sandboxes.
* **Dados assimilados**: os dados assimilados na Adobe Experience Platform que podem ser consultados usando o Data Distiller estão sujeitos às limitações descritas em sua licença atual para Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer.
* **Armazenamento Data Lake**: o armazenamento em data lake fornecido em sua licença existente na Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer também pode ser usado com o Data Distiller. O Armazenamento Data Lake é um recurso compartilhado.
* **Usuários do serviço de consulta**: o número de usuários do Serviço de consulta detalhados em sua licença atual para Adobe Real-time Customer Data Platform, Customer Journey Analytics e/ou Adobe Journey Optimizer também pode ser usado com o Data Distiller. Usuários do serviço de consulta é um recurso compartilhado.

## Medidas de proteção

Consulte a [Proteções do serviço de consulta](../guardrails.md) documento sobre limites de uso padrão para dados do Serviço de consulta em relação ao seu direito de licenciamento.

## Limites estáticos

Um limite estático é o limite de uso relacionado aos limites funcionais da Ativação do Adobe Experience Platform. [Mais informações sobre a Adobe Experience Platform Ativation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) podem ser encontrados nos documentos de ajuda do Adobe. Um resumo dos limites estáticos do Data Distiller está listado abaixo. Para obter informações mais completas, consulte o documento de proteção do Serviço de consulta.

* **Consultas em lote**: as consultas em lote agendadas expiram após 24 horas.
* **Serviço de consulta**: Você pode usar o Serviço de consulta para os seguintes propósitos:
   * Para executar queries SQL para análise de dados e preparação de dados pós-assimilação (limpeza, modelagem e manipulação).
   * Para executar consultas SQL e criar métricas de roll-up para superfície diretamente em uma ferramenta de BI.
   * Para inspecionar dados rapidamente no Adobe Experience Platform.
   * Para gerar insights significativos dos seus dados.
* **Chamada de API de relatório**: para garantir que as queries sejam executadas em dados agregados usando a API de relatórios, tenham recursos suficientes para serem executados com eficiência. Isso inclui queries que melhoram os modelos de dados existentes, como os fornecidos pela Real-time Customer Data Platform. A API de relatórios rastreia a utilização de recursos atribuindo slots de simultaneidade a cada query. Um máximo de 4 chamadas de API de relatórios estão disponíveis simultaneamente. Se você acessar a API de relatórios por meio de uma ferramenta de BI e precisar de mais slots de simultaneidade, será necessário um servidor de BI.


