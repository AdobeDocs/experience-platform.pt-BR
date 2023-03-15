---
keywords: Experience Platform;página inicial;tópicos populares;
title: Guia de solução de problemas de preparação de dados
description: Este documento fornece respostas a perguntas frequentes sobre o Preparo de dados da Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Prep], bem como um guia de solução de problemas para erros comuns. Para obter perguntas e informações de solução de problemas relacionadas às APIs da plataforma em geral, consulte o [Guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista das perguntas frequentes sobre [!DNL Data Prep] e suas respostas.

### Como os erros de transformação são resolvidos?

[!DNL Data Prep] localiza todos os erros de transformação na coluna em que ocorreram. Como resultado, essa coluna é anulada e o restante da linha continuará a ser processado. Esses problemas de transformação são registrados como **Avisos**. É recomendável que você revise os avisos periodicamente e ajuste a lógica de transformação para levar em conta os problemas de transformação. Isso aumentará a qualidade dos dados assimilados no Experience Platform.

Se as colunas marcadas como **Obrigatório** forem anuladas devido a problemas de transformação, a linha não será assimilada. Quando a assimilação parcial de dados está ativada, é possível definir o limite dessas rejeições antes que todo o fluxo falhe. Se o atributo nulo não tiver afetado nenhuma validação de nível de esquema, a linha continuará sendo assimilada.

Quaisquer linhas inválidas, mesmo sem erros de transformação, também serão rejeitadas. Por exemplo, um fluxo de assimilação de dados pode ter um mapeamento de passagem (sem lógica de transformação) para um campo obrigatório e não há valor de entrada para esse atributo. Esta linha será rejeitada.

### Como posso escapar caracteres especiais em um campo?

É possível escapar caracteres especiais em um campo usando `${...}`. No entanto, os arquivos JSON que contêm campos com um ponto (`.`) não são compatíveis com esse mecanismo. Ao interagir com hierarquias, se um atributo filho tiver um ponto (`.`), você deve usar uma barra invertida (`\`) para evitar caracteres especiais. Por exemplo, `address` é um objeto que contém o atributo `street.name`, pode ser referido como `address.street\.name` em vez de `address.street.name`.

### Qual é o comprimento máximo dos campos calculados?

Os campos calculados têm um comprimento máximo de 4096 caracteres.