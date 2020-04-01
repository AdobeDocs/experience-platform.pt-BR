---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral das políticas de uso de dados
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Visão geral das políticas de uso de dados

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados na Experience Platform.

Um exemplo de uma ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor dizendo que tipos específicos de dados, como Informações pessoais identificáveis (PII), não podem ser exportados e um rótulo &quot;I&quot; (Dados de identidade) tiver sido aplicado ao conjunto de dados, você receberá uma resposta do Serviço de política informando que uma política de uso de dados foi violada.

## Como criar e trabalhar com políticas de uso de dados

Depois que os rótulos de uso de dados forem aplicados, os administradores de dados poderão criar políticas usando a API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE.

Como um administrador de dados, você pode usar a API do Serviço de política para gerenciar e avaliar políticas relacionadas às ações de marketing que estão sendo realizadas em dados que contêm rótulos DULE. Usando a API, você pode criar e atualizar políticas, determinar o status de uma política e trabalhar com ações de marketing para avaliar se uma ação específica viola uma política de uso de dados.

Na API do Serviço de Política, todas as políticas e ações de marketing são referidas como `core` `custom` recursos ou recursos. `core` os recursos são definidos e mantidos pela Adobe, enquanto `custom` os recursos são criados e mantidos por clientes individuais. Os `custom` recursos são, portanto, únicos e visíveis apenas para a organização que os criou.

Para obter mais informações sobre como executar as operações principais fornecidas pela DULE Policy Service API, consulte o guia [do desenvolvedor do](../api/getting-started.md)Policy Service. Para obter instruções passo a passo sobre como trabalhar com políticas DULE, consulte o tutorial sobre como [criar e avaliar políticas](create.md)DULE.