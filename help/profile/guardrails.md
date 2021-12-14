---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, medidas de proteção, diretrizes, limite, entidade, entidade primária, entidade de dimensão;
title: Grades de proteção padrão para dados de perfil do cliente em tempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: 'O Adobe Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacionais tradicional. Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados de perfil para obter o melhor desempenho do sistema. '
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 8a343ad275dcfc33eb304e3fc19d375b81277448
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 3%

---

# Grades de proteção padrão para [!DNL Real-time Customer Profile] dados

O Adobe Experience Platform permite fornecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis do cliente em tempo real. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados de perfil para obter o melhor desempenho do sistema. Ao revisar as seguintes medidas de proteção, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do serviço de atendimento ao cliente.

>[!NOTE]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com seu representante de atendimento ao cliente.

## Introdução

Os seguintes serviços do Experience Platform estão envolvidos com a modelagem de dados do Perfil do cliente em tempo real:

* [[!DNL Real-time Customer Profile]](home.md): Crie perfis de consumidor unificados usando dados de várias fontes.
* [Identidades](../identity-service/home.md): Unir identidades de fontes de dados diferentes à medida que são assimiladas na plataforma.
* [Esquemas](../xdm/home.md): Os esquemas do Experience Data Model (XDM) são a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [Segmentos](../segmentation/home.md): O mecanismo de segmentação na Platform é usado para criar segmentos a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.

## Tipos de limite

Existem dois tipos de limites padrão neste documento:

* **Limite suave:** É possível ir além de um limite suave, no entanto, os limites suaves fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido:** Um limite rígido fornece um máximo absoluto.

>[!NOTE]
>
>Os limites indicados neste documento são constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com seu representante de atendimento ao cliente.

## Limites do modelo de dados

