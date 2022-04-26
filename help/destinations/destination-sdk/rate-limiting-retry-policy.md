---
description: Saiba como o Experience Platform lida com diferentes tipos de erros retornados por destinos de transmissão e como ele tenta enviar dados novamente para a plataforma de destino.
title: Taxa de limitação e política de tentativa para destinos de streaming criados com o Destination SDK
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Taxa de limitação e política de tentativa para destinos de streaming criados com o Destination SDK

## Visão geral {#overview}

Destinos criados por parceiros podem retornar vários erros e ter diferentes políticas de limitação de taxa. Esta página explica como o Experience Platform lida com diferentes tipos de erros retornados por destinos de transmissão.

Ao configurar um destino usando o Destination SDK, você pode selecionar entre dois tipos de agregação - [melhor agregação de esforço](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) e [agregação configurável](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Dependendo do tipo de agregação selecionado, leia abaixo como o Experience Platform lida com erros e limitações de taxa.

## Melhor agregação de esforço {#best-effort-aggregation}

Para qualquer chamada HTTP feita para seu destino que falhe, o Experience Platform tenta fazer a chamada novamente mais uma vez imediatamente após a primeira chamada. Se a chamada ainda falhar na segunda tentativa, o Experience Platform descarta a chamada e não a tenta novamente uma terceira vez.

## Agregação configurável {#configurable-aggregation}

No caso de plataformas de destino configuradas com agregação configurável, o Experience Platform faz a distinção entre o tipo de erro retornado pela plataforma:

* Erros em que o Experience Platform tenta enviar os dados para a sua plataforma:
   * Códigos de resposta HTTP 420 e 429
   * Códigos de resposta HTTP maiores que 500
* Erros em que Experience Platform *não* tente enviar os dados novamente para a sua plataforma: todos os outros retornados pela plataforma

### Método de repetição descrito {#retry-approach}

A abordagem Experience Platform para agregação configurável é descrita abaixo. Esse exemplo assume que o Experience Platform envia dados para uma plataforma de destino que começa a retornar códigos de erro 429 se receber mais de 50 mil solicitações por minuto:

* Minuto 1: O Experience Platform agrega 40 mil lotes com perfis para enviar à plataforma de destino. O Experience Platform faz solicitações HTTP 40k e todas são bem-sucedidas.
* Minuto 2: O Experience Platform agrega 70k lotes com perfis para enviar à plataforma de destino. O Experience Platform faz solicitações HTTP de 70k e 50k são bem-sucedidas. Os outros 20k recebem um erro de limite de taxa do seu ponto de extremidade e serão tentados novamente em 30 minutos.
* Minuto 3: O Experience Platform agrega 30k lotes com perfis para enviar à plataforma de destino. O Experience Platform faz solicitações HTTP de 30k e todas são bem-sucedidas.
* ...
* ...
* Minuto 32: O Experience Platform tenta reenviar os lotes de 20 mil que falharam no minuto 2. Todas as chamadas são bem-sucedidas.

## Próximas etapas {#next-steps}

Agora você sabe como o Experience Platform trata os erros e a limitação de taxa das plataformas de destino, dependendo da política de agregação selecionada ao configurar seu destino de transmissão. Em seguida, você pode revisar a seguinte documentação:

* [Testar a configuração de destino](/help/destinations/destination-sdk/test-destination.md)
* [Enviar para revisão de um destino criado no Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
