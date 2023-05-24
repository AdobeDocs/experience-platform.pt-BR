---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;medidas de proteção;diretrizes;limite;entidade;entidade primária;entidade de dimensão;
title: Proteções padrão para dados de perfil do cliente em tempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: A Adobe Experience Platform usa um modelo de dados híbrido não normalizado que difere do modelo de dados relacional tradicional. Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados de perfil para obter o melhor desempenho do sistema.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 8ee68e5416c28a08dffc358dad70055e9b4cdd28
workflow-type: tm+mt
source-wordcount: '1980'
ht-degree: 5%

---

# Proteções padrão para [!DNL Real-Time Customer Profile] dados

O Adobe Experience Platform permite fornecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis de clientes em tempo real. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados de perfil para obter o melhor desempenho do sistema. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

>[!NOTE]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Introdução

Os seguintes serviços de Experience Platform estão envolvidos na modelagem de dados do Perfil do cliente em tempo real:

* [[!DNL Real-Time Customer Profile]](home.md): crie perfis de consumidores unificados usando dados de várias fontes.
* [Identidades](../identity-service/home.md): identidades de ponte de fontes de dados diferentes, à medida que são assimiladas na Platform.
* [Esquemas](../xdm/home.md): os esquemas do Experience Data Model (XDM) são a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
* [Segmentos](../segmentation/home.md): o mecanismo de segmentação na Platform é usado para criar segmentos a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.

## Tipos de limite

Há dois tipos de limites padrão neste documento:

* **Limite flexível:** É possível ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido:** Um limite rígido fornece um máximo absoluto.

>[!NOTE]
>
>Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Limites do modelo de dados

As medidas de proteção a seguir fornecem limites recomendados ao modelar dados do Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no apêndice.

