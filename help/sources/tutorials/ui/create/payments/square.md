---
keywords: Experience Platform;página inicial;tópicos populares;Quadrado;quadrado
title: Criar uma Conexão de Origem Quadrada na Interface do Usuário
description: Saiba como criar uma conexão de origem do Square usando a interface do usuário do Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Criar um [!DNL Square] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Square] conector de origem usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para acessar seu [!DNL Square] Plataforma da conta, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| --- | --- |
| Host | O URL do [!DNL Square] instância. |
| ID do cliente | A ID do cliente associada à [!DNL Square] conta. |
| Segredo do cliente | O segredo do cliente associado à [!DNL Square] conta. |
| Token de acesso | O token de acesso é usado para autenticar seu [!DNL Square] conta com autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| Atualizar token | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expira. O token de atualização pode ser obtido em [!DNL Square]. |

Para obter mais informações sobre essas credenciais e como obtê-las, consulte [[!DNL Square] documentação sobre o OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Square] para a Platform.

## Conecte seu [!DNL Square] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL Pagamentos] categoria, selecione **[!UICONTROL Quadrado]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/square/catalog.png)

A variável **[!UICONTROL Conectar ao Quadrado]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Square] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/square/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para o [!DNL Square] credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/square/new.png)

## Próximas etapas

Ao seguir este tutorial, você autenticou e criou uma conexão de origem entre [!DNL Square] conta e plataforma. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer dados de pagamentos para a Plataforma](../../dataflow/payments.md).
