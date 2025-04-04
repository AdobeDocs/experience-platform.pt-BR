---
keywords: Experience Platform;página inicial;tópicos populares;onetrust;OneTrust
solution: Experience Platform
title: Criar uma Conexão OneTrust Source na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do OneTrust usando a interface do usuário do Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL OneTrust Integration] na interface

>[!NOTE]
>
>A fonte [!DNL OneTrust Integration] oferece suporte apenas à assimilação de dados de consentimento e preferências, e não a cookies.

Este tutorial fornece etapas para criar uma conexão de origem [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) para assimilar dados de consentimento históricos e agendados na Adobe Experience Platform usando a interface do usuário do Experience Platform.

## Pré-requisitos

>[!IMPORTANT]
>
>O conector de origem e a documentação [!DNL OneTrust Integration] foram criados pela equipe [!DNL OneTrust Integration]. Para qualquer consulta ou solicitação de atualização, contate a [[!DNL OneTrust] equipe](https://my.onetrust.com/s/contactsupport?language=en_US) diretamente.

Antes de conectar o [!DNL OneTrust Integration] ao Experience Platform, você deve primeiro recuperar o token de acesso. Para obter instruções detalhadas sobre como encontrar o token de acesso, consulte o [[!DNL OneTrust Integration] guia do OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

O token de acesso não é atualizado automaticamente depois que expira porque os tokens de atualização de sistema para sistema não têm suporte no [!DNL OneTrust]. Portanto, é necessário garantir que seu token de acesso seja atualizado na conexão antes que ela expire. O tempo de vida máximo configurável para um token de acesso é de um ano. Para saber mais sobre como atualizar seu token de acesso, consulte o [[!DNL OneTrust] documento sobre como gerenciar suas credenciais de cliente do OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Coletar credenciais necessárias

Para conectar [!DNL OneTrust Integration] ao Experience Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Nome do host | O ambiente do qual os dados [!DNL OneTrust Integration] precisam ser obtidos. | `app.onetrust.com` |
| URL de teste de autorização | (Opcional) O URL de teste de autorização é usado para validar credenciais ao criar uma conexão base. Se não forem fornecidas, as credenciais serão automaticamente verificadas durante a etapa de criação da conexão de origem. | |
| Token de acesso | O token de acesso que corresponde à sua conta do [!DNL OneTrust Integration]. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obter mais informações sobre essas credenciais, consulte a [[!DNL OneTrust Integration] documentação de autenticação](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conectar sua conta do [!DNL OneTrust Integration]

>[!NOTE]
>
>As especificações da API [!DNL OneTrust Integration] estão sendo compartilhadas com a Adobe para assimilação de dados.

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes] de um catálogo de fontes disponíveis no Experience Platform.

Use o menu *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a categoria [!UICONTROL Consentimento e Preferências] do cartão de origem [!DNL OneTrust Integration]. Para começar, selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes da interface do usuário do Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

A página **[!UICONTROL Conectar conta de Integração do OneTrust]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL OneTrust Integration] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![A etapa de autenticação de conta existente no fluxo de trabalho de fontes.](../../../../images/tutorials/create/onetrust/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova etapa de autenticação de conta no fluxo de trabalho de origens.](../../../../images/tutorials/create/onetrust/new.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL OneTrust Integration]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados de consentimento para a Experience Platform](../../dataflow/consent-and-preferences.md).
