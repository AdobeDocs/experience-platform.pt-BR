---
keywords: Experience Platform;página inicial;tópicos populares;Nuvem do serviço de Oracle;nuvem do serviço de oracle
title: Criar uma conexão de origem do Oracle Service Cloud na interface
description: Saiba como criar uma conexão de origem do Oracle Service Cloud usando a interface do Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Criar uma conexão de origem do Oracle Service Cloud na interface

Este tutorial fornece etapas para criar uma conexão de origem do Oracle Service Cloud usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão de origem válida do Oracle Service Cloud, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/customer-success.md)

### Coletar credenciais necessárias

Para acessar sua conta da Oracle Service Cloud em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Host | O URL do host da instância da Nuvem do Oracle Service. |
| Nome de usuário | O nome de usuário da sua conta de usuário da Oracle Service Cloud. |
| Senha | A senha da sua conta da Oracle Service Cloud. |

Para obter mais informações sobre como autenticar sua conta da Oracle Service Cloud, consulte o [[!DNL Oracle] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conectar sua conta da Oracle Service Cloud

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] A tela exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL Sucesso do cliente] categoria, selecione **[!UICONTROL Oracle Service Cloud]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem da Nuvem do Oracle Service destacada.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

A variável **[!UICONTROL Conectar-se à Oracle Service Cloud]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta da Oracle Service Cloud com a qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![A interface de conta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais da Nuvem do Oracle Service. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta com valores de espaço reservado para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta da Oracle Service Cloud. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para a Platform](../../dataflow/crm.md).
