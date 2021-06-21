---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, perfil unificado, perfil unificado, unificado, perfil, rtcp, gráficos XDM
title: Visão geral do perfil do cliente em tempo real
topic-legacy: guide
description: O Perfil do cliente em tempo real é um armazenamento de entidade de pesquisa genérico que mescla dados de vários ativos de dados corporativos e, em seguida, fornece acesso a esses dados na forma de perfis de clientes individuais e eventos de séries de tempo relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com seus públicos-alvo em vários canais.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] visão geral

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada que oferece uma conta acionável com carimbo de data e hora de cada interação com o cliente. Esta visão geral ajudará você a entender a função e o uso de [!DNL Real-time Customer Profile] em [!DNL Experience Platform].

## [!DNL Profile] no Experience Platform

A relação entre o Perfil do cliente em tempo real e outros serviços no Experience Platform é destacada no diagrama a seguir:

![](images/profile-overview/profile-in-platform.png)

## Como entender perfis

[!DNL Real-time Customer Profile] mescla dados de vários sistemas corporativos e fornece acesso a esses dados na forma de perfis de clientes com eventos de séries cronológicas relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com seus públicos-alvo em vários canais. As seções a seguir destacam alguns dos conceitos principais que você deve entender para criar e manter perfis com eficácia no Platform.

### Armazenamento de dados do perfil

Embora [!DNL Real-time Customer Profile] processe dados assimilados e use o Adobe Experience Platform [!DNL Identity Service] para mesclar dados relacionados por meio do mapeamento de identidade, ele mantém seus próprios dados no armazenamento de dados [!DNL Profile]. O armazenamento [!DNL Profile] é separado dos dados do catálogo no lago de dados e dos dados [!DNL Identity Service] no gráfico de identidade.

O Repositório de Perfis usa uma infraestrutura do Microsoft Azure Cosmos DB e o Platform Data Lake usa o armazenamento do Microsoft Azure Data Lake.

### Medidas de proteção de perfil

O Experience Platform fornece uma série de medidas de proteção para ajudar você a evitar a criação de [Esquemas do Experience Data Model (XDM)](../xdm/home.md) que o Perfil do cliente em tempo real não suporta. Isso inclui limites suaves que resultarão em degradação do desempenho, além de limites rígidos que resultarão em erros e interrupções do sistema. Para obter mais informações, incluindo uma lista de diretrizes e casos de uso de exemplo, leia a documentação [Perfil de medidas de proteção](guardrails.md).

### (Beta) Painel do perfil {#profile-dashboard}

>[!IMPORTANT]
>
>A funcionalidade do painel está atualmente na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Experience Platform fornece um painel através do qual você pode visualizar informações importantes sobre os dados do Perfil do cliente em tempo real, conforme capturado durante um instantâneo diário. Para saber como acessar e trabalhar com o painel [!DNL Profile] na interface do usuário, e informações detalhadas sobre as métricas exibidas no painel, consulte o [Guia da interface do usuário do painel de perfis](ui/profile-dashboard.md).

### Fragmentos de perfil versus perfis mesclados {#profile-fragments-vs-merged-profiles}

Cada perfil de cliente individual é composto de vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente.

