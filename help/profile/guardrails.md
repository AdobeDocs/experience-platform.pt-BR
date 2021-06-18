---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, medidas de proteção, diretrizes, limite, entidade, entidade primária, entidade de dimensão;
title: Grades de proteção para dados de perfil do cliente em tempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: A Adobe Experience Platform fornece uma série de medidas de proteção para ajudar você a evitar a criação de modelos de dados que o Perfil do cliente em tempo real não suporta. Este documento descreve as práticas recomendadas e restrições que devem ser levadas em conta ao modelar dados do perfil.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 441c2978b90a4703874787b3ed8b94c4a7779aa8
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 2%

---

# Grades de proteção para dados [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] O fornece perfis individuais que permitem fornecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente. Para atingir esse direcionamento, [!DNL Profile] e o mecanismo de segmentação no Adobe Experience Platform usam um modelo de dados híbrido altamente desnormalizado que oferece uma nova abordagem para desenvolver perfis de clientes. O uso desse modelo de dados híbrido torna importante que os dados coletados sejam modelados corretamente. Embora o armazenamento de dados [!DNL Profile] que mantém dados de perfil não seja um armazenamento relacional, [!DNL Profile] permite a integração com pequenas entidades de dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como segmentação de várias entidades.

O Adobe Experience Platform fornece uma série de medidas de proteção para ajudar você a evitar a criação de modelos de dados que [!DNL Real-time Customer Profile] não podem suportar. Este documento descreve essas medidas de proteção e as práticas recomendadas e restrições ao usar dados de perfil para segmentação.

>[!NOTE]
>
>As medidas de proteção e os limites indicados neste documento estão a ser constantemente melhorados. Verifique regularmente se há atualizações.

## Introdução

É recomendável ler a documentação de serviços do Experience Platform a seguir antes de tentar criar modelos de dados para uso em [!DNL Real-time Customer Profile]. Trabalhar com modelos de dados e as medidas de proteção descritas neste documento requer uma compreensão dos vários serviços do Experience Platform envolvidos no gerenciamento de [!DNL Real-time Customer Profile] entidades:

* [[!DNL Real-time Customer Profile]](home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Serviço](../identity-service/home.md) de identidade da Adobe Experience Platform: Oferece suporte à criação de uma &quot;visão única do cliente&quot;, unindo identidades de fontes de dados diferentes à medida que são assimiladas no  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../xdm/schema/composition.md) do schema: Uma introdução a schemas e modelagem de dados no Experience Platform.
* [Serviço](../segmentation/home.md) de segmentação do Adobe Experience Platform: O mecanismo de segmentação no  [!DNL Platform] usado para criar segmentos de público-alvo a partir dos perfis de clientes com base nos comportamentos e atributos do cliente.
   * [Segmentação](../segmentation/multi-entity-segmentation.md) de várias entidades: Um guia para criar segmentos que integram entidades de dimensão aos dados do perfil.

## Tipos de entidade

O modelo de dados de armazenamento [!DNL Profile] consiste em dois tipos de entidade principais:

* **Entidade primária:** uma entidade primária, ou entidade de perfil, une os dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;exibição de união&quot;. Uma exibição de união agrega os campos de todos os esquemas que implementam a mesma classe em um único schema de união. O schema de união para [!DNL Real-time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um contêiner para todos os atributos de perfil e eventos comportamentais.

   Atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot;, são modelados usando [!DNL XDM Individual Profile], enquanto os dados da série de tempo, também conhecidos como &quot;dados de evento&quot;, são modelados usando [!DNL XDM ExperienceEvent]. À medida que os dados de registro e de série de tempo são assimilados no Adobe Experience Platform, ele aciona [!DNL Real-time Customer Profile] para começar a assimilar dados que foram ativados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos serão os perfis individuais.

   ![](images/guardrails/profile-entity.png)

* **Dimension entity:** sua organização também pode definir classes XDM para descrever coisas diferentes de indivíduos, como lojas, produtos ou propriedades. Esses esquemas que não são [!DNL XDM Individual Profile] são conhecidos como &quot;entidades de dimensão&quot; e não contêm dados de séries de tempo. As entidades de Dimension fornecem dados de pesquisa que auxilia e simplifica definições de segmentos de várias entidades e devem ser pequenos o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa de ponto rápido).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Fragmentos de perfil

