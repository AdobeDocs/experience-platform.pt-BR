---
title: Criar uma conexão de origem de Snowflake na interface
type: Tutorial
description: Saiba como criar uma conexão de origem de Snowflake usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# Criar um [!DNL Snowflake] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Snowflake] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas para a criação de um [!DNL Snowflake] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Para acessar sua conta Snowflake em [!DNL Platform], você deve fornecer o seguinte valor de autenticação:

| Credencial | Descrição |
| ---------- | ----------- |
| Conta | O nome completo da conta associado à [!DNL Snowflake] conta. Um [!DNL Snowflake] o nome da conta inclui o nome da conta, a região e a plataforma de nuvem. Por exemplo, `cj12345.east-us-2.azure`. Para obter mais informações sobre nomes de conta, consulte esta [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Warehouse | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| Banco de dados | A variável [!DNL Snowflake] contém os dados que você deseja trazer para a Platform. |
| Nome de usuário | O nome de usuário para o [!DNL Snowflake] conta. |
| Senha | A senha para o [!DNL Snowflake] conta de usuário. |
| Função | A função de controle de acesso padrão a ser usada na [!DNL Snowflake] sessão. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| String de conexão | A cadeia de conexão usada para se conectar ao [!DNL Snowflake] instância. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Para obter mais informações sobre esses valores, consulte [este documento Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>Você deve definir o `PREVENT_UNLOAD_TO_INLINE_URL` sinalizador para `FALSE` para permitir o descarregamento de dados do [!DNL Snowflake] banco de dados para Experience Platform.

## Conectar sua conta Snowflake

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL Bancos de dados] categoria, selecione **[!UICONTROL Snowflake]** e selecione **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

A variável **[!UICONTROL Conectar ao Snowflake]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta do Snowflake à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que é exibido, forneça um nome, uma descrição opcional e suas credenciais de Snowflake. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![](../../../../images/tutorials/create/snowflake/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Snowflake. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
