---
title: Fluxo de publicação
description: Saiba mais sobre o processo de criação de bibliotecas, o teste de builds e a aprovação deles para produção no Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 2d71eafb00098d958c8cff9350caa27bd3f0260d
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 84%

---

# Fluxo de publicação {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Fluxo de publicação"
>abstract="Entenda os níveis de permissões de usuário necessários para o fluxo de publicação, incluindo os direitos de Desenvolver, Aprovar e Publicar."

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O fluxo de publicação de tags na Adobe Experience Platform se refere ao processo de criação de bibliotecas, ao teste de builds e à aprovação deles para produção.

As ações disponíveis que você pode realizar em uma biblioteca dependem do estado da biblioteca e do nível de permissão que você possui. Além disso, o estado de uma biblioteca também afeta os recursos que ela contém (regras, elementos de dados e extensões) dependendo do que está upstream no fluxo de publicação.

As seções abaixo abordam os detalhes sobre as permissões, o estado da biblioteca e o upstream, pois fazem parte do fluxo de publicação.

## Permissões {#permissions}

Há diferentes níveis de permissões de usuário importantes para o fluxo de publicação; especificamente, os direitos das propriedades [!UICONTROL Develop], [!UICONTROL Approve] e [!UICONTROL Publish]:

* **[!UICONTROL Develop]**: inclui a capacidade de criação de bibliotecas, de criação de builds para a fase de desenvolvimento e de envio para aprovação.
* **[!UICONTROL Approve]**: inclui a capacidade de criação de builds para a fase de preparo e aprovação de builds preparadas.
* **[!UICONTROL Publish]**: inclui a capacidade de publicar uma biblioteca aprovada.

Os direitos não são inclusivos. Para uma única pessoa executar o fluxo de trabalho desde o início até o fim, essa pessoa deve receber os três direitos em uma propriedade específica.

Consulte o [manual de permissões do usuário](../administration/user-permissions.md) para obter mais informações sobre o gerenciamento de permissões para tags.

## Estado da biblioteca {#state}

Quando se trata do fluxo de publicação, uma biblioteca pode estar em quatro estados básicos:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Esses quatro estados são representados como colunas na guia **[!UICONTROL Publishing Flow]**.

![](./images/approval-workflow/flow-ui.png)

É necessário realizar ações específicas para mover uma biblioteca entre esses estados. O diagrama a seguir descreve cada ação que faz uma biblioteca variar de estado:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Quando novas bibliotecas são criadas, elas começam no estado [!UICONTROL Development]. Qualquer alteração em uma biblioteca deve ser feita enquanto ela estiver no estado [!UICONTROL Development]. Quando as fases de desenvolvimento e teste forem concluídas, a biblioteca poderá ser enviada para aprovação.

A tabela a seguir descreve as ações disponíveis para uma biblioteca no estado [!UICONTROL Development]:

