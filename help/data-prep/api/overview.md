---
keywords: Experience Platform, preparação de dados, api de preparação de dados, solução de problemas, API
title: Visão geral da API de preparação de dados
description: A API de preparação de dados permite criar programaticamente conjuntos e funções de mapeamento, permitindo transformar seus dados entre esquemas de origem e de destino.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guia da API do serviço de mapeamento

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). A Preparação de dados aparece como uma etapa &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho de Assimilação CSV.

A API do serviço de mapeamento, também conhecida como API de preparação de dados, inclui vários pontos de extremidade descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

## Funções

As funções do conjunto de mapeamento permitem transformar seus dados entre os esquemas de origem e de destino. Você pode usar o `/languages/el` endpoint para validar suas expressões e obter uma lista de todas as funções e operações disponíveis do conjunto de mapeamentos.

Para obter informações detalhadas sobre como usar funções do conjunto de mapeamentos, leia o [guia do endpoint das funções](./functions.md).

## Conjunto de mapeamentos

Conjuntos de mapeamento podem ser usados para definir como os dados em um schema de origem mapeiam para o de um schema de destino. Você pode usar o `/mappingSets` endpoint na API de preparação de dados para recuperar, criar, atualizar e validar programaticamente os conjuntos de mapeamento.

Para obter informações detalhadas sobre como usar conjuntos de mapeamento, leia o [guia de endpoint do conjunto de mapeamento](./mapping-set.md).

## Próximas etapas

Para começar a fazer chamadas usando a API do Serviço de mapeamento, leia o [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar os endpoints específicos.
