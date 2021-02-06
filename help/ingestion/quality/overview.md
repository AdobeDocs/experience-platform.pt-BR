---
keywords: Experience Platform;home;popular topics;Qualidade;Validação com suporte;Validação;validação com suporte;;home;popular topics;Data quality;Quality;Supported validation;Validation;supported validation;
solution: Experience Platform
title: Qualidade dos dados
topic: overview
description: O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a ingestão em lote e streaming no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---


# Qualidade de dados no Adobe Experience Platform

A Adobe Experience Platform oferece garantias bem definidas de integridade, precisão e consistência para todos os dados carregados por meio de ingestão em lote ou streaming. O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a ingestão em lote e streaming em [!DNL Experience Platform].

## Controlos suportados

|   | Ingestão em lote | Ingestão de fluxo |
| ------ | --------------- | ------------------- |
| Verificação do tipo de dados | Sim | Sim |
| Verificação de enumeração | Sim | Sim |
| Verificação de intervalo (mín., máx.) | Sim | Sim |
| Verificação de campo obrigatória | Sim | Sim |
| Verificação de padrão | Não | Sim |
| Verificação de formato | Não | Sim |

## Comportamentos de validação suportados

A ingestão em lote e em streaming evita que os dados com falha sejam enviados para downstream movendo dados incorretos para recuperação e análise em [!DNL Data Lake]. A ingestão de dados fornece as seguintes validações para a ingestão em lote e streaming.

### Assimilação em lote

As validações a seguir são feitas para a ingestão em lote:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Certifique-se de que o schema esteja **e não** vazio e contenha uma referência ao schema da união, da seguinte forma: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| `createdUser` | Certifique-se de que o usuário que ingeriu o lote tenha permissão para ingerir o lote. |

### Assimilação por streaming

As validações a seguir são feitas para a ingestão de streaming:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Certifique-se de que o schema esteja **e não** vazio e contenha uma referência ao schema da união, da seguinte forma: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| JSON | Certifique-se de que o JSON seja válido. |
| Organização IMS | Certifique-se de que a Organização IMS listada é uma organização válida. |
| Nome da fonte | Garante que o nome da fonte de dados seja especificado. |
| Conjunto de dados | Garante que o conjunto de dados seja especificado, ativado e não tenha sido removido. |
| Header | Garante que o cabeçalho seja especificado e seja válido. |

Mais informações sobre como [!DNL Platform] monitora e valida dados podem ser encontradas na [documentação de fluxo de dados de monitoramento](./monitor-data-ingestion.md).
