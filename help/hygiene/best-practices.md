---
title: Práticas recomendadas para gerenciamento avançado do ciclo de vida dos dados
description: Saiba como gerenciar com eficiência as solicitações de higiene de dados no Adobe Experience Platform usando a interface do usuário do gerenciamento avançado do ciclo de vida dos dados e a API de higiene de dados. Este guia aborda as práticas recomendadas, como maximizar identidades por solicitação, especificar conjuntos de dados individuais e estar atento à limitação da API para evitar lentidão. O documento inclui diretrizes para a configuração da limpeza automática do conjunto de dados, como monitorar os status das ordens de serviço e métodos detalhados de recuperação de resposta. Siga estas práticas para simplificar o processamento de solicitações e otimizar os tempos de resposta.
source-git-commit: 92667fd4da093e56dcf06ae1696484671d9fdd38
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Práticas recomendadas para gerenciamento avançado do ciclo de vida dos dados

Use a interface do Gerenciamento avançado do ciclo de vida dos dados e a API de higiene de dados para gerenciar com eficiência as solicitações de limpeza e remover dados dos serviços da Adobe Experience Platform. Siga estas práticas recomendadas para agilizar o processamento de solicitações e otimizar os tempos de resposta de conclusão.

## Pré-requisitos {#prerequisites}

Este guia requer uma compreensão funcional do espaço de trabalho do ciclo de vida dos dados e da [API de higiene de dados](./api/overview.md). Antes de continuar com este documento, familiarize-se com os guias no [Gerenciamento avançado do ciclo de vida dos dados](./home.md) e [criando solicitações de exclusão de registro](./ui/record-delete.md) ou [expirações do conjunto de dados na interface](./ui/dataset-expiration.md)ou por meio da API.

## Diretrizes de criação da ordem de serviço {#work-order-creation-guidelines}

Você pode usar o `/workorder` na API da Limpeza de dados para gerenciar de forma programática as solicitações de exclusão de registros no Experience Platform. Com esse endpoint, é possível criar uma solicitação de exclusão, verificar seu status ou atualizar uma solicitação existente. Consulte a [Documento de ponto de extremidade de ordem de trabalho](./api/workorder.md) para saber como executar essas ações usando a API.

>[!TIP]
>
>Uma ordem de serviço é uma solicitação estruturada que executa operações específicas de gerenciamento de dados, como limpeza ou transformação de dados, para garantir um processamento eficiente e sistemático.

Siga estas diretrizes para otimizar os envios de solicitações de limpeza:

1. **Maximizar identidades por solicitação:** Inclua até 100.000 identidades por solicitação de limpeza para melhorar a eficiência. Agrupar várias identidades em uma única solicitação ajuda a reduzir a frequência de chamadas de API e minimiza o risco de problemas de desempenho devido a solicitações excessivas de identidade única.
2. **Especificar conjuntos de dados individuais:** Para obter eficiência máxima, especifique o conjunto de dados individual a ser processado.
3. **Enviar várias solicitações:** Submeta várias solicitações com o máximo de contagens de identidade para obter um processamento mais rápido, à medida que as ordens de serviço são processadas em lote para obter eficiência.
4. **Considerações de limitação de API:** Considere a limitação da API para evitar lentidão. Solicitações menores (&lt; 100 IDs) em frequências mais altas podem resultar em 429 respostas e exigir o reenvio em taxas aceitáveis.

### Gerenciar erros 429 {#manage-429-errors}

Se você receber um erro 429, ele indica que você excedeu o número permitido de solicitações em um determinado período de tempo. Siga estas práticas recomendadas para gerenciar erros 429 de maneira eficaz:

- **Leia o cabeçalho &quot;Retry-After&quot;**: quando um erro 429 é retornado, verifique o cabeçalho de resposta &quot;Retry-After&quot;. Esse cabeçalho especifica o tempo de espera antes de repetir a solicitação.
- **Implementar lógica de repetição**: use o valor &quot;Repetir-após&quot; para implementar a lógica de repetição no aplicativo, garantindo que as tentativas sejam feitas após o tempo especificado para evitar erros 429 subsequentes.
- **Colocar suas solicitações em lote**: Evite enviar várias solicitações pequenas em rápida sucessão. Em vez disso, agrupe várias identidades em uma única solicitação para reduzir a frequência das chamadas e minimizar o risco de atingir limites de taxa.

## Expiração do conjunto de dados {#dataset-expiration}

Configure a limpeza automática do conjunto de dados para dados de vida curta. Use o `/ttl` na API de higiene de dados para agendar datas de expiração para conjuntos de dados. Use o `/ttl` ponto de extremidade para acionar uma limpeza do conjunto de dados com base em uma hora ou data especificada. Consulte o manual de endpoint de expiração do conjunto de dados para saber como [criar uma expiração do conjunto de dados](./api/dataset-expiration.md) e a variável [parâmetros de consulta aceitos](./api/dataset-expiration.md#query-params).

## Monitorar status de expiração da ordem de trabalho e do conjunto de dados {#monitor}

Você pode monitorar com eficiência o progresso do gerenciamento do ciclo de vida dos dados por meio do uso de **Eventos de E/S**. Um Evento de E/S é um mecanismo para receber notificações em tempo real sobre alterações ou atualizações em vários serviços na Plataforma.

Os alertas de Evento de E/S podem ser enviados para um webhook configurado para habilitar a automação do monitoramento de atividades. Para receber alertas via webhook, você deve registrar o webhook para alertas da Platform no Console do Adobe Developer. Consulte o guia sobre [assinatura de notificações de Adobe I/O Event](../observability/alerts/subscribe.md) para obter as instruções detalhadas.

Use os seguintes métodos e diretrizes do ciclo de vida dos dados para recuperar e monitorar efetivamente os status dos trabalhos:

### Eventos de E/S {#io-events}

Para monitorar com eficiência o progresso das tarefas do ciclo de vida dos dados, configure e use Eventos de I/O seguindo estas etapas:

- Configure webhooks para receber notificações por push sobre alterações de status.
- Use notificações para monitorar o progresso e receber atualizações após a conclusão.
- Evite implementar mecanismos de pesquisa para minimizar o tráfego da API.

### Recuperar respostas detalhadas para uma única ordem de serviço {#retrieve-detailed-work-order-response}

Para obter informações detalhadas sobre ordens de serviço individuais, use a seguinte abordagem:

- Faça uma solicitação GET para o `/workorder{work_order_id}` para obter dados de resposta detalhados.
- Recupere respostas específicas do produto e mensagens de sucesso.
- Evite usar esse método para atividades de pesquisa regulares.

Seguindo essas práticas recomendadas, você pode gerenciar com eficiência as solicitações de limpeza e otimizar os tempos de resposta no Gerenciamento avançado do ciclo de vida dos dados.
