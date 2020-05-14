---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem ServiceNow na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Criar um conector de origem ServiceNow na interface do usuário

>[!NOTE]
>O conector ServiceNow está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem ServiceNow usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão ServiceNow, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Reunir credenciais obrigatórias

Para acessar sua conta do ServiceNow na Plataforma, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O terminal do servidor ServiceNow. |
| `username` | O nome de usuário usado para conectar-se ao servidor ServiceNow para autenticação. |
| `password` | A senha para conectar-se ao servidor ServiceNow para autenticação. |

Para obter mais informações sobre a introdução, consulte [este documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

## Ligar a sua conta ServiceNow

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta ServiceNow para se conectar ao Platform.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes para as quais você pode criar uma conta, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Customer Success (Sucesso* do cliente), selecione **ServiceNow (ServiçoAgora** ) para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conta, selecione Origem **do** Connect.

![](../../../../images/tutorials/create/servicenow/catalog.png)

A página *Conectar-se ao ServiceNow* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do ServiceNow. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conta ser estabelecida.

![](../../../../images/tutorials/create/servicenow/new-credentials.png)

### Conta existente

Para conectar uma conta existente, selecione a conta ServiceNow à qual deseja se conectar e, em seguida, selecione **Avançar** para continuar.

![](../../../../images/tutorials/create/servicenow/existing-credentials.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta ServiceNow. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/customer-success.md).
