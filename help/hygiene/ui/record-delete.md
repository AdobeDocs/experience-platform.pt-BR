---
title: Excluir Registros
description: Saiba como excluir registros na interface do Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---

# Excluir registros

A variável [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do usuário do Adobe Experience Platform, é possível excluir registros que participam do Serviço de identidade e do Perfil do cliente em tempo real. Esses registros podem ser vinculados a consumidores individuais ou a qualquer outra entidade incluída no gráfico de identidade.

>[!IMPORTANT]
>
>As solicitações de exclusão de registro só estão disponíveis para organizações que compraram **Adobe Healthcare Shield**.
>
>
>As exclusões de registros devem ser usadas para limpeza de dados, remoção de dados anônimos ou minimização de dados. Eles são **não** a ser usado para solicitações de direitos do titular dos dados (conformidade) como relacionadas a regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Para todos os casos de uso de conformidade, use [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) em vez disso.

## Pré-requisitos

A exclusão de registros requer um entendimento prático de como os campos de identidade funcionam no Experience Platform. Especificamente, você deve saber os valores de identidade principais das entidades cujos registros deseja excluir, dependendo do conjunto de dados (ou conjuntos de dados) do qual você está excluindo.

Consulte a seguinte documentação para obter mais informações sobre identidades na Platform:

* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): une as identidades em dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais estão em conformidade.
   * [Namespaces de identidade](../../identity-service/namespaces.md): os namespaces de identidade definem os diferentes tipos de informações de identidade que podem se relacionar a uma única pessoa e são um componente obrigatório para cada campo de identidade.
* [Perfil do cliente em tempo real](../../profile/home.md): aproveita os gráficos de identidade para fornecer perfis de consumidor unificados com base em dados agregados de várias fontes, atualizados em tempo quase real.
* [Experience Data Model (XDM)](../../xdm/home.md): fornece definições e estruturas padrão para dados da Platform por meio do uso de esquemas. Todos os conjuntos de dados da Platform estão em conformidade com um esquema XDM específico, e o esquema define quais campos são identidades.
   * [Campos de identidade](../../xdm/ui/fields/identity.md): saiba como um campo de identidade é definido em um esquema XDM.

## Criar uma nova solicitação

Para iniciar o processo, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![Imagem mostrando o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/record-delete/create-request-button.png)

A caixa de diálogo de criação de solicitação é exibida. Por padrão, a variável **[!UICONTROL Excluir consumidor]** estiver selecionada na caixa de diálogo **[!UICONTROL Ação solicitada]** seção. Deixe essa opção selecionada.

![Imagem mostrando a opção de exclusão de consumidor selecionada na caixa de diálogo de criação](../images/ui/record-delete/consumer-action.png)

## Selecionar conjuntos de dados

No **[!UICONTROL Detalhes do consumidor]** , a próxima etapa é determinar se você deseja excluir registros de um único conjunto de dados ou de todos os conjuntos de dados.

Se você escolher **[!UICONTROL Selecionar conjunto de dados]**, selecione o ícone do banco de dados (![Imagem do ícone do banco de dados](../images/ui/record-delete/database-icon.png)) e uma caixa de diálogo é exibida permitindo selecionar o conjunto de dados desejado na lista.

![Imagem mostrando a caixa de diálogo de seleção do conjunto de dados](../images/ui/record-delete/select-dataset.png)

Se desejar excluir registros de todos os conjuntos de dados, selecione **[!UICONTROL Todos os conjuntos de dados]**.

