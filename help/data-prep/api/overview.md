---
keywords: Experience Platform, preparação de dados, api de preparação de dados, solução de problemas, API
title: Visão geral da API de preparação de dados
topic: guia
description: A API de preparação de dados permite criar programaticamente conjuntos e funções de mapeamento, permitindo transformar seus dados entre esquemas de origem e de destino.
translation-type: tm+mt
source-git-commit: cae6dc80d0394db51dc97478b92459be64c64498
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Guia da API do serviço de mapeamento

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). A Preparação de dados aparece como uma etapa &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho de Assimilação CSV.

A API do serviço de mapeamento, também conhecida como API de preparação de dados, inclui vários pontos de extremidade descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

## Funções

As funções do conjunto de mapeamento permitem transformar seus dados entre os esquemas de origem e de destino. Você pode usar o endpoint `/languages/el` para validar suas expressões, bem como obter uma lista de todas as funções e operações disponíveis do conjunto de mapeamentos.

Para obter informações detalhadas sobre como usar funções do conjunto de mapeamentos, leia o [guia do ponto de extremidade de funções](./functions.md).

## Conjunto de mapeamentos

Conjuntos de mapeamento podem ser usados para definir como os dados em um schema de origem mapeiam para o de um schema de destino. Você pode usar o terminal `/mappingSets` na API de Preparação de dados para recuperar, criar, atualizar e validar programaticamente os conjuntos de mapeamento.

Para obter informações detalhadas sobre como usar conjuntos de mapeamento, leia o [guia do ponto de extremidade do conjunto de mapeamento](./mapping-set.md).

## Próximas etapas

Para começar a fazer chamadas usando a API do Serviço de mapeamento, leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar os pontos de extremidade específicos.