---
description: Saiba como o Experience Platform lida com diferentes tipos de erros retornados por destinos de streaming e como ele tenta enviar dados novamente para a plataforma de destino.
title: Política de limitação de taxa e tentativa para destinos de transmissão criados com Destination SDK
exl-id: 7a4edf8d-f905-4d55-a25d-4b9c6063ff88
source-git-commit: 61b8d40d6ecade10b0793bf7ad7c3e83974a0f02
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Política de limitação de taxa e tentativa para destinos de transmissão criados com Destination SDK

## Visão geral {#overview}

Os destinos criados por parceiros podem retornar vários erros e ter diferentes políticas de limitação de taxa. Esta página explica como o Experience Platform lida com diferentes tipos de erros retornados por destinos de streaming.

Ao configurar um destino usando o Destination SDK, você pode selecionar entre dois tipos de agregação - [agregação de melhor esforço](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) e [agregação configurável](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Dependendo do tipo de agregação selecionado, leia abaixo como o Experience Platform trata os erros e as limitações de taxa.

## Agregação de melhor esforço {#best-effort-aggregation}

Para qualquer chamada HTTP feita para seu destino que falhar, o Experience Platform tenta fazer a chamada novamente mais uma vez imediatamente após a primeira chamada. Se a chamada ainda falhar na segunda tentativa, o Experience Platform desconectará a chamada e não tentará novamente na terceira vez.

## Agregação configurável {#configurable-aggregation}

No caso de plataformas de destino configuradas com agregação configurável, o Experience Platform distingue entre o tipo de erro retornado pela sua plataforma:

* Erros em que o Experience Platform tenta enviar os dados para a sua plataforma:
   * Códigos de resposta HTTP 420 e 429
   * Códigos de resposta HTTP maiores que 500
* Erros em que Experience Platform *não* tentar enviar novamente os dados para sua plataforma: todos os outros retornados pela plataforma

### Abordagem de repetição descrita {#retry-approach}

A abordagem Experience Platform para agregação configurável é descrita abaixo. Este exemplo assume que o Experience Platform envia dados para uma plataforma de destino que começa a retornar 429 códigos de erro se receber mais de 50 mil solicitações por minuto:

* Minuto 1: o Experience Platform agrega 40 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz 40 mil solicitações HTTP e todas são bem-sucedidas.
* Minuto 2: o Experience Platform agrega 70 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz 70 mil solicitações HTTP e 50 mil são bem-sucedidas. Os outros 20 mil recebem um erro de limitação de taxa do seu endpoint e tentarão novamente em 30 minutos.
* Minuto 3: o Experience Platform agrega 30 mil lotes com perfis para enviar à sua plataforma de destino. O Experience Platform faz solicitações HTTP de 30k e todas são bem-sucedidas.
* ...
* ...
* Minuto 32: o Experience Platform tenta novamente enviar os 20 mil lotes que falharam no minuto 2. Todas as chamadas foram bem-sucedidas.

## Próximas etapas {#next-steps}

Agora você sabe como o Experience Platform trata os erros e a limitação de taxa das plataformas de destino, dependendo da política de agregação selecionada ao configurar o destino de transmissão. Em seguida, você pode revisar a seguinte documentação:

* [Testar a configuração de destino](/help/destinations/destination-sdk/test-destination.md)
* [Enviar para análise um destino criado no Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
