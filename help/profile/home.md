---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Visão geral do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---


# Visão geral do Perfil do cliente em tempo real

O Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente. Esta visão geral o ajudará a entender a função e o uso do Perfil do cliente em tempo real no Experience Platform.

## Entendendo o Perfil do cliente em tempo real

O Perfil de cliente em tempo real é um repositório de entidade de pesquisa genérico que reúne dados de vários ativos de dados corporativos e, em seguida, fornece acesso a esses dados na forma de perfis individuais de clientes e eventos de séries de tempo relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com suas audiências em vários canais.

### repositório de dados do Perfil

Embora o Perfil Cliente em tempo real processe dados ingeridos e use o Adobe Experience Platform Identity Service para unir dados relacionados por meio do mapeamento de identidade, ele mantém seus próprios dados na loja de Perfis. Em outras palavras, o armazenamento do Perfil é separado dos dados do Catálogo (Data Lake) e dos dados do Serviço de identidade (gráfico de identidade).

### Serviços Perfil e Platform

A relação entre o Perfil do cliente em tempo real e outros serviços no Experience Platform é destacada no diagrama a seguir:

![A relação entre o Perfil e outros serviços de Experience Platform.](images/profile-overview/profile-in-platform.png)

### Perfis e dados de registro

Um perfil é uma representação de um sujeito, de uma organização ou de um indivíduo, também conhecido como dados de registro. Por exemplo, o perfil de um produto pode incluir um SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de e-mail. Usando o Experience Platform, você pode personalizar perfis para usar tipos de dados relevantes para sua empresa. A classe de Perfil individual padrão do Modelo de dados de experiência (XDM) é a classe preferida na qual construir um schema ao descrever dados de registro do cliente e fornece dados integrantes a muitas interações entre os serviços da Platform. Para obter mais informações sobre como trabalhar com schemas no Experience Platform, comece lendo a visão geral [do sistema](../xdm/home.md)XDM.

### eventos da série cronológica

Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por uma pessoa, bem como dados que detalham o próprio evento. Representados pela classe de schema padrão XDM ExperienceEvent, os dados da série de tempo podem descrever eventos como itens adicionados a um carrinho, links que estão sendo clicados e vídeos exibidos. Os dados das séries de tempo podem ser usados para basear as regras de segmentação em, e os eventos podem ser acessados individualmente no contexto de um perfil.

### Identidades

Toda empresa quer se comunicar com seus clientes de uma forma que se sinta pessoal. No entanto, um dos desafios de fornecer experiências digitais relevantes aos clientes é entender como unir seus dados desconectados, que geralmente é distribuído por diferentes canais digitais, como tablets, celulares e laptops. O Serviço de identidade permite que você reúna a imagem completa do seu cliente ao vincular identidades de vários canais, criando um gráfico de identidade para cada cliente, permitindo que você as entenda melhor. Visite a visão geral [do Serviço de](../identity-service/home.md) identidade para obter mais informações.

### Segmentação

O Serviço de segmentação de Adobe Experience Platform produz as audiências necessárias para potencializar as experiências de seus clientes individuais. Quando um segmento de audiência é criado, a ID desse segmento é adicionada à lista de associações de segmento para todos os perfis qualificados. As regras de segmento são criadas e aplicadas aos dados de Perfil do cliente em tempo real usando RESTful APIs e a interface do usuário do Construtor de segmentos. Para saber mais sobre a segmentação, comece lendo a visão geral [do Serviço de](../segmentation/home.md)segmentação.

### Fragmentos de Perfil e schemas de união {#profile-fragments-and-union-schemas}

Um dos principais recursos do Perfil do cliente em tempo real é a capacidade de unificar dados de vários canais. Quando o Perfil de cliente em tempo real é usado para acessar uma entidade, ele pode fornecer uma visualização unida de todos os fragmentos de perfil para essa entidade em conjuntos de dados, chamada de visualização de união, e tornada possível por meio do que é conhecido como schema de união. Os dados de Perfil do cliente em tempo real são unidos entre fontes quando uma entidade ou perfil é acessado por sua ID ou exportado como um segmento. Para saber mais sobre como acessar perfis e visualizações de união usando a API Perfil do cliente em tempo real, visite o guia [de ponto de extremidade de](api/entities.md)entidades.

### Mesclar políticas

Ao reunir dados de várias fontes e combiná-los para ver uma visualização completa de cada um de seus clientes individuais, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem usando a API de Perfil do cliente em tempo real, consulte o guia [de ponto de extremidade de políticas de](api/merge-policies.md)mesclagem. Para trabalhar com políticas de mesclagem usando a interface do usuário Experience Platform, consulte o guia [do usuário das políticas de](ui/merge-policies.md)mesclagem.

### (Alfa) Configurar atributos calculados

>[!IMPORTANT]
>A funcionalidade de atributo calculada descrita neste documento está em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos. Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Para obter mais informações sobre atributos calculados e instruções passo a passo para trabalhar com eles usando a API de Perfil do cliente em tempo real, consulte o guia [de endpoint de atributos](api/computed-attributes.md)computados. Este guia o ajudará a entender melhor a função dos atributos calculados no Adobe Experience Platform e inclui exemplos de chamadas de API para executar operações CRUD básicas.

