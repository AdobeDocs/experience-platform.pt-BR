---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Opções de configuração no SDK do Forms
topic-legacy: overview
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar o SDK das Fontes.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# Opções de configuração no SDK do Forms

>[!IMPORTANT]
>
>O SDK das Fontes está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade descrita nesta documentação está sujeita a alterações.

Este documento fornece uma visão geral das configurações que você precisa preparar para usar o SDK das Fontes.

## Especificação de conexão

As especificações de conexão retornam as propriedades do conector de origem. Eles incluem especificações de autenticação relacionadas à criação das conexões base e de origem e uma ID de especificação de conexão fixa que é atribuída a uma fonte específica. As especificações de conexão são independente do locatário e da IMS Organization. Uma especificação de conexão típica contém informações básicas sobre uma determinada fonte, bem como três seções distintas: `authSpec`, `sourceSpec`e `exploreSpec`.

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