As seguintes medidas de proteção fornecem limites recomendados ao modelar dados de Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção em [tipos de entidade](#entity-types) no apêndice.

### Medidas de proteção de entidade primária

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Conjuntos de dados de classe de Perfil individual XDM | 20 | Suave | Recomenda-se um máximo de 20 conjuntos de dados que aproveitam a classe de Perfil individual XDM. |
| Conjuntos de dados da classe XDM ExperienceEvent | 20º | Suave | Recomenda-se um máximo de 20 conjuntos de dados que aproveitam a classe XDM ExperienceEvent . |
| Conjuntos de dados do conjunto de relatórios do Adobe Analytics habilitados para o Perfil | 1 | Suave | No máximo um (1) conjunto de dados do conjunto de relatórios do Analytics deve ser ativado para o Perfil. A tentativa de ativar vários conjuntos de dados do conjunto de relatórios do Analytics para o Perfil pode ter consequências não intencionais para a qualidade dos dados. Para obter mais informações, consulte a seção em [Conjuntos de dados do Adobe Analytics](#aa-datasets) no apêndice. |
| Relacionamentos de várias entidades | 5 | Suave | Recomenda-se um máximo de 5 relacionamentos multientidades definidos entre entidades primárias e entidades de dimensão. Os mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Profundidade JSON para campo de ID usado em relacionamento de várias entidades | 4 | Suave | A profundidade máxima JSON recomendada para um campo de ID usado em relacionamentos de várias entidades é 4. Isso significa que, em um schema altamente aninhado, os campos aninhados com mais de 4 níveis de profundidade não devem ser usados como um campo de ID em um relacionamento. |
| cardinalidade da matriz em um fragmento de perfil | &lt;=500 | Suave | A cardinalidade ideal do array em um fragmento de perfil (dados independentes do tempo) é &lt;=500. |
| cardinalidade da matriz no ExperienceEvent | &lt;=10 | Suave | A cardinalidade ideal do array em um ExperienceEvent (dados de séries de tempo) é &lt;=10. |
| Contagem de identidade para o Gráfico de identidade de perfil individual | 50 | Grave | **O número máximo de identidades em um Gráfico de identidade para um perfil individual é 50.** Quaisquer perfis com mais de 50 identidades são excluídos da segmentação, exportações e pesquisas. |

{style=&quot;table-layout:auto&quot;}

### Medidas de proteção de Dimension entity

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Não são permitidos dados de séries cronológicas para[!DNL XDM Individual Profile] entities | 0 | Grave | **Não são permitidos dados de séries cronológicas para[!DNL XDM Individual Profile] entidades no Serviço de perfil.** Se um conjunto de dados de séries de tempo estiver associado a um[!DNL XDM Individual Profile] ID, o conjunto de dados não deve ser habilitado para [!DNL Profile]. |
| Nenhum relacionamento aninhado | 0 | Suave | Você não deve criar uma relação entre dois[!DNL XDM Individual Profile] esquemas. A capacidade de criar relacionamentos não é recomendada para qualquer schema que não faça parte do [!DNL Profile] esquema de união. |
| Profundidade JSON para campo de ID primário | 4 | Suave | A profundidade máxima JSON recomendada para o campo de ID principal é 4. Isso significa que, em um schema altamente aninhado, não é necessário selecionar um campo como ID primária se ele estiver aninhado com mais de quatro níveis de profundidade. Um campo que esteja no quarto nível aninhado pode ser usado como uma ID primária. |

{style=&quot;table-layout:auto&quot;}

## Limites de tamanho de dados

As medidas de proteção a seguir referem-se ao tamanho dos dados e fornecem limites recomendados para dados que podem ser assimilados, armazenados e consultados conforme planejado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção em [tipos de entidade](#entity-types) no apêndice.

>[!NOTE]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da ingestão.

### Medidas de proteção de entidade primária

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho máximo do ExperienceEvent | 10 KB | Grave | **O tamanho máximo de um evento é de 10 KB.** A assimilação continuará, no entanto, todos os eventos maiores que 10 KB serão descartados. |
| Tamanho máximo do registro de perfil | 100 KB | Grave | **O tamanho máximo de um registro de perfil é de 100 KB.** A assimilação continuará, no entanto, os registros de perfil com mais de 100 KB serão descartados. |
| Tamanho máximo do fragmento de perfil | 50 MB | Grave | **O tamanho máximo de um fragmento de perfil único é de 50 MB.** Segmentação, exportações e pesquisas podem falhar em qualquer [fragmento de perfil](#profile-fragments) maior que 50 MB. |
| Tamanho máximo de armazenamento de perfil | 50 MB | Suave | **O tamanho máximo de um perfil armazenado é de 50 MB.** Adicionar novo [fragmentos de perfil](#profile-fragments) em um perfil maior que 50 MB afetará o desempenho do sistema. Por exemplo, um perfil pode conter um único fragmento de 50 MB ou pode conter vários fragmentos em vários conjuntos de dados com um tamanho total combinado de 50 MB. A tentativa de armazenar um perfil com um único fragmento maior que 50 MB, ou vários fragmentos que totalizam mais de 50 MB em tamanho combinado, afetará o desempenho do sistema. |
| Número de lotes de Perfil ou ExperienceEvent assimilados por dia | 90 | Suave | **O número máximo de lotes de Perfil ou ExperienceEvent assimilados por dia é de 90.** Isso significa que o total combinado de lotes de Perfil e ExperienceEvent assimilados a cada dia não pode exceder 90. A inserção de lotes adicionais afetará o desempenho do sistema. |

{style=&quot;table-layout:auto&quot;}

### Medidas de proteção de Dimension entity

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total para todas as entidades dimensionais | 5 GB | Suave | O tamanho total recomendado para todas as entidades dimensionais é de 5 GB. Inserir grandes entidades de dimensão pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Conjuntos de dados por esquema de entidade dimensional | 5 | Suave | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao schema de produtos. |
| lotes de entidade Dimension ingeridos por dia | 4 por entidade | Suave | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. Inserir lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

{style=&quot;table-layout:auto&quot;}

## Medidas de proteção de segmentação

As grades de proteção descritas nesta seção se referem ao número e à natureza dos segmentos que uma organização pode criar no Experience Platform, bem como ao mapeamento e ativação de segmentos para destinos.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Segmentos por sandbox | 10.000 | Suave | Uma organização pode ter mais de 10.000 segmentos no total, desde que haja menos de 10.000 segmentos em cada sandbox individual. Tentar criar segmentos adicionais pode afetar o desempenho do sistema. |
| Segmentos de fluxo por sandbox | 500 | Suave | Uma organização pode ter mais de 500 segmentos de transmissão no total, desde que haja menos de 500 segmentos de transmissão em cada sandbox individual. Tentar criar segmentos de transmissão adicionais pode afetar o desempenho do sistema. |
| Segmentos em lote por sandbox | 10.000 | Suave | Uma organização pode ter mais de 10.000 segmentos de lote no total, desde que haja menos de 10.000 segmentos de lote em cada sandbox individual. A tentativa de criar segmentos de lote adicionais pode afetar o desempenho do sistema. |

{style=&quot;table-layout:auto&quot;}

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

O [!DNL Profile] o modelo de dados de armazenamento consiste em dois tipos de entidade principais:

* **Entidade primária:** Uma entidade primária ou entidade de perfil une os dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;exibição de união&quot;. Uma exibição de união agrega os campos de todos os esquemas que implementam a mesma classe em um único schema de união. O schema de união para [!DNL Real-time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um contêiner para todos os atributos de perfil e eventos comportamentais.

   Atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot;, são modelados usando [!DNL XDM Individual Profile], enquanto que os dados das séries cronológicas, também conhecidos como &quot;dados de eventos&quot;, são modelados utilizando [!DNL XDM ExperienceEvent]. Como os dados de registro e de série de tempo são assimilados no Adobe Experience Platform, ele dispara [!DNL Real-time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos serão os perfis individuais.

   ![](images/guardrails/profile-entity.png)

* **Dimension entity:** Embora o armazenamento de dados do Perfil que mantém os dados do perfil não seja uma loja relacional, o Perfil permite a integração com pequenas entidades de dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/multi-entity-segmentation.md). Sua organização também pode definir classes XDM para descrever coisas diferentes de indivíduos, como lojas, produtos ou propriedades. Esses[!DNL XDM Individual Profile] os schemas são conhecidos como &quot;entidades de dimensão&quot; e não contêm dados de séries de tempo. As entidades de Dimension fornecem dados de pesquisa que auxilia e simplifica definições de segmentos de várias entidades e devem ser pequenos o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa de ponto rápido).

   ![](images/guardrails/profile-and-dimension-entities.png)

### Fragmentos de perfil

Neste documento, há várias grades de proteção que se referem a &quot;fragmentos de perfil&quot;. No Experience Platform, vários fragmentos de perfil são unidos para formar o Perfil do cliente em tempo real. Cada fragmento representa uma identidade primária exclusiva e o registro ou dados de evento correspondentes a essa ID em um determinado conjunto de dados. Para saber mais sobre fragmentos de perfil, consulte [Visão geral do perfil](home.md#profile-fragments-vs-merged-profiles).

### Mesclar políticas {#merge-policies}

Ao reunir dados de várias fontes, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa exibição unificada. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente. Quando os dados de várias fontes estão em conflito, a política de mesclagem determina quais informações devem ser incluídas no perfil do indivíduo. Para saber mais sobre as políticas de mesclagem, comece lendo o [visão geral das políticas de mesclagem](merge-policies/overview.md).

### Conjuntos de dados do conjunto de relatórios do Adobe Analytics na Platform {#aa-datasets}

Um máximo de um (1) conjunto de dados de conjunto de relatórios do Adobe Analytics deve ser ativado para o Perfil. Esse é um limite suave, o que significa que você pode ativar mais de um conjunto de dados do Analytics para o Perfil, mas não é recomendado, pois pode ter consequências não intencionais para os dados. Isso se deve às diferenças entre os esquemas do Experience Data Model (XDM), que fornecem a estrutura semântica para dados no Experience Platform e permitem consistência na interpretação de dados, e a natureza personalizável de eVars e variáveis de conversão no Adobe Analytics.

Por exemplo, no Adobe Analytics, uma única organização pode ter vários conjuntos de relatórios. Se o conjunto de relatórios A designar o eVar 4 como &quot;termo de pesquisa interno&quot; e o conjunto de relatórios B designar o eVar 4 como &quot;domínio de referência&quot;, esses valores serão assimilados no mesmo campo no Perfil, causando confusão e degradando a qualidade dos dados.
