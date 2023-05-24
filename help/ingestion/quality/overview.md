---
keywords: Experience Platform;página inicial;tópicos populares;Qualidade dos dados;qualidade;Qualidade;Validação suportada;Validação suportada;
solution: Experience Platform
title: Qualidade dos dados
description: O documento a seguir fornece um resumo das verificações compatíveis e dos comportamentos de validação para assimilação em lote e por transmissão no Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---

# Qualidade dos dados no Adobe Experience Platform

O Adobe Experience Platform fornece garantias bem definidas de integridade, precisão e consistência para quaisquer dados carregados por meio de assimilação em lote ou por transmissão. O documento a seguir fornece um resumo das verificações compatíveis e dos comportamentos de validação para assimilação em lote e por transmissão no [!DNL Experience Platform].

## Verificações suportadas

|   | Assimilação em lote | Assimilação de transmissão |
| ------ | --------------- | ------------------- |
| Verificação de tipo de dados | Sim | Sim |
| Verificação de enumeração | Sim | Sim |
| Verificação de intervalo (mín., máx.) | Sim | Sim |
| Verificação de campo obrigatória | Sim | Sim |
| Verificação de padrão | Não | Sim |
| Verificação de formato | Não | Sim |

## Comportamentos de validação compatíveis

A assimilação em lote e por transmissão evita que dados com falha sejam transferidos para downstream, movendo dados incorretos para recuperação e análise no [!DNL Data Lake]. A assimilação de dados fornece as seguintes validações para assimilação em lote e por transmissão.

### Assimilação em lote

As seguintes validações são feitas para assimilação em lote:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o esquema seja **não** vazio e contém uma referência ao esquema de união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| `createdUser` | Garante que o usuário que assimilou o lote tenha permissão para assimilar o lote. |

### Assimilação por streaming

As seguintes validações são feitas para a assimilação por transmissão:

| Área de validação | Descrição |
| --------------- | ----------- |
| Esquema | Garante que o esquema seja **não** vazio e contém uma referência ao esquema de união, da seguinte maneira: `"meta:immutableTags": ["union"]` |
| `identityField` | Garante que todos os descritores de identidade válidos sejam definidos. |
| JSON | Garante que o JSON seja válido. |
| Organização | Garante que a organização listada seja válida. |
| Nome de origem | Garante que o nome da fonte de dados seja especificado. |
| Conjunto de dados | Garante que o conjunto de dados seja especificado, ativado e não tenha sido removido. |
| Header | Garante que o cabeçalho seja especificado e seja válido. |

Mais informações sobre como [!DNL Platform] O monitora e valida dados que podem ser encontrados no [documentação de monitoramento de fluxos de dados](./monitor-data-ingestion.md).

## Validação do valor de identidade

A tabela a seguir descreve as regras existentes que devem ser seguidas para garantir uma validação bem-sucedida do valor de identidade.

| Namespace | Regra de validação | Comportamento do sistema quando a regra é violada |
| --- | --- | --- |
| ECID | <ul><li>O valor de identidade de uma ECID deve ter exatamente 38 caracteres.</li><li>O valor de identidade de uma ECID deve consistir apenas em números.</li></ul> | <ul><li>Se o valor de identidade da ECID não tiver exatamente 38 caracteres, o registro será ignorado.</li><li>Se o valor de identidade da ECID contiver caracteres não numéricos, o registro será ignorado.</li></ul> |
| Não ECID | O valor de identidade não pode exceder 1024 caracteres. | Se o valor de identidade exceder 1024 caracteres, o registro será ignorado. |

Para obter mais informações sobre [!DNL Identity Service] medidas de proteção, consulte o [[!DNL Identity Service] visão geral das medidas de proteção](../../identity-service/guardrails.md).
