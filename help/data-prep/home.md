---
keywords: Experience Platform; home; tópicos populares; mapear csv; mapear arquivo csv; mapear arquivo csv para xdm; mapear csv para xdm; guia da interface do usuário; mapeador; mapeamento; preparação de dados; preparação de dados;
solution: Experience Platform
title: Visão geral da preparação de dados
topic: visão geral
description: Este documento apresenta a Preparação de dados no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 73bf6abb143c0866a400aafe984f9a553ffc1abf
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# Visão geral da preparação de dados

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). A Preparação de dados aparece como uma etapa &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho de Assimilação CSV. Os engenheiros de dados podem usar a Preparação de dados para executar a seguinte manipulação de dados durante a assimilação:

- Definir mapeamentos de passagem simples para atribuir atributos de entrada a atributos XDM
- Criar campos calculados para executar cálculos na linha que podem ser atribuídos a atributos XDM
- Transforme os dados aplicando funções de manipulação de string, numérica ou de data
- Construir hierarquias XDM usando funções hierárquicas
- Visualizar os dados conforme são manipulados na Preparação de dados

A Preparação de dados também aplica várias validações de dados intrínsecas para garantir que a integridade dos dados seja mantida à medida que é assimilada. Sempre que possível, a Preparação de dados mapeia automaticamente os esquemas de dados recebidos para o XDM. Os engenheiros de dados podem alterar, corrigir e excluir os mapeamentos sugeridos e substituí-los pelos mapeamentos conforme apropriado.

## Mapeamento

Um mapeamento é uma associação de um atributo de entrada ou campo calculado a um atributo XDM. Um único atributo pode ser mapeado para vários atributos XDM criando mapeamentos individuais.

Para saber mais sobre as diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md).

## Conjunto de mapeamentos

Um conjunto de mapeamentos que transformam um schema em outro é conhecido coletivamente como um conjunto de mapeamentos. Um único conjunto de mapeamento é criado como parte de cada fluxo de dados. Um conjunto de mapeamento é parte integrante dos fluxos de dados e é criado, editado e monitorado como parte dos fluxos de dados.

## Próximas etapas

Este documento cobriu as noções básicas sobre Preparação de dados no Adobe Experience Platform. Para saber mais sobre diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md). Para saber mais sobre as diferentes sequências de data e hora, leia o [guia de sequências de data](./dates.md). Para saber como usar a API de preparação de dados, leia o [Guia do desenvolvedor de preparação de dados](api/overview.md).