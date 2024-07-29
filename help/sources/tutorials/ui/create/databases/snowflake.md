---
title: Criar uma conexão Snowflake Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem de Snowflake usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: d89e0c81bd250e41a863b8b28d358cc6ddea1c37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# Criar uma conexão de origem [!DNL Snowflake] na interface

>[!IMPORTANT]
>
>A origem [!DNL Snowflake] está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas para a criação de um conector de origem [!DNL Snowflake] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Você deve fornecer valores para as seguintes propriedades de credencial para autenticar sua origem [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

| Credencial | Descrição |
| ---------- | ----------- |
| Conta | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia o guia em [recuperando seu [!DNL Snowflake] identificador de conta](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) para obter orientação adicional. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a plataforma. |
| Banco de dados | O banco de dados [!DNL Snowflake] contém os dados que você deseja trazer para a Plataforma. |
| Nome de usuário | O nome de usuário da conta [!DNL Snowflake]. |
| Senha | A senha da conta de usuário [!DNL Snowflake]. |
| Função | A função de controle de acesso padrão a ser usada na sessão [!DNL Snowflake]. A função deve ser uma função existente que já foi atribuída ao usuário especificado. A função padrão é `PUBLIC`. |
| String de conexão | A cadeia de conexão usada para se conectar à sua instância do [!DNL Snowflake]. O padrão da cadeia de conexão para [!DNL Snowflake] é `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, você deve gerar um par de chaves RSA de 2048 bits e fornecer os seguintes valores ao criar uma conta para sua origem [!DNL Snowflake].

| Credencial | Descrição |
| --- | --- |
| Conta | Um nome de conta identifica exclusivamente uma conta na organização. Nesse caso, você deve identificar exclusivamente uma conta em diferentes organizações do [!DNL Snowflake]. Para fazer isso, você deve anexar o nome da organização ao nome da conta. Por exemplo: `orgname-account_name`. Leia o guia em [recuperando seu [!DNL Snowflake] identificador de conta](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) para obter orientação adicional. Para obter mais informações, consulte a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nome de usuário | O nome de usuário da sua conta [!DNL Snowflake]. |
| Chave privada | A chave privada [!DNL Base64-]codificada da sua conta [!DNL Snowflake]. Você pode gerar chaves privadas criptografadas ou não. Se você estiver usando uma chave privada criptografada, também deverá fornecer uma senha de chave privada ao autenticar no Experience Platform. Leia o guia em [recuperando sua [!DNL Snowflake] chave privada](../../../../connectors/databases/snowflake.md) para obter mais informações. |
| Senha da chave privada | A senha da chave privada é uma camada adicional de segurança que deve ser usada ao autenticar com uma chave privada criptografada. Não é necessário fornecer a senha se você estiver usando uma chave privada não criptografada. |
| Banco de dados | O banco de dados [!DNL Snowflake] que contém os dados que você deseja assimilar no Experience Platform. |
| Warehouse | O warehouse [!DNL Snowflake] gerencia o processo de execução da consulta para o aplicativo. Cada warehouse [!DNL Snowflake] é independente um do outro e deve ser acessado individualmente ao trazer dados para a plataforma. |

Para obter mais informações sobre esses valores, consulte [este documento Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Você deve definir o sinalizador `PREVENT_UNLOAD_TO_INLINE_URL` como `FALSE` para permitir o descarregamento de dados do banco de dados [!DNL Snowflake] para o Experience Platform.

## Conectar sua conta Snowflake

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes].

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Bancos de dados], selecione **[!UICONTROL Snowflake]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes com [!DNL Snowflake] realçado.](../../../../images/tutorials/create/snowflake/catalog.png)

A página **[!UICONTROL Conectar-se ao Snowflake]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Snowflake] à qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![A interface de conta existente no fluxo de trabalho de origens.](../../../../images/tutorials/create/snowflake/existing.png)

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para sua nova conta [!DNL Snowflake].

![A nova interface de conta no fluxo de trabalho de origens.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, forneça sua cadeia de conexão no formulário de entrada e selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação da chave da conta.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticação de par de chaves]

Para usar a autenticação de par de chaves, forneça valores para sua conta, nome de usuário, chave privada, senha de chave privada, banco de dados e warehouse e selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação de par de chaves da conta.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Snowflake. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Platform]](../../dataflow/databases.md).
