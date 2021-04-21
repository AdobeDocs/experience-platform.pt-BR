---
keywords: Experience Platform; home; tópicos populares; qualidade de dados; qualidade; Qualidade; Validação suportada; Validação; validação suportada;
solution: Experience Platform
title: Qualidade dos dados
topic-legacy: overview
description: O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a assimilação em lote e streaming no Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---

# Qualidade dos dados no Adobe Experience Platform

O Adobe Experience Platform fornece garantias bem definidas de integridade, precisão e consistência de todos os dados carregados por meio de assimilação em lote ou streaming. O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a assimilação em lote e streaming em [!DNL Experience Platform].

## Controlos compatíveis

|   | Assimilação em lote | Assimilação de fluxo |
| ------ | --------------- | ------------------- |
| Verificação do tipo de dados | Sim | Sim |
| Verificação de enumeração | Sim | Sim |
| Verificação do intervalo (mín., máx.) | Sim | Sim |
| Verificação de campo necessária | Sim | Sim |
| Verificação de padrão | Não | Sim |
| Verificação de formato | Não | Sim |

## Comportamentos de validação suportados

Tanto a assimilação em lote quanto a transmissão impedem que os dados com falha sejam downstream ao mover dados incorretos para recuperação e análise em [!DNL Data Lake]. A assimilação de dados fornece as seguintes validações para a assimilação em lote e streaming.

### Assimilação em lote

As seguintes validações são feitas para a assimilação em lote:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o schema esteja **não** vazio e contenha uma referência ao schema da união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| `createdUser` | Garante que o usuário que ingeriu o lote tenha permissão para ingerir o lote. |

### Assimilação por streaming

As seguintes validações são feitas para assimilação de streaming:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o schema esteja **não** vazio e contenha uma referência ao schema da união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| JSON | Garante que o JSON seja válido. |
| IMS Organization | Garante que a Organização IMS listada seja uma organização válida. |
| Nome da origem | Garante que o nome da fonte de dados seja especificado. |
| Conjunto de dados | Garante que o conjunto de dados seja especificado, ativado e não tenha sido removido. |
| Header | Garante que o cabeçalho seja especificado e seja válido. |

Mais informações sobre como [!DNL Platform] monitora e valida dados podem ser encontradas na [documentação de monitoramento de fluxos de dados](./monitor-data-ingestion.md).
