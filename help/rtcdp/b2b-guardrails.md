---
keywords: perfil, perfil do cliente em tempo real, solução de problemas, medidas de proteção, diretrizes, limite, entidade, entidade primária, entidade de dimensão, RTCDP, CDP, B2B Edition, Real-time Customer Data Platform, plataforma de dados do cliente em tempo real, cdp em tempo real, b2b, cdp;
title: Grades de proteção padrão para Real-time Customer Data Platform B2B Edition
type: Documentation
description: A Adobe Experience Platform usa um modelo de dados híbrido não normalizado que difere do modelo de dados relacional tradicional. Este documento fornece limites de uso e taxa padrão para ajudá-lo a modelar seus dados para obter o melhor desempenho do sistema usando o Real-time Customer Data Platform B2B Edition.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# Grades de proteção padrão para Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Os limites descritos neste documento representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

O Real-time Customer Data Platform B2B Edition permite que você forneça experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis do cliente em tempo real e Perfis de conta. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados para obter o melhor desempenho do sistema. Ao revisar as seguintes medidas de proteção, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do serviço de atendimento ao cliente.

>[!INFO]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com seu representante de atendimento ao cliente.

## Tipos de limite

Existem dois tipos de limites padrão neste documento:

* **Limite suave:** É possível ir além de um limite suave, no entanto, os limites suaves fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido:** Um limite rígido fornece um máximo absoluto.

>[!INFO]
>
>Os limites indicados neste documento são constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com seu representante de atendimento ao cliente.

## Limites do modelo de dados

As seguintes medidas de proteção fornecem limites recomendados ao modelar dados de Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção em [tipos de entidade](#entity-types) no apêndice.

### Medidas de proteção de entidade primária

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Conjuntos de dados padrão da classe XDM da CDP B2B Edition em tempo real | 60 | Suave | Recomenda-se um máximo de 60 conjuntos de dados que aproveitam as classes padrão do Experience Data Model (XDM) fornecidas pela CDP B2B Edition em tempo real. Para obter uma lista completa das classes XDM padrão para casos de uso B2B, consulte [esquemas na documentação da Real-time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Observação: Devido à natureza do modelo de dados híbridos personalizado, a maioria dos clientes não excede esse limite. Em caso de dúvidas sobre como modelar seus dados ou se você deseja saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.* |
| Relações de várias entidades herdadas | 20 | Suave | Recomenda-se um máximo de 20 relacionamentos de várias entidades definidos entre entidades primárias e entidades de dimensão. Os mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Relações de muitos para um por classe XDM | 2 | Suave | Recomenda-se um máximo de 2 relações muitos para um definidas por classe XDM. Não deve ser estabelecida uma relação adicional enquanto não for removida ou desativada uma relação existente. Para obter etapas sobre como criar uma relação entre dois schemas, consulte o tutorial em [definição de relações de esquema B2B](../xdm/tutorials/relationship-b2b.md). |

### Medidas de proteção de Dimension entity

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Nenhum relacionamento herdado aninhado | 0 | Suave | Você não deve criar uma relação entre dois[!DNL XDM Individual Profile] esquemas. A capacidade de criar relacionamentos não é recomendada para qualquer schema que não faça parte do [!DNL Profile] esquema de união. |
| Somente objetos B2B podem participar de relacionamentos muitos para um | 0 | Grave | O sistema suporta apenas relações muitos para um entre objetos B2B. Para obter mais informações sobre relacionamentos muitos para um, consulte o tutorial em [definição de relações de esquema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profundidade máxima dos relacionamentos aninhados entre objetos B2B | 3 | Grave | A profundidade máxima de relacionamentos aninhados entre objetos B2B é 3. Isso significa que em um schema altamente aninhado, você não deve ter uma relação entre objetos B2B aninhados com mais de três níveis de profundidade. |

## Limites de tamanho de dados

As medidas de proteção a seguir referem-se ao tamanho dos dados e fornecem limites recomendados para dados que podem ser assimilados, armazenados e consultados conforme planejado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção em [tipos de entidade](#entity-types) no apêndice.

>[!INFO]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da ingestão.

### Medidas de proteção de entidade primária

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Lotes assimilados por classe XDM por dia | 45 | Suave | O número total de lotes ingeridos por dia por classe XDM não deve exceder 45. A incorporação de lotes adicionais pode impedir o desempenho ideal. |

### Medidas de proteção de Dimension entity

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho total para todas as entidades dimensionais | 5 GB | Suave | O tamanho total recomendado para todas as entidades dimensionais é de 5 GB. Inserir grandes entidades de dimensão pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Conjuntos de dados por esquema de entidade dimensional | 5 | Suave | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao schema de produtos. |
| lotes de entidade Dimension ingeridos por dia | 4 por entidade | Suave | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. Inserir lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

## Medidas de proteção de segmentação

As grades de proteção descritas nesta seção se referem ao número e à natureza dos segmentos que uma organização pode criar no Experience Platform, bem como ao mapeamento e ativação de segmentos para destinos.

>[!NOTE]
>
>Os limites de segmentação descritos nesta seção representam as alterações habilitadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Segmentos por sandbox B2B | 400 | Suave | Uma organização pode ter mais de 400 segmentos no total, desde que haja menos de 400 segmentos em cada sandbox B2B individual. Tentar criar segmentos adicionais pode afetar o desempenho do sistema. |

## Próximas etapas

Os limites descritos neste documento representam as alterações ativadas pelo Real-time Customer Data Platform B2B Edition. Para obter uma lista completa dos limites padrão da CDP B2B Edition em tempo real, combine esses limites com os limites gerais da Adobe Experience Platform descritos na [medidas de proteção para a documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

O [!DNL Profile] o modelo de dados de armazenamento consiste em dois tipos de entidade principais:

* **Entidade primária:** Uma entidade primária ou entidade de perfil une os dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;exibição de união&quot;. Uma exibição de união agrega os campos de todos os esquemas que implementam a mesma classe em um único schema de união. O schema de união para [!DNL Real-time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um contêiner para todos os atributos de perfil e eventos comportamentais.

   Atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot;, são modelados usando [!DNL XDM Individual Profile], enquanto que os dados das séries cronológicas, também conhecidos como &quot;dados de eventos&quot;, são modelados utilizando [!DNL XDM ExperienceEvent]. Como os dados de registro e de série de tempo são assimilados no Adobe Experience Platform, ele dispara [!DNL Real-time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos serão os perfis individuais.

   ![](../profile/images/guardrails/profile-entity.png)

* **Dimension entity:** Embora o armazenamento de dados do Perfil que mantém os dados do perfil não seja uma loja relacional, o Perfil permite a integração com pequenas entidades de dimensão para criar segmentos de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/multi-entity-segmentation.md). Sua organização também pode definir classes XDM para descrever coisas diferentes de indivíduos, como lojas, produtos ou propriedades. Esses[!DNL XDM Individual Profile] os schemas são conhecidos como &quot;entidades de dimensão&quot; e não contêm dados de séries de tempo. As entidades de Dimension fornecem dados de pesquisa que auxilia e simplifica definições de segmentos de várias entidades e devem ser pequenos o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa de ponto rápido).

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)
