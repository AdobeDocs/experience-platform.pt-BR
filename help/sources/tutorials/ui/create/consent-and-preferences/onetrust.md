---
keywords: Experience Platform, home, tópicos populares, ontrust, OneTrust
solution: Experience Platform
title: (Beta) Criar uma Conexão de Fonte OneTrust na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do OneTrust usando a interface do usuário do Adobe Experience Platform.
source-git-commit: adefaeb895c91d45727f791b73b73a17a2b1ccf9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# (Beta) Criar um [!DNL OneTrust Integration] conexão de origem na interface do usuário

>[!NOTE]
>
>O [!DNL OneTrust Integration] A fonte está em beta. Seus recursos e documentação estão sujeitos a alterações. Para obter informações sobre o uso de fontes com rótulo beta, consulte o [visão geral das fontes](../../../../home.md#terms-and-conditions).

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
| Host | O ambiente a partir do qual o [!DNL OneTrust Integration] Os dados do precisam ser obtidos do. | `https://uat.onetrust.com/` |
| URL de teste de autorização | (Opcional) O URL do teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não for fornecido, as credenciais serão verificadas automaticamente durante a etapa de criação da conexão de origem. |  |
| Token de acesso | O token de acesso que corresponde ao seu [!DNL OneTrust Integration] conta. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obter mais informações sobre essas credenciais, consulte o [[!DNL OneTrust Integration] documentação de autenticação](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conecte seu [!DNL OneTrust Integration] account

>[!NOTE]
>
>O [!DNL OneTrust Integration] As especificações da API estão sendo compartilhadas com o Adobe para assimilação de dados.

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em *[!UICONTROL Consentimento e preferências]* categoria , selecione [!DNL OneTrust Integration]e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/onetrust/catalog.png)

O **[!UICONTROL Conta de Integração do Connect OneTrust]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL OneTrust Integration] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/onetrust/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/onetrust/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL OneTrust Integration] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de consentimento para a plataforma](../../dataflow/consent-and-preferences.md).