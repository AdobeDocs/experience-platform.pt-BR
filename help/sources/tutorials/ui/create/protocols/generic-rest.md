---
keywords: Experience Platform, home, tópicos populares, API REST genérica
title: Criar uma conexão de fonte de API REST genérica na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem da API REST genérica usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 94809a8e98c8de7a9a474fb5543b590fc51cb075
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Crie um [!DNL Generic REST API] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Generic REST API] A fonte está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Generic REST API] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Obter credenciais necessárias

Para acessar o [!DNL Generic REST API] na Platform, você deve fornecer credenciais válidas para o tipo de autenticação de sua escolha. A API REST genérica suporta o código de atualização OAuth 2 e a autenticação básica. Consulte as tabelas a seguir para obter informações sobre as credenciais dos dois tipos de autenticação compatíveis.

#### Código de atualização do OAuth 2

| Credencial | Descrição |
| --- | --- |
| Host | O URL do host da fonte para a qual você está fazendo sua solicitação. Esse valor é necessário e não pode ser ignorado usando a substituição do parâmetro de solicitação. |
| URL do teste de autorização | (Opcional) O URL do teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |
| ID do cliente | (Opcional) A ID do cliente associada à sua conta de usuário. |
| Segredo do cliente | (Opcional) O segredo do cliente associado à sua conta de usuário. |
| Token de acesso | A credencial de autenticação primária usada para acessar seu aplicativo. O token de acesso representa a autorização de seu aplicativo, para acessar aspectos específicos dos dados de um usuário. Esse valor é necessário e não pode ser ignorado usando a substituição do parâmetro de solicitação. |
| Atualizar token | (Opcional) Um token usado para gerar um novo token de acesso, quando o token de acesso tiver expirado. |
| URL do token de acesso | (Opcional) O endpoint do URL usado para buscar seu token de acesso. |
| Substituição do parâmetro da solicitação | (Opcional) Uma propriedade que permite especificar quais parâmetros de credenciais serão substituídos. |


#### Autenticação básica

| Credencial | Descrição |
| --- | --- |
| Host | O URL do host da fonte para a qual você está fazendo sua solicitação. |
| Nome do usuário | O nome de usuário que corresponde à sua conta de usuário. |
| Senha | A senha que corresponde à sua conta de usuário. |

## Conecte sua conta da API REST genérica

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Protocolos] categoria , selecione **[!UICONTROL API REST genérica]** e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/generic-rest/catalog.png)

O **[!UICONTROL Conectar à API REST genérica]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta da API REST genérica à qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/generic-rest/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição de opção para o novo [!DNL Generic REST API] conta.

![novo](../../../../images/tutorials/create/generic-rest/new.png)

#### Autentique usando o código de atualização OAuth 2

[!DNL Generic REST API] O suporta o código de atualização OAuth 2 e a autenticação básica. Para autenticar usando uma autenticação OAuth2, selecione **[!UICONTROL OAuth2RefreshCode]**, forneça suas credenciais do OAuth 2 e selecione **[!UICONTROL Conectar-se à origem]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autenticar usando autenticação básica

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]**, forneça seu host, nome de usuário e senha e selecione **[!UICONTROL Conectar-se à origem]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta da API REST genérica. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](../../dataflow/protocols.md).
