---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Visão geral do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Visão geral do Perfil do cliente em tempo real

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente. Esta visão geral o ajudará a entender a função e o uso do Perfil do cliente em tempo real na plataforma da experiência.

## Entendendo o Perfil do cliente em tempo real

O Perfil de cliente em tempo real é um repositório de entidade de pesquisa genérico que reúne dados de vários ativos de dados corporativos e, em seguida, fornece acesso a esses dados na forma de perfis individuais de clientes e eventos de séries de tempo relacionados. Esse recurso permite que os profissionais de marketing conduzam experiências coordenadas, consistentes e relevantes com suas audiências em vários canais, como resumido no vídeo abaixo:

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&enable10seconds=on&speedcontrol=on)

### repositório de dados do Perfil

Embora o Perfil Cliente em tempo real processe dados ingeridos e use o Adobe Experience Platform Identity Service para unir dados relacionados por meio do mapeamento de identidade, ele mantém seus próprios dados na loja de Perfis. Em outras palavras, o armazenamento do Perfil é separado dos dados do Catálogo (Data Lake) e dos dados do Serviço de identidade (gráfico de identidade).

### Serviços de Perfil e plataforma

A relação entre o Perfil do cliente em tempo real e outros serviços na plataforma da experiência é destacada no diagrama a seguir:

![A relação entre o Perfil e outros serviços da plataforma de experiência.](images/profile-overview/profile-in-platform.png)

### Perfis e dados de registro

Um perfil é uma representação de um sujeito, de uma organização ou de um indivíduo, também conhecido como dados de registro. Por exemplo, o perfil de um produto pode incluir um SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de e-mail. Usando a plataforma Experience, você pode personalizar perfis para usar tipos de dados relevantes para sua empresa. A classe de Perfil individual padrão do Modelo de dados de experiência (XDM) é a classe preferida na qual criar um schema ao descrever dados de registro do cliente e fornece dados integrantes a muitas interações entre os serviços da plataforma. Para obter mais informações sobre como trabalhar com schemas na plataforma Experience, comece lendo a visão geral [do sistema](../xdm/home.md)XDM.

### eventos da série cronológica

Os dados das séries cronológicas fornecem um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por uma pessoa, bem como dados que detalham o próprio evento. Representados pela classe de schema padrão XDM ExperienceEvent, os dados da série de tempo podem descrever eventos como itens adicionados a um carrinho, links que estão sendo clicados e vídeos exibidos. Os dados das séries de tempo podem ser usados para basear as regras de segmentação em, e os eventos podem ser acessados individualmente no contexto de um perfil.

### Identidades

Toda empresa quer se comunicar com seus clientes de uma forma que se sinta pessoal. No entanto, um dos desafios de fornecer experiências digitais relevantes aos clientes é entender como unir seus dados desconectados, que geralmente é distribuído por diferentes canais digitais, como tablets, celulares e laptops. O Serviço de identidade permite que você reúna a imagem completa do seu cliente ao vincular identidades de vários canais, criando um gráfico de identidade para cada cliente, permitindo que você as entenda melhor. Visite a visão geral [do Serviço de](../identity-service/home.md) identidade para obter mais informações.

### Segmentação

O Adobe Experience Platform Segmentation Service produz as audiências necessárias para potencializar as experiências de seus clientes individuais. Quando um segmento de audiência é criado, a ID desse segmento é adicionada à lista de associações de segmento para todos os perfis qualificados. As regras de segmento são criadas e aplicadas aos dados de Perfil do cliente em tempo real usando RESTful APIs e a interface do usuário do Construtor de segmentos. Para saber mais sobre a segmentação, comece lendo a visão geral [do Serviço de](../segmentation/home.md)segmentação.

### Fragmentos de Perfil e visualizações de união {#profile-fragments-and-union-schemas}

Um dos principais recursos do Perfil do cliente em tempo real é a capacidade de unificar dados de vários canais. Quando o Perfil de cliente em tempo real é usado para acessar uma entidade, ele pode fornecer uma visualização unida de todos os fragmentos de perfil para essa entidade em conjuntos de dados, chamada de visualização de união. Os dados de Perfil do cliente em tempo real são unidos entre fontes quando uma entidade ou perfil é acessado por sua ID ou exportado como um segmento. Para saber mais sobre como acessar perfis e visualizações de união, visite o subguia do desenvolvedor da API Perfil do cliente em tempo real em [Entidades, também conhecido como &quot;Acesso ao Perfil&quot;](api/entities.md).

