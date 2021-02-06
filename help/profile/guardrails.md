---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;guardrails;diretrizes;limite;entidade;entidade primária;entidade de dimensão;
title: Garantias para dados de Perfil do cliente em tempo real
solution: Experience Platform
product: experience platform
topic: guide
type: Documentation
description: 'A Adobe Experience Platform oferece uma série de garantias para ajudá-lo a evitar a criação de modelos de dados que o Perfil do cliente em tempo real não suporta. Esse documento descreve as práticas recomendadas e as restrições a serem levadas em conta ao modelar os dados do Perfil. '
translation-type: tm+mt
source-git-commit: ba1cbed3b5e3f3a8879b3882856a03ef4be9b96a
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 2%

---


# Guardões para dados [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fornece perfis individuais que permitem fornecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente. Para atingir essa definição de metas, [!DNL Profile] e o mecanismo de segmentação dentro da Adobe Experience Platform usam um modelo de dados híbridos altamente desnormalizado que oferta uma nova abordagem para perfis de clientes em desenvolvimento. O uso desse modelo de dados híbridos torna extremamente importante que os dados coletados sejam modelados corretamente. Embora o armazenamento de dados [!DNL Profile] que mantém os dados do perfil não seja um armazenamento relacional, [!DNL Profile] permite a integração com pequenas entidades de dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como segmentação de várias entidades.

A Adobe Experience Platform fornece uma série de garantias para ajudá-lo a evitar a criação de modelos de dados que [!DNL Real-time Customer Profile] não suportam. Esse documento descreve essas garantias, bem como as práticas recomendadas e as restrições ao usar os dados do Perfil para segmentação.

>[!NOTE]
>
>Os níveis de garantia e os limites indicados neste documento estão constantemente a ser melhorados. Verifique regularmente se há atualizações.

## Introdução

É recomendável que você leia a seguinte documentação dos serviços de Experience Platform antes de tentar criar modelos de dados para uso em [!DNL Real-time Customer Profile]. Trabalhar com modelos de dados e as garantias descritas neste documento requer uma compreensão dos vários serviços da Experience Platform com o gerenciamento de entidades [!DNL Real-time Customer Profile]:

* [[!DNL Real-time Customer Profile]](home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Serviço](../identity-service/home.md) de identidade Adobe Experience Platform: Suporta a criação de uma &quot;visualização única do cliente&quot;, fazendo a ponte entre identidades de fontes de dados diferentes conforme são assimiladas  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../xdm/schema/composition.md) do schema: Uma introdução aos schemas e modelagem de dados dentro do Experience Platform.
* [Serviço](../segmentation/home.md) de segmentação do Adobe Experience Platform: O mecanismo de segmentação dentro do qual você  [!DNL Platform] usa para criar segmentos de audiência a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.
   * [Segmentação](../segmentation/multi-entity-segmentation.md) de várias entidades: Um guia para a criação de segmentos que integram entidades de dimensão aos dados do perfil.

## Tipos de entidade

O modelo de dados de armazenamento [!DNL Profile] consiste em dois tipos de entidades principais:

* **Entidade primária:** Uma entidade primária ou entidade perfil une os dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização união agregação os campos de todos os schemas que implementam a mesma classe em um único schema de união. O schema de união para [!DNL Real-time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um container para todos os atributos do perfil e eventos comportamentais.

   Os atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot; são modelados usando [!DNL XDM Individual Profile], enquanto os dados da série de tempo, também conhecidos como &quot;dados de evento&quot; são modelados usando [!DNL XDM ExperienceEvent]. À medida que os dados de registro e de série de tempo são ingeridos no Adobe Experience Platform, ele aciona [!DNL Real-time Customer Profile] para começar a assimilar dados que foram habilitados para seu uso. Quanto mais interações e detalhes forem ingeridos, mais robustos serão os perfis individuais.

   ![](images/guardrails/profile-entity.png)

* **Dimension entity:** Sua organização também pode definir classes XDM para descrever coisas diferentes de indivíduos, como lojas, produtos ou propriedades. Esses schemas não[!DNL XDM Individual Profile] são conhecidos como &quot;entidades de dimensão&quot; e não contêm dados de série de tempo. As entidades de Dimension fornecem dados de pesquisa que auxiliam e simplificam as definições de segmentos de várias entidades e devem ser suficientemente pequenos para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa de ponto rápido).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Tipos de limite

Ao definir o modelo de dados, é recomendável que você fique dentro dos coletores fornecidos para garantir o desempenho correto e evitar erros do sistema. Os coletores fornecidos neste documento incluem dois tipos de limite:

* **Limite suave:** um limite suave fornece um máximo recomendado para o desempenho ideal do sistema. É possível ir além de um limite flexível sem quebrar o sistema ou receber mensagens de erro, no entanto, ir além de um limite flexível resultará em degradação do desempenho. É recomendável permanecer dentro do limite flexível para evitar diminuições no desempenho geral.

* **Limite rígido:** um limite rígido fornece um máximo absoluto para o sistema. Ultrapassar um limite rígido resultará em interrupções e erros, impedindo o sistema de funcionar conforme esperado.

## Tampões do modelo de dados

É recomendável seguir os seguintes coletores ao criar um modelo de dados para uso com [!DNL Real-time Customer Profile].

### Garantias da entidade principal