Há várias grades de proteção neste documento se referindo a &quot;fragmentos de perfil&quot;. O Perfil do cliente em tempo real é composto de vários fragmentos de perfil. Cada fragmento representa os dados da identidade de um conjunto de dados em que é a identidade primária. Isso significa que um fragmento pode conter uma ID primária e dados de evento (série de tempo) em um conjunto de dados XDM ExperienceEvent ou pode ser composto de uma ID primária e dados de registro (atributos independentes de tempo) em um conjunto de dados XDM Individual Profile.

## Tipos de limite

Ao definir seu modelo de dados, é recomendável permanecer dentro das grades de proteção fornecidas para garantir o desempenho adequado e evitar erros do sistema.

As medidas de proteção fornecidas neste documento incluem dois tipos de limite:

* **Limite suave:** um limite suave fornece um máximo recomendado para obter o desempenho ideal do sistema. É possível ir além de um limite suave sem quebrar o sistema ou receber mensagens de erro, no entanto, ir além de um limite suave resultará em degradação do desempenho. É recomendável permanecer dentro do limite flexível para evitar reduções no desempenho geral.

* **Limite rígido:** um limite rígido fornece um máximo absoluto para o sistema. Ir além de um limite rígido resultará em interrupções e erros, impedindo o sistema de funcionar conforme esperado.

## Medidas de proteção do modelo de dados

É recomendável seguir as seguintes grades de proteção ao criar um modelo de dados para uso com [!DNL Real-time Customer Profile].

### Medidas de proteção de entidade primária

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número de conjuntos de dados recomendados para contribuir para o schema de união [!DNL Profile] | 20 | Suave | **Recomenda-se um máximo de 20 conjuntos de dados  [!DNL Profile]habilitados.** Para habilitar outro conjunto de dados para  [!DNL Profile], um conjunto de dados existente deve ser removido ou desabilitado primeiro. |
| Número de relacionamentos de várias entidades recomendados | 5 | Suave | **Recomenda-se um máximo de 5 relacionamentos multientidades definidos entre entidades primárias e entidades de dimensão.** Os mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Profundidade JSON máxima para o campo de ID usado em relacionamento de várias entidades | 4 | Suave | **A profundidade máxima JSON recomendada para um campo de ID usado em relacionamentos de várias entidades é 4.** Isso significa que, em um schema altamente aninhado, os campos aninhados com mais de 4 níveis de profundidade não devem ser usados como um campo de ID em um relacionamento. |
| cardinalidade da matriz em um fragmento de perfil | &lt;=500 | Suave | **A cardinalidade ideal do array em um fragmento de perfil (dados independentes do tempo) é  &lt;>** |
| cardinalidade da matriz no ExperienceEvent | &lt;=10 | Suave | **A cardinalidade ideal do array em um ExperienceEvent (dados de séries de tempo) é  &lt;>** |

### Medidas de proteção de Dimension entity

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Não são permitidos dados de séries de tempo para entidades que não são [!DNL XDM Individual Profile] | 0 | Grave | **Os dados de séries de tempo não são permitidos para [!DNL XDM Individual Profile] entidades não-entidades no Serviço de perfil.** Se um conjunto de dados de séries de tempo estiver associado a uma não [!DNL XDM Individual Profile] ID, o conjunto de dados não deverá ser habilitado para  [!DNL Profile]. |
| Nenhum relacionamento aninhado | 0 | Suave | **Você não deve criar uma relação entre dois [!DNL XDM Individual Profile] schemas que não são do .** A capacidade de criar relações não é recomendada para qualquer schema que não faça parte do schema da  [!DNL Profile] união. |
| Profundidade máxima de JSON para o campo de ID principal | 4 | Suave | **A profundidade máxima JSON recomendada para o campo de ID principal é 4.** Isso significa que, em um schema altamente aninhado, não é necessário selecionar um campo como ID primária se ele estiver aninhado com mais de quatro níveis de profundidade. Um campo que esteja no quarto nível aninhado pode ser usado como uma ID primária. |

