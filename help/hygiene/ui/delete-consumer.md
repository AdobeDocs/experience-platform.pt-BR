---
title: Excluir registros do consumidor
description: Saiba como excluir registros do consumidor na interface do usuário do Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: 95d75292b7697ef4f98e3ebd34c04724019ac37f
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 0%

---

# Excluir registros do consumidor

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Shield for Healthcare.

O [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do usuário do Adobe Experience Platform permite excluir registros do consumidor que estão participando do Serviço de identidade e do Perfil do cliente em tempo real.

## Pré-requisitos

A exclusão de registros do consumidor requer uma compreensão funcional de como os campos de identidade funcionam no Experience Platform. Especificamente, você deve saber os principais valores de identidade dos consumidores cujos registros deseja excluir, dependendo do conjunto de dados (ou conjuntos de dados) do qual você os está excluindo.

Consulte a seguinte documentação para obter mais informações sobre identidades na Platform:

* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais eles estão em conformidade.
   * [Namespaces de identidade](../../identity-service/namespaces.md): Os namespaces de identidade definem os diferentes tipos de informações de identidade que podem estar relacionadas a uma única pessoa e são um componente obrigatório para cada campo de identidade.
* [Perfil do cliente em tempo real](../../profile/home.md): Usa gráficos de identidade do consumidor para fornecer perfis unificados do consumidor com base em dados agregados de várias fontes, atualizados em tempo quase real.
* [Experience Data Model (XDM)](../../xdm/home.md): Fornece definições e estruturas padrão para dados da plataforma por meio do uso de esquemas. Todos os conjuntos de dados da Platform estão em conformidade com um esquema XDM específico e o esquema define quais campos são identidades.
   * [Campos de identidade](../../xdm/ui/fields/identity.md): Saiba como um campo de identidade é definido em um esquema XDM.

## Criar uma nova solicitação

Para iniciar o processo, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![Imagem que mostra o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/delete-consumer/create-request-button.png)

A caixa de diálogo de criação da solicitação é exibida. Por padrão, a variável **[!UICONTROL Consumidor]** está selecionada sob a variável **[!UICONTROL Ação]** seção. Deixe essa opção selecionada.

![Imagem mostrando a opção consumidor selecionada na caixa de diálogo de criação](../images/ui/delete-consumer/consumer-action.png)

## Selecionar conjuntos de dados

Em **[!UICONTROL Detalhes do consumidor]** , a próxima etapa é determinar se deseja excluir dados do consumidor de um único conjunto de dados ou de todos os conjuntos de dados.

Se você escolher **[!UICONTROL Selecionar conjunto de dados]**, selecione o ícone do banco de dados (![Imagem do ícone do banco de dados](../images/ui/delete-consumer/database-icon.png)) e uma caixa de diálogo é exibida permitindo selecionar o conjunto de dados desejado na lista.

![Imagem que mostra a caixa de diálogo de seleção do conjunto de dados](../images/ui/delete-consumer/select-dataset.png)

Se desejar excluir dados do consumidor de todos os conjuntos de dados, selecione **[!UICONTROL Todos os conjuntos de dados]**.

![Imagem que mostra o [!UICONTROL Todos os conjuntos de dados] opção selecionada](../images/ui/delete-consumer/all-datasets.png)

>[!NOTE]
>
>Selecionar o **[!UICONTROL Todos os conjuntos de dados]** A opção pode fazer com que a operação de exclusão demore mais e pode não resultar em uma exclusão de registro precisa.

## Fornecer identidades do consumidor {#provide-consumer-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identidade primária"
>abstract="Uma identidade primária é um atributo que vincula um registro ao perfil do consumidor no Experience Platform. O campo de identidade principal de um conjunto de dados é definido pelo esquema em que o conjunto de dados se baseia. Nesta coluna, você deve fornecer o tipo (ou namespace) da identidade primária do consumidor, como &quot;email&quot; para endereços de email e &quot;ecid&quot; para IDs de Experience Cloud. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidade"
>abstract="Nesta coluna, você deve fornecer o valor da identidade primária do consumidor, que deve corresponder ao tipo de identidade fornecido na coluna esquerda. Se o tipo de identidade principal for &quot;email&quot;, o valor deve ser o endereço de email do consumidor. Para saber mais, consulte o guia da interface do usuário de higiene de dados."

Ao excluir dados do consumidor, você deve fornecer informações de identidade para que o sistema possa determinar quais registros devem ser excluídos. Para qualquer conjunto de dados na Platform, os registros são excluídos com base na variável **identidade primária** que é definido pelo esquema do conjunto de dados.

Como todos os campos de identidade na Platform, uma identidade primária é composta de duas coisas: a **type** (às vezes chamado de namespace de identidade) e um **value**. O tipo de identidade fornece contexto sobre como o campo identifica um consumidor (como um endereço de email), e o valor representa a identidade específica de um consumidor para esse tipo (por exemplo, `jdoe@example.com` para `email` tipo de identidade).  Campos comuns usados como identidades incluem informações de conta, IDs de dispositivo e IDs de cookie.

>[!TIP]
>
>Se você não souber a identidade primária de um conjunto de dados específico, poderá encontrá-la na interface do usuário da plataforma. No **[!UICONTROL Conjuntos de dados]** no espaço de trabalho, selecione o conjunto de dados em questão na lista. Na página de detalhes do conjunto de dados, passe o mouse sobre o nome do esquema do conjunto de dados no painel direito. A identidade primária é exibida junto com o nome e a descrição do schema.
>
>![Imagem que mostra a identidade primária de um conjunto de dados destacado na interface do usuário](../images/ui/delete-consumer/dataset-primary-identity.png)

Se você estiver excluindo registros do consumidor de um único conjunto de dados, todas as identidades fornecidas deverão ter o mesmo tipo, já que um conjunto de dados só poderá ter uma identidade primária. Se estiver excluindo de todos os conjuntos de dados, é possível incluir vários tipos de identidade, pois conjuntos de dados diferentes podem ter identidades primárias diferentes.

Há duas opções para fornecer identidades de consumidor ao excluir registros de consumidor:

* [Fazer upload de um arquivo JSON](#upload-json)
* [Inserir valores de identidade manualmente](#manual-identity)

### Fazer upload de um arquivo JSON {#upload-json}

Para fazer upload de um arquivo JSON, você pode arrastar e soltar o arquivo na área de fornecimento ou selecionar **[!UICONTROL Escolher arquivos]** para navegar e selecionar no diretório local.

![Imagem que mostra os métodos para fazer upload do JSON na interface do usuário](../images/ui/delete-consumer/upload-json.png)

O arquivo JSON deve ser formatado como uma matriz de objetos, cada objeto que representa uma identidade do consumidor.

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
| `value` | A identidade do consumidor, tal como indicada pelo tipo. |

Depois que o arquivo for carregado, você poderá continuar [enviar o pedido](#submit).

### Inserir identidades manualmente {#manual-identity}

Para inserir identidades manualmente, selecione **[!UICONTROL Adicionar identidade]**.

![Imagem que mostra o [!UICONTROL Adicionar identidade] botão sendo selecionado](../images/ui/delete-consumer/add-identity.png)

São exibidos controles que permitem inserir identidades de consumidor, uma de cada vez. Em **[!UICONTROL Identidade principal]**, use o menu suspenso para selecionar o tipo de identidade. Em **[!UICONTROL Valor de identidade]**, fornecer o valor de identidade principal para o consumidor.

![Imagem que mostra um campo de identidade adicionado manualmente](../images/ui/delete-consumer/identity-added.png)

Para adicionar mais identidades, selecione o ícone de adição (![Imagem do ícone de adição](../images/ui/delete-consumer/plus-icon.png)) ao lado de uma das linhas ou selecione **[!UICONTROL Adicionar identidade]**.

![Imagem que mostra como adicionar mais identidades à solicitação](../images/ui/delete-consumer/more-identities.png)

## Enviar a solicitação (#submit)

Depois de concluir a adição de identidades à solicitação, selecione **[!UICONTROL Enviar]**.

![Imagem que mostra o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/delete-consumer/submit.png)

Você deverá confirmar a lista de identidades cujos dados deseja excluir. Selecionar **[!UICONTROL Enviar]** para confirmar a seleção.

![Imagem que mostra a caixa de diálogo de confirmação](../images/ui/delete-consumer/confirm-request.png)

Depois que a solicitação é enviada, uma ordem de serviço é criada e exibida no [!UICONTROL Consumidor] da guia [!UICONTROL Higiene de dados] espaço de trabalho. A partir daqui, você pode monitorar o status da ordem de serviço enquanto ela processa a solicitação. A maioria dos pedidos de trabalho de exclusão do consumidor levará vários dias para serem concluídos.

## Próximas etapas

Este documento cobriu como excluir registros do consumidor na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de higiene de dados na interface do usuário, consulte [visão geral da interface do usuário da higiene de dados](./overview.md).

Para saber como excluir registros do consumidor usando a API de Higiene de Dados, consulte o [guia do endpoint de ordem de trabalho](../api/workorder.md).
