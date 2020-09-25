---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Migração do Adobe Experience Platform Data Lake para o Gen2

A Adobe Experience Platform está migrando para o Gen2 Data Lake. Esta é uma nova geração de lacuna de dados que oferece aos usuários da plataforma benefícios como replicação geo-regional, controles de acesso baseados em funções mais finas (RBAC) e melhor dimensionamento.

## Impacto do usuário

Enquanto a Adobe está migrando o Data Lake da geração 1 para a geração 2, os usuários poderão **ler** do Data Lake, mas todos os recursos que **gravarem** no Data Lake serão afetados. Abaixo está uma lista de recursos afetados:

- **Fontes**: Os dados provenientes das fontes e de vários workflows de ingestão de dados serão atrasados. Os usuários verão seus dados assim que a migração for concluída.
- **Serviço** de query: Os usuários podem executar query, mas não poderão gravar a saída do query em um conjunto de dados.
- **Perfil** do cliente em tempo real: Os dados ingeridos no repositório de Perfis por meio da ingestão em **lote** não estarão disponíveis durante a migração. No entanto, os dados ingeridos por meio da ingestão de **streaming** estarão disponíveis durante a migração. Além disso, as exportações de Perfis não estarão disponíveis durante a migração.
- **Área de trabalho** da ciência de dados: As gravações da Data Science Workspace falharão.
- **Serviço** de segmentação: Audiências derivadas da segmentação de **lote** não podem ser ativadas durante a migração. Audiências derivadas da segmentação de **streaming** não serão afetadas.
- **Customer Journey Analytics**: Os dados dos relatórios de Customer Journey Analytics podem estar desatualizados e não serão atualizados durante a migração, pois os lotes não estão sendo ingeridos no Data Lake.

## Comunicação aos usuários da plataforma

O Adobe entrará em contato com os administradores de sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações IMS específicas.