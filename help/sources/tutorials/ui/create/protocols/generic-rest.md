---
keywords: Experience Platform;página inicial;tópicos populares;API REST genérica
title: Criar uma conexão de origem da API REST genérica na interface
type: Tutorial
description: Saiba como criar uma conexão de origem da API REST genérica usando a interface do usuário do Adobe Experience Platform.
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Criar um [!DNL Generic REST API] conexão de origem na interface

>[!NOTE]
>
> A variável [!DNL Generic REST API] a fonte está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Este tutorial fornece etapas para a criação de um [!DNL Generic REST API] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Para acessar seu [!DNL Generic REST API] na Platform, você deve fornecer credenciais válidas para o tipo de autenticação de sua escolha. A API REST genérica oferece suporte ao código de atualização OAuth 2 e à autenticação básica. Consulte as tabelas a seguir para obter informações sobre as credenciais dos dois tipos de autenticação compatíveis.

#### Código de atualização do OAuth 2

| Credencial | Descrição |
| --- | --- |
| Host | O URL do host da origem para a qual você está fazendo sua solicitação. Este valor é obrigatório e não pode ser ignorado usando a substituição do parâmetro de solicitação. |
| URL de teste de autorização | (Opcional) O URL de teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não forem fornecidas, as credenciais serão automaticamente verificadas durante a etapa de criação da conexão de origem. |
| ID do cliente | (Opcional) A ID do cliente associada à sua conta de usuário. |
| Segredo do cliente | (Opcional) O segredo do cliente associado à sua conta de usuário. |
| Token de acesso | A credencial de autenticação primária usada para acessar seu aplicativo. O token de acesso representa a autorização do aplicativo para acessar aspectos específicos dos dados de um usuário. Este valor é obrigatório e não pode ser ignorado usando a substituição do parâmetro de solicitação. |
| Atualizar token | (Opcional) Um token usado para gerar um novo token de acesso, quando o token de acesso expirou. |
| URL do token de acesso | (Opcional) O endpoint do URL usado para buscar seu token de acesso. |
| Solicitar substituição de parâmetro | (Opcional) Uma propriedade que permite especificar quais parâmetros de credencial serão substituídos. |


#### Autenticação básica

| Credencial | Descrição |
| --- | --- |
| Host | O URL do host da origem para a qual você está fazendo sua solicitação. |
| Nome de usuário | O nome de usuário que corresponde à sua conta de usuário. |
| Senha | A senha que corresponde à sua conta de usuário. |

## Conectar sua conta de API REST genérica

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL Protocolos] categoria, selecione **[!UICONTROL API REST genérica]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/generic-rest/catalog.png)

A variável **[!UICONTROL Conectar-se à API REST genérica]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta da API REST genérica à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/generic-rest/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição de opção para o novo [!DNL Generic REST API] conta.

![novo](../../../../images/tutorials/create/generic-rest/new.png)

#### Autenticar usando código de atualização OAuth 2

[!DNL Generic REST API] O oferece suporte ao código de atualização OAuth 2 e à autenticação básica. Para autenticar usando uma autenticação OAuth2, selecione **[!UICONTROL OAuth2RefreshCode]**, forneça suas credenciais do OAuth 2 e selecione **[!UICONTROL Conectar à origem]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autenticar usando autenticação básica

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]**, forneça seu host, nome de usuário e senha e selecione **[!UICONTROL Conectar à origem]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta da API REST genérica. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/protocols.md).
