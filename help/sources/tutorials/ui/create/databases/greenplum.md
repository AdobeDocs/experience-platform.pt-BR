---
keywords: Experience Platform, home, tópicos populares, Greenplum, greenplum
solution: Experience Platform
title: Criar uma conexão de origem GreenPlum na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem GreenPlum usando a interface do usuário do Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL GreenPlum] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL GreenPlum] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL GreenPlum], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL GreenPlum] usando a API [!DNL Flow Service].

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para se conectar à instância [!DNL GreenPlum]. O padrão da string de conexão para [!DNL GreenPlum] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre a introdução, consulte [este documento do GreenPlum](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn).

## Conecte sua conta [!DNL GreenPlum]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL GreenPlum] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos de Dados]**, selecione **[!UICONTROL GreenPlum]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL GreenPlum].

![catálogo](../../../../images/tutorials/create/greenplum/catalog.png)

A página **[!UICONTROL Connect to GreenPlum]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL GreenPlum]. Quando terminar, selecione **[!UICONTROL Connect]** e deixe algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL GreenPlum] com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/greenplum/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL GreenPlum]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