### Mesclar políticas

Ao reunir dados de várias fontes e combiná-los para ver uma visualização completa de cada um de seus clientes individuais, as políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem usando APIs, consulte o subguia [de políticas de](api/merge-policies.md) mesclagem da API do cliente em tempo real ou o guia [do usuário das políticas de](ui/merge-policies.md) mesclagem para saber como trabalhar com políticas de mesclagem usando a interface do usuário da plataforma.

## Componentes em tempo real

Esta seção apresenta os componentes que permitem ao Perfil de cliente em tempo real atualizar e monitorar dados de registro e de série de tempo em tempo real.

### Segmentação de fluxo e ingestão

A entrada em tempo real é possível por meio de um processo chamado de ingestão de streaming. À medida que os dados de perfil e de série cronológica são ingeridos, o Perfil de cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de fluxo contínuo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente computações e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes à medida que eles interagem com sua marca. Enquanto são ingeridos, os dados também passam pela validação para garantir que sejam ingeridos corretamente e estejam em conformidade com o schema no qual o conjunto de dados se baseia. Para obter mais informações sobre o que a validação é feita durante a ingestão, comece lendo a visão geral [da qualidade da ingestão de](../ingestion/quality/overview.md)dados.

### Projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. A plataforma Adobe Experience permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Por exemplo, os aplicativos da Adobe, como o Público alvo da Adobe e o Adobe Campaign, usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda.

Para saber mais e começar a trabalhar com bordas e projeções, consulte o subguia [Projeções de](api/edge-projections.md)borda da API do cliente em tempo real.

## Controle de dados e privacidade

O controle de dados é uma série de estratégias e tecnologias usadas para gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.

Como está relacionado ao acesso aos dados, o controle de dados desempenha um papel fundamental na plataforma da experiência em vários níveis:
* Rotulação de uso de dados
* Políticas de acesso aos dados
* Controle de acesso de dados para ações de marketing

O gerenciamento de dados é gerenciado em vários pontos. Eles incluem decidir quais dados são ingeridos na Plataforma e quais dados são acessíveis após a ingestão para uma determinada ação de marketing. Para obter mais informações, comece lendo a visão geral [do controle de](../data-governance/home.md)dados.

### Tratamento de solicitações de não participação e privacidade de dados

A plataforma Experience permite que seus clientes enviem solicitações de não participação relacionadas ao uso e armazenamento de seus dados no Perfil do cliente em tempo real. Para obter mais informações sobre como as solicitações de não participação são tratadas, consulte a documentação sobre como [atender às solicitações](../segmentation/honoring-opt-outs.md)de não participação.

## Adicionar dados ao Perfil do cliente em tempo real

A plataforma pode ser configurada para enviar seus dados de registro e de série de tempo ao Perfil, suportando a ingestão de streaming em tempo real e a ingestão em lote. Para obter mais informações, consulte o tutorial que descreve como [adicionar dados ao Perfil](tutorials/add-profile-data.md)do cliente em tempo real.

>[!Note]
>Os dados coletados por meio das soluções da Adobe, incluindo a Analytics Cloud, a Marketing Cloud e a Advertising Cloud, fluem para a plataforma Experience e são assimilados ao Perfil.

## Criar segmentos de audiência

A pedra angular da sua campanha de marketing é a sua audiência. O Perfil de cliente em tempo real fornece as ferramentas para segmentar sua base de clientes em audiências, consistindo em membros que atendem aos critérios precisos que você precisa. Com a segmentação, é possível isolar membros da audiência usando critérios como:

* Clientes para os quais uma semana se passou desde a última compra.
* Clientes para os quais a soma das compras é superior a US$ 10.000.
* Os clientes que viram um número definido de campanhas de marketing exclusivas de uma lista predefinida, especificada por sua ID de Campanha, e as exploraram dentro de 30 minutos.

Para começar a segmentação, consulte a visão geral [da](../segmentation/home.md)segmentação.

## (Alfa) Configurar atributos calculados

>[!IMPORTANT]
>A funcionalidade de atributo calculada descrita neste documento está em alfa. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos. Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Para obter mais informações sobre atributos calculados e instruções passo a passo para trabalhar com eles, consulte o [subguia da API de Perfil do cliente em tempo real sobre atributos](api/computed-attributes.md)calculados. Este guia ajudará você a entender melhor a função dos atributos calculados na Adobe Experience Platform e inclui exemplos de chamadas de API para executar operações CRUD básicas usando a API de Perfil do cliente em tempo real.