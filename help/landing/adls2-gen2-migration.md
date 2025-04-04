---
title: Migração do Data Lake para Gen2
description: Saiba mais sobre os novos recursos fornecidos pela migração do Data Lake para Gen2 no Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Migração do Adobe Experience Platform Data Lake para Gen2

O Adobe Experience Platform está migrando para o Gen2 Data Lake. Esta é uma nova geração de data lake que oferece aos usuários da Experience Platform benefícios como replicação de geo-região, controles de acesso com base em função (RBAC) mais refinados e melhor dimensionamento.

## Impacto do usuário

Enquanto a Adobe está migrando o Data Lake de Gen1 para Gen 2, os usuários poderão **ler** do Data Lake, mas todos os recursos que **gravar** no Data Lake serão afetados. Veja abaixo uma lista dos recursos afetados:

- **Fontes**: os dados provenientes das fontes e vários fluxos de trabalho de assimilação de dados serão atrasados. Os usuários verão seus dados quando a migração for concluída.
- **Serviço de consulta**: os usuários podem realizar consultas, mas não poderão gravar a saída da consulta em um conjunto de dados.
- **Perfil de cliente em tempo real**: os dados assimilados no repositório de perfis por meio da assimilação de **lote** não estarão disponíveis durante a migração. Entretanto, os dados assimilados por meio da **transmissão** assimilação estarão disponíveis durante a migração. Além disso, as exportações de perfil não estarão disponíveis durante a migração.
- **Data Science Workspace**: as gravações do Data Science Workspace falharão.
- **Serviço de segmentação**: públicos-alvo derivados da segmentação **batch** não podem ser ativados durante a migração. Os públicos derivados da segmentação **streaming** não serão afetados.
- **Customer Journey Analytics**: os dados de relatórios do Customer Journey Analytics podem estar desatualizados e não serão atualizados durante a migração, pois os lotes não estão sendo assimilados no Data Lake.

## Comunicação com usuários do Experience Platform

A Adobe entrará em contato com os administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações específicas.
