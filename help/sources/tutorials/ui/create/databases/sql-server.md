---
title: Criar uma Conexão do Microsoft SQL Server Source na interface
description: Saiba como criar uma conexão de origem do Microsoft SQL Server usando a interface do usuário do Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Microsoft SQL Server] na interface

Leia este tutorial para saber como conectar sua conta do [!DNL Microsoft SQL Server] ao Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL SQL Server] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para se conectar a [!DNL SQL Server] em [!DNL Experience Platform], você deve fornecer a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| String de conexão | A cadeia de conexão associada à sua conta [!DNL Microsoft SQL Server]. O padrão da cadeia de caracteres de conexão depende se você está usando o nome do servidor ou o nome da instância para a fonte de dados:<ul><li>Cadeia de conexão usando o nome do servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadeia de conexão usando nome de instância:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` <br> `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` </li></ul> |

Para obter mais informações sobre a introdução, consulte [este [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Conectar sua conta do [!DNL SQL Server]

Na interface do Experience Platform, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Bancos de dados*, selecione **[!DNL Microsoft SQL Server]** e **[!UICONTROL Set up]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Set up]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção mudará para **[!UICONTROL Add data]**.

![O catálogo de origens com a origem do Microsoft SQL Server selecionada.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

A página **[!UICONTROL Connect to Microsoft SQL Server]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome, uma descrição opcional e suas credenciais.

Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde algum tempo para a nova conexão ser estabelecida.

![A nova interface de conta com os detalhes de conexão de origem inseridos e realçados.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e, em seguida, selecione a conta que deseja usar no catálogo de contas existente.

Selecione **[!UICONTROL Next]** para continuar.

![A interface de conta existente que exibe uma lista de contas existentes.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL SQL Server]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/databases.md).
