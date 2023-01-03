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

O Adobe Experience Platform está migrando para o Gen2 Data Lake. Esta é uma nova geração de data lake que oferece benefícios aos usuários da plataforma, como replicação de região geográfica, controles de acesso baseados em funções (RBAC) mais refinados e melhor dimensionamento.

## Impacto do usuário

Enquanto o Adobe está migrando o Data Lake do Gen1 para o Gen 2, os usuários poderão **read** do Data Lake, mas todos os recursos que **gravação** no Data Lake será afetado. Veja abaixo uma lista de recursos afetados:

- **Fontes**: Os dados provenientes das fontes e de vários workflows de assimilação de dados serão atrasados. Os usuários verão seus dados após a conclusão da migração.
- **Serviço de query**: Os usuários podem realizar consultas, mas não poderão gravar a saída da consulta em um conjunto de dados.
- **Perfil do cliente em tempo real**: Dados assimilados no armazenamento do Perfil por meio de **lote** a assimilação não estará disponível durante a migração. No entanto, os dados assimilados por **transmissão** a assimilação estará disponível durante a migração. Além disso, as exportações do perfil não estarão disponíveis durante a migração.
- **Data Science Workspace**: As gravações do Data Science Workspace falharão.
- **Serviço de segmentação**: Públicos-alvo derivados de **lote** não é possível ativar a segmentação durante a migração. Públicos-alvo derivados de **transmissão** a segmentação não será afetada.
- **Customer Journey Analytics**: Os dados dos relatórios de Customer Journey Analytics podem estar desatualizados e não serão atualizados durante a migração, pois os lotes não estão sendo assimilados no Data Lake.

## Comunicação com os usuários da plataforma

O Adobe entrará em contato com os administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas de migração de determinadas organizações IMS.
