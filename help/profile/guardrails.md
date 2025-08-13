---
title: Proteções padrão para dados e segmentação do perfil do cliente em tempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: Saiba mais sobre o desempenho e as medidas de proteção aplicadas pelo sistema para segmentação e dados de perfil para garantir o uso ideal da funcionalidade da Real-Time CDP.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 56bf7ae20c33b013a1710fba8c04d9edc23baf89
workflow-type: tm+mt
source-wordcount: '2649'
ht-degree: 2%

---

# Medidas de proteção padrão para [!DNL Real-Time Customer Profile] dados e segmentação

O Adobe Experience Platform permite fornecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis de clientes em tempo real. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

Este documento fornece limites de uso e taxa padrão para ajudar você a modelar seus dados de perfil para obter o melhor desempenho do sistema. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

>[!NOTE]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Introdução

Os seguintes serviços da Experience Platform estão envolvidos na modelagem de dados do Perfil do cliente em tempo real:

* [[!DNL Real-Time Customer Profile]](home.md): Criar perfis de consumidor unificados usando dados de várias fontes.
* [Identidades](../identity-service/home.md): identidades Bridge de fontes de dados diferentes conforme são assimiladas na Experience Platform.
* [Esquemas](../xdm/home.md): os esquemas do Experience Data Model (XDM) são a estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
* [Públicos-alvo](../segmentation/home.md): o mecanismo de segmentação no Experience Platform é usado para criar públicos-alvo a partir de perfis de clientes com base em comportamentos e atributos do cliente.

## Tipos de limite

Há dois tipos de limites padrão neste documento:

| Tipo de grade de proteção | Descrição |
| -------------- | ----------- |
| **Proteção de desempenho (limite flexível)** | As medidas de proteção de desempenho são limites de uso relacionados ao escopo dos seus casos de uso. Ao exceder as medidas de proteção de desempenho, você pode enfrentar degradação e latência do desempenho. A Adobe não é responsável por essa degradação de desempenho. Os clientes que excederem consistentemente uma garantia de desempenho podem optar por licenciar capacidade adicional para evitar a degradação do desempenho. |
| **Medidas de proteção aplicadas pelo sistema (Limite rígido)** | As medidas de proteção aplicadas pelo sistema são aplicadas pela interface do usuário ou API do Real-Time CDP. Esses são limites que você não pode exceder, pois a interface do usuário e a API o bloquearão de fazer isso ou retornarão um erro. |

{style="table-layout:auto"}

>[!NOTE]
>
>Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Limites do modelo de dados

As medidas de proteção a seguir fornecem limites recomendados ao modelar dados do Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no Apêndice.

