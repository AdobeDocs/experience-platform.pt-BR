---
keywords: Experience Platform, home, tópicos populares, Snowflake
title: Criar uma conexão de fonte Snowflake na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Snowflake usando a interface do usuário do Adobe Experience Platform.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Crie um [!DNL Snowflake] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Snowflake] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL Snowflake] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Obter credenciais necessárias

Para acessar a conta do Snowflake em [!DNL Platform], você deve fornecer o seguinte valor de autenticação:

| Credencial | Descrição |
| ---------- | ----------- |
| Conta | O nome completo da conta associado ao [!DNL Snowflake] conta. Um [!DNL Snowflake] o nome da conta inclui o nome da conta, a região e a plataforma da nuvem. Por exemplo, `cj12345.east-us-2.azure`. Para obter mais informações sobre nomes de conta, consulte esta seção [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Depósito | O [!DNL Snowflake] warehouse gerencia o processo de execução de consulta do aplicativo. Cada [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| Banco de dados | O [!DNL Snowflake] O banco de dados contém os dados que você deseja trazer para a Plataforma. |
| Nome do usuário | O nome de usuário para a [!DNL Snowflake] conta. |
| Senha | A senha do [!DNL Snowflake] conta do usuário. |
| Cadeia de conexão | A cadeia de conexão usada para se conectar ao seu [!DNL Snowflake] instância. O padrão da string de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Para obter mais informações sobre esses valores, consulte [este documento de Snowflake](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Conecte sua conta do Snowflake

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Bancos de dados] categoria , selecione **[!UICONTROL Snowflake]** e depois selecione **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

O **[!UICONTROL Ligar ao Snowflake]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta do Snowflake com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais de Snowflake. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/snowflake/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Snowflake. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
