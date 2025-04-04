---
title: Práticas recomendadas para gerenciamento avançado do ciclo de vida dos dados
description: Saiba como gerenciar com eficiência as solicitações de higiene de dados no Adobe Experience Platform usando a interface do usuário do gerenciamento avançado do ciclo de vida dos dados e a API de higiene de dados. Este guia aborda as práticas recomendadas, como maximizar identidades por solicitação, especificar conjuntos de dados individuais e estar atento à limitação da API para evitar lentidão. O documento inclui diretrizes para a configuração da limpeza automática do conjunto de dados, como monitorar os status das ordens de serviço e métodos detalhados de recuperação de resposta. Siga estas práticas para simplificar o processamento de solicitações e otimizar os tempos de resposta.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Práticas recomendadas para gerenciamento avançado do ciclo de vida dos dados

Use a interface do Gerenciamento avançado do ciclo de vida dos dados e a API de higiene de dados para gerenciar com eficiência as solicitações de limpeza e remover dados dos serviços da Adobe Experience Platform. Siga estas práticas recomendadas para agilizar o processamento de solicitações e otimizar os tempos de resposta de conclusão.

## Pré-requisitos {#prerequisites}

Este guia requer uma compreensão funcional do espaço de trabalho do Ciclo de Vida de Dados e da [API de Higiene de Dados](./api/overview.md). Antes de continuar com este documento, familiarize-se com os guias em [Gerenciamento avançado do ciclo de vida dos dados](./home.md) e [criação de solicitações de exclusão de registros](./ui/record-delete.md) ou [expirações de conjuntos de dados na interface do usuário](./ui/dataset-expiration.md) ou por meio da API.

## Diretrizes de criação da ordem de serviço {#work-order-creation-guidelines}

Você pode usar o ponto de extremidade `/workorder` na API da higiene de dados para gerenciar programaticamente solicitações de exclusão de registros no Experience Platform. Com esse endpoint, é possível criar uma solicitação de exclusão, verificar seu status ou atualizar uma solicitação existente. Consulte o [Documento de ponto de extremidade de ordem de trabalho](./api/workorder.md) para saber como executar essas ações usando a API.

>[!TIP]
>
>Uma ordem de serviço é uma solicitação estruturada que executa operações específicas de gerenciamento de dados, como limpeza ou transformação de dados, para garantir um processamento eficiente e sistemático.

Siga estas diretrizes para otimizar os envios de solicitações de limpeza:

1. **Maximizar identidades por solicitação:** Inclua até 100.000 identidades por solicitação de limpeza para aumentar a eficiência. Agrupar várias identidades em uma única solicitação ajuda a reduzir a frequência de chamadas de API e minimiza o risco de problemas de desempenho devido a solicitações excessivas de identidade única. Submeta solicitações com o máximo de contagens de identidade para obter um processamento mais rápido, já que as ordens de serviço são processadas em lote para eficiência.
2. **Especificar conjuntos de dados individuais:** Para obter eficiência máxima, especifique o conjunto de dados individual a ser processado.
3. **Considerações sobre a limitação de API:** lembre-se da limitação de API para evitar lentidão. Solicitações menores (&lt; 100 IDs) em frequências mais altas podem resultar em 429 respostas e exigir o reenvio em taxas aceitáveis.

### Gerenciar erros 429 {#manage-429-errors}

Se você receber um erro 429, ele indica que você excedeu o número permitido de solicitações em um determinado período de tempo. Siga estas práticas recomendadas para gerenciar erros 429 de maneira eficaz:

- **Ler o cabeçalho &#39;Retry-After&#39;**: quando um erro 429 é retornado, verifique o cabeçalho de resposta &#39;Retry-After&#39;. Esse cabeçalho especifica o tempo de espera antes de repetir a solicitação.
- **Implementar lógica de repetição**: use o valor &#39;Retry-After&#39; para implementar lógica de repetição no aplicativo, garantindo que as tentativas sejam feitas após o tempo especificado para evitar erros 429 subsequentes.
- **Enviar solicitações em lote**: evite enviar várias solicitações pequenas em rápida sucessão. Em vez disso, agrupe várias identidades em uma única solicitação para reduzir a frequência das chamadas e minimizar o risco de atingir limites de taxa.

## Expiração do conjunto de dados {#dataset-expiration}

Configure a limpeza automática do conjunto de dados para dados de vida curta. Use o ponto de extremidade `/ttl` na API de higiene de dados para agendar datas de expiração para conjuntos de dados para limpeza com base em uma hora ou data especificada. Consulte o manual de ponto de extremidade de expiração do conjunto de dados para saber como [criar uma expiração de conjunto de dados](./api/dataset-expiration.md) e os [parâmetros de consulta aceitos](./api/dataset-expiration.md#query-params).

## Monitorar status de expiração da ordem de trabalho e do conjunto de dados {#monitor}

Você pode monitorar com eficiência o progresso do gerenciamento do ciclo de vida dos dados por meio do uso dos **Eventos de E/S**. Um Evento de E/S é um mecanismo para receber notificações em tempo real sobre alterações ou atualizações em vários serviços na Experience Platform.

Os alertas de Evento de E/S podem ser enviados para um webhook configurado para habilitar a automação do monitoramento de atividades. Para receber alertas via webhook, você deve registrar o webhook para alertas do Experience Platform na Adobe Developer Console. Consulte o manual sobre [assinatura de notificações de eventos do Adobe I/O](../observability/alerts/subscribe.md) para obter instruções detalhadas.

Use os seguintes métodos e diretrizes do ciclo de vida dos dados para recuperar e monitorar efetivamente os status dos trabalhos:

### Eventos de E/S {#io-events}

Para monitorar com eficiência o progresso das tarefas do ciclo de vida dos dados, configure e use Eventos de I/O seguindo estas etapas:

- Configure webhooks para receber notificações por push sobre alterações de status.
- Use notificações para monitorar o progresso e receber atualizações após a conclusão.
- Evite implementar mecanismos de pesquisa para minimizar o tráfego da API.

### Recuperar respostas detalhadas para uma única ordem de serviço {#retrieve-detailed-work-order-response}

Para obter informações detalhadas sobre ordens de serviço individuais, use a seguinte abordagem:

- Faça uma solicitação GET ao ponto de extremidade `/workorder/{work_order_id}` para obter dados detalhados da resposta.
- Recupere respostas específicas do produto e mensagens de sucesso.
- Evite usar esse método para atividades de pesquisa regulares.

Seguindo essas práticas recomendadas, você pode gerenciar com eficiência as solicitações de limpeza e otimizar os tempos de resposta no Gerenciamento avançado do ciclo de vida dos dados.
