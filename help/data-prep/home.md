---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;preparação de dados;preparação de dados;
solution: Experience Platform
title: Visão geral da preparação de dados
description: Este documento apresenta o Preparo de dados na Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Visão geral do Preparo de dados

O Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). O Preparo de dados é exibido como uma etapa de &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho Assimilação de CSV. Os engenheiros de dados podem usar o Preparo de dados para executar a seguinte manipulação de dados durante a assimilação:

- Definir mapeamentos de passagem simples para atribuir atributos de entrada a atributos XDM
- Criar campos calculados para realizar cálculos em linha que podem ser atribuídos a atributos XDM
- Transforme os dados aplicando funções de string, numéricas ou de manipulação de data
- Construir hierarquias XDM usando funções hierárquicas
- Visualizar os dados conforme são manipulados no Preparo de dados

O Preparo de dados também aplica várias validações de dados intrínsecas para garantir que a integridade dos dados seja mantida à medida que forem assimilados. Sempre que possível, o Preparo de dados mapeia automaticamente os esquemas de dados recebidos no XDM. Os engenheiros de dados podem alterar, corrigir e excluir os mapeamentos sugeridos e substituí-los pelos mapeamentos conforme apropriado.

>[!NOTE]
>
>A menos que a mensagem resultante seja um XDM inválido, quaisquer erros de transformação no Preparo de dados resultarão na definição desses atributos como `null`, enquanto o restante da linha será assimilado. Se a linha não resolver para XDM inválido, a linha **não** será assimilada. Em ambos os casos, o erro será documentado.

## Mapeamento

Um mapeamento é uma associação de um atributo de entrada ou campo calculado a um atributo XDM. Um único atributo pode ser mapeado para vários atributos XDM criando mapeamentos individuais.

Para saber mais sobre as diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md).

### Campos calculados

Os campos calculados permitem que valores sejam criados com base nos atributos no esquema de entrada. Esses valores podem ser atribuídos a atributos no esquema de destino e receber um nome e uma descrição para facilitar a referência. Os campos calculados têm um comprimento máximo de 4096 caracteres.

Para saber mais sobre campos calculados, leia o [guia de campos calculados](./functions.md#calculated-fields).

### Evitar caracteres especiais {#escape-special-characters}

Você pode escapar caracteres especiais em um campo usando `${...}`. No entanto, arquivos JSON que contêm campos com um ponto (`.`) não são suportados por esse mecanismo. Ao interagir com hierarquias, se um atributo filho tiver um ponto (`.`), você deverá usar uma barra invertida (`\`) para usar escape em caracteres especiais. Por exemplo, `address` é um objeto que contém o atributo `street.name`, ele pode ser chamado de `address.street\.name` em vez de `address.street.name`.

## Conjunto de mapeamentos

Um conjunto de mapeamentos que transformam um esquema em outro é coletivamente conhecido como um conjunto de mapeamentos. Um único conjunto de mapeamento é criado como parte de cada fluxo de dados. Um conjunto de mapeamento é parte integral dos fluxos de dados e é criado, editado e monitorado como parte dos fluxos de dados.

Para saber mais sobre conjuntos de mapeamento, incluindo como usar os campos em um conjunto de mapeamento, leia o [guia do conjunto de mapeamento](./mapping-set.md). Para saber como criar um conjunto de mapeamento e usar outras chamadas de API relacionadas aos conjuntos de mapeamento, leia a seção sobre o conjunto de mapeamento no [guia do desenvolvedor](./api/mapping-set.md).

## Manuseio de formato de dados

O Preparo de dados pode lidar com diferentes formatos de dados assimilados na Experience Platform. Para saber mais sobre como o Preparo de Dados lida com diferentes tipos de dados, leia a [visão geral do manuseio de formato de dados](./data-handling.md).

## Enviar atualizações parciais de linha usando [!DNL Data Prep]

A transmissão de sobreposições em [!DNL Data Prep] permite enviar atualizações de linhas parciais para dados de [!DNL Profile Service], além de criar e estabelecer novos links de identidade com uma única solicitação de API. Para saber mais sobre como fazer streaming de upserts em [!DNL Data Prep], consulte o documento em [enviando atualizações de linhas parciais](./upserts.md).

## Controle de acesso baseado em atributo em [!DNL Data Prep]

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

O controle de acesso baseado em atributos garante que você possa mapear apenas os atributos aos quais você tem acesso. Os atributos aos quais você não tem acesso não podem ser usados em mapeamentos de passagem e campos calculados. Dessa forma, se você não tiver acesso a um campo obrigatório, não poderá salvar um mapeamento com êxito. Além disso, não será possível mapear objetos ou arrays de objetos se você não tiver acesso a nenhum dos atributos filhos. No entanto, você pode mapear outros elementos no objeto ou na matriz de objetos individualmente.

Consulte a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md) para obter mais informações.

## Próximas etapas

Esse documento abordou as noções básicas sobre o Preparo de dados no Adobe Experience Platform. Para saber mais sobre as diferentes funções de mapeamento, leia o [guia de funções de mapeamento](./functions.md). Para saber mais sobre como o Preparo de Dados lida com diferentes tipos de dados, leia o [guia de manipulação de formato de dados](./data-handling.md#dates). Para saber como usar a API de Preparo de Dados, leia o [guia do desenvolvedor de Preparo de Dados](api/overview.md).