![Um diagrama que mostra as diferentes medidas de proteção para os dados do Perfil no Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Medidas de proteção da entidade principal

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Conjuntos de dados da classe Perfil individual XDM | 20 | Proteção de desempenho | Recomenda-se um máximo de 20 conjuntos de dados que usam a classe Perfil individual XDM. |
| Conjuntos de dados da classe XDM ExperienceEvent | 20 | Proteção de desempenho | Recomenda-se um máximo de 20 conjuntos de dados que usam a classe XDM ExperienceEvent. |
| Conjuntos de dados do conjunto de relatórios do Adobe Analytics ativados para Perfil | 1 | Proteção de desempenho | No máximo um (1) conjunto de dados do conjunto de relatórios do Analytics deve estar ativado para o Perfil. A tentativa de ativar vários conjuntos de dados do Analytics para o Perfil pode ter consequências não intencionais para a qualidade dos dados. Para obter mais informações, consulte a seção sobre [conjuntos de dados do Adobe Analytics](#aa-datasets) no Apêndice. |
| Relacionamentos de várias entidades | 5 | Proteção de desempenho | Recomenda-se um máximo de 5 relacionamentos de várias entidades definidos entre entidades primárias e entidades de dimensão. Mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Profundidade JSON para o campo de ID usado no relacionamento de várias entidades | 4 | Proteção de desempenho | A profundidade máxima de JSON recomendada para um campo de ID usado em relacionamentos de várias entidades é 4. Isso significa que, em um esquema altamente aninhado, os campos aninhados com mais de 4 níveis de profundidade não devem ser usados como um campo de ID em uma relação. |
| Cardinalidade de matriz em um fragmento de perfil | &lt;=500 | Proteção de desempenho | A cardinalidade de matriz ideal em um fragmento de perfil (dados independentes do tempo) é &lt;=500. |
| Cardinalidade de matriz no ExperienceEvent | &lt;=10 | Proteção de desempenho | A cardinalidade de array ideal em um ExperienceEvent (dados de série temporal) é &lt;=10. |
| Contagem de identidades para o gráfico de identidade de perfil individual | 50 | Proteção imposta pelo sistema | **O número máximo de identidades em um Gráfico de identidade para um perfil individual é 50.** Todos os perfis com mais de 50 identidades são excluídos da segmentação, exportações e pesquisas. Para obter mais informações, leia o manual sobre [noções básicas sobre a lógica de exclusão de identidade](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). |

{style="table-layout:auto"}

### Medidas de proteção de entidade do Dimension

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Nenhum dado de série temporal permitido para entidades que não sejam [!DNL XDM Individual Profile] | 0 | Proteção imposta pelo sistema | **Dados de série temporal não são permitidos para entidades que não sejam [!DNL XDM Individual Profile] no Serviço de Perfil.** Se um conjunto de dados de série temporal estiver associado a uma ID não-[!DNL XDM Individual Profile], o conjunto de dados não deverá ser habilitado para [!DNL Profile]. |
| Nenhuma relação aninhada | 0 | Proteção de desempenho | Você não deve criar uma relação entre dois esquemas diferentes de [!DNL XDM Individual Profile]. A capacidade de criar relações não é recomendada para esquemas que não fazem parte do esquema de união [!DNL Profile]. |
| Profundidade JSON para o campo de ID principal | 4 | Proteção de desempenho | A profundidade máxima recomendada de JSON para o campo de ID primária é 4. Isso significa que em um esquema altamente aninhado, você não deve selecionar um campo como uma ID primária se ele estiver aninhado a mais de 4 níveis de profundidade. Um campo que esteja no quarto nível aninhado pode ser usado como uma ID primária. |

{style="table-layout:auto"}

## Limites de tamanho de dados

As medidas de proteção a seguir se referem ao tamanho dos dados e fornecem limites recomendados para os dados que podem ser assimilados, armazenados e consultados conforme esperado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no Apêndice.

>[!NOTE]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da assimilação.

### Medidas de proteção da entidade principal

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Tamanho máximo do ExperienceEvent | 10 KB | Proteção imposta pelo sistema | **O tamanho máximo de um evento é 10KB.A assimilação de** continuará, entretanto, qualquer evento maior que 10 KB será descartado. |
| Tamanho máximo do registro de perfil | 100 KB | Proteção imposta pelo sistema | **O tamanho máximo de um registro de perfil é 100KB.A assimilação de** continuará, entretanto, registros de perfil maiores que 100 KB serão descartados. |
| Tamanho máximo do fragmento do perfil | 50 MB | Proteção imposta pelo sistema | **O tamanho máximo de um único fragmento de perfil é de 50 MB.A segmentação, as exportações e as pesquisas de** podem falhar para qualquer [fragmento de perfil](#profile-fragments) com mais de 50 MB. |
| Tamanho máximo de armazenamento do perfil | 50 MB | Proteção de desempenho | **O tamanho máximo de um perfil armazenado é 50MB.** Adicionar novos [fragmentos de perfil](#profile-fragments) em um perfil com mais de 50 MB afetará o desempenho do sistema. Por exemplo, um perfil pode conter um único fragmento de 50 MB ou pode conter vários fragmentos em vários conjuntos de dados com um tamanho total combinado de 50 MB. Tentar armazenar um perfil com um único fragmento maior que 50 MB, ou com vários fragmentos que totalizam mais de 50 MB em tamanho combinado, afetará o desempenho do sistema. |
| Número de lotes Profile ou ExperienceEvent assimilados por dia | 90 | Proteção de desempenho | **O número máximo de lotes de Profile ou ExperienceEvent assimilados por dia é 90.** Isso significa que o total combinado de lotes Profile e ExperienceEvent assimilados a cada dia não pode exceder 90. A ingestão de lotes adicionais afetará o desempenho do sistema. |
| Número de ExperienceEvents por registro de perfil | 5000 | Proteção de desempenho | **O número máximo de ExperienceEvents por registro de perfil é 5000.** Perfis com mais de 5000 ExperienceEvents usarão somente os **mais recentes** 5000 ExperienceEvents quando usados com segmentação. |

{style="table-layout:auto"}

### Medidas de proteção de entidade do Dimension

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Tamanho total de todas as entidades dimensionais | 5GB | Proteção de desempenho | O tamanho total recomendado para todas as entidades dimensionais é 5 GB. A ingestão de entidades de dimensão grandes pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Esquema de entidade dimensional de conjuntos de dados | 5 | Proteção de desempenho | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao esquema de produtos. |
| Lotes de entidades do Dimension assimilados por dia | 4 por entidade | Proteção de desempenho | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. A ingestão de lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

{style="table-layout:auto"}

## Proteções de segmentação {#segmentation-guardrails}

As medidas de proteção descritas nesta seção referem-se ao número e à natureza dos públicos que uma organização pode criar no Experience Platform, bem como mapear e ativar públicos para destinos.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Públicos-alvo por sandbox | 4000 | Proteção de desempenho | Você pode ter até 4000 **públicos-alvo** ativos por sandbox. Você pode ter mais de 4000 públicos-alvo por organização, desde que haja menos de 4000 públicos-alvo em cada sandbox **individual**. Isso inclui públicos em lote, de streaming e de borda. Tentar criar públicos adicionais pode afetar o desempenho do sistema. Leia mais sobre [criação de públicos-alvo](/help/segmentation/ui/segment-builder.md) por meio do construtor de segmentos. |
| Públicos-alvo do Edge por sandbox | 150 | Proteção de desempenho | Você pode ter até 150 públicos-alvo de borda **ativos** por sandbox. Você pode ter mais de 150 públicos-alvo de borda por organização, desde que haja menos de 150 públicos-alvo de borda em cada sandbox **individual**. Tentar criar públicos-alvo de borda adicionais pode afetar o desempenho do sistema. Leia mais sobre [públicos-alvo de borda](/help/segmentation/methods/edge-segmentation.md). |
| Taxa de transferência do Edge em todas as sandboxes | 1500 RPS | Proteção de desempenho | A segmentação do Edge é compatível com um valor de pico combinado de 1.500 eventos de entrada por segundo ao entrar no Adobe Experience Platform Edge Network em suas sandboxes de produção e desenvolvimento. A segmentação do Edge pode levar até 350 milissegundos para processar um evento de entrada depois que ele entra no Adobe Experience Platform Edge Network. Leia mais sobre [públicos-alvo de borda](/help/segmentation/methods/edge-segmentation.md). |
| Públicos-alvo de transmissão por sandbox | 500 | Proteção de desempenho | Você pode ter até 500 **públicos-alvo de streaming** ativos por sandbox. Você pode ter mais de 500 públicos-alvo de streaming por organização, desde que haja menos de 500 públicos-alvo de streaming em cada sandbox **individual**. Isso inclui públicos de transmissão e de borda. Tentar criar públicos de transmissão adicionais pode afetar o desempenho do sistema. Leia mais sobre [públicos-alvo de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Taxa de transferência de transmissão em todas as sandboxes | 1500 RPS | Proteção de desempenho | A segmentação de transmissão oferece suporte a um valor de pico combinado de 1.500 eventos de entrada por segundo em suas sandboxes de produção e desenvolvimento. A segmentação de transmissão pode levar até 5 minutos para qualificar um perfil para associação de segmento. Leia mais sobre [públicos-alvo de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Públicos em lote por sandbox | 4000 | Proteção de desempenho | Você pode ter até 4000 públicos-alvo em lote **ativos** por sandbox. Você pode ter mais de 4000 públicos-alvo em lote por organização, desde que haja menos de 4000 públicos-alvo em lote em cada sandbox **individual**. Tentar criar públicos-alvo em lote adicionais pode afetar o desempenho do sistema. |
| Públicos-alvo da conta por sandbox | 50 | Proteção imposta pelo sistema | Você pode criar no máximo 50 públicos-alvo de conta em uma sandbox. Depois de atingir 50 públicos-alvo em uma sandbox, o controle **[!UICONTROL Criar público-alvo]** é desabilitado ao tentar criar um novo público-alvo para a conta. Leia mais sobre [públicos-alvo da conta](/help/segmentation/types/account-audiences.md). |
| Composições publicadas por sandbox | 10 | Proteção de desempenho | Você pode ter no máximo 10 composições publicadas em uma sandbox. Leia mais sobre [composição de público-alvo no guia da interface](/help/segmentation/ui/audience-composition.md). **Observação**: as composições criadas com a Composição de Público Federado são **não** contadas com esta garantia. |
| Tamanho máximo do público | 30 por cento | Proteção de desempenho | A associação máxima recomendada de um público-alvo é de 30% do número total de perfis no sistema. É possível criar públicos-alvo com mais de 30% dos perfis como membros ou vários públicos-alvo grandes, mas isso afetará o desempenho do sistema. |
| Execuções flexíveis de avaliação de público | 50 por ano (sandbox de produção)<br/>100 por ano (sandbox de desenvolvimento) | Proteção imposta pelo sistema | Você tem no máximo 50 execuções de avaliação de público flexíveis por ano por sandbox de **produção**. Você tem no máximo 100 execuções de avaliação de público-alvo flexíveis por ano por sandbox de **desenvolvimento**. |
| Execuções flexíveis de avaliação de público | 2 por dia | Proteção imposta pelo sistema | Você tem no máximo 2 execuções por dia por sandbox. |
| Públicos-alvo por execução de avaliação de público-alvo flexível | 20 | Proteção imposta pelo sistema | Você pode ter no máximo 20 públicos-alvo por execução de avaliação de público-alvo flexível. |

{style="table-layout:auto"}

## Disponibilidade esperada

A seção a seguir descreve a disponibilidade **esperada** para públicos-alvo e políticas de mesclagem em serviços downstream, como destinos do Real-Time CDP:

| Tipo de sandbox | Hora |
| ------------ | ---- |
| Sandboxes existentes | 1 hora |
| Novas sandboxes | 2 horas |
| Redefinir sandboxes recentemente | 2 horas |

{style="table-layout:auto"}

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

O modelo de dados de repositório [!DNL Profile] consiste em dois tipos de entidade principais: [entidades primárias](#primary-entity) e [entidades de dimensão](#dimension-entity).

#### Entidade principal

Uma entidade principal, ou entidade de perfil, mescla dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização de união agrega os campos de todos os esquemas que implementam a mesma classe em um único esquema de união. O esquema de união para [!DNL Real-Time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um contêiner para todos os atributos de perfil e eventos comportamentais.

Atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot; são modelados usando [!DNL XDM Individual Profile], enquanto dados de série temporal, também conhecidos como &quot;dados de evento&quot; são modelados usando [!DNL XDM ExperienceEvent]. Como os dados de registro e série temporal são assimilados na Adobe Experience Platform, ele aciona [!DNL Real-Time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos os perfis individuais se tornarão.

![Um infográfico que descreve as diferenças entre os dados de registro e os dados de série temporal.](images/guardrails/profile-entity.png)

#### Entidade Dimension

Embora o armazenamento de dados do perfil que mantém os dados do perfil não seja um armazenamento relacional, o Perfil permite a integração com entidades de pequena dimensão para criar públicos-alvo de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/tutorials/multi-entity-segmentation.md).

Sua organização também pode definir classes XDM para descrever coisas que não sejam indivíduos, como lojas, produtos ou propriedades. Esses esquemas, que são modelados usando classes XDM diferentes da classe Perfil individual XDM, são chamados de &quot;entidades de dimensão&quot; (também conhecidas como &quot;entidades de pesquisa&quot;) e não contêm dados de série temporal. Esquemas que representam entidades de dimensão são vinculados a entidades de perfil por meio do uso de [relações de esquema](../xdm/tutorials/relationship-ui.md).

As entidades Dimension fornecem dados de pesquisa que auxiliam e simplificam as definições de segmento de várias entidades e devem ser pequenas o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa rápida por ponto).

![Um infográfico que mostra que uma entidade de perfil é composta de entidades de dimensão.](images/guardrails/profile-and-dimension-entities.png)

### Fragmentos de perfil

Neste documento, há várias medidas de proteção que se referem aos &quot;fragmentos de perfil&quot;. No Experience Platform, vários fragmentos de perfil são mesclados para formar o Perfil do cliente em tempo real. Cada fragmento representa uma identidade primária exclusiva e o registro correspondente ou conjunto completo de dados do evento para essa ID em um determinado conjunto de dados. Para saber mais sobre fragmentos de perfil, consulte a [Visão geral do perfil](home.md#profile-fragments-vs-merged-profiles).

### Mesclar políticas {#merge-policies}

Ao reunir dados de várias fontes, as políticas de mesclagem são as regras usadas pela Experience Platform para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Experience Platform, eles são mesclados para criar um único perfil para esse cliente. Quando os dados de várias origens entram em conflito, a política de mesclagem determina quais informações incluir no perfil para o indivíduo. Um máximo de cinco (5) políticas de mesclagem que usam o esquema `_xdm.context.profile` são permitidas por sandbox. Para saber mais sobre políticas de mesclagem, leia a [visão geral das políticas de mesclagem](merge-policies/overview.md).

### Conjuntos de dados do conjunto de relatórios do Adobe Analytics no Experience Platform {#aa-datasets}

Vários conjuntos de relatórios podem ser ativados para o Perfil desde que todos os conflitos de dados sejam resolvidos. Você pode usar a funcionalidade Preparo de dados para resolver conflitos de dados entre eVars, Listas e Props. Para saber mais sobre como usar a funcionalidade Preparo de dados, leia o [guia da interface do usuário do conector do Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços da Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto da Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=pt-BR#end-to-end-latency-diagrams) para vários serviços da Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
