---
title: Migração do Data Lake para Gen2
description: Saiba mais sobre os novos recursos fornecidos pela migração do Data Lake para Gen2 no Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migração do Adobe Experience Platform Data Lake para Gen2

O Adobe Experience Platform está migrando para o Gen2 Data Lake. Esta é uma nova geração de data lake que oferece benefícios aos usuários da Platform, como replicação de regiões geográficas, controles de acesso mais refinados com base em funções (RBAC) e melhor dimensionamento.

## Impacto do usuário

Enquanto o Adobe estiver migrando o Data Lake de Gen1 para Gen 2, os usuários poderão **ler** do Data Lake, mas todos os recursos que **gravação** no Data Lake serão afetados. Veja abaixo uma lista dos recursos afetados:

- **Origens**: os dados provenientes das fontes e vários workflows de assimilação de dados serão atrasados. Os usuários verão seus dados quando a migração for concluída.
- **Serviço de consulta**: os usuários podem realizar consultas, mas não poderão gravar a saída da consulta em um conjunto de dados.
- **Perfil do cliente em tempo real**: dados assimilados no armazenamento de perfil por meio do **lote** a assimilação não estará disponível durante a migração. No entanto, os dados assimilados por meio do **transmissão** a assimilação estará disponível durante a migração. Além disso, as exportações de perfil não estarão disponíveis durante a migração.
- **Data Science Workspace**: as gravações do Espaço de trabalho de ciência de dados falharão.
- **Serviço de segmentação**: Públicos-alvo derivados de **lote** a segmentação não pode ser ativada durante a migração. Públicos-alvo derivados de **transmissão** a segmentação não será afetada.
- **Customer Journey Analytics**: os dados dos relatórios de Customer Journey Analytics podem estar desatualizados e não serão atualizados durante a migração, pois os lotes não estão sendo assimilados no Data Lake.

## Comunicação com os usuários da Platform

O Adobe entrará em contato com administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações IMS específicas.
