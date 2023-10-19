---
title: Excluir Registros
description: Saiba como excluir registros na interface do Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 8%

---

# [!BADGE Beta]{type=Informative} Excluir registros {#record-delete}

Use o [[!UICONTROL Ciclo de vida dos dados] espaço de trabalho](./overview.md) para excluir registros no Adobe Experience Platform com base em suas identidades principais. Esses registros podem ser vinculados a consumidores individuais ou a qualquer outra entidade incluída no gráfico de identidade.

>[!IMPORTANT]
> 
>O recurso de Exclusão de registro está atualmente na versão beta e só está disponível em um **versão limitada**. Não está disponível para todos os clientes. As solicitações de exclusão de registro só estão disponíveis para organizações na versão limitada.
> 
> 
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles são **não** a ser usado para solicitações de direitos do titular dos dados (conformidade) como relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) em vez disso.

## Pré-requisitos {#prerequisites}

A exclusão de registros requer um entendimento prático de como os campos de identidade funcionam no Experience Platform. Especificamente, você deve saber os valores de identidade principais das entidades cujos registros deseja excluir, dependendo do conjunto de dados (ou conjuntos de dados) do qual você está excluindo.

Consulte a seguinte documentação para obter mais informações sobre identidades na Platform:

* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): une as identidades em dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais estão em conformidade.
* [Namespaces de identidade](../../identity-service/namespaces.md): os namespaces de identidade definem os diferentes tipos de informações de identidade que podem se relacionar a uma única pessoa e são um componente obrigatório para cada campo de identidade.
* [Perfil do cliente em tempo real](../../profile/home.md): usa gráficos de identidade para fornecer perfis de consumidor unificados com base em dados agregados de várias fontes, atualizados em tempo quase real.
* [Experience Data Model (XDM)](../../xdm/home.md): fornece definições e estruturas padrão para dados da Platform por meio do uso de esquemas. Todos os conjuntos de dados da Platform estão em conformidade com um esquema XDM específico, e o esquema define quais campos são identidades.
* [Campos de identidade](../../xdm/ui/fields/identity.md): saiba como um campo de identidade é definido em um esquema XDM.

## Criar uma solicitação {#create-request}

Para iniciar o processo, selecione **[!UICONTROL Ciclo de vida dos dados]** na navegação à esquerda da interface do usuário da Platform. A variável [!UICONTROL Solicitações de ciclo de vida de dados] espaço de trabalho é exibido. Em seguida, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![A variável [!UICONTROL Solicitações de ciclo de vida de dados] espaço de trabalho com [!UICONTROL Criar solicitação] selecionado.](../images/ui/record-delete/create-request-button.png)

O workflow de criação da solicitação é exibido. Por padrão, a variável **[!UICONTROL Excluir registro]** estiver selecionada na caixa de diálogo **[!UICONTROL Ação solicitada]** seção. Deixe essa opção selecionada.

