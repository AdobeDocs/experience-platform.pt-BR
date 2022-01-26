---
keywords: Experience Platform, home, tópicos populares, Amazon Redshift, amazon redshift, Redshift, redshift
solution: Experience Platform
title: Criar uma conexão de origem do Amazon Redshift na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Amazon Redshift usando a interface do Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 2fb972b0ec8d1f679c6ce104a439265b5cc4d535
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Crie um [!DNL Amazon Redshift] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Amazon Redshift] (a seguir designado por &quot;[!DNL Redshift]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Redshift] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar o [!DNL Redshift] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| `server` | O servidor associado ao [!DNL Redshift] conta. |
| `username` | O nome de usuário associado à [!DNL Redshift] conta. |
| `password` | A senha associada à sua [!DNL Redshift] conta. |
| `database` | O [!DNL Redshift] banco de dados que você está acessando. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Conecte seu [!DNL Redshift] account

>[!NOTE]
>
>O padrão de codificação para [!DNL Redshift] é Unicode. Isso não pode ser alterado.

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Redshift] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Amazon Redshift]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Redshift] conector.

![](../../../../images/tutorials/create/redshift/catalog.png)

O **[!UICONTROL Conecte-se ao Amazon Redshift]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Redshift] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/redshift/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Redshift] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Redshift] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