## Componentes em tempo real

Esta seção apresenta os componentes que permitem ao Perfil do cliente em tempo real atualizar e monitorar dados de registro e séries de tempo em tempo real.

### Segmentação de fluxo e ingestão

A entrada em tempo real é possível por meio de um processo chamado de ingestão de streaming. À medida que os dados de perfil e de série cronológica são ingeridos, o Perfil de cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de fluxo contínuo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente computações e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes à medida que eles interagem com sua marca. Enquanto são ingeridos, os dados também passam pela validação para garantir que sejam ingeridos corretamente e estejam em conformidade com o schema no qual o conjunto de dados se baseia. Para obter mais informações sobre o que a validação é feita durante a ingestão, comece lendo a visão geral [da qualidade da ingestão de](../ingestion/quality/overview.md)dados.

### Configurações e destinos de projeção de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. O Adobe Experience Platform permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Por exemplo, os aplicativos da Adobe, como Adobe Target e Adobe Campaign, usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda. Para saber mais e começar a trabalhar com projeções usando a API do Perfil do cliente em tempo real, consulte o guia [de pontos finais de projeção](api/edge-projections.md)avançado.

## Adicionar dados ao Perfil do cliente em tempo real

A Platform pode ser configurada para enviar seus dados de registro e série de tempo para o Perfil, com suporte para a ingestão em tempo real e a ingestão em lote. Para obter mais informações, consulte o tutorial que descreve como [adicionar dados ao Perfil](tutorials/add-profile-data.md)do cliente em tempo real.

>[!NObservação]
>Os dados coletados por meio das soluções da Adobe, incluindo a Analytics Cloud, a Marketing Cloud e a Advertising Cloud, fluem para o Experience Platform e são assimilados ao Perfil.

### Métricas de ingestão de Perfil

Insights de Observabilidade permitem que você exponha métricas principais no Adobe Experience Platform. Além das estatísticas de uso e indicadores de desempenho do Platform para várias funcionalidades do Platform, há métricas específicas relacionadas ao Perfil que permitem obter informações sobre as taxas de solicitação recebidas, taxas de ingestão bem-sucedidas, tamanhos de registro ingeridos e muito mais. Para saber mais, comece lendo a visão geral [do](../observability/home.md)Observability Insights e para obter uma lista completa das métricas de Perfil, consulte a documentação sobre as métricas [](../observability/metrics.md)disponíveis.

## Controle de dados e privacidade

O controle de dados é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.

Como está relacionado ao acesso aos dados, o controle de dados desempenha um papel fundamental dentro da Experience Platform em vários níveis:
* Rotulação de uso de dados
* Políticas de acesso aos dados
* Controle de acesso de dados para ações de marketing

O gerenciamento de dados é gerenciado em vários pontos. Eles incluem decidir quais dados são ingeridos no Platform e quais dados são acessíveis após a ingestão para uma determinada ação de marketing. Para obter mais informações, comece lendo a visão geral [do controle de](../data-governance/home.md)dados.

### Tratamento de solicitações de não participação e privacidade de dados

O Experience Platform permite que seus clientes enviem solicitações de não participação relacionadas ao uso e armazenamento de seus dados no Perfil do cliente em tempo real. Para obter mais informações sobre como as solicitações de não participação são tratadas, consulte a documentação sobre como [atender às solicitações](../segmentation/honoring-opt-outs.md)de não participação.

## Diretrizes para o Perfil

O Experience Platform tem uma série de diretrizes a serem seguidas para usar o Perfil com eficácia.

| Seção | Limite |
| ------- | -------- |
| schema união Perfil | Um máximo de **20** conjuntos de dados pode contribuir para o schema da união do Perfil. |
| Relações de várias entidades | É possível criar um máximo de **5** relações de várias entidades. |
| Profundidade JSON para associação de várias entidades | A profundidade máxima do JSON é **4**. |
| Dados das séries cronológicas | Os dados de séries de tempo **não** são permitidos em Perfil para entidades que não sejam de pessoas. |
| Relações de schema não-pessoas | Relações de schema de não pessoas **não** são permitidas. |
| fragmento do Perfil | O tamanho máximo recomendado de um fragmento de perfil é de **10 kB**.<br><br> O tamanho máximo absoluto de um fragmento de perfil é de **1 MB**. |
| Entidade não-pessoa | O tamanho total máximo para uma única entidade que não seja uma pessoa é de **200 MB**. |
| Conjuntos de dados por entidade não-pessoa | Um máximo de **1** conjunto de dados pode ser associado a uma entidade que não seja uma pessoa. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Uma entidade que não seja uma pessoa se refere a qualquer classe XDM que **não** faz parte do Perfil.

## Próximos passos e recursos adicionais

Para saber mais sobre o Perfil do cliente em tempo real, continue lendo a documentação e complemente sua aprendizagem assistindo ao vídeo abaixo ou explorando outros tutoriais [em vídeo sobre o](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)Experience Platform.

>[!WARNING]
>A interface do usuário do Platform mostrada no vídeo a seguir está desatualizada. Consulte o guia [de usuário do Perfil do cliente em tempo](ui/user-guide.md) real para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)