>[!IMPORTANT]
> 
>Como parte das alterações contínuas para melhorar a eficiência e reduzir o custo das operações do conjunto de dados, as organizações que foram movidas para o formato Delta podem excluir dados do Serviço de identidade, do Perfil do cliente em tempo real e do data lake. Esse tipo de usuário é chamado de delta-migrado. Os usuários de organizações que receberam a migração delta podem optar por excluir registros de um único conjunto de dados ou de todos eles. Os usuários de organizações que não foram migradas pelo delta não podem optar por excluir registros de um único conjunto de dados ou de todos os conjuntos de dados, como visto na imagem abaixo. Nesse caso, prossiga para o [fornecer identidades](#provide-identities) seção do guia.

![O fluxo de trabalho de criação da solicitação com o [!UICONTROL Excluir registro] selecionada e realçada.](../images/ui/record-delete/delete-record.png)

## Selecionar conjuntos de dados {#select-dataset}

A próxima etapa é determinar se você deseja excluir registros de um único conjunto de dados ou de todos os conjuntos de dados. Se esta opção não estiver disponível para você, continue para a [fornecer identidades](#provide-identities) seção do guia.

No **[!UICONTROL Detalhes do registro]** use o botão de opção para selecionar entre um conjunto de dados específico e todos os conjuntos de dados. Se você escolher **[!UICONTROL Selecionar conjunto de dados]**, prossiga para selecionar o ícone do banco de dados (![O ícone do banco de dados](../images/ui/record-delete/database-icon.png)) para abrir uma caixa de diálogo que fornece uma lista de conjuntos de dados disponíveis. Selecione o conjunto de dados desejado na lista seguida por **[!UICONTROL Concluído]**.

![A variável [!UICONTROL Selecionar conjunto de dados] com um conjunto de dados selecionado e [!UICONTROL Concluído] destacado.](../images/ui/record-delete/select-dataset.png)

Se desejar excluir registros de todos os conjuntos de dados, selecione **[!UICONTROL Todos os conjuntos de dados]**.

![A variável [!UICONTROL Selecionar conjunto de dados] com a [!UICONTROL Todos os conjuntos de dados] opção selecionada.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selecionar o **[!UICONTROL Todos os conjuntos de dados]** pode fazer com que a operação de exclusão demore mais e pode não resultar na exclusão precisa do registro.

## Fornecer identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identidade principal"
>abstract="Uma identidade principal é um atributo que vincula um registro ao perfil do consumidor na Experience Platform. O campo de identidade principal de um conjunto de dados é definido pelo esquema em que o conjunto de dados se baseia. Nessa coluna, você deve fornecer o tipo (ou namespace) da identidade principal do registro, como `email` para endereços de email e `ecid` para IDs da Experience Cloud. Para saber mais, consulte o manual da interface do ciclo de vida dos dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidade"
>abstract="Nessa coluna, você deve fornecer o valor da identidade principal do registro, que deve corresponder ao tipo de identidade fornecido na coluna esquerda. Se o tipo de identidade principal for `email`, o valor deve ser o endereço de email do registro. Para saber mais, consulte o manual da interface do ciclo de vida dos dados."

Ao excluir registros, você deve fornecer informações de identidade para que o sistema possa determinar quais registros devem ser excluídos. Para qualquer conjunto de dados na Plataforma, os registros são excluídos com base no **identidade principal** que é definido pelo esquema do conjunto de dados.

Como todos os campos de identidade na Platform, uma identidade primária é composta de duas coisas: uma **type** (às vezes chamado de namespace de identidade) e um **value**. O tipo de identidade fornece contexto sobre como o campo identifica um registro (como um endereço de email), e o valor representa a identidade específica de um registro para esse tipo (por exemplo, `jdoe@example.com` para o `email` tipo de identidade). Campos comuns usados como identidades incluem informações da conta, IDs do dispositivo e IDs de cookie.

>[!TIP]
>
>Se você não souber a identidade principal de um conjunto de dados específico, poderá encontrá-la na interface do usuário da plataforma. No **[!UICONTROL Conjuntos de dados]** selecione o conjunto de dados em questão na lista. Na página de detalhes do conjunto de dados, passe o mouse sobre o nome do esquema do conjunto de dados no painel direito. A identidade principal é exibida junto com o nome e a descrição do schema.
>
>![O painel Conjuntos de dados com um conjunto de dados selecionado e uma caixa de diálogo de esquema aberta no painel Detalhes do conjunto de dados. A ID primária do conjunto de dados é realçada.](../images/ui/record-delete/dataset-primary-identity.png)

Se você estiver excluindo registros de um único conjunto de dados, todas as identidades fornecidas deverão ser do mesmo tipo, já que um conjunto de dados só pode ter uma identidade principal. Se estiver excluindo de todos os conjuntos de dados, você poderá incluir vários tipos de identidade, pois conjuntos de dados diferentes podem ter identidades principais diferentes.

Há duas opções para fornecer identidades ao excluir registros:

* [Fazer upload de um arquivo JSON](#upload-json)
* [Inserir valores de identidade manualmente](#manual-identity)

### Fazer upload de um arquivo JSON {#upload-json}

Para fazer upload de um arquivo JSON, você pode arrastar e soltar o arquivo na área fornecida ou selecionar **[!UICONTROL Escolher arquivos]** para procurar e selecionar no diretório local.

![O fluxo de trabalho de criação da solicitação com a interface escolher arquivos e arrastar e soltar para fazer upload de arquivos JSON foi realçado.](../images/ui/record-delete/upload-json.png)

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
| `value` | O valor de identidade conforme indicado pelo tipo. |

Depois que o arquivo for carregado, você poderá continuar para [enviar a solicitação](#submit).

### Inserir identidades manualmente {#manual-identity}

Para inserir identidades manualmente, selecione **[!UICONTROL Adicionar identidade]**.

![O fluxo de trabalho de criação da solicitação com o [!UICONTROL Adicionar identidade] opção realçada.](../images/ui/record-delete/add-identity.png)

São exibidos controles que permitem inserir identidades, uma de cada vez. Em **[!UICONTROL Identidade principal]**, use o menu suspenso para selecionar o tipo de identidade. Em **[!UICONTROL Valor de identidade]**, fornecem o valor de identidade principal do registro.

![O fluxo de trabalho de criação da solicitação com um campo de identidade adicionado manualmente.](../images/ui/record-delete/identity-added.png)

Para adicionar mais identidades, selecione o ícone de adição (![Um ícone de adição.](../images/ui/record-delete/plus-icon.png)) ao lado de uma das linhas ou selecione **[!UICONTROL Adicionar identidade]**.

![O fluxo de trabalho de criação da solicitação com o ícone de adição e o ícone de adição de identidade é realçado.](../images/ui/record-delete/more-identities.png)

## Enviar a solicitação {#submit}

Quando terminar de adicionar identidades à solicitação, em **[!UICONTROL Configurações de solicitação]**, forneça um nome e uma descrição opcional para a solicitação antes de selecionar **[!UICONTROL Enviar]**.

>[!IMPORTANT]
> 
>Há diferentes limites para o número total de exclusões de registros de identidade únicos que podem ser enviadas a cada mês. Esses limites são baseados no seu contrato de licença. As organizações que compraram todas as edições do Adobe Real-time Customer Data Platform e do Adobe Journey Optimizer podem enviar até 100.000 exclusões de registro de identidade a cada mês. Organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe** O pode enviar até 600.000 exclusões de registros de identidade a cada mês.<br>Uma única solicitação de exclusão de registro por meio da interface do permite enviar 10.000 IDs de uma vez. A variável [Método de API para excluir registros](../api/workorder.md#create) O permite o envio de 100.000 IDs de uma só vez.<br>É uma prática recomendada enviar o máximo possível de IDs por solicitação, até o limite de ID. Quando você pretende excluir um grande volume de IDs, deve evitar o envio de um pequeno volume ou de uma única ID por solicitação de exclusão de registro.

![As configurações de solicitação do [!UICONTROL Nome] e [!UICONTROL Descrição] campos com [!UICONTROL Enviar] destacado.](../images/ui/record-delete/submit.png)

A [!UICONTROL Confirmar solicitação] aparece para indicar que as identidades não podem ser recuperadas após a exclusão. Selecionar **[!UICONTROL Enviar]** para confirmar a lista de identidades cujos dados você deseja excluir.

![A variável [!UICONTROL Confirmar solicitação] diálogo.](../images/ui/record-delete/confirm-request.png)

Depois que a solicitação é submetida, uma ordem de serviço é criada e é exibida no [!UICONTROL Gravar] guia do [!UICONTROL Ciclo de vida dos dados] espaço de trabalho. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
>
>Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#record-delete-transparency) para obter detalhes sobre como as exclusões de registro são processadas após serem executadas.

![A variável [!UICONTROL Gravar] guia do [!UICONTROL Ciclo de vida dos dados] espaço de trabalho com a nova solicitação realçada.](../images/ui/record-delete/request-log.png)

## Próximas etapas

Este documento abordou como excluir registros na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de gerenciamento do ciclo de vida dos dados na interface, consulte [Visão geral da interface do usuário do ciclo de vida dos dados](./overview.md).

Para saber como excluir registros usando a API de higiene de dados, consulte o [guia de ponto de extremidade de ordem de trabalho](../api/workorder.md).
