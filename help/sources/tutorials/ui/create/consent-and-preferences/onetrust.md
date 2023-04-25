---
keywords: Experience Platform, home, tópicos populares, ontrust, OneTrust
solution: Experience Platform
title: Criar uma conexão de origem OneTrust na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do OneTrust usando a interface do usuário do Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Crie um [!DNL OneTrust Integration] conexão de origem na interface do usuário

>[!NOTE]
>
>O [!DNL OneTrust Integration] A fonte suporta apenas a assimilação de dados de consentimento e preferências, e não cookies.

Este tutorial fornece etapas para criar um [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) conexão de origem para assimilar dados de consentimento históricos e programados no Adobe Experience Platform usando a interface do usuário da plataforma.

## Pré-requisitos

>[!IMPORTANT]
>
>O [!DNL OneTrust Integration] o conector de origem e a documentação foram criados pelo [!DNL OneTrust Integration] equipe. Para quaisquer consultas ou solicitações de atualização, entre em contato com o [[!DNL OneTrust] equipe](https://my.onetrust.com/s/contactsupport?language=en_US) diretamente.

Antes de se conectar [!DNL OneTrust Integration] para o Platform, você deve primeiro recuperar o token de acesso. Para obter instruções detalhadas sobre como encontrar seu token de acesso, consulte o [[!DNL OneTrust Integration] Guia OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

O token de acesso não é atualizado automaticamente depois de expirar porque os tokens de atualização do sistema para o sistema não são suportados por [!DNL OneTrust]. Portanto, é necessário garantir que o token de acesso seja atualizado na conexão antes de expirar. A duração máxima configurável para um token de acesso é de um ano. Para saber mais sobre como atualizar seu token de acesso, consulte o [[!DNL OneTrust] documento sobre como gerenciar suas credenciais de cliente do OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Obter credenciais necessárias

Para se conectar [!DNL OneTrust Integration] para o Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Nome do host | O ambiente a partir do qual o [!DNL OneTrust Integration] Os dados do precisam ser obtidos do. | `app.onetrust.com` |
| URL de teste de autorização | (Opcional) O URL do teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |  |
| Token de acesso | O token de acesso que corresponde ao seu [!DNL OneTrust Integration] conta. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obter mais informações sobre essas credenciais, consulte o [[!DNL OneTrust Integration] documentação de autenticação](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conecte seu [!DNL OneTrust Integration] account

>[!NOTE]
>
>O [!DNL OneTrust Integration] As especificações da API estão sendo compartilhadas com o Adobe para assimilação de dados.

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho para um catálogo de fontes disponíveis no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica no catálogo.

Vá para o [!UICONTROL Consentimento e preferências] categoria para a [!DNL OneTrust Integration] cartão de origem. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens da interface do usuário do Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

O **[!UICONTROL Conta de Integração do Connect OneTrust]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL OneTrust Integration] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![A etapa de autenticação da conta existente no fluxo de trabalho de fontes.](../../../../images/tutorials/create/onetrust/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![A nova etapa de autenticação de conta no fluxo de trabalho de fontes.](../../../../images/tutorials/create/onetrust/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL OneTrust Integration] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de consentimento para a plataforma](../../dataflow/consent-and-preferences.md).
