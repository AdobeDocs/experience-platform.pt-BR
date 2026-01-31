---
title: Atualizações de arquitetura para o Real-Time CDP B2B edition
description: Leia este documento para saber mais sobre as atualizações abrangentes da arquitetura do Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: da288d1a917df85b3c003bc6592fda7a6f1eafe7
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---

# Atualizações de arquitetura no Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Este documento descreve as atualizações de arquitetura das edições B2B e B2P do Real-Time CDP. As atualizações não exigirão nenhuma ação da maioria dos clientes. No entanto, há públicos que não podem ser atualizados automaticamente. A Adobe trabalhará diretamente com você para abordar esses cenários. Consulte este documento para obter informações sobre como as atualizações afetarão os recursos existentes do Adobe Experience Platform. Em caso de dúvidas, entre em contato com a equipe de conta da Adobe.

A Adobe reprojetou as edições B2B e B2P do Real-Time CDP para aprimorar a escalabilidade, o desempenho e a confiabilidade, além de oferecer suporte a casos de uso B2B mais avançados. Para garantir que todos os clientes se beneficiem dessas melhorias, a Adobe atualizará todos os clientes B2B e B2P existentes para a nova arquitetura.

Use a arquitetura aprimorada para obter os seguintes benefícios:

* **Escalabilidade da assimilação de dados**: melhoria do suporte para relações B2B de alta cardinalidade, como contas conectadas a milhares de pessoas.
* **Avaliação de público-alvo confiável e eficiente**: segmentação mais rápida e resiliente para públicos-alvo B2B complexos.
* **resolução da entidade**: resolução de identidade aprimorada para entidades B2B, qualidade de dados aprimorada e duplicação reduzida para permitir segmentação e agregação mais precisas.

## Novos recursos

Leia a seguir os principais aprimoramentos incluídos na atualização de arquitetura.

### Instantâneos de conta para associação de público-alvo

Com a nova arquitetura B2B, os detalhes de associação de público-alvo agora são incluídos para entidades de conta em exportações de instantâneo. Esse recurso permite acessar o status do público-alvo no nível da conta, carimbos de data e hora e indicadores de associação.

Com essa atualização, agora é possível:

* Permita que as equipes de marketing e operações validem diretamente a associação ao público-alvo da conta.
* Obtenha paridade de recursos entre seus modelos de segmentação de perfil (pessoa) e conta, garantindo uma experiência consistente em todas as entidades.

Leia a documentação em [públicos-alvo da conta](../segmentation/types/account-audiences.md) para obter mais informações.

### Contagem de público-alvo para públicos-alvo que incluem entidades B2B

As estimativas de tamanho do público-alvo para públicos-alvo com entidades B2B agora são calculadas com precisão exata. Essas estimativas estão disponíveis durante a pré-visualização e fornecem insights mais precisos e confiáveis para públicos-alvo que envolvem relacionamentos B2B complexos.

Com essa atualização, agora é possível:

* Use insights de estimativas precisas de tamanho do público-alvo para melhorar o planejamento e a tomada de decisões durante o processo de criação do público-alvo.
* Projete públicos-alvo complexos B2B com confiança, sabendo de uma estimativa de público-alvo mais precisa.
* Permita um planejamento de campanha mais inteligente, um direcionamento mais preciso e uma melhor alocação de recursos.

Leia a documentação em [públicos-alvo da conta](../segmentation/types/account-audiences.md) para obter mais informações.

## Atualizações para recursos existentes

Os seguintes recursos foram atualizados como parte das atualizações de arquitetura B2B.

### Atualizações para público-alvo de várias entidades com atributos B2B e eventos de experiência

Como parte da nova atualização da arquitetura, os filtros de Evento de experiência não podem mais ser usados em um único público de várias entidades que inclui atributos B2B.

