---
title: Criar uma conexão de origem do Amazon Redshift na interface do usuário
description: Saiba como criar uma conexão de origem do Amazon Redshift usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# Conecte seu [!DNL Amazon Redshift] conta usando o espaço de trabalho de origens

>[!IMPORTANT]
>
>A variável [!DNL Amazon Redshift] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas sobre como conectar seu [!DNL Amazon Redshift] (a seguir designado por &quot;[!DNL Redshift]&quot;) para a Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Redshift] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Redshift] conta no Experience Platform, você deve fornecer os seguintes valores:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| Servidor | O servidor associado ao seu [!DNL Redshift] conta. |
| Porta  | A porta TCP que um [!DNL Redshift] O servidor usa o para detectar conexões de clientes. |
| Nome de usuário | O nome de usuário associado à [!DNL Redshift] conta. |
| Senha | A senha associada ao seu [!DNL Redshift] conta. |
| Banco de dados | A variável [!DNL Redshift] banco de dados que você está acessando. |

Para obter mais informações sobre a introdução, consulte [este [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Redshift] conta para Experience Platform.

## Conecte seu [!DNL Redshift] account

>[!NOTE]
>
>O padrão de codificação para [!DNL Redshift] é Unicode. Isso não pode ser alterado.

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Bancos de dados]** categoria, selecione **[!UICONTROL Amazon Redshift]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Redshift] conector.

![](../../../../images/tutorials/create/redshift/catalog.png)

A variável **[!UICONTROL Conectar-se ao Amazon Redshift]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Redshift] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![](../../../../images/tutorials/create/redshift/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Redshift] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Redshift] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Experience Platform](../../dataflow/databases.md).
