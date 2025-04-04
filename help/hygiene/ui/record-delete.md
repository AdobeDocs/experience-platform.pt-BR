---
title: Excluir Registros
description: Saiba como excluir registros na interface do Adobe Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 8%

---

# Excluir registros {#record-delete}

Use o [[!UICONTROL espaço de trabalho do Ciclo de Vida de Dados]](./overview.md) para excluir registros no Adobe Experience Platform com base em suas identidades primárias. Esses registros podem ser vinculados a consumidores individuais ou a qualquer outra entidade incluída no gráfico de identidade.

>[!IMPORTANT]
> 
>O recurso de Exclusão de Registro está atualmente no Beta e só está disponível em uma **versão limitada**. Não está disponível para todos os clientes. As solicitações de exclusão de registro só estão disponíveis para organizações na versão limitada.
> 
> 
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles **não** devem ser usados para solicitações de direitos do titular dos dados (conformidade) relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use o [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Pré-requisitos {#prerequisites}

A exclusão de registros requer um entendimento prático de como os campos de identidade funcionam no Experience Platform. Especificamente, você deve conhecer os valores de namespace de identidade das entidades cujos registros deseja excluir, dependendo do conjunto de dados (ou conjuntos de dados) do qual você está excluindo.

Consulte a seguinte documentação para obter mais informações sobre identidades no Experience Platform:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): une identidades em dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais estão em conformidade.
* [Namespaces de identidade](../../identity-service/features/namespaces.md): os namespaces de identidade definem os diferentes tipos de informações de identidade que podem se relacionar a uma única pessoa e são um componente necessário para cada campo de identidade.
* [Perfil do cliente em tempo real](../../profile/home.md): usa gráficos de identidade para fornecer perfis de consumidor unificados com base em dados agregados de várias fontes, atualizados em tempo quase real.
* [Experience Data Model (XDM)](../../xdm/home.md): fornece definições e estruturas padrão para dados do Experience Platform por meio do uso de esquemas. Todos os conjuntos de dados do Experience Platform estão em conformidade com um esquema XDM específico, e o esquema define quais campos são identidades.
* [Campos de identidade](../../xdm/ui/fields/identity.md): saiba como um campo de identidade é definido em um esquema XDM.

## Criar uma solicitação {#create-request}

Para iniciar o processo, selecione **[!UICONTROL Ciclo de Vida dos Dados]** na navegação à esquerda da interface do Experience Platform. O espaço de trabalho [!UICONTROL Solicitações do ciclo de vida dos dados] é exibido. Em seguida, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![O espaço de trabalho [!UICONTROL Solicitações do ciclo de vida dos dados] com [!UICONTROL Solicitação de criação] selecionada.](../images/ui/record-delete/create-request-button.png)

O workflow de criação da solicitação é exibido. Por padrão, a opção **[!UICONTROL Excluir registro]** está selecionada na seção **[!UICONTROL Ação solicitada]**. Deixe essa opção selecionada.

>[!IMPORTANT]
> 
>Para melhorar a eficiência e tornar as operações do conjunto de dados mais baratas, as organizações que foram movidas para o formato Delta podem excluir dados do Serviço de identidade, do Perfil do cliente em tempo real e do data lake. Esse tipo de usuário é chamado de delta-migrado. Os usuários de organizações que receberam a migração delta podem optar por excluir registros de um único conjunto de dados ou de todos eles. Os usuários de organizações que não passaram pela migração delta não podem excluir seletivamente registros de um único conjunto de dados ou de todos os conjuntos de dados, conforme mostrado na imagem abaixo. Nesse caso, continue para a seção [Fornecer identidades](#provide-identities) do guia.

![O fluxo de trabalho de criação da solicitação com a opção [!UICONTROL Excluir registro] foi selecionado e realçado.](../images/ui/record-delete/delete-record.png)

## Selecionar conjuntos de dados {#select-dataset}

A próxima etapa é determinar se você deseja excluir registros de um único conjunto de dados ou de todos os conjuntos de dados. Se esta opção não estiver disponível para você, continue na seção [Fornecer identidades](#provide-identities) do guia.

Na seção **[!UICONTROL Detalhes do registro]**, use o botão de opção para selecionar entre um conjunto de dados específico e todos os conjuntos de dados. Se você escolher **[!UICONTROL Selecionar conjunto de dados]**, prossiga para selecionar o ícone do banco de dados (![O ícone do banco de dados](/help/images/icons/database.png)) para abrir uma caixa de diálogo que fornece uma lista de conjuntos de dados disponíveis. Selecione o conjunto de dados desejado na lista, seguido por **[!UICONTROL Concluído]**.

![A caixa de diálogo [!UICONTROL Selecionar conjunto de dados] com um conjunto de dados selecionado e [!UICONTROL Concluído] realçado.](../images/ui/record-delete/select-dataset.png)

Para excluir registros de todos os conjuntos de dados, selecione **[!UICONTROL Todos os conjuntos de dados]**.

![A caixa de diálogo [!UICONTROL Selecionar conjunto de dados] com a opção [!UICONTROL Todos os conjuntos de dados] selecionada.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selecionar a opção **[!UICONTROL Todos os conjuntos de dados]** pode fazer com que a operação de exclusão demore mais e não resulte na exclusão precisa do registro.

## Fornecer identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Namespace de identidade"
>abstract="Um namespace de identidade é um atributo que vincula um registro ao perfil de consumidor na Experience Platform. O campo de namespace de identidade de um conjunto de dados é definido pelo esquema em que o conjunto de dados se baseia. Nessa coluna, é necessário fornecer o tipo (ou namespace) para namespace da identidade do registro, como `email` para endereços de email e `ecid` para IDs da Experience Cloud. Para saber mais, consulte o guia da interface do ciclo de vida dos dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidade principal"
>abstract="Nessa coluna, é necessário fornecer o valor do namespace de identidade do registro, que deve corresponder ao tipo de identidade fornecido na coluna esquerda. Se o tipo de namespace de identidade for `email`, o valor deverá ser o endereço de email do registro. Para saber mais, consulte o guia da interface do ciclo de vida dos dados."

Ao excluir registros, você deve fornecer informações de identidade para que o sistema possa determinar quais registros devem ser excluídos. Para qualquer conjunto de dados no Experience Platform, os registros são excluídos com base no campo **namespace de identidade** definido pelo esquema do conjunto de dados.

Como todos os campos de identidade no Experience Platform, um namespace de identidade é composto de dois itens: um **tipo** (às vezes chamado de namespace de identidade) e um **valor**. O tipo de identidade fornece contexto sobre como o campo identifica um registro (como um endereço de email). O valor representa a identidade específica de um registro para esse tipo (por exemplo, `jdoe@example.com` para o tipo de identidade `email`). Campos comuns usados como identidades incluem informações da conta, IDs do dispositivo e IDs de cookie.

>[!TIP]
>
>Se você não souber o namespace de identidade de um conjunto de dados específico, poderá encontrá-lo na interface do usuário do Experience Platform. No espaço de trabalho **[!UICONTROL Conjuntos de Dados]**, selecione o conjunto de dados em questão na lista. Na página de detalhes do conjunto de dados, passe o mouse sobre o nome do esquema do conjunto de dados no painel direito. O namespace de identidade é exibido junto com o nome e a descrição do esquema.
>
>![O painel Conjuntos de Dados com um conjunto de dados selecionado e uma caixa de diálogo de esquema aberta no painel de detalhes do conjunto de dados. A ID primária do conjunto de dados está realçada.](../images/ui/record-delete/dataset-primary-identity.png)

Se você estiver excluindo registros de um único conjunto de dados, todas as identidades fornecidas deverão ter o mesmo tipo, já que um conjunto de dados só pode ter um namespace de identidade. Se estiver excluindo de todos os conjuntos de dados, você poderá incluir vários tipos de identidade, pois conjuntos de dados diferentes podem ter identidades principais diferentes.

Há duas opções para fornecer identidades ao excluir registros:

* [Fazer upload de um arquivo JSON](#upload-json)
* [Inserir valores de identidade primários manualmente](#manual-identity)

### Fazer upload de um arquivo JSON {#upload-json}

Para carregar um arquivo JSON, você pode arrastar e soltar o arquivo na área fornecida ou selecionar **[!UICONTROL Escolher arquivos]** para procurar e selecionar no diretório local.

![O fluxo de trabalho de criação da solicitação com a interface escolher arquivos e arrastar e soltar para carregar arquivos JSON foi realçado.](../images/ui/record-delete/upload-json.png)

O arquivo JSON deve ser formatado como uma matriz de objetos, cada objeto representando uma identidade.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Propriedade | Descrição |
| --- | --- |
| `namespaceCode` | O tipo de identidade. |
| `value` | O valor de identidade principal conforme indicado pelo tipo. |

Depois que o arquivo for carregado, você poderá continuar a [enviar a solicitação](#submit).

### Inserir identidades manualmente {#manual-identity}

Para inserir identidades manualmente, selecione **[!UICONTROL Adicionar identidade]**.

![O fluxo de trabalho de criação da solicitação com a opção [!UICONTROL Adicionar identidade] foi realçado.](../images/ui/record-delete/add-identity.png)

São exibidos controles que permitem inserir identidades, uma de cada vez. Em **[!UICONTROL namespace de identidade]**, use o menu suspenso para selecionar o tipo de identidade. Em **[!UICONTROL Valor de Identidade Principal]**, forneça o valor do namespace de identidade para o registro.

![O fluxo de trabalho de criação da solicitação com um campo de identidade adicionado manualmente.](../images/ui/record-delete/identity-added.png)

Para adicionar mais identidades, selecione o ícone de adição (![A ícone de adição.](/help/images/icons/tree-expand-all.png)) ao lado de uma das linhas ou selecione **[!UICONTROL Adicionar identidade]**.

![Fluxo de trabalho de criação de solicitação com o ícone de adição e o ícone de adição de identidade realçados.](../images/ui/record-delete/more-identities.png)

## Enviar a solicitação {#submit}

Quando terminar de adicionar identidades à solicitação, em **[!UICONTROL Configurações da solicitação]**, forneça um nome e uma descrição opcional para a solicitação antes de selecionar **[!UICONTROL Enviar]**.

>[!IMPORTANT]
> 
>Há diferentes limites para o número total de exclusões de registros de identidade únicos que podem ser enviadas a cada mês. Esses limites são baseados no seu contrato de licença. As organizações que compraram todas as edições do Adobe Real-Time Customer Data Platform ou do Adobe Journey Optimizer podem enviar até 100.000 exclusões de registro de identidade a cada mês. As organizações que compraram o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield** podem enviar até 600.000 exclusões de registros de identidade a cada mês.<br>Uma única solicitação de exclusão de registro por meio da interface do usuário permite enviar 10.000 IDs de uma vez. O [método de API para excluir registros](../api/workorder.md#create) permite o envio de 100.000 IDs de uma vez.<br>É prática recomendada enviar o máximo possível de IDs por solicitação, até o limite de ID. Quando você pretende excluir um grande volume de IDs, deve evitar o envio de um pequeno volume ou de uma única ID por solicitação de exclusão de registro.

![Campos de [!UICONTROL Nome] e [!UICONTROL Descrição] da configuração de solicitação com [!UICONTROL Envio] realçados.](../images/ui/record-delete/submit.png)

Uma caixa de diálogo [!UICONTROL Confirmar solicitação] aparece para indicar que as identidades não podem ser recuperadas após serem excluídas. Selecione **[!UICONTROL Enviar]** para confirmar a lista de identidades cujos dados você deseja excluir.

![A caixa de diálogo [!UICONTROL Confirmar solicitação].](../images/ui/record-delete/confirm-request.png)

Depois que a solicitação for enviada, uma ordem de serviço será criada e exibida na guia [!UICONTROL Registro] do espaço de trabalho [!UICONTROL Ciclo de vida dos dados]. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
>
>Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#record-delete-transparency) para obter detalhes sobre como as exclusões de registros são processadas após a execução.

![A guia [!UICONTROL Registro] do espaço de trabalho [!UICONTROL Ciclo de Vida dos Dados] com a nova solicitação realçada.](../images/ui/record-delete/request-log.png)

## Próximas etapas

Este documento abordou como excluir registros na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de gerenciamento do ciclo de vida dos dados na interface, consulte a [visão geral da interface do ciclo de vida dos dados](./overview.md).

Para saber como excluir registros usando a API de Limpeza de Dados, consulte o [manual de ponto de extremidade de ordem de trabalho](../api/workorder.md).