## Medidas de proteção de tamanho de dados

As seguintes medidas de proteção referem-se ao tamanho dos dados e são recomendadas para garantir que os dados possam ser assimilados, armazenados e consultados conforme o esperado.

>[!NOTE]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da ingestão.

### Medidas de proteção de entidade primária

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho máximo do ExperienceEvent | 10 KB | Grave | **O tamanho máximo de um evento é de 10 KB.** A assimilação continuará, no entanto, todos os eventos maiores que 10 KB serão descartados. |
| Tamanho máximo do registro de perfil | 100 KB | Grave | **O tamanho máximo de um registro de perfil é de 100 KB.** A assimilação continuará, no entanto, os registros de perfil com mais de 100 KB serão descartados. |
| Tamanho máximo do fragmento de perfil | 50 MB | Grave | **O tamanho máximo de um fragmento de perfil é de 50 MB.** Segmentação, exportações e pesquisas podem falhar em qualquer  [fragmento de ](#profile-fragments) perfil maior que 50 MB. |
| Tamanho máximo de armazenamento de perfil | 50 MB | Suave | **O tamanho máximo de um perfil armazenado é de 50 MB.** Adicionar novos  [fragmentos ](#profile-fragments) de perfil a um perfil maior que 50 MB afetará o desempenho do sistema. |
| Número de lotes de Perfil ou ExperienceEvent assimilados por dia | 90 | Suave | **O número máximo de lotes de Perfil ou ExperienceEvent assimilados por dia é de 90.** Isso significa que o total combinado de lotes de Perfil e ExperienceEvent assimilados a cada dia não pode exceder 90. A inserção de lotes adicionais afetará o desempenho do sistema. |

### Medidas de proteção de Dimension entity

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total máximo para todas as entidades dimensionais | 5 GB | Suave | **O tamanho total máximo recomendado para todas as entidades dimensionais é de 5 GB.** Ao inserir grandes entidades de dimensão, o desempenho do sistema será degradado. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Conjuntos de dados por esquema de entidade dimensional | 5 | Suave | **Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional.** Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao schema de produtos. |
| Número de lotes de entidades de dimensão ingeridos por dia | 4 por entidade | Suave | **O número máximo de lotes de entidades de dimensão assimilados por dia é 4 por entidade.** Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. A inserção de lotes de entidades de dimensão adicionais para a mesma entidade afetará o desempenho do sistema. |

## Medidas de proteção de segmentação

As grades de proteção descritas nesta seção se referem ao número e à natureza dos segmentos que uma organização pode criar no Experience Platform, bem como ao mapeamento e ativação de segmentos para destinos.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de segmentos por sandbox | 10 mil | Suave | **O número máximo de segmentos que uma organização pode criar é de 10 mil por sandbox.** Uma organização pode ter mais de 10 mil segmentos no total, desde que haja menos de 10.000 segmentos em cada sandbox individual. Tentar criar segmentos adicionais resultará em um desempenho degradado do sistema. |
| Número máximo de segmentos de transmissão por sandbox | 500 | Suave | **O número máximo de segmentos de transmissão que uma organização pode criar é de 500 por sandbox.** Uma organização pode ter mais de 500 segmentos de transmissão no total, desde que haja menos de 500 segmentos de transmissão em cada sandbox individual. A tentativa de criar segmentos adicionais de transmissão resultará em desempenho degradado do sistema. |
| Número máximo de segmentos de lote por sandbox | 10 mil | Suave | **O número máximo de segmentos em lote que uma organização pode criar é de 10 mil por sandbox.** Uma organização pode ter mais de 10 mil segmentos em lote no total, desde que haja menos de 10.000 segmentos em lote em cada sandbox individual. A tentativa de criar segmentos de lote adicionais resultará em um desempenho degradado do sistema. |