![Um diagrama que mostra as diferentes medidas de proteção para os dados do Perfil no Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Medidas de proteção da entidade principal

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Conjuntos de dados da classe Perfil individual XDM | 20 | Suave | Recomenda-se um máximo de 20 conjuntos de dados que usam a classe Perfil individual XDM. |
| Conjuntos de dados da classe XDM ExperienceEvent | 20 | Suave | Recomenda-se um máximo de 20 conjuntos de dados que usam a classe XDM ExperienceEvent. |
| Conjuntos de dados do conjunto de relatórios do Adobe Analytics ativados para Perfil | 1 | Suave | No máximo um (1) conjunto de dados do conjunto de relatórios do Analytics deve estar ativado para o Perfil. A tentativa de ativar vários conjuntos de dados do Analytics para o Perfil pode ter consequências não intencionais para a qualidade dos dados. Para obter mais informações, consulte a seção sobre [Conjuntos de dados do Adobe Analytics](#aa-datasets) no apêndice. |
| Relacionamentos de várias entidades | 5 | Suave | Recomenda-se um máximo de 5 relacionamentos de várias entidades definidos entre entidades primárias e entidades de dimensão. Mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Profundidade JSON para o campo de ID usado no relacionamento de várias entidades | 4 | Suave | A profundidade máxima de JSON recomendada para um campo de ID usado em relacionamentos de várias entidades é 4. Isso significa que, em um esquema altamente aninhado, os campos aninhados com mais de 4 níveis de profundidade não devem ser usados como um campo de ID em uma relação. |
| Cardinalidade de matriz em um fragmento de perfil | &lt;=500 | Suave | A cardinalidade de matriz ideal em um fragmento de perfil (dados independentes do tempo) é &lt;=500. |
| Cardinalidade de matriz no ExperienceEvent | &lt;=10 | Suave | A cardinalidade de array ideal em um ExperienceEvent (dados de série temporal) é &lt;=10. |
| Contagem de identidades para o gráfico de identidade de perfil individual | 50 | Grave | **O número máximo de identidades em um Gráfico de identidade para um perfil individual é 50.** Quaisquer perfis com mais de 50 identidades são excluídos da segmentação, das exportações e das pesquisas. |

{style="table-layout:auto"}

### Medidas de proteção de entidade Dimension

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Não são permitidos dados de séries temporais para[!DNL XDM Individual Profile] entidades | 0 | Grave | **Os dados de série temporal não são permitidos para[!DNL XDM Individual Profile] entidades no Serviço de perfil.** Se um conjunto de dados de séries temporais estiver associado a um[!DNL XDM Individual Profile] ID, o conjunto de dados não deve ser ativado para [!DNL Profile]. |
| Nenhuma relação aninhada | 0 | Suave | Você não deve criar uma relação entre dois[!DNL XDM Individual Profile] esquemas. A capacidade de criar relações não é recomendada para esquemas que não fazem parte da [!DNL Profile] esquema de união. |
| Profundidade JSON para o campo de ID principal | 4 | Suave | A profundidade máxima recomendada de JSON para o campo de ID primária é 4. Isso significa que em um esquema altamente aninhado, você não deve selecionar um campo como uma ID primária se ele estiver aninhado a mais de 4 níveis de profundidade. Um campo que esteja no quarto nível aninhado pode ser usado como uma ID primária. |

{style="table-layout:auto"}

## Limites de tamanho de dados

As medidas de proteção a seguir se referem ao tamanho dos dados e fornecem limites recomendados para os dados que podem ser assimilados, armazenados e consultados conforme esperado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no apêndice.

>[!NOTE]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da assimilação.

### Medidas de proteção da entidade principal

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho máximo do ExperienceEvent | 10 KB | Grave | **O tamanho máximo de um evento é 10KB.** A assimilação continuará, mas os eventos maiores que 10 KB serão descartados. |
| Tamanho máximo do registro de perfil | 100 KB | Grave | **O tamanho máximo de um registro de perfil é 100 KB.** A assimilação continuará, no entanto, registros de perfil maiores que 100 KB serão descartados. |
| Tamanho máximo do fragmento do perfil | 50MB | Grave | **O tamanho máximo de um único fragmento de perfil é de 50 MB.** A segmentação, as exportações e as pesquisas podem falhar para qualquer [fragmento do perfil](#profile-fragments) que seja maior que 50 MB. |
| Tamanho máximo de armazenamento do perfil | 50MB | Suave | **O tamanho máximo de um perfil armazenado é 50 MB.** Adição de novo [fragmentos de perfil](#profile-fragments) em um perfil com mais de 50 MB afetará o desempenho do sistema. Por exemplo, um perfil pode conter um único fragmento de 50 MB ou pode conter vários fragmentos em vários conjuntos de dados com um tamanho total combinado de 50 MB. Tentar armazenar um perfil com um único fragmento maior que 50 MB, ou com vários fragmentos que totalizam mais de 50 MB em tamanho combinado, afetará o desempenho do sistema. |
| Número de lotes Profile ou ExperienceEvent assimilados por dia | 90 | Suave | **O número máximo de lotes Profile ou ExperienceEvent assimilados por dia é 90.** Isso significa que o total combinado de lotes Profile e ExperienceEvent assimilados a cada dia não pode exceder 90. A ingestão de lotes adicionais afetará o desempenho do sistema. |
| Número de ExperienceEvents por registro de perfil | 5000 | Suave | **O número máximo de ExperienceEvents por registro de perfil é 5000.** Perfis com mais de 5000 ExperienceEvents **não** ser consideradas para segmentação. |

{style="table-layout:auto"}

### Medidas de proteção de entidade Dimension

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total de todas as entidades dimensionais | 5 GB | Suave | O tamanho total recomendado para todas as entidades dimensionais é 5 GB. A ingestão de entidades de dimensão grandes pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Esquema de entidade dimensional de conjuntos de dados | 5 | Suave | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao esquema de produtos. |
| Lotes de entidades Dimension assimilados por dia | 4 por entidade | Suave | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. A ingestão de lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

{style="table-layout:auto"}

## Proteções de segmentação

As medidas de proteção descritas nesta seção referem-se ao número e à natureza dos segmentos que uma organização pode criar no Experience Platform, bem como mapear e ativar segmentos para destinos.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Segmentos por sandbox | 4000 | Suave | Uma organização pode ter mais de 4000 segmentos no total, desde que haja menos de 4000 segmentos em cada sandbox individual. Tentar criar segmentos adicionais pode afetar o desempenho do sistema. |
| Segmentos de borda por sandbox | 150 | Suave | Uma organização pode ter mais de 150 segmentos de borda no total, desde que haja menos de 150 segmentos de borda em cada sandbox individual. Tentar criar segmentos de borda adicionais pode afetar o desempenho do sistema. |
| Segmentos de transmissão por sandbox | 500 | Suave | Uma organização pode ter mais de 500 segmentos de transmissão no total, desde que haja menos de 500 segmentos de transmissão em cada sandbox individual. Tentar criar segmentos de transmissão adicionais pode afetar o desempenho do sistema. |
| Segmentos em lote por sandbox | 4000 | Suave | Uma organização pode ter mais de 4000 segmentos em lote no total, desde que haja menos de 4000 segmentos em lote em cada sandbox individual. Tentar criar segmentos em lote adicionais pode afetar o desempenho do sistema. |

{style="table-layout:auto"}

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

A variável [!DNL Profile] o modelo de armazenamento de dados consiste em dois tipos de entidade principais: [entidades principais](#primary-entity) e [entidades de dimensão](#dimension-entity).

#### Entidade principal

Uma entidade principal, ou entidade de perfil, mescla dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização de união agrega os campos de todos os esquemas que implementam a mesma classe em um único esquema de união. O esquema de união para [!DNL Real-Time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um container para todos os atributos de perfil e eventos comportamentais.

Os atributos independentes do tempo, também conhecidos como &quot;dados de registro&quot;, são modelados usando [!DNL XDM Individual Profile], enquanto os dados de série temporal, também conhecidos como &quot;dados de evento&quot;, são modelados usando [!DNL XDM ExperienceEvent]. À medida que os dados de registro e de série temporal são assimilados no Adobe Experience Platform, ele é acionado [!DNL Real-Time Customer Profile] para começar a assimilar dados que foram ativados para seu uso. Quanto mais interações e detalhes forem assimilados, mais robustos os perfis individuais se tornarão.

![Um infográfico que descreve as diferenças entre os dados de registro e os dados de série temporal.](images/guardrails/profile-entity.png)

#### entidade Dimension

Embora o armazenamento de dados do perfil que mantém os dados do perfil não seja um armazenamento relacional, o Perfil permite a integração com entidades de pequena dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/multi-entity-segmentation.md).

Sua organização também pode definir classes XDM para descrever coisas que não sejam indivíduos, como lojas, produtos ou propriedades. Esses programas,[!DNL XDM Individual Profile] os esquemas são chamados de &quot;entidades de dimensão&quot; (também conhecidas como &quot;entidades de pesquisa&quot;) e não contêm dados de série temporal. Os esquemas que representam entidades de dimensão são vinculados a entidades de perfil por meio do uso de [relacionamentos de esquema](../xdm/tutorials/relationship-ui.md).

As entidades Dimension fornecem dados de pesquisa que auxiliam e simplificam as definições de segmento de várias entidades e devem ser pequenas o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa rápida por ponto).

![Um infográfico que mostra que uma entidade de perfil é composta de entidades de dimensão.](images/guardrails/profile-and-dimension-entities.png)

### Fragmentos de perfil

Neste documento, há várias medidas de proteção que se referem aos &quot;fragmentos de perfil&quot;. No Experience Platform, vários fragmentos de perfil são mesclados para formar o Perfil do cliente em tempo real. Cada fragmento representa uma identidade primária exclusiva e o registro correspondente ou conjunto completo de dados do evento para essa ID em um determinado conjunto de dados. Para saber mais sobre fragmentos de perfil, consulte a [Visão geral do perfil](home.md#profile-fragments-vs-merged-profiles).

### Políticas de mesclagem {#merge-policies}

Ao reunir dados de várias fontes, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente. Quando os dados de várias origens entram em conflito, a política de mesclagem determina quais informações incluir no perfil para o indivíduo. São permitidas no máximo cinco (5) políticas de mesclagem por organização. Para saber mais sobre políticas de mesclagem, leia o [visão geral das políticas de mesclagem](merge-policies/overview.md).

### Conjuntos de dados do conjunto de relatórios do Adobe Analytics na plataforma {#aa-datasets}

Vários conjuntos de relatórios podem ser ativados para o Perfil desde que todos os conflitos de dados sejam resolvidos. Você pode usar a funcionalidade Preparo de dados para resolver conflitos de dados entre eVars, Listas e Props. Para saber mais sobre como usar a funcionalidade Preparo de dados, leia a [Guia da interface do conector do Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).
