---
title: Criar uma conexão de origem de Snowflake na interface
type: Tutorial
description: Saiba como criar uma conexão de origem de Snowflake usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Criar um [!DNL Snowflake] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Snowflake] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas para a criação de um [!DNL Snowflake] conector de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Origens](../../../../home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes propriedades de credencial para autenticar seu [!DNL Snowflake] origem.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

| Credencial | Descrição |
| ---------- | ----------- |
| Conta | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes [!DNL Snowflake] organizações internacionais. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Para obter mais informações sobre nomes de conta, leia a [!DNL Snowflake] documentação sobre [identificadores de conta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |
| Banco de dados | A variável [!DNL Snowflake] contém os dados que você deseja trazer para a Platform. |
| Nome de usuário | O nome de usuário para o [!DNL Snowflake] conta. |
| Senha | A senha para o [!DNL Snowflake] conta de usuário. |
| Função | A função de controle de acesso padrão a ser usada na [!DNL Snowflake] sessão. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| String de conexão | A cadeia de conexão usada para se conectar ao [!DNL Snowflake] instância. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, você deve gerar um par de chaves RSA de 2048 bits e fornecer os seguintes valores ao criar uma conta para o [!DNL Snowflake] origem.

| Credencial | Descrição |
| --- | --- |
| Conta | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes [!DNL Snowflake] organizações internacionais. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Para obter mais informações sobre nomes de conta, leia a [!DNL Snowflake] documentação sobre [identificadores de conta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nome de usuário | O nome de usuário do seu [!DNL Snowflake] conta. |
| Chave privada | A variável [!DNL Base64-]chave privada codificada de seu [!DNL Snowflake] conta. Você pode gerar chaves privadas criptografadas ou não. Se você estiver usando uma chave privada criptografada, também deverá fornecer uma senha de chave privada ao autenticar no Experience Platform. |
| Senha da chave privada | A senha da chave privada é uma camada adicional de segurança que deve ser usada ao autenticar com uma chave privada criptografada. Não é necessário fornecer a senha se você estiver usando uma chave privada não criptografada. |
| Banco de dados | A variável [!DNL Snowflake] banco de dados que contém os dados que você deseja assimilar no Experience Platform. |
| Warehouse | A variável [!DNL Snowflake] O warehouse gerencia o processo de execução da consulta para o aplicativo. Each [!DNL Snowflake] O warehouse é independente um do outro e deve ser acessado individualmente ao trazer os dados para a Platform. |

Para obter mais informações sobre esses valores, consulte [este documento Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Para acessar sua conta Snowflake no Experience Platform, você deve fornecer o seguinte valor de autenticação:

>[!NOTE]
>
>Você deve definir o `PREVENT_UNLOAD_TO_INLINE_URL` sinalizador para `FALSE` para permitir o descarregamento de dados do [!DNL Snowflake] banco de dados para Experience Platform.

## Conectar sua conta Snowflake

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL Bancos de dados] categoria, selecione **[!UICONTROL Snowflake]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com [!DNL Snowflake] destacado.](../../../../images/tutorials/create/snowflake/catalog.png)

A variável **[!UICONTROL Conectar ao Snowflake]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Snowflake] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![A interface de conta existente no fluxo de trabalho de origens.](../../../../images/tutorials/create/snowflake/existing.png)

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL Snowflake] conta.

![A nova interface de conta no workflow de origens.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, forneça sua cadeia de conexão no formulário de entrada e selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação da chave da conta.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, forneça valores para sua conta, nome de usuário, chave privada, senha de chave privada, banco de dados e warehouse e, em seguida, selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação de par de chaves da conta.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Snowflake. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
