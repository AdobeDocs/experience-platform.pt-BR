---
keywords: Experience Platform;página inicial;tópicos populares;onetrust;OneTrust
solution: Experience Platform
title: Criar uma Conexão de Origem do OneTrust na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do OneTrust usando a interface do usuário do Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Criar um [!DNL OneTrust Integration] conexão de origem na interface

>[!NOTE]
>
>A variável [!DNL OneTrust Integration] A fonte do só oferece suporte à assimilação de dados de consentimento e preferências, e não de cookies.

Este tutorial fornece etapas para a criação de um [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) conexão de origem para assimilar dados de consentimento históricos e programados na Adobe Experience Platform usando a interface do usuário da Platform.

## Pré-requisitos

>[!IMPORTANT]
>
>A variável [!DNL OneTrust Integration] o conector de origem e a documentação foram criados pela [!DNL OneTrust Integration] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato com o [[!DNL OneTrust] equipe](https://my.onetrust.com/s/contactsupport?language=en_US) diretamente.

Antes de se conectar [!DNL OneTrust Integration] Para acessar a Platform, você deve primeiro recuperar o token de acesso. Para obter instruções detalhadas sobre como encontrar o token de acesso, consulte [[!DNL OneTrust Integration] Guia do OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

O token de acesso não é atualizado automaticamente após a expiração, pois os tokens de atualização de sistema para sistema não são compatíveis com o [!DNL OneTrust]. Portanto, é necessário garantir que seu token de acesso seja atualizado na conexão antes que ela expire. O tempo de vida máximo configurável para um token de acesso é de um ano. Para saber mais sobre como atualizar o token de acesso, consulte a [[!DNL OneTrust] documento sobre o gerenciamento de credenciais do cliente OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Coletar credenciais necessárias

Para se conectar [!DNL OneTrust Integration] Para o Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Nome do host | O ambiente a partir do qual o [!DNL OneTrust Integration] Os dados do precisam ser obtidos de. | `app.onetrust.com` |
| URL de teste de autorização | (Opcional) O URL de teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não forem fornecidas, as credenciais serão automaticamente verificadas durante a etapa de criação da conexão de origem. |  |
| Token de acesso | O token de acesso que corresponde ao seu [!DNL OneTrust Integration] conta. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obter mais informações sobre essas credenciais, consulte a [[!DNL OneTrust Integration] documentação de autenticação](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conecte seu [!DNL OneTrust Integration] account

>[!NOTE]
>
>A variável [!DNL OneTrust Integration] As especificações da API estão sendo compartilhadas com o Adobe para assimilação de dados.

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho para um catálogo de fontes disponíveis no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a [!UICONTROL Consentimento e preferências] categoria para a [!DNL OneTrust Integration] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes da interface de Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

A variável **[!UICONTROL Conectar a conta de Integração do OneTrust]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL OneTrust Integration] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![A etapa de autenticação de conta existente no fluxo de trabalho de fontes.](../../../../images/tutorials/create/onetrust/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova etapa de autenticação de conta no fluxo de trabalho de fontes.](../../../../images/tutorials/create/onetrust/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL OneTrust Integration] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de consentimento para a Platform](../../dataflow/consent-and-preferences.md).
