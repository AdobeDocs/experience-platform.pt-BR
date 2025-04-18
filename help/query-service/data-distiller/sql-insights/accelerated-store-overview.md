---
title: Visão geral da loja acelerada
description: Saiba como usar o armazenamento acelerado no Adobe Experience Platform para insights rápidos e baseados em SQL usando dados agregados. Esta página descreve o uso pretendido, restrições de identidade e dados de BI e práticas recomendadas para garantir a conformidade com as políticas de governança de dados da Adobe.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Visão geral da loja acelerada

O armazenamento acelerado no Adobe Experience Platform é uma camada de armazenamento otimizada para desempenho disponível por meio da SKU do Data Distiller. Ele foi projetado para conter conjuntos de dados pré-agregados, permitindo insights rápidos e baseados em SQL e renderização de painéis.

Este documento descreve como usar o armazenamento acelerado adequadamente, explica por que os conjuntos de dados agregados estão isentos dos processos padrão de higiene de dados e enfatiza que os dados de identidade não devem ser armazenados. Para estar em conformidade com as diretrizes do Adobe, você deve seguir as políticas de governança de dados e as restrições de uso descritas neste documento.

## Principais recursos {#key-capabilities}

O armazenamento acelerado foi desenvolvido especificamente para oferecer desempenho e eficiência. Ele permite workflows simplificados de consulta e relatórios, concentrando-se em dados agregados. A lista abaixo destaca seus principais recursos:

- Servir painéis e widgets de alto desempenho usando queries SQL
- Armazene conjuntos de dados pré-agregados projetados para insights recorrentes
- Oferecer suporte à criação de modelo de dados personalizado para relatórios de casos de uso

## Uso previsto {#intended-use}

O armazenamento acelerado foi criado **exclusivamente** para armazenar dados agregados que permitem o painel e a visualização otimizados. Sua arquitetura não se destina a suportar cargas de trabalho complexas, como processamento de business intelligence ou data warehouse.

>[!IMPORTANT]
>
>O armazenamento acelerado não substitui o data lake nem uma solução de armazenamento de uso geral.

## Restrições de uso {#usage-restrictions}

Para garantir a conformidade com o modelo de governança de dados e os termos de licenciamento da Adobe, as seguintes restrições se aplicam:

- **Não armazenar dados brutos do evento**
- **Não armazenar dados de identidade**
- **Não armazenar informações de identificação pessoal (PII)**, como endereços de email, dados da área de saúde ou identificadores de clientes
- **Não use o repositório acelerado para replicar todo o seu data lake**

Somente dados agregados não identificáveis podem ser armazenados no armazenamento acelerado. Conjuntos de dados agregados não podem ter a engenharia revertida para revelar os dados originais da origem, o que os torna isentos dos processos centralizados de higiene de dados da Experience Platform.

## Controle e conformidade {#governance-and-compliance}

Usar o armazenamento acelerado fora da finalidade pretendida pode colocar sua organização em risco de violar o contrato de licença da Adobe e os limites de governança de dados. Se ocorrerem incidentes de governança de dados devido a padrões de uso não compatíveis, sua organização assumirá total responsabilidade.

A Adobe não será responsável por quaisquer consequências decorrentes do uso indevido desse recurso.

Para saber mais sobre como gerenciar dados com responsabilidade no Experience Platform, consulte [Governança, privacidade e segurança no Experience Platform](../../../landing/governance-privacy-security/overview.md). Esta página descreve os serviços e as ferramentas que ajudam você a controlar os dados da experiência em alinhamento com as políticas de negócios, os requisitos legais e os padrões de desenvolvimento. Para obter links para orientações mais detalhadas sobre rotulagem de uso e aplicação de políticas, visite a [visão geral da Governança de dados](../../../data-governance/home.md).

## Práticas recomendadas {#best-practices}

Para garantir o uso eficiente e compatível do armazenamento acelerado, siga estas práticas recomendadas:

- Use conjuntos de dados derivados para criar tabelas pré-agregadas especificamente personalizadas para suas necessidades de painel
- Evite usar o armazenamento acelerado como local de preparo ou backup para conjuntos de dados brutos
- Revise regularmente seu uso para garantir o alinhamento com as medidas de proteção recomendadas pela Adobe

## Próximas etapas

Ao ler este documento, você aprendeu o que é o armazenamento acelerado, seu uso pretendido para dados agregados em cenários de relatórios e as regras de governança que devem ser seguidas para garantir o uso em conformidade. Para aprofundar sua compreensão e aplicar essas diretrizes de maneira eficaz, explore os seguintes recursos:

- [Visão geral do SQL Insights](./overview.md): saiba como o SQL Insights permite relatórios com desempenho otimizado usando conjuntos de dados agregados.
- [Enviar consultas aceleradas](./send-accelerated-queries.md): saiba como executar consultas no repositório acelerado para alimentar painéis e widgets.
- [Governança e higiene de dados](../../data-governance/overview.md): analise as políticas de higiene de dados e as diretrizes de governança da Adobe para garantir o uso em conformidade.
