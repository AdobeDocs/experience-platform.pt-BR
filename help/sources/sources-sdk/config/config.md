---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Opções de configuração em Fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Opções de configuração em Fontes de autoatendimento (SDK em lote)

Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).

## Especificação de conexão

As especificações de conexão retornam as propriedades do conector de origem. Eles incluem especificações de autenticação relacionadas à criação das conexões base e de origem e uma ID de especificação de conexão fixa que é atribuída a uma fonte específica. As especificações de conexão são independentes de locatários e organizações. Uma especificação de conexão típica contém informações básicas sobre uma determinada fonte, bem como três seções distintas: `authSpec`, `sourceSpec`e `exploreSpec`.

| Especificações | Descrição |
| --- | --- |
| `authSpec` | O `authSpec` A matriz contém informações sobre os parâmetros de autenticação necessários para conectar uma fonte à Platform. Qualquer origem pode suportar vários tipos diferentes de autenticação. |
| `sourceSpec` | O `sourceSpec` O array contém informações gerais relacionadas a uma fonte, incluindo informações sobre atributos necessários para apresentar a fonte na interface do usuário, link de documentação e parâmetros relacionados à paginação, cabeçalho, corpo e agendamento. Além disso, `sourceSpec` descreve o esquema dos parâmetros necessários para criar uma conexão de origem a partir de uma conexão base e é necessário para criar uma conexão de origem. |
| `exploreSpec` | O `exploreSpec` array define os parâmetros necessários para explorar e inspecionar objetos contidos em sua origem. O `exploreSpec` também define o formato de resposta retornado quando os objetos são explorados e inspecionados. |

{style=&quot;table-layout:auto&quot;}

## Preencher valores de especificação de conexão

Uma especificação de conexão pode ser dividida em três partes distintas: as especificações de autenticação, as especificações de origem e as especificações de exploração.

Consulte os seguintes documentos para obter instruções sobre como preencher os valores de cada parte de uma especificação de conexão:

* [Configurar a especificação de autenticação](./authspec.md)
* [Configurar a especificação de origem](./sourcespec.md)
* [Configurar a especificação do explorador](./explorespec.md)
