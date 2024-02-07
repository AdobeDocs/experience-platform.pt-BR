---
title: Visão geral do Perfil do cliente em tempo real
description: O Perfil do cliente em tempo real mescla dados de várias fontes e fornece acesso a esses dados na forma de perfis de clientes individuais e eventos de séries de tempo relacionados. Esse recurso permite que os profissionais de marketing promovam experiências coordenadas, consistentes e relevantes com seus públicos-alvo em vários canais.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: dde38e230a6bcb10cd38a12f644f2dd03f0cebaf
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# Visão geral do [!DNL Real-Time Customer Profile]

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-Time Customer Profile]No entanto, você pode ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente. Esta visão geral ajudará você a entender a função e o uso de [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] no Experience Platform

A relação entre o Perfil do cliente em tempo real e outros serviços no Experience Platform é destacada no diagrama a seguir:

![A relação entre o Perfil do cliente em tempo real e outros serviços na Adobe Experience Platform. Este diagrama mostra que o Perfil é um dos componentes principais do Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Noções básicas sobre perfis

[!DNL Real-Time Customer Profile] O mescla dados de vários sistemas corporativos e, em seguida, fornece acesso a esses dados na forma de perfis de clientes com eventos de série temporal relacionados. Esse recurso permite que os profissionais de marketing promovam experiências coordenadas, consistentes e relevantes com seus públicos-alvo em vários canais. As seções a seguir destacam alguns dos conceitos principais que você deve entender para criar e manter perfis na Platform com eficiência.

### Composição da entidade de perfil

Um Perfil de cliente em tempo real é composto por uma entidade principal, chamada **entidade principal** e várias entidades de suporte. No contexto do Experience Platform, a entidade primária é normalmente uma **entidade de perfil**, que é composto por características, comportamentos e associações de público-alvo de uma pessoa individual. Outras entidades permitem que o mecanismo de segmentação utilize dados fora da entidade principal do perfil e incluem o seguinte:

- **Entidade dimensional**: a entidade usada para simplificar o processo de modelagem de dados para informações compartilhadas entre eventos ou registros de perfil. Também é conhecida como entidade de pesquisa ou entidade de classificação.
- **Entidade B2B**: entidades que descrevem o relacionamento do perfil com contas e oportunidades de negócios para negócios.

![Um diagrama que explica a composição da entidade do perfil.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Como as entidades dimensionais e B2B só existem fora da entidade principal, elas são usadas apenas para segmentação em lote.

As entidades dimensionais e B2B estão vinculadas à entidade principal por meio de **relacionamentos de esquema**. Consulte a seguinte documentação para obter mais informações:

- [Criar uma relação de esquema um para um para entidades de pesquisa](../xdm/tutorials/relationship-ui.md)
- [Criar uma relação de esquema muitos para um para entidades B2B](../xdm/tutorials/relationship-b2b.md)

### Armazenamento de dados do perfil

Embora [!DNL Real-Time Customer Profile] processa dados assimilados e usa o Adobe Experience Platform [!DNL Identity Service] para mesclar dados relacionados por meio do mapeamento de identidade, ele mantém seus [!DNL Profile] armazenamento de dados. A variável [!DNL Profile] o armazenamento é separado dos dados do catálogo no data lake e [!DNL Identity Service] dados no gráfico de identidade.

O armazenamento de perfis usa uma infraestrutura do Microsoft Azure Cosmos DB e o Platform Data Lake usa o armazenamento do Microsoft Azure Data Lake.

### Medidas de proteção de perfil

O Experience Platform fornece uma série de medidas de proteção para ajudar você a evitar a criação de [Esquemas do Experience Data Model (XDM)](../xdm/home.md) que o Perfil de cliente em tempo real não pode suportar. Isso inclui limites flexíveis que resultarão em degradação do desempenho, bem como limites rígidos que resultarão em erros e quebras do sistema. Para obter mais informações, incluindo uma lista de diretrizes e casos de uso de exemplo, leia o [Medidas de proteção de perfil](guardrails.md) documentação.

### Painel do perfil {#profile-dashboard}

A interface do usuário do Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre os dados do Perfil do cliente em tempo real, conforme capturados durante um instantâneo diário. Para saber como acessar e trabalhar com a [!DNL Profile] painel na interface e informações detalhadas sobre as métricas exibidas no painel, consulte as [Guia da interface do usuário do painel de perfil](ui/profile-dashboard.md).

### Fragmentos de perfil versus perfis mesclados {#profile-fragments-vs-merged-profiles}

Cada perfil de cliente individual é composto por vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente.

Em outras palavras, os fragmentos de perfil representam uma identidade principal exclusiva e a variável [gravar](#record-data) ou [evento](#time-series-events) para essa ID em um determinado conjunto de dados.

Quando os dados de vários conjuntos de dados estão em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a variável [política de mesclagem](#merge-policies) determina quais informações priorizar e incluir no perfil do indivíduo. Portanto, o número total de fragmentos de perfil na Platform provavelmente sempre será maior que o número total de perfis mesclados, pois cada perfil normalmente é composto de vários fragmentos de vários conjuntos de dados.

### Registrar dados {#record-data}

Um perfil é uma representação de um sujeito, uma organização ou um indivíduo, composto por muitos atributos (também conhecidos como dados de registro). Por exemplo, o perfil de um produto pode incluir uma SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de email. Usar [!DNL Experience Platform], você pode personalizar perfis para usar dados específicos relevantes para sua empresa. O padrão [!DNL Experience Data Model] classe (XDM), [!DNL XDM Individual Profile], é a classe preferida sobre a qual criar um esquema ao descrever dados de registro do cliente e fornece os dados integrais a muitas interações entre os serviços da plataforma. Para obter mais informações sobre como trabalhar com esquemas em [!DNL Experience Platform], comece lendo o [Visão geral do sistema XDM](../xdm/home.md).

### Eventos de série temporal {#time-series-events}

Os dados de série temporal fornecem um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um sujeito, bem como dados detalhando o próprio evento. Representados pela classe de esquema padrão XDM ExperienceEvent, os dados de série temporal podem descrever eventos como itens adicionados ao carrinho, links clicados e vídeos visualizados. Os dados de série temporal podem ser usados para basear as regras de segmentação em, e os eventos podem ser acessados individualmente no contexto de um perfil.

### Identidades

Toda empresa quer se comunicar com seus clientes de uma forma que pareça pessoal. No entanto, um dos desafios de fornecer experiências digitais relevantes para os clientes é entender como unir seus dados desconectados, que geralmente estão distribuídos em diferentes canais digitais, como tablets, celulares e notebooks. [!DNL Identity Service] O permite unir a imagem completa do cliente, vinculando identidades de vários canais e criando um gráfico de identidade para cada cliente. Visite o [Visão geral do serviço de identidade](../identity-service/home.md) para obter mais informações.

### Políticas de mesclagem

Ao reunir fragmentos de dados de várias fontes e combiná-los para ter uma visualização completa de cada cliente individual, as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão usados para criar o perfil do cliente.

Quando há dados conflitantes de vários conjuntos de dados, a política de mesclagem determina como esses dados devem ser tratados e qual valor deve ser usado. Por meio das APIs RESTful ou da interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização.

Para saber mais sobre as políticas de mesclagem e sua função no Experience Platform, comece lendo o [visão geral das políticas de mesclagem](merge-policies/overview.md).

### Esquemas de união {#profile-fragments-and-union-schemas}

Um dos principais recursos do [!DNL Real-Time Customer Profile] é a capacidade de unificar dados de vários canais. Quando [!DNL Real-Time Customer Profile] for usada para acessar uma entidade, ela poderá fornecer uma exibição mesclada de todos os fragmentos de perfil dessa entidade em conjuntos de dados, conhecida como &quot;exibição de união&quot;, e possibilitada por meio do que é conhecido como esquema de união.

Para saber mais sobre esquemas de união, incluindo como acessar esquemas de união na interface do usuário, visite o [guia da interface do esquema de união](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Perfis e públicos-alvo

Adobe Experience Platform [!DNL Segmentation Service] O produz os públicos-alvo necessários para potencializar experiências para seus clientes individuais. Quando um público-alvo é criado, a ID dele é adicionada à lista de associações de público-alvo para todos os perfis qualificados. As regras de segmento são criadas e aplicadas a [!DNL Real-Time Customer Profile] dados usando APIs RESTful e a interface do usuário do Construtor de segmentos. Para saber mais sobre segmentação, comece lendo o [Visão geral do serviço de segmentação](../segmentation/home.md).

### Assimilação e segmentação de transmissão

A entrada em tempo real é possibilitada por meio de um processo chamado assimilação de streaming. À medida que os dados de perfil e série temporal são assimilados, [!DNL Real-Time Customer Profile] O decide automaticamente incluir ou excluir esses dados dos públicos-alvo por meio de um processo contínuo chamado segmentação por transmissão, antes de mesclá-los aos dados existentes e atualizar a visualização de união. Como resultado, você pode realizar cálculos instantaneamente e tomar decisões para fornecer experiências aprimoradas e individualizadas aos clientes, à medida que eles interagem com sua marca. Enquanto são assimilados, os dados também são submetidos a validação para garantir que sejam assimilados corretamente e estejam em conformidade com o esquema no qual o conjunto de dados se baseia. Para obter mais informações sobre qual validação é feita durante a assimilação, comece lendo o [visão geral da qualidade de assimilação de dados](../ingestion/quality/overview.md).

## Assimilar dados no [!DNL Profile]

[!DNL Platform] pode ser configurado para enviar dados de registro e série temporal para [!DNL Profile], com suporte para assimilação por transmissão em tempo real e assimilação em lote. Para obter mais informações, consulte o tutorial descrevendo como [adicionar dados ao Perfil de cliente em tempo real](tutorials/add-profile-data.md).

>[!NOTE]
>
>Dados coletados por meio de soluções Adobe, incluindo [!DNL Analytics Cloud], [!DNL Marketing Cloud], e [!DNL Advertising Cloud], flui para [!DNL Experience Platform] e é assimilado em [!DNL Profile].

### Métricas de assimilação de perfil

Os Insights de capacidade de observação permitem expor as métricas principais no Adobe Experience Platform. Além de [!DNL Experience Platform] estatísticas de uso e indicadores de desempenho para vários [!DNL Platform] existem métricas específicas relacionadas ao perfil que permitem obter informações sobre taxas de solicitação recebidas, taxas de assimilação bem-sucedidas, tamanhos de registro assimilados e muito mais. Para saber mais, comece lendo o [Visão geral da API do Observability Insights](../observability/api/overview.md)e para obter uma lista completa das métricas do Perfil do cliente em tempo real, consulte a documentação em [métricas disponíveis](../observability/api/metrics.md#available-metrics).

## Atualizar dados da Loja de Perfis

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis da sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag upsert. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributo, consulte o tutorial para [ativar um conjunto de dados para Perfil e substituição](../catalog/datasets/enable-upsert.md).

## Governança de dados e [!DNL Privacy]

O controle de dados é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com normas, restrições e políticas aplicáveis ao uso de dados.

No que diz respeito ao acesso aos dados, a governança de dados desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis:

- Rótulo de uso de dados
- Políticas de acesso a dados
- Controle de acesso em dados para ações de marketing

A governança de dados é gerenciada em vários pontos. Isso inclui decidir em quais dados são assimilados [!DNL Platform] e quais dados estão acessíveis após a assimilação para uma determinada ação de marketing. Para obter mais informações, comece lendo o [visão geral da governança de dados](../data-governance/home.md).

### Lidar com solicitações de recusa e privacidade de dados

[!DNL Experience Platform] O permite que os clientes enviem solicitações de recusa relacionadas ao uso e ao armazenamento de seus dados no [!DNL Real-Time Customer Profile]. Para obter mais informações sobre como as solicitações de recusa são tratadas, consulte a documentação em [atender às solicitações de recusa](../segmentation/consents.md).

## Próximas etapas e recursos adicionais

Para saber mais sobre como trabalhar com dados de Perfil do cliente em tempo real usando a interface do usuário do Experience Platform ou a API de perfil, comece lendo o [Guia da interface do usuário do perfil](ui/user-guide.md) ou [Guia do desenvolvedor de API](api/overview.md), respectivamente.