| Guarda | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número de conjuntos de dados recomendados para contribuir com o schema de união [!DNL Profile] | 20 | Suave | **É recomendado um máximo de 20 conjuntos de dados  [!DNL Profile]habilitados.** Para habilitar outro conjunto de dados para  [!DNL Profile], um conjunto de dados existente deve ser removido ou desabilitado primeiro. |
| Número de relacionamentos de várias entidades recomendados | 5 | Suave | **É recomendado um máximo de 5 relacionamentos multientidades definidos entre entidades primárias e entidades de dimensão.** Mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desativado. |
| Profundidade máxima do JSON para o campo de ID usado em relação de várias entidades | 4 | Suave | **A profundidade máxima de JSON recomendada para um campo de ID usado em relações de várias entidades é 4.** Isso significa que em um schema altamente aninhado, os campos que têm mais de 4 níveis de profundidade não devem ser usados como campo de ID em um relacionamento. |
| cardinalidade de matriz em um fragmento de perfil | &lt;=500 | Suave | **A cardinalidade ideal do storage em um fragmento de perfil (dados independentes de tempo) é  &lt;>** |
| cardinalidade de matriz em ExperienceEvent | &lt;=10 | Suave | **A cardinalidade ideal do storage em um ExperienceEvent (dados da série cronológica) é  &lt;>** |

### Dimension

| Guarda | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Nenhum dado de série de tempo permitido para entidades que não são[!DNL XDM Individual Profile] | 0 | Grave | **Dados de séries de tempo não são permitidos para não [!DNL XDM Individual Profile] entidades no Serviço de Perfis.** Se um conjunto de dados de séries de tempo estiver associado a uma não-[!DNL XDM Individual Profile] ID, o conjunto de dados não deverá ser ativado para  [!DNL Profile]. |
| Sem relações aninhadas | 0 | Suave | **Você não deve criar uma relação entre dois não-[!DNL XDM Individual Profile] schemas.** A capacidade de criar relações não é recomendada para schemas que não façam parte do schema da  [!DNL Profile] união. |
| Profundidade máxima do JSON para o campo de ID principal | 4 | Suave | **A profundidade máxima de JSON recomendada para o campo de ID principal é 4.** Isso significa que em um schema altamente aninhado, você não deve selecionar um campo como ID principal se ele estiver aninhado com mais de quatro níveis de profundidade. Um campo que está no quarto nível aninhado pode ser usado como uma ID primária. |

## Resgates de tamanho de dados

Os seguintes coletores se referem ao tamanho dos dados e são recomendados para garantir que os dados possam ser assimilados, armazenados e consultados conforme desejado.

>[!NOTE]
>
>O tamanho dos dados será medido como dados não comprimidos no JSON no momento da ingestão.

### Garantias da entidade principal

| Guarda | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho máximo por fragmento de perfil | 10 KB | Suave | **O tamanho máximo recomendado de um fragmento de perfil é de 10 KB.** A inserção de fragmentos maiores de perfil afetará o desempenho do sistema. Por exemplo, carregar um conjunto de dados CRM pesado onde alguns fragmentos de perfil têm tamanho de 50 kB resultará em desempenho degradado do sistema. |
| Tamanho máximo absoluto por fragmento de perfil | 1 MB | Grave | **O tamanho máximo absoluto de um fragmento de perfil é de 1MB.** A ingestão falhará ao tentar carregar um fragmento de perfil maior que 1MB. |

### Dimension

| Guarda | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total máximo para todas as entidades dimensionais | 5 GB | Suave | **O tamanho total máximo recomendado para todas as entidades dimensionais é de 5 GB.** Ingerir entidades de dimensão grande resultará em desempenho degradado do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Conjuntos de dados por schema de entidade dimensional | 5 | Suave | **É recomendado um máximo de cinco conjuntos de dados associados a cada schema de entidade dimensional.** Por exemplo, se você criar um schema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao schema de produtos. |

## Testes de segmentação

Os painéis de controle descritos nesta seção referem-se ao número e à natureza dos segmentos que uma organização pode criar dentro do Experience Platform, bem como ao mapeamento e ativação de segmentos para destinos.

| Guarda | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de segmentos por caixa de proteção | 10.000 | Suave | **O número máximo de segmentos que uma organização pode criar é de 10 mil por caixa de proteção.** Uma organização pode ter mais de 10 mil segmentos no total, desde que haja menos de 10.000 segmentos em cada caixa de proteção individual. A tentativa de criar segmentos adicionais resultará em um desempenho degradado do sistema. |
| Número máximo de segmentos de transmissão por caixa de proteção | 500 | Suave | **O número máximo de segmentos de fluxo contínuo que uma organização pode criar é de 500 por caixa de proteção.** Uma organização pode ter mais de 500 segmentos de streaming no total, desde que haja menos de 500 segmentos de streaming em cada caixa de proteção individual. A tentativa de criar segmentos de streaming adicionais resultará em desempenho degradado do sistema. |
| Número máximo de segmentos de lote por caixa de proteção | 10.000 | Suave | **O número máximo de segmentos em lote que uma organização pode criar é de 10 mil por caixa de proteção.** Uma organização pode ter mais de 10 mil segmentos em lote no total, desde que haja menos de 10.000 segmentos em lote em cada caixa de proteção individual. A tentativa de criar segmentos de lote adicionais resultará em desempenho degradado do sistema. |