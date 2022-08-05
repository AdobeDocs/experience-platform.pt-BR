---
keywords: Experience Platform; home; tópicos populares; mapear csv; mapear arquivo csv; mapear arquivo csv para xdm; mapear csv para xdm; guia da interface do usuário; mapeador; mapeamento; preparação de dados; preparação de dados;
solution: Experience Platform
title: Visão geral da preparação de dados
topic-legacy: overview
description: Este documento apresenta a Preparação de dados no Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d0f5d1f55101ce15934289d4fcfd1f70c1b63fc7
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---


# Visão geral da preparação de dados

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). A Preparação de dados aparece como uma etapa &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho de Assimilação CSV. Os engenheiros de dados podem usar a Preparação de dados para executar a seguinte manipulação de dados durante a assimilação:

- Definir mapeamentos de passagem simples para atribuir atributos de entrada a atributos XDM
- Criar campos calculados para executar cálculos na linha que podem ser atribuídos a atributos XDM
- Transforme os dados aplicando funções de manipulação de string, numérica ou de data
- Construir hierarquias XDM usando funções hierárquicas
- Visualizar os dados conforme são manipulados na Preparação de dados

A Preparação de dados também aplica várias validações de dados intrínsecas para garantir que a integridade dos dados seja mantida à medida que é assimilada. Sempre que possível, a Preparação de dados mapeia automaticamente os esquemas de dados recebidos para o XDM. Os engenheiros de dados podem alterar, corrigir e excluir os mapeamentos sugeridos e substituí-los pelos mapeamentos conforme apropriado.

>[!NOTE]
>
>A menos que a mensagem resultante seja um XDM inválido, qualquer erro de transformação na Preparação de dados resultará na definição desses atributos como `null`, enquanto o restante da linha será assimilado. Se a linha resolver para XDM inválido, a linha **not** ser assimilado. Em ambos os casos, o erro será documentado.

## Mapeamento

Um mapeamento é uma associação de um atributo de entrada ou campo calculado a um atributo XDM. Um único atributo pode ser mapeado para vários atributos XDM criando mapeamentos individuais.

Para saber mais sobre as diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md).

### Campos calculados

Os campos calculados permitem que os valores sejam criados com base nos atributos no schema de entrada. Esses valores podem ser atribuídos aos atributos no schema de destino e receber um nome e uma descrição para permitir uma referência mais fácil. Os campos calculados têm um comprimento máximo de 4096 caracteres.

Para saber mais sobre campos calculados, leia a [guia de campos calculados](./functions.md#calculated-fields).

### Evitar caracteres especiais

É possível evitar caracteres especiais em um campo usando `${...}`. No entanto, os arquivos JSON que contêm campos com um ponto final (`.`) não são compatíveis com esse mecanismo. Ao interagir com hierarquias, se um atributo filho tiver um ponto (`.`), você deve usar uma barra invertida (`\`) para escapar caracteres especiais. Por exemplo, `address` é um objeto que contém o atributo `street.name`, pode então ser referido como `address.street\.name` em vez de `address.street.name`.

## Conjunto de mapeamentos

Um conjunto de mapeamentos que transformam um schema em outro é conhecido coletivamente como um conjunto de mapeamentos. Um único conjunto de mapeamento é criado como parte de cada fluxo de dados. Um conjunto de mapeamento é parte integrante dos fluxos de dados e é criado, editado e monitorado como parte dos fluxos de dados.

Para saber mais sobre conjuntos de mapeamento, incluindo como usar os campos em um conjunto de mapeamento, leia o [guia de conjunto de mapeamento](./mapping-set.md). Para saber como criar um conjunto de mapeamento e usar outras chamadas de API relacionadas a conjuntos de mapeamento, leia a seção do conjunto de mapeamento no [guia do desenvolvedor](./api/mapping-set.md).

## Tratamento do formato de dados

A Preparação de dados pode lidar de forma robusta com diferentes formatos de dados assimilados na Plataforma. Para saber mais sobre como a Preparação de dados lê os diferentes tipos de dados, [visão geral do manuseio do formato de dados](./data-handling.md).

## Enviar atualizações de linha parciais usando o [!DNL Data Prep]

Streaming de upserts em [!DNL Data Prep] permite enviar atualizações de linha parciais para o [!DNL Profile Service] dados, além de criar e estabelecer novos links de identidade com uma única solicitação de API. Para saber mais sobre como fazer streaming de upserts em [!DNL Data Prep], consulte o documento em [envio de atualizações de linha parcial](./upserts.md).

## Controle de acesso com base em atributos no [!DNL Data Prep]

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

O controle de acesso baseado em atributos garante que você possa mapear apenas os atributos aos quais tem acesso. Os atributos aos quais você não tem acesso não podem ser usados em mapeamentos de passagem e campos calculados. Dessa forma, se você não tiver acesso a um campo obrigatório, não poderá salvar um mapeamento com êxito. Além disso, não é possível mapear objetos ou arrays de objetos se você não tiver acesso a nenhum dos atributos secundários. No entanto, é possível mapear outros elementos no objeto ou na matriz de objetos individualmente.

Consulte a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md) para obter mais informações.

## Próximas etapas

Este documento cobriu as noções básicas sobre Preparação de dados no Adobe Experience Platform. Para saber mais sobre as diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md). Para saber mais sobre como a Preparação de dados lê os diferentes tipos de dados, [guia de manipulação do formato de dados](./data-handling.md#dates). Para saber como usar a API de preparação de dados, leia o [Guia do desenvolvedor de Preparação de dados](api/overview.md).
