---
keywords: Experience Platform;home;tópicos populares;Oracle Service Cloud;oracle service cloud
title: Criar uma conexão do Oracle Service Cloud Source na interface
description: Saiba como criar uma conexão de origem do Oracle Service Cloud usando a interface do Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---

# Criar uma conexão de origem do Oracle Service Cloud na interface

>[!WARNING]
>
>A origem [!DNL Oracle Service Cloud] será substituída no final de junho de 2025.

Este tutorial fornece etapas para criar uma conexão de origem do Oracle Service Cloud usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão de origem válida do Oracle Service Cloud, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/customer-success.md)

### Coletar credenciais necessárias

Para acessar sua conta da Oracle Service Cloud em [!DNL Experience Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Host | O URL do host da sua instância da Oracle Service Cloud. |
| Nome de usuário | O nome de usuário da sua conta de usuário da Oracle Service Cloud. |
| Senha | A senha da sua conta da Oracle Service Cloud. |

Para obter mais informações sobre como autenticar sua conta da Oracle Service Cloud, consulte o [[!DNL Oracle] manual sobre autenticação](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conectar sua conta da Oracle Service Cloud

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Sucesso do cliente], selecione **[!UICONTROL Oracle Service Cloud]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem da Oracle Service Cloud foi realçado.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

A página **[!UICONTROL Conectar-se à Oracle Service Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta da Oracle Service Cloud com a qual deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![A interface de conta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que é exibido, forneça um nome, uma descrição opcional e suas credenciais da Oracle Service Cloud. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova interface de conta com valores de espaço reservado para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta da Oracle Service Cloud. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para a Experience Platform](../../dataflow/crm.md).
