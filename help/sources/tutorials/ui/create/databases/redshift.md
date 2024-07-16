---
title: Criar uma conexão Amazon Redshift Source na interface do usuário
description: Saiba como criar uma conexão de origem do Amazon Redshift usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 3%

---

# Conectar sua conta do [!DNL Amazon Redshift] usando o espaço de trabalho de origens

>[!IMPORTANT]
>
>A origem [!DNL Amazon Redshift] está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas sobre como conectar sua conta do [!DNL Amazon Redshift] (doravante denominada &quot;[!DNL Redshift]&quot;) ao Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Redshift] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Redshift] no Experience Platform, você deve fornecer os seguintes valores:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| Servidor | O servidor associado à sua conta do [!DNL Redshift]. |
| Porta | A porta TCP que um servidor [!DNL Redshift] usa para escutar conexões de clientes. |
| Nome de usuário | O nome de usuário associado à sua conta [!DNL Redshift]. |
| Senha | A senha associada à sua conta [!DNL Redshift]. |
| Banco de dados | O banco de dados [!DNL Redshift] que você está acessando. |

Para obter mais informações sobre a introdução, consulte [este [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Redshift] ao Experience Platform.

## Conectar sua conta do [!DNL Redshift]

>[!NOTE]
>
>O padrão de codificação para [!DNL Redshift] é Unicode. Isso não pode ser alterado.

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Amazon Redshift]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Redshift].

![](../../../../images/tutorials/create/redshift/catalog.png)

A página **[!UICONTROL Conectar-se ao Amazon Redshift]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Redshift]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/redshift/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Redshift] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Redshift]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Experience Platform](../../dataflow/databases.md).
