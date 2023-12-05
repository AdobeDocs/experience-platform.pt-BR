---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributos;
title: Visão Geral do Controle de Acesso Baseado em Atributo
description: Este documento fornece informações sobre o controle de acesso baseado em atributos no Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 44ffcc09edcfe35bdd456b509fac6f096ef8e022
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 13%

---

# Visão geral do controle de acesso baseado em atributos

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso em torno de campos de esquema XDM e gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos não deve ser confundido com os recursos de governança de dados do Experience Platform, que permitem usar rótulos e políticas para controlar como os dados são usados na Platform, em vez de quais usuários em sua organização têm acesso a eles. Consulte a [visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD), informações de identificação pessoal (PII) e tipo personalizado de dados em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

O vídeo a seguir é destinado a ajudá-lo a entender o controle de acesso baseado em atributos e descreve como configurar funções, recursos e políticas.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Terminologia de controle de acesso baseado em atributo

O controle de acesso baseado em atributos envolve os seguintes componentes:

| Terminologia | Definição |
| --- | --- |
| Atributos | Atributos são os identificadores que indicam a correlação entre um usuário e os recursos da Platform aos quais ele tem acesso. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário. |
| Rótulos | Os rótulos permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles forem assimilados na Platform ou assim que os dados estiverem disponíveis para uso na Platform. |
| Permissões | As permissões incluem a capacidade de visualizar e/ou usar recursos da Platform, como criar sandboxes, definir esquemas e gerenciar conjuntos de dados. |
| Conjuntos de permissões | Os conjuntos de permissões representam um grupo de permissões que um administrador pode aplicar a uma função. Um administrador pode atribuir conjuntos de permissões a uma função, em vez de atribuir permissões individuais. Isso permite criar funções personalizadas com base em uma função predefinida que contém um grupo de permissões. |
| Políticas | Políticas são declarações que reúnem atributos para estabelecer ações permitidas e não permitidas. As políticas podem ser locais ou globais e podem substituir outras políticas. |
| Recurso | Um recurso é o ativo ou objeto que um assunto pode ou não acessar. Os recursos podem ser segmentos ou campos de esquema. |
| Funções | Funções são maneiras de categorizar os tipos de usuários que estão interagindo com sua instância da Platform. São os pilares das políticas de controle de acesso. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões, e os membros da organização podem ter uma ou mais funções atribuídas, dependendo do escopo do acesso de visualização ou gravação necessário. |
| Assunto | Um assunto é o usuário que solicita acesso a um recurso para executar uma ação. |
| Grupos de usuários | Os grupos de usuários são vários usuários que foram agrupados e têm acesso para executar as mesmas funções. |

## Permissões

>[!IMPORTANT]
>
>Quando sua organização estiver habilitada para o controle de acesso baseado em atributos, você poderá começar a usar Permissões no Adobe Experience Cloud, em vez de Funções no Adobe Admin Console, para gerenciar permissões para usuários, funcionalidades, rótulos e outros recursos em sua organização.

Permissões é a área do Experience Cloud em que os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto.

Através das Permissões, é possível criar e gerenciar funções, bem como atribuir as permissões de recurso desejadas para essas funções. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica. Para obter mais informações, consulte [Guia de permissões](ui/browse.md).

## API de controle de acesso baseado em atributo

A API de controle de acesso baseada em atributos permite gerenciar programaticamente funções, políticas e produtos na Platform usando APIs. Para obter mais informações, consulte o guia no [usar a API para gerenciar configurações de controle de acesso baseadas em atributos](api/overview.md).

## Controle de acesso baseado em atributos no Adobe Experience Platform

As seções a seguir fornecem informações sobre como o controle de acesso baseado em atributos é integrado a outros componentes da Platform:

### Controle de acesso

