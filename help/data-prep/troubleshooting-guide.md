---
keywords: Experience Platform; home; tópicos populares;
title: Guia de solução de problemas da preparação de dados
topic-legacy: troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre a Preparação de dados do Adobe Experience Platform.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# [!DNL Data Prep] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Prep], bem como um guia de solução de problemas para erros comuns. Em caso de dúvidas e informações de solução de problemas relacionadas às APIs da plataforma em geral, consulte o [Guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista de perguntas frequentes sobre [!DNL Data Prep] e suas respostas.

### Como os erros de transformação são resolvidos?

[!DNL Data Prep] localiza todos os erros de transformação para a coluna em que ocorreram. Como resultado, essa coluna é nula e o restante da linha continuará sendo processado. Esses problemas de transformação são registrados como **Avisos**. É recomendável revisar os avisos periodicamente e ajustar a lógica de transformação para levar em conta os problemas de transformação. Isso aumentará a qualidade dos dados assimilados no Experience Platform.

Se as colunas forem marcadas como **Obrigatório** são anuladas devido a problemas de transformação, então a linha não será assimilada. Quando a assimilação de dados parciais estiver ativada, você pode definir o limite dessas rejeições antes que todo o fluxo falhe. Se o atributo anulado não afetou nenhuma validação de nível de esquema, a linha continuará a ser assimilada.

Todas as linhas que são inválidas mesmo sem erros de transformação também serão rejeitadas. Por exemplo, um fluxo de assimilação de dados pode ter um mapeamento de passagem (nenhuma lógica de transformação) para um campo obrigatório e não há valor de entrada para esse atributo. Esta linha será rejeitada.