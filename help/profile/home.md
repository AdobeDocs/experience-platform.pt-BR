---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Visão geral do Perfil do cliente em tempo real
topic: guide
description: O Perfil de cliente em tempo real é um repositório de entidade de pesquisa genérico que reúne dados de vários ativos de dados corporativos e, em seguida, fornece acesso a esses dados na forma de perfis individuais de clientes e eventos de séries de tempo relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com suas audiências em vários canais.
translation-type: tm+mt
source-git-commit: b8d6bd5caf6c6f4d1da218b6ca12cec154d64412
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]visão geral

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-time Customer Profile]o, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente. Esta visão geral o ajudará a entender a função e o uso do [!DNL Real-time Customer Profile] em [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

A relação entre o Perfil do cliente em tempo real e outros serviços no Experience Platform é destacada no diagrama a seguir:

![Serviços Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

### repositório de dados do perfil

Embora [!DNL Real-time Customer Profile] processe dados ingeridos e use o Adobe Experience Platform [!DNL Identity Service] para unir dados relacionados por meio do mapeamento de identidade, ele mantém seus próprios dados na [!DNL Profile] loja. O [!DNL Profile] armazenamento é separado dos [!DNL Catalog] dados no [!DNL Data Lake] e dos [!DNL Identity Service] dados no gráfico de identidade.

O repositório de Perfis usa uma infraestrutura de BD do Microsoft Azure Cosmos e o Lago de Dados da Plataforma usa o armazenamento Data Lake do Microsoft Azure.

### Perfil

O Experience Platform oferece uma série de garantias para ajudar você a evitar a criação de schemas [do Modelo de Dados de](../xdm/home.md) Experiência (XDM) que o Perfil do Cliente em tempo real não suporta. Isso inclui limites suaves que resultarão na degradação do desempenho, além de limites rígidos que resultarão em erros e quebras do sistema. Para obter mais informações, incluindo uma lista de diretrizes e casos de uso de exemplo, leia a documentação do [Perfil guardrails](guardrails.md) .

## Como entender perfis

[!DNL Real-time Customer Profile] une dados de vários sistemas corporativos e, em seguida, fornece acesso a esses dados na forma de perfis do cliente com eventos de séries cronológicas relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com suas audiências em vários canais. As seções a seguir destacam alguns dos conceitos principais que você deve entender para construir e manter perfis com eficácia na Plataforma.

### Fragmentos de perfil vs perfis mesclados {#profile-fragments-vs-merged-profiles}

Cada perfil de cliente individual é composto de vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são ingeridos na Plataforma, eles são unidos para criar um único perfil para o cliente.

Quando os dados de várias fontes entram em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política [de](#merge-policies) mesclagem determina quais informações priorizar e incluir no perfil do indivíduo. Portanto, é provável que o número total de fragmentos de perfil na Plataforma sempre seja maior do que o número total de perfis unidos, já que cada perfil é composto de vários fragmentos.

### Registrar dados

Um perfil é uma representação de um sujeito, uma organização ou um indivíduo, composto por vários atributos (também conhecidos como dados de registro). Por exemplo, o perfil de um produto pode incluir um SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de e-mail. Usando [!DNL Experience Platform], você pode personalizar perfis para usar dados específicos relevantes à sua empresa. A classe padrão [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], é a classe preferida na qual construir um schema ao descrever os dados de registro do cliente, e fornece os dados integrantes a muitas interações entre os serviços da plataforma. Para obter mais informações sobre como trabalhar com schemas no, [!DNL Experience Platform]comece lendo a visão geral [do Sistema](../xdm/home.md)XDM.

### Eventos da série cronológica

Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por uma pessoa, bem como dados que detalham o próprio evento. Representados pela classe de schema padrão XDM ExperienceEvent, os dados da série de tempo podem descrever eventos como itens adicionados a um carrinho, links que estão sendo clicados e vídeos exibidos. Os dados das séries de tempo podem ser usados para basear as regras de segmentação em, e os eventos podem ser acessados individualmente no contexto de um perfil.

### Identidades

Toda empresa quer se comunicar com seus clientes de uma forma que se sinta pessoal. No entanto, um dos desafios de fornecer experiências digitais relevantes aos clientes é entender como unir seus dados desconectados, que geralmente é distribuído por diferentes canais digitais, como tablets, celulares e laptops. [!DNL Identity Service] permite reunir a imagem completa do cliente ao vincular identidades de vários canais e criar um gráfico de identidade para cada cliente. Visite a visão geral [do Serviço de](../identity-service/home.md) identidade para obter mais informações.

### Mesclar políticas

Ao reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa de cada um de seus clientes individuais, as políticas de mesclagem são as regras que [!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão usados para criar o perfil do cliente. Quando houver dados conflitantes de vários conjuntos de dados, a política de mesclagem determinará como esses dados devem ser tratados e qual valor deve ser usado. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem usando a [!DNL Real-time Customer Profile] API, consulte o guia [de ponto de extremidade de políticas de](api/merge-policies.md)mesclagem. Para trabalhar com políticas de mesclagem usando a [!DNL Experience Platform] interface do usuário, consulte o guia [do usuário das políticas de](ui/merge-policies.md)mesclagem.

### Schemas uniões {#profile-fragments-and-union-schemas}

Um dos principais recursos do é [!DNL Real-time Customer Profile] a capacidade de unificar dados de vários canais. Quando [!DNL Real-time Customer Profile] é usado para acessar uma entidade, ela pode fornecer uma visualização unida de todos os fragmentos de perfil para essa entidade em conjuntos de dados, chamada de visualização de união e tornada possível por meio do que é conhecido como schema de união. [!DNL Real-time Customer Profile] os dados são unidos entre fontes quando uma entidade ou perfil é acessado por sua ID ou exportado como um segmento. Para saber mais sobre como acessar perfis e visualizações de união usando a [!DNL Real-time Customer Profile] API, visite o guia [de ponto de extremidade de](api/entities.md)entidades.

### Segmentação

A Adobe Experience Platform [!DNL Segmentation Service] produz as audiências necessárias para potencializar as experiências de seus clientes individuais. Quando um segmento de audiência é criado, a ID desse segmento é adicionada à lista de associações de segmento para todos os perfis qualificados. As regras de segmento são criadas e aplicadas aos [!DNL Real-time Customer Profile] dados usando RESTful APIs e a interface do usuário do Construtor de segmentos. Para saber mais sobre a segmentação, comece lendo a visão geral [do Serviço de](../segmentation/home.md)segmentação.

### (Alfa) Configurar atributos calculados

>[!IMPORTANT]
>
>A funcionalidade do atributo calculado está em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos. Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Para obter mais informações sobre atributos calculados e instruções passo a passo para trabalhar com eles usando a [!DNL Real-time Customer Profile] API, consulte o guia [de ponto de extremidade de atributos](api/computed-attributes.md)computados. Este guia o ajudará a entender melhor a função dos atributos calculados no Adobe Experience Platform e inclui exemplos de chamadas de API para executar operações CRUD básicas.

## Componentes em tempo real

Esta seção apresenta os componentes que permitem atualizar e monitorar dados de registros e séries de tempo em tempo real. [!DNL Real-time Customer Profile]

### Segmentação de fluxo e ingestão

A entrada em tempo real é possível por meio de um processo chamado de ingestão de streaming. À medida que os dados do perfil e da série cronológica são ingeridos, [!DNL Real-time Customer Profile] decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de streaming, antes de mesclá-los aos dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente computações e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes à medida que eles interagem com sua marca. Enquanto são ingeridos, os dados também passam pela validação para garantir que sejam ingeridos corretamente e estejam em conformidade com o schema no qual o conjunto de dados se baseia. Para obter mais informações sobre o que a validação é feita durante a ingestão, comece lendo a visão geral [da qualidade da ingestão de](../ingestion/quality/overview.md)dados.

### Configurações e destinos de projeção de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. A Adobe Experience Platform permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Por exemplo, aplicativos de Adobe como Adobe Target e Adobe Campaign usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda. Para saber mais e começar a trabalhar com projeções usando a [!DNL Real-time Customer Profile] API, consulte o guia [de pontos finais de projeção de](api/edge-projections.md)borda.

## Ingest data into [!DNL Profile]

[!DNL Platform] pode ser configurado para enviar dados de registro e de série de tempo para [!DNL Profile], com suporte à ingestão de streaming em tempo real e à ingestão em lote. Para obter mais informações, consulte o tutorial que descreve como [adicionar dados ao Perfil](tutorials/add-profile-data.md)do cliente em tempo real.

>[!NOTE]
>
>Os dados coletados por meio de soluções de Adobe, incluindo [!DNL Analytics Cloud], [!DNL Marketing Cloud]e [!DNL Advertising Cloud], fluem [!DNL Experience Platform] e são assimilados [!DNL Profile].

### [!DNL Profile] métricas de ingestão

Insights de Observabilidade permitem que você exponha as métricas principais no Adobe Experience Platform. Além das estatísticas de [!DNL Platform] uso e dos indicadores de desempenho para várias [!DNL Platform] funcionalidades, há métricas [!DNL Profile]relacionadas especificamente que permitem obter informações sobre as taxas de solicitação recebidas, taxas de ingestão bem-sucedidas, tamanhos de registro ingeridos e muito mais. Para saber mais, comece lendo a visão geral [da API](../observability/api/overview.md)Observability Insights e para obter uma lista completa das [!DNL Profile] métricas, consulte a documentação sobre as métricas [](../observability/api/metrics.md#available-metrics)disponíveis.

## [!DNL Data governance] e [!DNL Privacy]

[!DNL Data governance] é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.

Como está relacionado ao acesso aos dados, o controle de dados desempenha um papel fundamental em vários [!DNL Experience Platform] níveis:
* Rotulação de uso de dados
* Políticas de acesso aos dados
* Controle de acesso de dados para ações de marketing

[!DNL Data governance] é gerenciada em vários pontos. Eles incluem decidir em quais dados são ingeridos [!DNL Platform] e quais dados são acessíveis após a ingestão para uma determinada ação de marketing. Para obter mais informações, comece lendo a visão geral [do controle de](../data-governance/home.md)dados.

### Tratamento de solicitações de não participação e privacidade de dados

[!DNL Experience Platform] permite que seus clientes enviem solicitações de recusa relacionadas ao uso e armazenamento de seus dados no [!DNL Real-time Customer Profile]. Para obter mais informações sobre como as solicitações de não participação são tratadas, consulte a documentação sobre como [atender às solicitações](../segmentation/honoring-opt-outs.md)de não participação.

## Próximos passos e recursos adicionais

Para saber mais sobre como trabalhar com [!DNL Real-time Customer Profile], leia o guia [da interface do usuário do](ui/user-guide.md) Perfil ou o guia [do desenvolvedor da](api/overview.md)API.

>[!WARNING]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter sido alterada desde a gravação deste vídeo. Consulte o guia [de usuário do Perfil do cliente em tempo](ui/user-guide.md) real para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)