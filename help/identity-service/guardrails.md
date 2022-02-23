---
keywords: Experience Platform, identidade, serviço de identidade, solução de problemas, medidas de proteção, diretrizes, limite;
title: Garantias do serviço de identidade
description: Este documento fornece informações sobre limites de uso e de taxa para dados do Serviço de identidade para ajudar você a otimizar o uso do gráfico de identidade.
source-git-commit: b36ace84acdb13b89deb6f77a02c298acade8d8e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Medidas de proteção [!DNL Identity Service] dados

Este documento fornece informações sobre o uso e limites de taxa para [!DNL Identity Service] dados para ajudá-lo a otimizar o uso do gráfico de identidade. Ao revisar as seguintes medidas de proteção, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do serviço de atendimento ao cliente.

## Introdução

Os seguintes serviços do Experience Platform estão envolvidos com a modelagem de dados de identidade:

* [Identidades](home.md): Unir identidades de fontes de dados diferentes à medida que são assimiladas na plataforma.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Crie perfis de consumidor unificados usando dados de várias fontes.

## Limites do modelo de dados

As tabelas abaixo fornecem orientação sobre grades para limites estáticos, bem como regras de validação a serem consideradas para namespaces de identidade.

### Limites estáticos

A tabela a seguir descreve os limites estáticos aplicados aos dados de identidade.

| Grade de Proteção | Limite | Notas |
| --- | --- | --- |
| Número de identidades em um gráfico | 150 | O gráfico de identidade não será atualizado assim que o limite for atingido. |
| Número de identidades em um registro XDM | 20 | O número mínimo de registros XDM necessários é dois. |
| Número de namespaces personalizados | None | Não há limites para o número de namespaces personalizados que podem ser criados. |
| Número de gráficos | Nenhum | Não há limites para o número de gráficos de identidade que você pode criar. |
| Número de caracteres para um nome de exibição de namespace ou símbolo de identidade | Nenhum | Não há limites para o número de caracteres de um nome de exibição de namespace ou símbolo de identidade. |

### Validação do valor de identidade

A tabela a seguir descreve as regras existentes que devem ser seguidas para garantir uma validação bem-sucedida do seu valor de identidade.

| Namespace | Regra de validação | Comportamento do sistema quando a regra é violada |
| --- | --- | --- |
| ECID | <ul><li>O valor de identidade de uma ECID deve ter exatamente 38 caracteres.</li><li>O valor de identidade de uma ECID deve consistir apenas em números.</li></ul> | <ul><li>Se o valor de identidade de ECID não for exatamente 38 caracteres, o registro será ignorado.</li><li>Se o valor de identidade de ECID contiver caracteres não numéricos, o registro será ignorado.</li></ul> |
| Não ECID | O valor de identidade não pode exceder 1024 caracteres. | Se o valor de identidade exceder 1024 caracteres, o registro será ignorado. |

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre [!DNL Identity Service]:

* [[!DNL Identity Service] visão geral](home.md)
* [Visualizador de gráfico de identidade](ui/identity-graph-viewer.md)
