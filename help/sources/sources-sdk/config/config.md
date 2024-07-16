---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Opções de configuração em fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Opções de configuração em fontes de autoatendimento (SDK em lote)

Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).

## Especificação de conexão

As especificações de conexão retornam as propriedades do conector de uma origem. Eles incluem especificações de autenticação relacionadas à criação de conexões de base e de origem e uma ID de especificação de conexão fixa que é atribuída a uma origem específica. As especificações de conexão são independentes de locatário e de organização. Uma especificação de conexão típica contém informações básicas sobre uma determinada origem, bem como três seções distintas: `authSpec`, `sourceSpec` e `exploreSpec`.

| Especificações | Descrição |
| --- | --- |
| `authSpec` | A matriz `authSpec` contém informações sobre os parâmetros de autenticação necessários para conectar uma origem à Platform. Qualquer origem fornecida pode suportar vários tipos diferentes de autenticação. |
| `sourceSpec` | A matriz `sourceSpec` contém informações gerais relacionadas a uma origem, incluindo informações sobre atributos necessários para apresentar a origem na interface, link de documentação e parâmetros relacionados à paginação, cabeçalho, corpo e agendamento. Além disso, `sourceSpec` descreve o esquema dos parâmetros necessários para criar uma conexão de origem a partir de uma conexão de base e é necessário para criar uma conexão de origem. |
| `exploreSpec` | A matriz `exploreSpec` define os parâmetros necessários para explorar e inspecionar objetos contidos na sua origem. O `exploreSpec` também define o formato de resposta retornado quando objetos são explorados e inspecionados. |

{style="table-layout:auto"}

## Preencher valores de especificação de conexão

Uma especificação de conexão pode ser dividida em três partes distintas: as especificações de autenticação, as especificações de origem e as especificações de exploração.

Consulte os seguintes documentos para obter instruções sobre como preencher os valores de cada parte de uma especificação de conexão:

* [Configurar sua especificação de autenticação](./authspec.md)
* [Configurar a especificação de origem](./sourcespec.md)
* [Configurar a especificação de exploração](./explorespec.md)
