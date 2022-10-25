---
keywords: Experience Platform, home, tópicos populares, Oracle Service Cloud, nuvem de serviço do oracle
title: Criar uma conexão de origem na nuvem do serviço do Oracle na interface do usuário
description: Saiba como criar uma conexão de origem da Nuvem do serviço do Oracle usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 8e4f2170489d7e4e73bbc726e3253fac97c9f9f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# (Beta) Criar uma conexão de origem da nuvem do Oracle Service na interface do usuário

>[!NOTE]
>
>A origem da Nuvem do Oracle Service está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar uma conexão de origem da nuvem do Oracle Service usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão de origem válida do Oracle Service Cloud, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/customer-success.md)

### Obter credenciais necessárias

Para acessar sua conta da Oracle Service Cloud em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Host | O URL de host da instância da Oracle Service Cloud. |
| Nome de usuário | O nome de usuário da sua conta de usuário da Oracle Service Cloud. |
| Senha | A senha da sua conta do Oracle Service Cloud. |

Para obter mais informações sobre como autenticar sua conta do Oracle Service Cloud, consulte [[!DNL Oracle] guia de autenticação](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conectar sua conta do Oracle Service Cloud

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Sucesso do cliente] categoria , selecione **[!UICONTROL Oracle Service Cloud]** e depois selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem da nuvem do Oracle Service foi realçado.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

O **[!UICONTROL Conectar-se à Oracle Service Cloud]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta da Oracle Service Cloud à qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![A interface de conta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais da Oracle Service Cloud. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![A nova interface de conta com valores de espaço reservado para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Oracle Service Cloud . Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para a Platform](../../dataflow/crm.md).