![Imagem mostrando o [!UICONTROL Todos os conjuntos de dados] opção selecionada](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selecionar o **[!UICONTROL Todos os conjuntos de dados]** pode fazer com que a operação de exclusão demore mais e pode não resultar na exclusão precisa do registro.

## Fornecer identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identidade principal"
>abstract="Uma identidade principal é um atributo que vincula um registro ao perfil do consumidor na Experience Platform. O campo de identidade principal de um conjunto de dados é definido pelo esquema em que o conjunto de dados se baseia. Nessa coluna, você deve fornecer o tipo (ou namespace) da identidade principal do registro, como `email` para endereços de email e `ecid` para IDs da Experience Cloud. Para saber mais, consulte o guia da interface de higiene de dados."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidade"
>abstract="Nessa coluna, você deve fornecer o valor da identidade principal do registro, que deve corresponder ao tipo de identidade fornecido na coluna esquerda. Se o tipo de identidade principal for `email`, o valor deve ser o endereço de email do registro. Para saber mais, consulte o guia da interface de higiene de dados."

Ao excluir registros, você deve fornecer informações de identidade para que o sistema possa determinar quais registros devem ser excluídos. Para qualquer conjunto de dados na Plataforma, os registros são excluídos com base no **identidade principal** que é definido pelo esquema do conjunto de dados.

Como todos os campos de identidade na Platform, uma identidade primária é composta de duas coisas: uma **type** (às vezes chamado de namespace de identidade) e um **value**. O tipo de identidade fornece contexto sobre como o campo identifica um registro (como um endereço de email), e o valor representa a identidade específica de um registro para esse tipo (por exemplo, `jdoe@example.com` para o `email` tipo de identidade). Campos comuns usados como identidades incluem informações da conta, IDs do dispositivo e IDs de cookie.

>[!TIP]
>
>Se você não souber a identidade principal de um conjunto de dados específico, poderá encontrá-la na interface do usuário da plataforma. No **[!UICONTROL Conjuntos de dados]** selecione o conjunto de dados em questão na lista. Na página de detalhes do conjunto de dados, passe o mouse sobre o nome do esquema do conjunto de dados no painel direito. A identidade principal é exibida junto com o nome e a descrição do schema.
>
>![Imagem que mostra a identidade principal de um conjunto de dados destacado na interface](../images/ui/record-delete/dataset-primary-identity.png)

Se você estiver excluindo registros de um único conjunto de dados, todas as identidades fornecidas deverão ser do mesmo tipo, já que um conjunto de dados só pode ter uma identidade principal. Se estiver excluindo de todos os conjuntos de dados, você poderá incluir vários tipos de identidade, pois conjuntos de dados diferentes podem ter identidades principais diferentes.

Há duas opções para fornecer identidades ao excluir registros:

* [Fazer upload de um arquivo JSON](#upload-json)
* [Inserir valores de identidade manualmente](#manual-identity)

### Fazer upload de um arquivo JSON {#upload-json}

Para fazer upload de um arquivo JSON, você pode arrastar e soltar o arquivo na área fornecida ou selecionar **[!UICONTROL Escolher arquivos]** para procurar e selecionar no diretório local.

![Imagem que mostra os métodos para fazer upload do JSON na interface](../images/ui/record-delete/upload-json.png)

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

![Imagem mostrando o [!UICONTROL Adicionar identidade] botão sendo selecionado](../images/ui/record-delete/add-identity.png)

São exibidos controles que permitem inserir identidades, uma de cada vez. Em **[!UICONTROL Identidade principal]**, use o menu suspenso para selecionar o tipo de identidade. Em **[!UICONTROL Valor de identidade]**, fornecem o valor de identidade principal do registro.

![Imagem mostrando um campo de identidade adicionado manualmente](../images/ui/record-delete/identity-added.png)

Para adicionar mais identidades, selecione o ícone de adição (![Imagem do ícone de adição](../images/ui/record-delete/plus-icon.png)) ao lado de uma das linhas ou selecione **[!UICONTROL Adicionar identidade]**.

![Imagem que mostra como adicionar mais identidades à solicitação](../images/ui/record-delete/more-identities.png)

## Enviar a solicitação (#submit)

Quando terminar de adicionar identidades à solicitação, em **[!UICONTROL Configurações de solicitação]**, forneça um nome e uma descrição opcional para a solicitação antes de selecionar **[!UICONTROL Enviar]**.

![Imagem mostrando o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/record-delete/submit.png)

Você será solicitado a confirmar a lista de identidades cujos dados deseja excluir. Selecionar **[!UICONTROL Enviar]** para confirmar a seleção.

![Imagem mostrando a caixa de diálogo de confirmação](../images/ui/record-delete/confirm-request.png)

Depois que a solicitação é submetida, uma ordem de serviço é criada e é exibida no [!UICONTROL Consumidor] guia do [!UICONTROL Higiene de dados] espaço de trabalho. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
>
>Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#record-delete-transparency) para obter detalhes sobre como as exclusões de registro são processadas após serem executadas.

## Próximas etapas

Este documento abordou como excluir registros na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de higiene de dados na interface do usuário, consulte [visão geral da interface da higiene de dados](./overview.md).

Para saber como excluir registros usando a API de higiene de dados, consulte o [guia de ponto de extremidade de ordem de trabalho](../api/workorder.md).
