---
keywords: perfil;perfil do cliente em tempo real;solução de problemas;medidas de proteção;diretrizes;limite;entidade;entidade primária;entidade de dimensão;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;plataforma de dados do cliente em tempo real;cdp em tempo real;b2b;cdp;
title: Proteções padrão para o Real-time Customer Data Platform B2B Edition
type: Documentation
description: A Adobe Experience Platform usa um modelo de dados híbrido não normalizado que difere do modelo de dados relacional tradicional. Este documento fornece limites de uso e taxa padrão para ajudar você a modelar seus dados para obter o melhor desempenho do sistema usando o Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 2%

---

# Proteções padrão para o Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Os limites descritos neste documento representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

O Real-time Customer Data Platform B2B Edition permite que você forneça experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis de clientes em tempo real e Perfis de conta. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

Este documento fornece limites de uso e taxa padrão para ajudar você a modelar seus dados para obter o melhor desempenho do sistema. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

>[!INFO]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Tipos de limite

Há dois tipos de limites padrão neste documento:

* **Limite flexível:** É possível ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido:** Um limite rígido fornece um máximo absoluto.

>[!INFO]
>
>Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Limites do modelo de dados

As medidas de proteção a seguir fornecem limites recomendados ao modelar dados do Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no apêndice.

### Medidas de proteção da entidade principal

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Conjuntos de dados da classe XDM padrão do Real-Time CDP B2B Edition | 60 | Suave | Recomenda-se um máximo de 60 conjuntos de dados que usam as classes padrão do Experience Data Model (XDM) fornecidas pelo Real-Time CDP B2B Edition. Para obter uma lista completa de classes XDM padrão para casos de uso B2B, consulte o [esquemas na documentação do Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Observação: devido à natureza do modelo de dados híbrido desnormalizado de Experience Platform, a maioria dos clientes não excede esse limite. Para perguntas sobre como modelar seus dados ou se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.* |
| Relacionamentos herdados de várias entidades | 20 | Suave | Recomenda-se um máximo de 20 relacionamentos de várias entidades definidos entre entidades primárias e entidades de dimensão. Mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Relacionamentos muitos para um por classe XDM | 2 | Suave | Recomenda-se um máximo de 2 relações muitos para um definidas por classe XDM. Uma relação adicional não deve ser feita até que uma relação existente seja removida ou desabilitada. Para obter etapas sobre como criar uma relação entre dois schemas, consulte o tutorial sobre [definição de relacionamentos de esquema B2B](../xdm/tutorials/relationship-b2b.md). |

### Medidas de proteção de entidade Dimension

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Nenhuma relação herdada aninhada | 0 | Suave | Você não deve criar uma relação entre dois[!DNL XDM Individual Profile] esquemas. A capacidade de criar relações não é recomendada para esquemas que não fazem parte da [!DNL Profile] esquema de união. |
| Somente objetos B2B podem participar de relações muitos para um | 0 | Grave | O sistema só suporta relações muitos para um entre objetos B2B. Para obter mais informações sobre relações muitos para um, consulte o tutorial em [definição de relacionamentos de esquema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profundidade máxima de relações aninhadas entre objetos B2B | 3 | Grave | A profundidade máxima das relações aninhadas entre objetos B2B é 3. Isso significa que em um esquema altamente aninhado, você não deve ter uma relação entre objetos B2B aninhados a mais de 3 níveis de profundidade. |

## Limites de tamanho de dados

As medidas de proteção a seguir se referem ao tamanho dos dados e fornecem limites recomendados para os dados que podem ser assimilados, armazenados e consultados conforme esperado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no apêndice.

>[!INFO]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da assimilação.

### Medidas de proteção da entidade principal

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Lotes assimilados por classe XDM por dia | 45 | Suave | O número total de lotes assimilados a cada dia por classe XDM não deve exceder 45. A ingestão de lotes adicionais pode impedir o desempenho ideal. |

### Medidas de proteção de entidade Dimension

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total de todas as entidades dimensionais | 5 GB | Suave | O tamanho total recomendado para todas as entidades dimensionais é 5 GB. A ingestão de entidades de dimensão grandes pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Esquema de entidade dimensional de conjuntos de dados | 5 | Suave | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao esquema de produtos. |
| Lotes de entidades Dimension assimilados por dia | 4 por entidade | Suave | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. A ingestão de lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

## Proteções de segmentação

As medidas de proteção descritas nesta seção referem-se ao número e à natureza dos segmentos que uma organização pode criar no Experience Platform, bem como mapear e ativar segmentos para destinos.

>[!NOTE]
>
>Os limites de segmentação descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Segmentos por sandbox B2B | 400 | Suave | Uma organização pode ter mais de 400 segmentos no total, desde que haja menos de 400 segmentos em cada sandbox B2B individual. Tentar criar segmentos adicionais pode afetar o desempenho do sistema. |

## Próximas etapas

Os limites descritos neste documento representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa de limites padrão para o Real-Time CDP B2B Edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

A variável [!DNL Profile] o modelo de armazenamento de dados consiste em dois tipos de entidade principais: [entidades principais](#primary-entity) e [entidades de dimensão](#dimension-entity).

#### Entidade principal

Uma entidade principal, ou entidade de perfil, mescla dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização de união agrega os campos de todos os esquemas que implementam a mesma classe em um único esquema de união. O esquema de união para [!DNL Real-Time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um container para todos os atributos de perfil e eventos comportamentais.

Os atributos independentes do tempo, também conhecidos como &quot;dados de registro&quot;, são modelados usando [!DNL XDM Individual Profile], enquanto os dados de série temporal, também conhecidos como &quot;dados de evento&quot;, são modelados usando [!DNL XDM ExperienceEvent]. À medida que os dados de registro e de série temporal são assimilados no Adobe Experience Platform, ele é acionado [!DNL Real-Time Customer Profile] para começar a assimilar dados que foram ativados para seu uso. Quanto mais interações e detalhes forem assimilados, mais robustos os perfis individuais se tornarão.

![Um infográfico que descreve as diferenças entre os dados de registro e os dados de série temporal.](../profile/images/guardrails/profile-entity.png)

#### entidade Dimension

Embora o armazenamento de dados do perfil que mantém os dados do perfil não seja um armazenamento relacional, o Perfil permite a integração com entidades de pequena dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/multi-entity-segmentation.md).

Sua organização também pode definir classes XDM para descrever coisas que não sejam indivíduos, como lojas, produtos ou propriedades. Esses programas,[!DNL XDM Individual Profile] os esquemas são chamados de &quot;entidades de dimensão&quot; (também conhecidas como &quot;entidades de pesquisa&quot;) e não contêm dados de série temporal. Os esquemas que representam entidades de dimensão são vinculados a entidades de perfil por meio do uso de [relacionamentos de esquema](../xdm/tutorials/relationship-ui.md).

As entidades Dimension fornecem dados de pesquisa que auxiliam e simplificam as definições de segmento de várias entidades e devem ser pequenas o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa rápida por ponto).

![Um infográfico que mostra que uma entidade de perfil é composta de entidades de dimensão.](../profile/images/guardrails/profile-and-dimension-entities.png)