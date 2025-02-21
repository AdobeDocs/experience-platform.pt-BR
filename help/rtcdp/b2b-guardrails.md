---
keywords: perfil;perfil de cliente em tempo real;solução de problemas;medidas de proteção;diretrizes;limite;entidade;entidade primária;entidade de dimensão;RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;
title: Proteções padrão para o Real-Time Customer Data Platform B2B edition
type: Documentation
description: A Adobe Experience Platform usa um modelo de dados híbrido não normalizado que difere do modelo de dados relacional tradicional. Este documento fornece limites de uso e taxa padrão para ajudar a modelar seus dados para obter o melhor desempenho do sistema usando o Adobe Real-Time Customer Data Platform B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: bc399f3af0524232671af780ea1380f1a71a5b7e
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# Proteções padrão para o Real-Time Customer Data Platform B2B edition

>[!NOTE]
>
>Os limites descritos neste documento representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

O Real-Time Customer Data Platform B2B edition permite oferecer experiências personalizadas entre canais com base em insights comportamentais e atributos do cliente na forma de Perfis de clientes em tempo real e Perfis de conta. Para dar suporte a essa nova abordagem aos perfis, o Experience Platform usa um modelo de dados híbrido altamente desnormalizado que difere do modelo de dados relacional tradicional.

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

Este documento fornece limites de uso e taxa padrão para ajudar você a modelar seus dados para obter o melhor desempenho do sistema. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

>[!INFO]
>
>A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Tipos de limite

Há dois tipos de limites padrão neste documento:

| Tipo de grade de proteção | Descrição |
| -------------- | ----------- |
| **Proteção de desempenho (limite flexível)** | As medidas de proteção de desempenho são limites de uso relacionados ao escopo dos seus casos de uso. Ao exceder as medidas de proteção de desempenho, você pode enfrentar degradação e latência do desempenho. A Adobe não é responsável por essa degradação de desempenho. Os clientes que excederem consistentemente uma garantia de desempenho podem optar por licenciar capacidade adicional para evitar a degradação do desempenho. |
| **Medidas de proteção aplicadas pelo sistema (Limite rígido)** | As medidas de proteção aplicadas pelo sistema são aplicadas pela interface do usuário ou API do Real-Time CDP. Esses são limites que você não pode exceder, pois a interface do usuário e a API o bloquearão de fazer isso ou retornarão um erro. |

>[!INFO]
>
>Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações. Se você estiver interessado em saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.

## Limites do modelo de dados

As medidas de proteção a seguir fornecem limites recomendados ao modelar dados do Perfil do cliente em tempo real. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no Apêndice.

### Medidas de proteção da entidade principal

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Conjuntos de dados da classe XDM padrão do Real-Time CDP B2B edition | 60 | Proteção de desempenho | Recomenda-se um máximo de 60 conjuntos de dados que usam as classes padrão do Experience Data Model (XDM) fornecidas pelo Real-Time CDP B2B edition. Para obter uma lista completa de classes XDM padrão para casos de uso B2B, consulte [esquemas na documentação do Real-Time CDP B2B edition](schemas/b2b.md). <br/><br/>*Observação: devido à natureza do modelo de dados híbrido desnormalizado da Experience Platform, a maioria dos clientes não excede esse limite. Para perguntas sobre como modelar seus dados, ou se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.* |
| Contagem de identidades da conta individual em um gráfico de identidade | 50 | Proteção de desempenho | O número máximo de identidades em um Gráfico de identidade para uma conta individual é 50. Quaisquer perfis com mais de 50 identidades são excluídos da segmentação, das exportações e das pesquisas. |
| Relacionamentos herdados de várias entidades | 20 | Proteção de desempenho | Recomenda-se um máximo de 20 relacionamentos de várias entidades definidos entre entidades primárias e entidades de dimensão. Mapeamentos de relacionamento adicionais não devem ser feitos até que um relacionamento existente seja removido ou desabilitado. |
| Relacionamentos muitos para um por classe XDM | 2 | Proteção de desempenho | Recomenda-se um máximo de 2 relações muitos para um definidas por classe XDM. Uma relação adicional não deve ser feita até que uma relação existente seja removida ou desabilitada. Para obter etapas sobre como criar uma relação entre dois esquemas, consulte o tutorial em [definindo relações de esquema B2B](../xdm/tutorials/relationship-b2b.md). |

### Medidas de proteção de entidade do Dimension

