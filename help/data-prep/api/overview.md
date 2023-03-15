---
keywords: Experience Platform;preparação de dados;api preparação de dados;solução de problemas;API
title: Visão geral da API de preparação de dados
description: A API de Preparo de dados permite criar programaticamente conjuntos de mapeamento e funções, permitindo transformar seus dados entre esquemas de origem e de destino.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guia da API do serviço de mapeamento

O Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). O Preparo de dados é exibido como uma etapa de &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho Assimilação de CSV.

A API do serviço de mapeamento, também conhecida como API de preparação de dados, inclui vários endpoints descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

## Funções

As funções do conjunto de mapeamento permitem transformar seus dados entre esquemas de origem e de destino. Você pode usar o `/languages/el` para validar suas expressões, bem como obter uma lista de todas as funções e operações do conjunto de mapeamento disponíveis.

Para obter informações detalhadas sobre como usar funções de conjunto de mapeamento, leia o [manual de endpoint de funções](./functions.md).

## Conjunto de mapeamento

Os conjuntos de mapeamento podem ser usados para definir como os dados em um esquema de origem são mapeados para o de um esquema de destino. Você pode usar o `/mappingSets` endpoint na API de Preparo de dados para recuperar, criar, atualizar e validar conjuntos de mapeamento de forma programática.

Para obter informações detalhadas sobre como usar conjuntos de mapeamento, leia o [guia de endpoint do conjunto de mapeamento](./mapping-set.md).

## Próximas etapas

Para começar a fazer chamadas usando a API do Serviço de mapeamento, leia a [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar os endpoints específicos.
