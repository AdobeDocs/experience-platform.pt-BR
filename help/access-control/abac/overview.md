---
keywords: Experience Platform; home; tópicos populares; controle de acesso; controle de acesso baseado em atributos;
title: Visão geral do controle de acesso baseado em atributos
description: Este documento fornece informações sobre o controle de acesso baseado em atributos no Adobe Experience Platform
hide: true
hidefromtoc: true
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 70c0ba81c682fd512c24265f12d1fef6ca14b34e
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 1%

---

# Visão geral do controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuário e função para definir políticas de acesso em torno dos campos do esquema XDM e gerenciar melhor o acesso dado aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários aos dados pessoais confidenciais (SPD) e às informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que têm acesso apenas a campos e dados específicos que correspondem a esses campos.

## Terminologia do controle de acesso baseado em atributos

O controle de acesso baseado em atributos envolve os seguintes componentes:

| Terminologia | Definição |
| --- | --- |
| Atributos | Atributos são os identificadores que indicam a correlação entre um usuário e os recursos da plataforma aos quais eles têm acesso. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário. |
| Rótulos | Rótulos permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados na plataforma ou assim que os dados forem disponibilizados para uso na plataforma. |
| Permissões | As permissões incluem a capacidade de exibir e/ou usar recursos da plataforma, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados. |
| Conjuntos de permissões | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas a partir de uma função predefinida que contém um grupo de permissões. |
| Políticas | Políticas são declarações que reúnem atributos para estabelecer ações admissíveis e não permissíveis. As políticas podem ser locais ou globais e podem substituir outras políticas. |
| Recurso | Um recurso é o ativo ou objeto que um assunto pode ou não acessar. Os recursos podem ser arquivos, aplicativos, servidores ou até mesmo APIs. |
| Funções | As funções definem o acesso que um administrador, especialista ou usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso de exibição ou gravação necessário. |
| Assunto | Um assunto é o usuário que solicita acesso a um recurso para executar uma ação. |
| Grupos de usuários | Os grupos de usuários são vários usuários que foram agrupados e têm acesso para executar as mesmas funções. |

## Permissões

>[!IMPORTANT]
>
>Depois que sua organização estiver habilitada para o controle de acesso com base em atributos, você poderá começar a usar as Permissões no Adobe Experience Cloud, em vez de Perfis de produto no Adobe Admin Console, para gerenciar permissões para usuários, funcionalidades, rótulos e outros recursos em sua organização.

Permissões é a área do Experience Cloud, onde os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto.

Por meio das Permissões, é possível criar e gerenciar funções, bem como atribuir as permissões de recurso desejadas para essas funções. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica. Para obter mais informações, consulte o [Guia de permissões](ui/browse.md).

## API de controle de acesso com base em atributos

A API de controle de acesso baseada em atributos permite gerenciar programaticamente funções, políticas e produtos na Platform usando APIs. Para obter mais informações, consulte o guia sobre [usando a API para gerenciar configurações de controle de acesso baseadas em atributos](api/overview.md).

## Controle de acesso baseado em atributos no Adobe Experience Platform

As seções a seguir fornecem informações sobre como o controle de acesso baseado em atributos é integrado a outros componentes da Plataforma:

### Controle de acesso

Aproveitamento da plataforma [Adobe Admin Console](https://adminconsole.adobe.com) perfis de produto para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a uma variedade de recursos da plataforma, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox. Depois que sua organização estiver habilitada para o controle de acesso com base em atributos, você poderá começar a usar as Permissões no Adobe Experience Cloud, em vez de Perfis de produto no Adobe Admin Console, para gerenciar permissões para usuários, funcionalidades, rótulos e outros recursos em sua organização.

Para obter mais informações sobre o controle de acesso, consulte [visão geral do controle de acesso](../home.md).

### Destinos

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

Como administrador, você pode usar as funcionalidades de controle de acesso baseadas em atributos para:

* Configure o acesso do usuário para visualizar segmentos específicos no processo de ativação, com base na função, nas permissões e nos rótulos;
   * No processo de ativação, os usuários podem ser solicitados a selecionar segmentos que desejam ativar para um destino. Como administrador, você pode provisionar usuários em sua organização para ver somente segmentos rotulados com rótulos aos quais os usuários têm acesso e segmentos que não contêm rótulos.
* Configure o acesso do usuário para exibir campos específicos no processo de ativação, com base na função, nas permissões e nos rótulos;
   * No processo de ativação, os usuários podem ser solicitados a selecionar campos que desejam ativar para um destino. Como administrador, você pode provisionar usuários em sua organização para ver apenas campos rotulados com rótulos aos quais os usuários têm acesso e campos que não contêm rótulos.

Para obter mais informações sobre [!DNL Destinations], consulte o [[!DNL Destinations] visão geral](../../destinations/home.md).

### Identity Service

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

Como parte do controle de acesso baseado em atributos, a variável `view-identity-graph` permite determinar quais usuários em sua organização podem acessar o gráfico de identidade por meio da interface do usuário ou das APIs. Para obter mais informações, consulte o guia sobre [usando o visualizador de gráfico de identidade](../../identity-service/ui/identity-graph-viewer.md).

Para obter mais informações sobre [!DNL Identity Service], consulte o [[!DNL Identity Service] visão geral](../../identity-service/home.md).

### Perfil do cliente em tempo real

A plataforma permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar seus diferentes dados do cliente em uma visualização unificada que oferece uma conta acionável com carimbo de data e hora de cada interação com o cliente.

Como administrador, você pode usar as funcionalidades de controle de acesso baseadas em atributos para:

* Configure o acesso do usuário a atributos de perfil específicos com base na função, nas permissões e nos rótulos;
   * Como administrador, você pode provisionar usuários em sua organização para ver apenas atributos de perfil rotulados com rótulos aos quais os usuários têm acesso e atributos de perfil que não contêm rótulo;
   * Como administrador, você pode provisionar usuários em sua organização para ver somente os atributos do perfil rotulados com rótulos aos quais os usuários têm acesso ao criar segmentos;
* Configure o acesso do usuário à visualização de dados, rotulando campos de dados específicos usados no esquema XDM do modelo de dados.

Para obter mais informações sobre Perfil, consulte o [Visão geral do perfil](../../profile/home.md).

### Serviço de segmentação

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

Como administrador, você pode usar as funcionalidades de controle de acesso baseadas em atributos para:

* Configure o acesso do usuário para visualizar e gerenciar segmentos específicos, com base na função, nas permissões e nos rótulos;
   * Como administrador, você pode provisionar usuários em sua organização para ver apenas segmentos rotulados com rótulos aos quais os usuários têm acesso e segmentos que não contêm rótulos, ao usar a interface de segmentação.

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [[!DNL Segmentation Service] visão geral](../../segmentation/home.md).

### XDM

O Experience Data Model (XDM) é uma especificação de código aberto criada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços na plataforma. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

Com o controle de acesso baseado em atributos, você pode:

* Aplicar atributos a grupos de campos e ou classes. Isso permite que vários esquemas com os mesmos grupos de campos ou classes, tenham campos marcados com os mesmos atributos, dependendo das configurações no grupo de campos ou nível de classe;
* Configure o acesso do usuário a campos de esquema XDM específicos, dependendo dos conjuntos de permissões aplicados a funções atribuídas a usuários.

Para obter mais informações sobre o XDM, consulte [Visão geral do XDM](../../xdm/home.md).