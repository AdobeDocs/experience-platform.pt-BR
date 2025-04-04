---
keywords: Experience Platform;página inicial;tópicos populares;Quadrado;quadrado
title: Criar uma Conexão Square Source na interface do usuário
description: Saiba como criar uma conexão de origem do Square usando a interface do usuário do Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# Criar uma conexão de origem [!DNL Square] na interface

Este tutorial fornece etapas para a criação de um conector de origem [!DNL Square] usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para acessar sua Experience Platform de conta [!DNL Square], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| --- | --- |
| Host | A URL da instância [!DNL Square]. |
| ID de cliente | A ID do cliente associada à sua conta do [!DNL Square]. |
| Segredo do cliente | O segredo do cliente associado à sua conta do [!DNL Square]. |
| Token de acesso | O token de acesso é usado para autenticar sua conta do [!DNL Square] com a autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| Atualizar token | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expira. O token de atualização pode ser obtido de [!DNL Square]. |

Para obter mais informações sobre essas credenciais e como obtê-las, consulte a [[!DNL Square] documentação sobre OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Square] à Experience Platform.

## Conectar sua conta do [!DNL Square]

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Pagamentos], selecione **[!UICONTROL Quadrado]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/square/catalog.png)

A página **[!UICONTROL Conectar ao Quadrado]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Square] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/square/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para suas credenciais do [!DNL Square]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/square/new.png)

## Próximas etapas

Seguindo este tutorial, você autenticou e criou uma conexão de origem entre sua conta do [!DNL Square] e a Experience Platform. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer dados de pagamentos para a Experience Platform](../../dataflow/payments.md).
