---
title: Visão geral da publicação
description: Saiba mais sobre o processo de publicação de alterações nas bibliotecas de código do gerenciamento de tags no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 83%

---

# Visão geral da publicação

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O Adobe Experience Platform permite encapsular alterações no código de gerenciamento de tags em bibliotecas individuais. Como várias bibliotecas agora podem ser desenvolvidas em paralelo por diferentes equipes, essas bibliotecas devem seguir um processo deliberado e permissionado para unir alterações antes de serem enviadas para o ambiente de produção.

Em um nível básico, cada biblioteca passa pelo seguinte processo de publicação:

1. Criação de uma nova biblioteca (ou edição de uma biblioteca existente) em um ambiente de desenvolvimento.
1. Teste da funcionalidade da biblioteca em um ambiente de preparo onde necessário.
1. Implantação da biblioteca no seu ambiente de produção.

Considere uma situação em que você cria um novo evento de “checkout”, cria um elemento de dados de receita relacionado a esse evento e faz uma alteração na configuração da extensão do Adobe Analytics para que se torne compatível com o novo evento e elemento de dados. É possível incluir todas essas alterações em uma nova biblioteca e usar o processo de publicação para testá-las, aprová-las e publicá-las como uma única unidade.

Para obter uma visão geral de alto nível do fluxo de trabalho de publicação da biblioteca, incluindo detalhes sobre como as bibliotecas herdam recursos de builds upstream dependendo de seu estado de publicação, consulte o [manual do fluxo de publicação](./publishing-flow.md).

Além do fluxo de publicação, é preciso compreender vários componentes e relacionamentos importantes para o desenvolvimento e publicação das suas bibliotecas com eficácia. A tabela a seguir descreve cada um desses conceitos importantes e fornece links para a documentação para ajudá-lo a saber mais sobre cada um deles:

| Componente | Descrição |
| --- | --- |
| Bibliotecas | Uma biblioteca é um conjunto de instruções sobre como as extensões, os elementos de dados e as regras interagem entre si e com o site. Quando uma biblioteca é compilada para ser implantada em um ambiente, essa biblioteca se torna uma build.<br><br>Consulte a visão geral sobre [bibliotecas](./libraries.md) para obter mais informações sobre como criar, gerenciar e ativar bibliotecas na interface do usuário. |
| Builds | Uma build é uma biblioteca compilada. Quando implantada em um ambiente, uma build fornece o conjunto de arquivos que de fato contém o código entregue ao navegador de cada usuário quando ele visualiza o site.<br><br>Consulte a visão geral das [builds](./builds.md) para obter mais informações sobre o conteúdo e o formato das builds. |
| Ambientes | Um ambiente de tag é um conjunto de instruções de implantação que informa o Platform em que formato você gostaria de criar e onde você gostaria que essa build fosse entregue.<br><br>Consulte a visão geral sobre [ambientes](./environments.md) para obter mais informações sobre os diferentes tipos de ambientes, como instalar e configurar ambientes existentes e como criar novos ambientes. |
| Hosts | Um host representa os detalhes da conexão de um ambiente para que ele forneça uma build ao seu site. Você pode optar por permitir que a Adobe gerencie a hospedagem da build ou, em vez disso, você pode fornecer as informações dos seus próprios servidores hosts.<br><br>Consulte a visão geral sobre [hosts](./hosts/hosts-overview.md) para obter mais informações sobre cada opção de hospedagem. |
| Código do lado do cliente | O código do lado do cliente é o conjunto de scripts que você insere no código-fonte do site ou aplicativo que informa a cada dispositivo cliente onde buscar a build. O código é anexado a um ambiente e pode ser alterado quando você fizer alterações na configuração do ambiente.<br><br>Consulte a seção sobre  [ ](./environments.md#embed-code) código incorporado na visão geral de ambientes para saber mais. |

## Próximas etapas

Este documento forneceu uma visão geral dos vários componentes envolvidos com as bibliotecas de tags de publicação no Adobe Experience Platform. Consulte a documentação referenciada neste manual para saber mais sobre o processo de publicação em detalhes.