Quando os dados de várias fontes estão em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a [política de mesclagem](#merge-policies) determina quais informações priorizar e incluir no perfil do indivíduo. Portanto, o número total de fragmentos de perfil no Platform provavelmente será sempre maior que o número total de perfis mesclados, pois cada perfil é composto de vários fragmentos.

### Registrar dados

Um perfil é uma representação de um assunto, uma organização ou um indivíduo, composta de vários atributos (também conhecidos como dados de registro). Por exemplo, o perfil de um produto pode incluir um SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de email. Usando [!DNL Experience Platform], você pode personalizar perfis para usar dados específicos relevantes para sua empresa. A classe padrão [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], é a classe preferida sobre a qual criar um schema ao descrever dados de registro do cliente e fornece os dados integrantes a muitas interações entre os serviços da plataforma. Para obter mais informações sobre como trabalhar com esquemas em [!DNL Experience Platform], comece lendo a [Visão geral do Sistema XDM](../xdm/home.md).

### Eventos de séries cronológicas

Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um indivíduo, bem como dados que detalham o próprio evento. Representado pela classe de esquema padrão XDM ExperienceEvent, os dados de séries de tempo podem descrever eventos como itens adicionados a um carrinho, links clicados e vídeos visualizados. Os dados das séries de tempo podem ser usados para basear as regras de segmentação e os eventos podem ser acessados individualmente no contexto de um perfil.

### Identidades

Todas as empresas querem se comunicar com seus clientes de uma forma que se sinta pessoal. No entanto, um dos desafios de fornecer experiências digitais relevantes aos clientes é entender como unir seus dados desconectados, que geralmente é espalhado por diferentes canais digitais, como tablets, celulares e laptops. [!DNL Identity Service] O permite agrupar a imagem completa do cliente ao vincular identidades de vários canais e criar um gráfico de identidade para cada cliente. Visite a [Visão geral do Serviço de identidade](../identity-service/home.md) para obter mais informações.

### Mesclar políticas

Ao reunir fragmentos de dados de várias fontes e combiná-los para ver uma exibição completa de cada um de seus clientes individuais, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão usados para criar o perfil do cliente.

Quando há dados em conflito de vários conjuntos de dados, a política de mesclagem determina como esses dados devem ser tratados e qual valor deve ser usado. Por meio das RESTful APIs ou da interface do usuário, é possível criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização.

Para saber mais sobre as políticas de mesclagem e sua função no Experience Platform, comece lendo a [visão geral das políticas de mesclagem](merge-policies/overview.md).

### Esquemas de união {#profile-fragments-and-union-schemas}

Um dos principais recursos de [!DNL Real-time Customer Profile] é a capacidade de unificar dados de vários canais. Quando [!DNL Real-time Customer Profile] é usado para acessar uma entidade, ela pode fornecer uma visualização mesclada de todos os fragmentos de perfil para essa entidade em conjuntos de dados, chamada de &quot;visualização de união&quot; e disponibilizada por meio do que é conhecido como schema de união.

Para saber mais sobre schemas de união, incluindo como acessar schemas de união na interface do usuário, visite o [guia da interface do usuário do schema de união](ui/union-schema.md).

### (Alfa) Atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculada está em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são calculadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Para obter mais informações sobre atributos calculados, incluindo entender a função que os atributos calculados desempenham no Adobe Experience Platform, comece lendo a [visão geral dos atributos calculados](computed-attributes/overview.md).

## Perfis e segmentos

O Adobe Experience Platform [!DNL Segmentation Service] produz os públicos-alvo necessários para potencializar as experiências de seus clientes individuais. Quando um segmento de público-alvo é criado, a ID desse segmento é adicionada à lista de associações de segmento para todos os perfis qualificados. As regras de segmento são criadas e aplicadas aos dados [!DNL Real-time Customer Profile] usando APIs RESTful e a interface do usuário do Construtor de segmento. Para saber mais sobre a segmentação, comece lendo a [Visão geral do serviço de segmentação](../segmentation/home.md).

### Assimilação de streaming e segmentação de streaming

A entrada em tempo real é disponibilizada por meio de um processo chamado assimilação de streaming. Conforme os dados do perfil e da série de tempo são assimilados, [!DNL Real-time Customer Profile] decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado segmentação de fluxo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente os cálculos e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes, à medida que eles interagem com a sua marca. Ao serem assimilados, os dados também são validados para garantir que sejam assimilados corretamente e em conformidade com o esquema no qual o conjunto de dados se baseia. Para obter mais informações sobre o que a validação é feita durante a assimilação, comece lendo a [visão geral da qualidade da assimilação de dados](../ingestion/quality/overview.md).

## Projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente conforme as mudanças acontecem. O Adobe Experience Platform permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e a torna acessível para os aplicativos. Por exemplo, aplicativos Adobe como Adobe Target e Adobe Campaign usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo as informações específicas que serão disponibilizadas na borda. Para saber mais e começar a trabalhar com projeções usando a API [!DNL Real-time Customer Profile], consulte o [guia de endpoints de projeção de borda](api/edge-projections.md).

## Inserção de dados em [!DNL Profile]

[!DNL Platform] pode ser configurado para enviar dados de registro e de série de tempo para o  [!DNL Profile], com suporte para assimilação de streaming em tempo real e assimilação de lote. Para obter mais informações, consulte o tutorial descrevendo como [adicionar dados ao Perfil do cliente em tempo real](tutorials/add-profile-data.md).

>[!NOTE]
>
>Os dados coletados por meio de soluções Adobe, incluindo [!DNL Analytics Cloud], [!DNL Marketing Cloud] e [!DNL Advertising Cloud], fluem para [!DNL Experience Platform] e são assimilados em [!DNL Profile].

### Métricas de assimilação de perfil

O Observability Insights permite expor as métricas principais no Adobe Experience Platform. Além das [!DNL Experience Platform] estatísticas de uso e indicadores de desempenho para várias [!DNL Platform] funcionalidades, há métricas específicas relacionadas a perfis que permitem obter informações sobre as taxas de solicitação recebidas, taxas de ingestão bem-sucedidas, tamanhos de registro assimilados e muito mais. Para saber mais, comece lendo a [Visão geral da API do Observability Insights](../observability/api/overview.md) e para obter uma lista completa das métricas do Perfil do cliente em tempo real, consulte a documentação sobre [métricas disponíveis](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] e [!DNL Privacy]

[!DNL Data governance] O é uma série de estratégias e tecnologias usadas para gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.

Como está relacionado ao acesso aos dados, o controle de dados desempenha uma função essencial em [!DNL Experience Platform] em vários níveis:
* Rotulação de uso de dados
* Políticas de acesso a dados
* Controle de acesso em dados para ações de marketing

[!DNL Data governance] é gerenciada em vários pontos. Isso inclui decidir quais dados são assimilados em [!DNL Platform] e quais dados podem ser acessados após a assimilação de uma determinada ação de marketing. Para obter mais informações, comece lendo a [visão geral de governança de dados](../data-governance/home.md).

### Tratamento de solicitações de recusa e privacidade de dados

[!DNL Experience Platform] O permite que os clientes enviem solicitações de recusa relacionadas ao uso e armazenamento de seus dados no  [!DNL Real-time Customer Profile]. Para obter mais informações sobre como as solicitações de recusa são tratadas, consulte a documentação sobre [como atender às solicitações de recusa](../segmentation/consents.md).

## Próximas etapas e recursos adicionais

Para saber mais sobre como trabalhar com dados [!DNL Real-time Customer Profile] usando a interface do usuário do Experience Platform ou a API de perfil, comece lendo o [Guia da interface do usuário de perfil](ui/user-guide.md) ou o [Guia do desenvolvedor da API](api/overview.md), respectivamente.