>[!NOTE]
>
>Os limites do modelo de dados descritos nesta seção representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Nenhuma relação herdada aninhada | 0 | Proteção de desempenho | Você não deve criar uma relação entre dois esquemas diferentes de [!DNL XDM Individual Profile]. A criação de relações **não** é recomendada para qualquer esquema que não faça parte do esquema de união [!DNL Profile]. |
| Somente objetos B2B podem participar de relações muitos para um | 0 | Proteção imposta pelo sistema | O sistema só suporta relações muitos para um entre objetos B2B. Para obter mais informações sobre relações muitos para um, consulte o tutorial em [definindo relações de esquema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profundidade máxima de relações aninhadas entre objetos B2B | 3 | Proteção imposta pelo sistema | A profundidade máxima das relações aninhadas entre objetos B2B é 3. Isso significa que em um esquema altamente aninhado, você não deve ter uma relação entre objetos B2B aninhados a mais de 3 níveis de profundidade. |
| Esquema único para cada entidade de dimensão | 1 | Proteção imposta pelo sistema | Cada entidade de dimensão deve ter um único esquema. Tentar usar entidades de dimensão criadas a partir de mais de um esquema pode afetar os resultados da segmentação. Espera-se que diferentes entidades de dimensão tenham esquemas separados. |

## Limites de tamanho de dados

As medidas de proteção a seguir se referem ao tamanho dos dados e fornecem limites recomendados para os dados que podem ser assimilados, armazenados e consultados conforme esperado. Para saber mais sobre entidades primárias e entidades de dimensão, consulte a seção sobre [tipos de entidade](#entity-types) no Apêndice.

>[!INFO]
>
>O tamanho dos dados é medido como dados descompactados no JSON no momento da assimilação.

### Medidas de proteção da entidade principal

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Lotes assimilados por classe XDM por dia | 45 | Proteção de desempenho | O número total de lotes assimilados a cada dia por classe XDM não deve exceder 45. A ingestão de lotes adicionais pode impedir o desempenho ideal. |

### Medidas de proteção de entidade do Dimension

>[!NOTE]
>
>Os limites de tamanho de dados descritos nesta seção representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Tamanho total de todas as entidades dimensionais | 5GB | Proteção de desempenho | O tamanho total recomendado para todas as entidades dimensionais é 5 GB. A ingestão de entidades de dimensão grandes pode afetar o desempenho do sistema. Por exemplo, não é recomendado tentar carregar um catálogo de produtos de 10 GB como uma entidade de dimensão. |
| Esquema de entidade dimensional de conjuntos de dados | 5 | Proteção de desempenho | Recomenda-se um máximo de 5 conjuntos de dados associados a cada esquema de entidade dimensional. Por exemplo, se você criar um esquema para &quot;produtos&quot; e adicionar cinco conjuntos de dados de contribuição, não deverá criar um sexto conjunto de dados vinculado ao esquema de produtos. |
| Lotes de entidades do Dimension assimilados por dia | 4 por entidade | Proteção de desempenho | O número máximo recomendado de lotes de entidades de dimensão assimilados por dia é 4 por entidade. Por exemplo, você pode assimilar atualizações em um catálogo de produtos até 4 vezes por dia. A ingestão de lotes de entidades de dimensão adicionais para a mesma entidade pode afetar o desempenho do sistema. |

## Proteções de segmentação

As medidas de proteção descritas nesta seção referem-se ao número e à natureza dos públicos que uma organização pode criar no Experience Platform, bem como mapear e ativar públicos para destinos.

>[!NOTE]
>
>Os limites de segmentação descritos nesta seção representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --------- | ----- | ---------- | ----------- |
| Definições de segmento por sandbox B2B | 400 | Proteção de desempenho | Uma organização pode ter mais de 400 definições de segmento no total, desde que haja menos de 400 definições de segmento em cada sandbox B2B individual. Tentar criar definições de segmento adicionais pode afetar o desempenho do sistema. |

## Próximas etapas

Os limites descritos neste documento representam as alterações ativadas pelo Real-Time Customer Data Platform B2B edition. Para obter uma lista completa dos limites padrão do Real-Time CDP B2B edition, combine esses limites com os limites gerais do Adobe Experience Platform descritos na [garantia da documentação de dados do Perfil do cliente em tempo real](../profile/guardrails.md).

## Apêndice

Esta seção fornece detalhes adicionais para os limites neste documento.

### Tipos de entidade

O modelo de dados de repositório [!DNL Profile] consiste em dois tipos de entidade principais: [entidades primárias](#primary-entity) e [entidades de dimensão](#dimension-entity).

#### Entidade principal

Uma entidade principal, ou entidade de perfil, mescla dados para formar uma &quot;única fonte de verdade&quot; para um indivíduo. Esses dados unificados são representados usando o que é conhecido como &quot;visualização de união&quot;. Uma visualização de união agrega os campos de todos os esquemas que implementam a mesma classe em um único esquema de união. O esquema de união para [!DNL Real-Time Customer Profile] é um modelo de dados híbrido desnormalizado que atua como um contêiner para todos os atributos de perfil e eventos comportamentais.

Atributos independentes de tempo, também conhecidos como &quot;dados de registro&quot; são modelados usando [!DNL XDM Individual Profile], enquanto dados de série temporal, também conhecidos como &quot;dados de evento&quot; são modelados usando [!DNL XDM ExperienceEvent]. Como os dados de registro e série temporal são assimilados na Adobe Experience Platform, ele aciona [!DNL Real-Time Customer Profile] para começar a assimilar dados que foram habilitados para uso. Quanto mais interações e detalhes forem assimilados, mais robustos os perfis individuais se tornarão.

![Um infográfico que descreve as diferenças entre os dados de registro e os dados de série temporal.](../profile/images/guardrails/profile-entity.png)

#### Entidade Dimension

Embora o armazenamento de dados do perfil que mantém os dados do perfil não seja um armazenamento relacional, o Perfil permite a integração com entidades de pequena dimensão para criar públicos-alvo de maneira simplificada e intuitiva. Essa integração é conhecida como [segmentação de várias entidades](../segmentation/tutorials/multi-entity-segmentation.md).

Sua organização também pode definir classes XDM para descrever coisas que não sejam indivíduos, como lojas, produtos ou propriedades. Esses esquemas não [!DNL XDM Individual Profile] são chamados de &quot;entidades de dimensão&quot; (também conhecidas como &quot;entidades de pesquisa&quot;) e não contêm dados de série temporal. Esquemas que representam entidades de dimensão são vinculados a entidades de perfil por meio do uso de [relações de esquema](../xdm/tutorials/relationship-ui.md).

As entidades Dimension fornecem dados de pesquisa que auxiliam e simplificam as definições de segmento de várias entidades e devem ser pequenas o suficiente para que o mecanismo de segmentação possa carregar todo o conjunto de dados na memória para um processamento ideal (pesquisa rápida por ponto).

![Um infográfico que mostra que uma entidade de perfil é composta de entidades de dimensão.](../profile/images/guardrails/profile-and-dimension-entities.png)