| Ação | Descrição |
| --- | --- |
| [!UICONTROL Edit] | Use a tela [!UICONTROL Edit Library] para adicionar ou remover componentes de uma biblioteca. |
| [!UICONTROL Build to Development] | Crie uma build para a biblioteca. A build será compilada e implantada no ambiente ao qual a biblioteca está atribuída. Essa etapa falhará se a biblioteca não tiver sido atribuída a um ambiente ou se contiver uma alteração que já esteja definida no upstream. |
| [!UICONTROL Submit for Approval] | Cancele a atribuição da biblioteca para o ambiente de desenvolvimento e mova a biblioteca para a coluna [!UICONTROL Submitted] para um usuário com permissões de aprovação poder trabalhar nela. A última criação da biblioteca deve ter sido bem-sucedida para que essa opção seja habilitada. |
| [!UICONTROL Submit & Build to Staging] | Isso só pode ser executado por um usuário com os direitos de Desenvolver e Aprovar. Essa ação desatribui a biblioteca do ambiente de desenvolvimento, move a biblioteca para o estado [!UICONTROL Submitted] e cria a biblioteca para o ambiente de preparo. A última criação da biblioteca deve ter sido bem-sucedida para que essa opção seja habilitada. |
| [!UICONTROL Approve for Publishing] | Isso só pode ser executado por um usuário com os direitos de Desenvolver e Aprovar. Essa ação desatribui a biblioteca do ambiente de desenvolvimento e a move para o estado [!UICONTROL Approved], ignorando completamente o ambiente de preparo e o estado [!UICONTROL Submitted]. A última criação da biblioteca deve ter sido bem-sucedida para que essa opção seja habilitada. |
| [!UICONTROL Approve & Publish to Production] | Isso só pode ser executado por um usuário com os direitos de Desenvolver, Aprovar e Publicar. Essa ação desatribui a biblioteca do ambiente de desenvolvimento, move a mesma para o estado [!UICONTROL Approved] e publica para a produção. Após a conclusão da compilação de produção, a biblioteca será movida para o estado [!UICONTROL Published]. A última criação da biblioteca deve ter sido bem-sucedida para que essa opção seja habilitada. |
| [!UICONTROL Delete] | Remova a biblioteca do sistema. Essa ação não removerá a build do ambiente. |

### [!UICONTROL Submitted] {#submitted}

Quando uma biblioteca está no estado [!UICONTROL Submitted], um usuário com permissões de aprovação pode testar a biblioteca no ambiente de preparo. Quando o teste for concluído, a biblioteca será aprovada ou rejeitada. As builds rejeitadas retornam para [!UICONTROL Development] para que alterações adicionais possam ser feitas antes de o fluxo de publicação ser reiniciado.

A tabela a seguir descreve as ações disponíveis para uma biblioteca no estado [!UICONTROL Submitted]:

| Ação | Descrição |
| --- | --- |
| [!UICONTROL Open] | Visualize o conteúdo da biblioteca. Não são permitidas alterações em bibliotecas fora da coluna [!UICONTROL Development]. Se forem necessárias alterações, a biblioteca deverá ser rejeitada para que as alterações possam ser feitas em [!UICONTROL Development]. |
| [!UICONTROL Build for Staging] | Crie a biblioteca no ambiente de preparo para implantação. |
| [!UICONTROL Approve for Publishing] | Mova a biblioteca para a coluna [!UICONTROL Approved] para que um usuário com permissões de publicação trabalhe nela. |
| [!UICONTROL Approve & Publish to Production] | Isso só pode ser executado por um usuário com direitos de Aprovar e Publicar. Essa ação desatribui a biblioteca do ambiente de preparo, move a mesma para o estado [!UICONTROL Approved] e publica para a produção. Após a conclusão da compilação de produção, a biblioteca será movida para o estado [!UICONTROL Published]. Isso pode ser executado com ou sem um build bem-sucedido no ambiente de preparo. |
| [!UICONTROL Reject] | Cancele a atribuição da biblioteca para o ambiente de preparo e mova-a de volta para a coluna [!UICONTROL Development] para fazer mais alterações. |

### [!UICONTROL Approved] {#approved}

Depois que uma biblioteca é aprovada, um usuário com permissões de publicação pode publicar ou rejeitar a biblioteca. As builds rejeitadas retornam para [!UICONTROL Development] para que mais alterações possam ser feitas antes de o fluxo de publicação recomeçar.

A tabela a seguir descreve as ações disponíveis para uma biblioteca no estado [!UICONTROL Approved]:

