---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualidade de ingestão de dados
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 6%

---


# Qualidade dos dados no Adobe Experience Platform

O Adobe Experience Platform oferece garantias bem definidas de integridade, precisão e consistência para todos os dados carregados por meio de ingestão em lote ou streaming. O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a ingestão em lote e streaming em [!DNL Experience Platform].

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

### Ingestão em lote

As validações a seguir são feitas para a ingestão em lote:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Certifique-se de que o schema **não** esteja vazio e contenha uma referência ao schema da união, da seguinte forma: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| `createdUser` | Certifique-se de que o usuário que ingeriu o lote tenha permissão para ingerir o lote. |

### Inclusão de transmissão

As validações a seguir são feitas para a ingestão de streaming:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Certifique-se de que o schema **não** esteja vazio e contenha uma referência ao schema da união, da seguinte forma: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| JSON | Certifique-se de que o JSON seja válido. |
| Organização IMS | Certifique-se de que a Organização IMS listada é uma organização válida. |
| Nome da fonte | Garante que o nome da fonte de dados seja especificado. |
| Conjunto de dados | Garante que o conjunto de dados seja especificado, ativado e não tenha sido removido. |
| Cabeçalho | Garante que o cabeçalho seja especificado e seja válido. |

Mais informações sobre como [!DNL Platform] monitores e validações de dados podem ser encontradas na documentação [de fluxos de dados de](./monitor-data-flows.md)monitoramento.
