---
keywords: Experience Platform; home; tópicos populares; qualidade de dados; qualidade; Qualidade; Validação suportada; Validação; validação suportada;
solution: Experience Platform
title: Qualidade dos dados
topic-legacy: overview
description: O documento a seguir fornece um resumo das verificações e comportamentos de validação suportados para a assimilação em lote e streaming no Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 7857b9a82dc1b5e12c9f8d757f6967b926124ec4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

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

Tanto a assimilação em lote quanto a transmissão impedem que os dados com falha sejam transferidos pela movimentação de dados incorretos para recuperação e análise em [!DNL Data Lake]. A assimilação de dados fornece as seguintes validações para a assimilação em lote e streaming.

### Assimilação em lote

As seguintes validações são feitas para a assimilação em lote:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o esquema seja **not** vazio e contém uma referência ao schema de união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| `createdUser` | Garante que o usuário que ingeriu o lote tenha permissão para ingerir o lote. |

### Assimilação por streaming

As seguintes validações são feitas para assimilação de streaming:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o esquema seja **not** vazio e contém uma referência ao schema de união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| JSON | Garante que o JSON seja válido. |
| IMS Organization | Garante que a Organização IMS listada seja uma organização válida. |
| Nome da origem | Garante que o nome da fonte de dados seja especificado. |
| Conjunto de dados | Garante que o conjunto de dados seja especificado, ativado e não tenha sido removido. |
| Header | Garante que o cabeçalho seja especificado e seja válido. |

Mais informações sobre como [!DNL Platform] monitora e valida dados que podem ser encontrados no [documentação de monitoramento de fluxos de dados](./monitor-data-ingestion.md).

## Validação do valor de identidade

A tabela a seguir descreve as regras existentes que devem ser seguidas para garantir uma validação bem-sucedida do seu valor de identidade.

| Namespace | Regra de validação | Comportamento do sistema quando a regra é violada |
| --- | --- | --- |
| ECID | <ul><li>O valor de identidade de uma ECID deve ter exatamente 38 caracteres.</li><li>O valor de identidade de uma ECID deve consistir apenas em números.</li></ul> | <ul><li>Se o valor de identidade de ECID não for exatamente 38 caracteres, o registro será ignorado.</li><li>Se o valor de identidade de ECID contiver caracteres não numéricos, o registro será ignorado.</li></ul> |
| Não ECID | O valor de identidade não pode exceder 1024 caracteres. | Se o valor de identidade exceder 1024 caracteres, o registro será ignorado. |

Para obter mais informações sobre [!DNL Identity Service] painéis, consulte o [[!DNL Identity Service] visão geral das medidas de proteção](../../identity-service/guardrails.md).
