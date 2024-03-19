---
title: Usar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de destino
description: Saiba como usar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de destino para que apenas um subconjunto de usuários em sua organização obtenha acesso a fluxos de dados de destino específicos.
badgePrivateBeta: label="Beta privado" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---


# Usar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de destino

Como parte da [!UICONTROL Controle de acesso baseado em atributos] na Real-Time CDP, agora é possível aplicar rótulos de acesso aos fluxos de dados de destino. Dessa forma, é possível garantir que apenas um subconjunto de usuários em sua organização tenha acesso a fluxos de dados de destino específicos.

Ao adicionar um rótulo de acesso a um destino específico, somente os usuários com acesso a uma função atribuída a esse rótulo podem ver e editar esse fluxo de dados de destino. Se um fluxo de dados de destino não estiver marcado com rótulos, ele ficará visível para todos os usuários que pertencem à sua organização.

Leia esta página para entender casos de uso de exemplo, pré-requisitos antes de aplicar rótulos de acesso a fluxos de dados de destino e outras chamadas importantes ao usar essa funcionalidade.

## Pré-requisitos {#prerequisites}

Observe os seguintes pré-requisitos para concluir antes de começar a usar essa funcionalidade. Para se familiarizar com [!UICONTROL Controle de acesso baseado em atributos] A Adobe também recomenda que você leia os seguintes artigos:

* [Visão geral do controle de acesso baseado em atributos](/help/access-control/abac/overview.md)
* [Guia completo do controle de acesso baseado em atributos](/help/access-control/abac/end-to-end-guide.md)

### Acesso à interface de permissões {#access-permissions-ui}

[!UICONTROL Permissões] é a área do Experience Cloud em que os administradores podem definir funções e políticas de usuário para gerenciar permissões de recursos e objetos em um aplicativo de produto do. Leia o [seção de permissões](/help/access-control/abac/end-to-end-guide.md#permissions) para começar.

### Criar funções, rótulos e atribuir usuários {#create-roles-labels-assign-users}

Após obter acesso à [!UICONTROL permissões] Você ou um membro de sua equipe deve configurar funções e adicionar os rótulos necessários a essas funções. Finalmente, os usuários que devem acessar recursos rotulados com os rótulos específicos devem ser adicionados à função. Consulte as seguintes seções de documentação:

* [Criar uma nova função](/help/access-control/abac/ui/roles.md)
* [Adicionar rótulos a uma função](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Adicionar usuários a uma função](/help/access-control/ui/users.md)

### Criar fluxos de dados de destino {#create-dataflow}

Primeiro, é necessário conectar-se ao destino desejado e criar um fluxo de dados para exportar dados, antes de aplicar rótulos de acesso ao fluxo de dados.

Leia as guias na [conexão com um destino](/help/destinations/ui/connect-destination.md) e [ativação de dados no destino](/help/destinations/ui/activation-overview.md). Em seguida, selecione o destino desejado na [catálogo de conectores disponíveis](/help/destinations/catalog/overview.md).

## Já disponível: aplicar rótulos de acesso a outros recursos de Experience Platform {#apply-labels-other-resources}

Embora esta versão permita conceder aos usuários acesso no nível do objeto a fluxos de dados de destino específicos, a funcionalidade para conceder controle de acesso em um nível de objeto já está geralmente disponível para outros recursos de Experience Platform, como [públicos](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Exemplo de caso de uso {#use-case-example}

Com o controle de acesso no nível do objeto para destinos, limite equipes específicas de profissionais de marketing para obter acesso somente aos destinos específicos. Por exemplo, se sua organização tiver dados de clientes em várias localizações geográficas, como os Estados Unidos e o Reino Unido, você poderá limitar uma equipe de marketing para exibir e editar os fluxos de dados somente para a localização dos EUA, e outra equipe de marketing para exibir e editar os fluxos de dados da localização do Reino Unido.

## Aplicar rótulos de acesso aos fluxos de dados de destino {#apply-labels-to-destination-dataflow}

Para aplicar rótulos de acesso a um fluxo de dados específico:

1. Navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e localize o fluxo de dados de destino ao qual você deseja limitar o acesso dos usuários.
1. Selecione as reticências (`...`) no [!UICONTROL Nome] e use o ![Editar controle de detalhes](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL Aplicar rótulos de acesso]** controle para adicionar novos rótulos e gerenciar os rótulos existentes para o fluxo de dados.
   ![Selecione Aplicar rótulos de acesso na exibição Procurar do espaço de trabalho de destinos.](/help/access-control/images/olac/apply-access-labels.png)
1. Selecione os rótulos que deseja adicionar ao fluxo de dados de destino e selecione **[!UICONTROL Salvar]**.
   ![Selecione os rótulos de acesso no que devem se aplicar ao fluxo de dados de destino.](/help/access-control/images/olac/view-access-labels.png)
1. Observe como o fluxo de dados agora tem um rótulo de acesso exibido na interface.
   ![Exibir vários fluxos de dados de destino com o fluxo de dados selecionado como exibir um rótulo de acesso.](/help/access-control/images/olac/dataflow-with-access-label.png)

Se um fluxo de dados de destino não estiver marcado com rótulos, ele será exibido para todos os usuários. Se o fluxo de dados for marcado com um ou mais rótulos de acesso, ele só será exibido para usuários pertencentes a uma função que tenha o mesmo rótulo ou combinação de rótulos.

Você pode adicionar rótulos padrão e personalizados aos fluxos de dados de destino. Depois de adicionar um rótulo aos fluxos de dados de destino:

* Os usuários atribuídos a funções com acesso ao mesmo rótulo podem exibir o fluxo de dados com o novo rótulo na interface. Eles podem exibir e editar o fluxo de dados de destino na interface do usuário ou por meio de APIs.

* Usuários que são *não* atribuídos a funções com acesso ao mesmo rótulo não têm acesso ao fluxo de dados de destino para exibi-lo ou editá-lo na interface do usuário ou por meio de APIs.

## Chamadas e itens importantes a saber {#important-callouts}

Atualmente, os rótulos de acesso só podem ser aplicados a fluxos de dados existentes. Isso significa que alguém precisa criar o fluxo de dados para o destino antes que os rótulos de acesso possam ser aplicados.

Não é possível aplicar um rótulo de acesso a um fluxo de dados de destino se você não tiver acesso a esse rótulo.

Ao adicionar vários rótulos a um fluxo de dados de destino, os usuários que devem poder visualizar e editar o fluxo de dados devem ser adicionados a uma função com pelo menos a mesma combinação de rótulos. Por exemplo, se você aplicar os rótulos C1, I2 e outro rótulo personalizado a um fluxo de dados de destino, somente os usuários adicionados às funções com acesso à combinação desses três rótulos poderão exibir e editar esse fluxo de dados de destino específico.

![Diagrama de Venn mostrando como somente determinados usuários têm acesso a destinos com vários rótulos aplicados.](/help/access-control/images/olac/multiple-labels-venn.png)

## Próximas etapas {#next-steps}

Seguindo as etapas deste documento, agora você sabe como aplicar rótulos de acesso a fluxos de dados de destino para que somente um subconjunto de usuários em sua organização tenha acesso a fluxos de dados de destino específicos.

Em seguida, você pode ler mais sobre outras funcionalidades compatíveis com o [!UICONTROL Controle de acesso baseado em atributos] ao ativar dados para destinos. Por exemplo, é possível limitar o acesso dos usuários a [exibir e ativar somente campos específicos](/help/access-control/abac/overview.md#destinations).