| Ação | Descrição |
| --- | --- |
| [!UICONTROL Open] | Visualize o conteúdo da biblioteca. Não são permitidas alterações em bibliotecas fora da coluna [!UICONTROL Development]. Se forem necessárias alterações, a biblioteca deverá ser rejeitada para que as alterações possam ser feitas em [!UICONTROL Development]. |
| [!UICONTROL Build and Publish to Production] | Desfaça a atribuição da biblioteca para o ambiente de preparo, atribua a biblioteca ao ambiente de produção e implante-a.<br><br>**Importante**: quando essa opção é selecionada, sua biblioteca fica ativa no ambiente de produção. Verifique se a biblioteca contém as alterações desejadas antes de selecionar essa opção. |
| [!UICONTROL Reject] | Desfaça a atribuição da biblioteca para o ambiente de preparo e mova a biblioteca para a coluna [!UICONTROL Development] para fazer mais alterações. |

### [!UICONTROL Published] {#published}

A coluna [!UICONTROL Published] mostra quais bibliotecas foram publicadas e quais foram as datas de publicação. No momento da publicação, a biblioteca será exibida ao lado de um ponto verde. A menos que você tenha realizado uma republicação em uma biblioteca anterior, essa sempre será a biblioteca na parte superior da coluna.

| Ação | Descrição |
| --- | --- |
| [!UICONTROL Open] | Visualize o conteúdo da biblioteca. Não são permitidas alterações em bibliotecas fora da coluna [!UICONTROL Development]. Se você quiser alterar o que está em seu ambiente de produção, crie uma nova biblioteca e a faça passar pelo processo de publicação completo. |
| [!UICONTROL Republish] | Essa ação só estará disponível nas cinco bibliotecas publicadas mais recentemente e somente se o ambiente de produção for (A) configurado com a opção Arquivar desativada e (B) usar um host [!UICONTROL Managed by Adobe] no momento da compilação. |
| [!UICONTROL Download] | Essa ação só estará disponível nas cinco bibliotecas publicadas mais recentemente e somente se o ambiente de produção for (A) configurado com a opção Arquivar ativada e (B) usar um host [!UICONTROL Managed by Adobe] no momento da compilação. |

## Upstream {#upstream}

Depois de publicar sua primeira biblioteca, é importante entender a função do upstream à medida que você faz as bibliotecas mais recentes passarem pelo fluxo de publicação.

Se uma biblioteca estiver atualmente nos estágios [!UICONTROL Development], [!UICONTROL Submitted] ou [!UICONTROL Approved], essa biblioteca herdará as regras, os elementos de dados e as extensões de quaisquer bibliotecas que estejam no upstream. Esses recursos herdados são uma “linha de base” para as bibliotecas à medida que passam pelo fluxo de publicação. Basicamente, você pode pensar em cada nova biblioteca como uma série de alterações na linha de base estabelecida pelo upstream. Isso garante que nada seja substituído inesperadamente de uma biblioteca anterior quando uma nova iteração for publicada.

O que está incluído no upstream depende do estágio atual da biblioteca. Por exemplo, as bibliotecas na coluna [!UICONTROL Approved] apenas herdam recursos da biblioteca [!UICONTROL Published], enquanto as bibliotecas em [!UICONTROL Development] herdam recursos de todas as outras colunas.

![](./images/approval-workflow/upstream.png)

Ao editar uma biblioteca na interface, todos os recursos herdados do upstream são representados na seção **[!UICONTROL Resources Upstream]**. Para visualizar esses recursos, selecione a guia de expansão abaixo do cabeçalho da seção.

![](./images/approval-workflow/upstream-collapse.png)

A seção é expandida para mostrar os recursos individuais herdados do upstream. Você pode usar o painel esquerdo para filtrar por [!UICONTROL Rules], [!UICONTROL Data Elements] e [!UICONTROL Extensions] ou usar a barra de pesquisa para procurar um recurso específico por nome.

![](./images/approval-workflow/upstream-resources.png)

## Próximas etapas

Este manual fornece uma visão geral de alto nível do fluxo de publicação de bibliotecas na Adobe Experience Platform. Para saber mais sobre como publicar suas bibliotecas, consulte a [visão geral de publicação](./overview.md).