Para obter a mesma lógica de público-alvo, você pode usar o construtor de segmentos para [adicionar públicos-alvo e públicos de referência](../segmentation/ui/segment-builder.md#adding-audiences)

Por exemplo:

* Criar um público-alvo do evento de experiência
   * Defina a condição comportamental separadamente. Por exemplo: &quot;Pessoas que visitaram a página de preços nos últimos três dias&quot;.
* Crie um público-alvo com várias entidades com atributos B2B.
   * Aqui, você pode fazer referência ao público-alvo do Evento de experiência como parte dos critérios deste público-alvo. Por exemplo: &quot;Pessoas que são **&#39;Tomador de Decisão&#39;** de qualquer oportunidade em que a conta esteja no setor **&#39;Finanças&#39;** e membro do público-alvo de pessoas que visitou a página de preços nos últimos três dias.

Quando a atualização for concluída, todos os novos públicos-alvo de várias entidades com atributos B2B e Eventos de experiência deverão ser criados usando a abordagem [segmento de segmento](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types).

>[!TIP]
>
>Um **segmento de segmentos** é qualquer definição de segmento que contenha um ou mais segmentos de lote ou de borda. **Observação**: se você usar um segmento de segmentos, a desqualificação de perfis ocorrerá **a cada 24 horas**.

### Mesclagem de resolução de entidade e precedência de tempo em públicos B2B

Como parte da atualização da arquitetura, a Adobe está introduzindo a resolução de entidades para contas e oportunidades. A resolução da entidade é baseada na correspondência de ID determinística e nos dados mais recentes. O trabalho de resolução da entidade é executado diariamente durante a segmentação em lote, antes da avaliação de públicos-alvo de várias entidades com atributos B2B.

>[!BEGINSHADEBOX]

#### Como funciona a resolução da entidade?

* **Antes**: se um número DUNS (Sistema de Numeração Universal de Dados) foi usado como uma identidade adicional e o número DUNS da conta foi atualizado em um sistema de origem como o CRM, a ID da conta será vinculada a números DUNS antigos e novos.
* **Depois**: se o número DUNS foi usado como uma identidade adicional e o número DUNS da conta foi atualizado em um sistema de origem como um CRM, a ID da conta será vinculada somente ao novo número DUNS, refletindo assim o estado atual da conta com mais precisão.

>[!ENDSHADEBOX]

Com essa atualização, agora é possível:

* Use as APIs [!DNL Profile Access] para exibir os perfis de mesclagem mais recentes assim que os trabalhos diários de resolução de entidade forem concluídos.
* Utilize a precisão e a consistência aprimoradas dos dados da conta e da oportunidade para segmentação, ativação e análise.

Leia a [[!DNL Profile Access] API](../profile/api/entities.md) para obter mais informações.

### Suporte a políticas de mesclagem em públicos B2B de várias entidades

Públicos-alvo de várias entidades com atributos B2B agora oferecem suporte a uma única política de mesclagem - a política de mesclagem padrão que você configura - em vez de várias políticas de mesclagem.

Leia o [guia de caso de uso de segmentação do Real-Time CDP B2B edition](./segmentation/b2b.md) para obter mais informações.

### Substituição de pesquisa e exclusão de entidade B2B na API [!DNL Profile Access]

As seguintes funcionalidades de pesquisa para entidades B2B que usam a API [!DNL Profile Access] estão sendo descontinuadas:

* Relação Conta-Pessoa
* Relação oportunidade-pessoa
* Campaign
* Membro da campanha
* Lista de marketing
* Membros da lista de marketing

As solicitações de exclusão das seguintes entidades B2B usando a API [!DNL Profile Access] estão sendo descontinuadas:

* Conta
* Relação Conta-Pessoa
* Oportunidade
* Relação oportunidade-pessoa
* Campaign
* Membro da campanha
* Lista de marketing
* Membros da lista de marketing

Leia a [[!DNL Profile Access] API](../profile/api/entities.md) para obter mais informações.

### Substituição da API de trabalho do segmento

Na nova arquitetura, o endpoint &quot;criar um trabalho de segmento&quot; e a avaliação de público-alvo flexível *não são compatíveis.

### Pesquisas de conta e perfil de oportunidade

Agora você pode recuperar esquemas de conta e de oportunidade como entidades de dimensão de pesquisa somente após eles terem concluído o processo diário de resolução da entidade. Os registros assimilados recentemente não estarão disponíveis para enriquecimento de perfil ou definições de segmento até que o próximo ciclo de resolução da entidade seja concluído (normalmente a cada 24 horas).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Alterações nas importações de público-alvo de várias entidades na ferramenta sandbox

Com as atualizações de arquitetura, você não poderá mais importar públicos-alvo de várias entidades com atributos B2B e Eventos de experiência se um pacote que inclui esses públicos-alvo for publicado antes da atualização. Esses públicos-alvo não serão importados e não poderão ser convertidos automaticamente para a nova arquitetura. Para contornar essa limitação, você deve criar um novo pacote com os públicos atualizados e, em seguida, importá-los para suas respectivas sandboxes de destino usando as ferramentas da sandbox.

As sandboxes de desenvolvimento serão atualizadas para a nova arquitetura. Os públicos que podem ser atualizados automaticamente serão atualizados; aqueles que não podem ser desativados. Públicos desativados devem ser recriados após a atualização.

Leia o [guia de ferramentas de sandbox](../sandboxes/ui/sandbox-tooling.md) para obter mais informações.
