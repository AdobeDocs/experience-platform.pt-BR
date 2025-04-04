---
keywords: Experience Platform;página inicial;tópicos populares;tableau;Tableau;serviço de consulta;Serviço de consulta;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Tableau ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Tableau ao Serviço de consulta da Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Conectar [!DNL Tableau] ao Serviço de consulta

Este documento fornece informações para conectar [!DNL Tableau] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Tableau] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Tableau] podem ser encontradas na [documentação [!DNL Tableau] oficial](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

As instruções sobre como [conectar-se a um servidor PostgreSQL com Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) estão disponíveis no site oficial do Tableau. Quando a caixa de diálogo das configurações de conexão for exibida, digite suas credenciais do Experience Platform nos campos de parâmetros para se conectar com o Adobe Experience Platform. Uma lista dos parâmetros de conexão necessários está listada abaixo.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Server]** | O endereço do local de armazenamento SFTP. Use o valor da sua credencial do Experience Platform **[!UICONTROL Host]**. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!DNL Database]** | Os bancos de dados que você deseja acessar. Use o valor da credencial do Experience Platform **[!UICONTROL Banco de Dados]**: `prod:all`. |
| **[!DNL Authentication]:** | O método escolhido para comprovar a identidade do usuário. É recomendável selecionar [!DNL Username and Password] nas opções disponíveis do menu suspenso. |
| **[!DNL Username]** | Esta é a sua ID da organização da Experience Platform. Use o valor da credencial **[!UICONTROL Username]** do Experience Platform. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta sequência alfanumérica é a credencial **[!UICONTROL Senha]** da Experience Platform. Se você quiser usar credenciais sem expiração, esse valor serão os argumentos concatenados de `technicalAccountID` e `credential` baixados no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual a Adobe não mantém uma cópia. |

Para obter mais informações sobre como encontrar seu nome de usuário, senha e credenciais de logon, leia o [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon em [!DNL Experience Platform] e selecione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciais]**.

>[!IMPORTANT]
>
>Como usuário do Tableau ou do Power BI, você pode conectar o Customer Journey Analytics às suas ferramentas de BI na guia de credenciais do Serviço de consulta. Consulte a documentação de credenciais para obter instruções sobre como [conectar suas ferramentas de BI ao Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

Verifique se você marcou a caixa **[!UICONTROL Exigir SSL]** antes de tentar se conectar. Consulte a [documentação sobre modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação sobre o recurso [`FLATTEN`](../key-concepts/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao conectar-se a um banco de dados.

Depois de preencher todas as credenciais, confirme as configurações para continuar. Agora você se conectou ao Adobe Experience Platform.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], pode usar [!DNL Tableau] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o manual em [executando consultas](../best-practices/writing-queries.md).