A Platform utiliza [Adobe Admin Console](https://adminconsole.adobe.com) funções para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a uma variedade de recursos da Platform, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox. Quando sua organização estiver habilitada para o controle de acesso baseado em atributos, você poderá começar a usar Permissões no Adobe Experience Cloud, em vez de Funções no Adobe Admin Console, para gerenciar permissões para usuários, funcionalidades, rótulos e outros recursos em sua organização.

Há disponibilidade limitada de controle de acesso baseado em atributos para clientes que compram os Healthcare and/ou Privacy Shields. Os recursos dessa funcionalidade incluem:

* Interface de permissões: fornece uma interface para que você defina funções de usuário, permissões e políticas para o controle de acesso baseado em atributos.

* Rotulagem: adicione, edite e remova rótulos de funções de usuário, campos de esquema, segmentos e outros objetos compatíveis para aproveitar as políticas de controle de acesso.

Os workflows de administração de todos os aplicativos alimentados por Experience Platform do Admin Console para a nova interface de Permissões estão sendo trocados.

>[!IMPORTANT]
>
>Suas funções são migradas automaticamente para a interface de Permissões quando a organização é habilitada. As funções no Admin Console permanecerão como estão por enquanto. Por favor **não** modifique suas funções depois que sua organização for habilitada.

Para obter mais informações sobre controle de acesso, consulte a [visão geral do controle de acesso](../home.md).

### Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

Como administrador, você pode usar as funcionalidades de controle de acesso baseado em atributos para:

* Configure o acesso do usuário para visualizar segmentos específicos no processo de ativação, com base na função, permissões e rótulos;
   * No processo de ativação, os usuários podem precisar selecionar os segmentos que desejam ativar para um destino. Como administrador, você pode provisionar usuários em sua organização para ver apenas os segmentos rotulados com rótulos aos quais os usuários têm acesso e os segmentos que não contêm rótulos.
* Configure o acesso do usuário para visualizar campos específicos no processo de ativação, com base na função, permissões e rótulos;
   * No processo de ativação, os usuários podem precisar selecionar os campos que desejam ativar para um destino. Como administrador, você pode provisionar usuários em sua organização para ver somente os campos rotulados com rótulos aos quais os usuários têm acesso e os campos que não contêm rótulos.

>[!IMPORTANT]
>
>Em resumo, lembre-se das seguintes implicações ao trabalhar com destinos e controle de acesso baseado em atributos:
>
>* Você só pode ativar segmentos aos quais tem permissão para acessar e visualizar no [visualização de navegação de segmento](/help/segmentation/ui/overview.md#browse) e [selecionar etapa do segmento](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) do workflow de ativação.
>* No [etapa de mapeamento do fluxo de trabalho de ativação](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), você só poderá exibir e selecionar para ativação os campos aos quais tem permissão de acesso.
>* Quando estiver procurando ativar segmentos adicionais para um destino existente no qual você não tem acesso a todos os campos mapeados para exportação, o fluxo de trabalho de ativação será bloqueado para você.

Para obter mais informações sobre [!DNL Destinations], consulte o [[!DNL Destinations] visão geral](../../destinations/home.md).

### Identity Service

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

Como parte do controle de acesso baseado em atributos, a variável `view-identity-graph` A permissão de permite determinar quais usuários em sua organização podem acessar o gráfico de identidade por meio da interface ou das APIs. Para obter mais informações, consulte o manual sobre [uso do visualizador de gráficos de identidade](../../identity-service/ui/identity-graph-viewer.md).

Para obter mais informações sobre [!DNL Identity Service], consulte o [[!DNL Identity Service] visão geral](../../identity-service/home.md).

### Perfil do cliente em tempo real

O Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar dados diferentes do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

Como administrador, você pode usar as funcionalidades de controle de acesso baseado em atributos para:

* Configurar o acesso do usuário a atributos específicos de perfil com base em função, permissões e rótulos;
   * Como administrador, você pode provisionar usuários em sua organização para ver apenas atributos de perfil rotulados com rótulos aos quais os usuários têm acesso e atributos de perfil que não contêm nenhum rótulo;
   * Como administrador, você pode provisionar usuários em sua organização para ver apenas os atributos de perfil rotulados com rótulos aos quais os usuários têm acesso ao criar segmentos;
* Configure o acesso do usuário à visualização de dados, rotulando campos de dados específicos usados no esquema XDM do modelo de dados.

Para obter mais informações sobre Perfil, consulte [Visão geral do perfil](../../profile/home.md).

### Serviço de segmentação

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

Como administrador, você pode usar as funcionalidades de controle de acesso baseado em atributos para:

* Configure o acesso do usuário para visualizar e gerenciar segmentos específicos com base em funções, permissões e rótulos;
   * Como administrador, você pode provisionar usuários em sua organização para ver apenas os segmentos rotulados com rótulos aos quais os usuários têm acesso e os segmentos que não contêm rótulos, ao usar a interface de segmentação.

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [[!DNL Segmentation Service] visão geral](../../segmentation/home.md).

### XDM

O Experience Data Model (XDM) é uma especificação de código aberto projetada para melhorar o poder das experiências digitais. Ele fornece estruturas e definições comuns para qualquer aplicativo se comunicar com os serviços na plataforma. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

Com o controle de acesso baseado em atributos, você pode:

* [Aplicar rótulos de uso de dados a grupos de campos e classes](../../xdm/tutorials/labels.md). Isso permite que vários esquemas com os mesmos grupos de campos ou classes tenham campos marcados com os mesmos atributos, dependendo das configurações no nível do grupo de campos ou da classe;
* Configure o acesso do usuário a campos de esquema XDM específicos, dependendo dos conjuntos de permissões aplicados às funções atribuídas aos usuários.

Para obter mais informações sobre o XDM, consulte o [Visão geral do XDM](../../xdm/home.md).