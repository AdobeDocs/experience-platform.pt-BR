---
description: Saiba como o Experience Platform lida com diferentes tipos de erros retornados por destinos de transmissão e como ele tenta enviar dados novamente para a plataforma de destino.
title: Política de limitação de taxa e repetição para destinos de transmissão criados com o Destination SDK
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Política de limitação de taxa e repetição para destinos de transmissão criados com o Destination SDK

Os destinos criados por parceiros podem retornar vários erros e ter diferentes políticas de limitação de taxa. Esta página explica como o Experience Platform lida com diferentes tipos de erros retornados por destinos de transmissão.

Ao configurar um destino usando o Destination SDK, você pode selecionar entre dois tipos de agregação - [agregação de melhor esforço](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) e [agregação configurável](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Dependendo do tipo de agregação selecionado, leia abaixo como o Experience Platform trata os erros e as limitações de taxa.

## Agregação de melhor esforço {#best-effort-aggregation}

O Experience Platform tenta novamente chamadas que retornam os seguintes códigos de resposta HTTP: **403, 408, 409, 429, 500, 502, 503, 504**. Duas tentativas são executadas nos seguintes intervalos:

* Primeira tentativa: após 15 segundos
* Segunda tentativa: após 30 segundos

O Experience Platform *não* repete chamadas que retornam outros códigos de resposta HTTP, como 400 (Solicitação inválida). Se a chamada ainda falhar após ambas as tentativas, o Experience Platform descartará a ativação e não tentará novamente.

Você pode solicitar uma política de novas tentativas diferente para fluxos de dados específicos entrando em contato com o Suporte ao cliente.

## Agregação configurável {#configurable-aggregation}

No caso de plataformas de destino configuradas com agregação configurável, o Experience Platform distingue entre o tipo de erro retornado pela sua plataforma:

* Erros em que o Experience Platform tenta enviar novamente os dados para a sua plataforma:
   * Códigos de resposta HTTP 420 e 429
   * Códigos de resposta HTTP maiores que 500
* Erros em que o Experience Platform *não* tenta enviar novamente os dados para a sua plataforma: todos os outros retornados pela sua plataforma

### Abordagem de repetição descrita {#retry-approach}

A abordagem do Experience Platform para agregação configurável é descrita abaixo. Este exemplo pressupõe que o Experience Platform envia dados para uma plataforma de destino que começa a retornar 429 códigos de erro se receber mais de 50 mil solicitações por minuto:

* Minuto 1: o Experience Platform agrega 40 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz 40 mil solicitações HTTP e todas são bem-sucedidas.
* Minuto 2: o Experience Platform agrega 70 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz 70 mil solicitações HTTP e 50 mil são bem-sucedidas. Os outros 20 mil recebem um erro de limitação de taxa do seu endpoint e tentarão novamente em 30 minutos.
* Minuto 3: o Experience Platform agrega 30 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz 30 mil solicitações HTTP e todas são bem-sucedidas.
* ...
* ...
* Minuto 32: o Experience Platform tenta novamente enviar os 20 mil lotes que falharam no minuto 2. Todas as chamadas foram bem-sucedidas.

## Próximas etapas {#next-steps}

Agora você sabe como o Experience Platform trata os erros e a limitação de taxa das plataformas de destino, dependendo da política de agregação selecionada ao configurar o destino de transmissão. Em seguida, você pode revisar a seguinte documentação:

* [Testar a configuração de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Enviar para revisão um destino criado no Destination SDK](../guides/submit-destination.md)
