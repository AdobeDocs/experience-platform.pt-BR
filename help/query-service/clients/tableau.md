---
keywords: Experience Platform;página inicial;tópicos populares;tableau;Tableau;serviço de consulta;serviço de consulta;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Tableau ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Tableau ao Serviço de consulta da Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Conectar [!DNL Tableau] para o Serviço de consulta

Este documento fornece informações para conexão [!DNL Tableau] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Tableau] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Tableau] pode ser encontrado no [oficial [!DNL Tableau] documentação](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instruções sobre como [conectar-se a um servidor PostgreSQL com Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) estão disponíveis no site oficial do Tableau. Quando a caixa de diálogo para configurações de conexão for exibida, insira suas credenciais da Platform nos campos de parâmetro para se conectar com o Adobe Experience Platform. Uma lista dos parâmetros de conexão necessários está listada abaixo.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Server]** | O endereço do local de armazenamento SFTP. Use o valor do seu Experience Platform **[!UICONTROL Host]** credencial. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!DNL Database]** | Os bancos de dados que você deseja acessar. Use o valor do seu Experience Platform **[!UICONTROL Banco de dados]** credencial: `prod:all`. |
| **[!DNL Authentication]:** | O método escolhido para comprovar a identidade do usuário. É recomendável selecionar [!DNL Username and Password] nas opções disponíveis do menu suspenso. |
| **[!DNL Username]** | Esta é a sua ID da organização da Platform. Use o valor do seu Experience Platform **[!UICONTROL Nome de usuário]** credencial. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais sem expiração, esse valor será os argumentos concatenados do `technicalAccountID` e a variável `credential` baixado no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual o Adobe não mantém uma cópia. |

Para obter mais informações sobre como localizar seu nome de usuário, senha e credenciais de login, leia a [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon no [!DNL Platform]e selecione **[!UICONTROL Consultas]**, seguido por **[!UICONTROL Credenciais]**.

Verifique se você marcou a opção **[!UICONTROL Exigir SSL]** antes de tentar se conectar. Consulte a [Documentação de modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação no[`FLATTEN` recurso](../key-concepts/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao conectar-se a um banco de dados.

Depois de preencher todas as credenciais, confirme as configurações para continuar. Agora você se conectou ao Adobe Experience Platform.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], você pode usar [!DNL Tableau] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o manual no [execução de consultas](../best-practices/writing-queries.md).
