---
title: Criar uma Conexão de Origem do Microsoft SQL Server na interface do usuário
description: Saiba como criar uma conexão de origem do Microsoft SQL Server usando a interface do usuário do Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Criar um [!DNL Microsoft SQL Server] conexão de origem na interface

Leia este tutorial para saber como conectar seu [!DNL Microsoft SQL Server] para a Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL SQL Server] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para se conectar a [!DNL SQL Server] em [!DNL Platform], você deve fornecer a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| String de conexão | A cadeia de conexão associada ao seu [!DNL Microsoft SQL Server] conta. O padrão da cadeia de caracteres de conexão depende se você está usando o nome do servidor ou o nome da instância para a fonte de dados:<ul><li>Cadeia de conexão usando o nome do servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadeia de conexão usando nome de instância:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Para obter mais informações sobre a introdução, consulte [este [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Conecte seu [!DNL SQL Server] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *Bancos de dados* categoria, selecione **[!DNL Microsoft SQL Server]** e selecione **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a variável **[!UICONTROL Configurar]** opção quando uma determinada fonte ainda não tiver uma conta autenticada. Quando uma conta autenticada existir, essa opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem do Microsoft SQL Server selecionada.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

A variável **[!UICONTROL Conectar ao Microsoft SQL Server]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova conta faz interface com os detalhes de conexão de origem inseridos e destacados.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e selecione a conta que deseja usar no catálogo de contas existente.

Selecione **[!UICONTROL Próximo]** para continuar.

![A interface de conta existente que exibe uma lista das contas existentes.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL SQL Server] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
