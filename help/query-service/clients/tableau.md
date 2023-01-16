---
keywords: Experience Platform, home, tópicos populares, tableau, Tableau, serviço de consulta, serviço de consulta, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Tableau ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Tableau ao Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 1d71cc4336747eb258ec2d8dcdc545cb2233692d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] para Serviço de Consulta

Este documento fornece informações para conexão [!DNL Tableau] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL Tableau] e estão familiarizados com como navegar em sua interface. Mais informações sobre [!DNL Tableau] podem ser encontradas no [funcionário [!DNL Tableau] documentação](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instruções sobre como [conectar-se a um servidor PostgreSQL com Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) estão disponíveis no site oficial do Tableau. Quando a caixa de diálogo para configurações de conexão for exibida, insira suas credenciais da plataforma nos campos de parâmetro para se conectar ao Adobe Experience Platform. Uma lista dos parâmetros de conexão necessários está listada abaixo.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!DNL Server]** | O endereço do local de armazenamento SFTP. Use o valor do seu Experience Platform **[!UICONTROL Host]** credencial. |
| **[!DNL Port]:** | A porta para [!DNL Query Service]. Você deve usar a porta **80º** ou **5432** para conectar-se com [!DNL Query Service]. |
| **[!DNL Database]** | Os bancos de dados que você deseja acessar. Use o valor do seu Experience Platform **[!UICONTROL Banco de dados]** credencial: `prod:all`. |
| **[!DNL Authentication]:** | Seu método escolhido para comprovar a identidade do usuário. É recomendável selecionar [!DNL Username and Password] nas opções disponíveis do menu suspenso. |
| **[!DNL Username]** | Esta é a ID da organização da plataforma. Use o valor do seu Experience Platform **[!UICONTROL Nome do usuário]** credencial. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais que não estejam expirando, esse valor será o argumento concatenado da variável `technicalAccountID` e `credential` baixado no arquivo JSON de configuração. O valor da senha assume o formulário: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais que não expiram é um download único durante a inicialização que o Adobe não mantém uma cópia. |

Para obter mais informações sobre como encontrar seu nome de usuário, senha e credenciais de logon, leia o [guia de credenciais](../ui/credentials.md). Para localizar suas credenciais, faça logon em [!DNL Platform], em seguida selecione **[!UICONTROL Queries]**, seguida de **[!UICONTROL Credenciais]**.

Verifique se você marcou a **[!UICONTROL Exigir SSL]** antes de tentar se conectar. Consulte a [Documentação dos modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros com o Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação no[`FLATTEN` recurso](../best-practices/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao se conectar a um banco de dados.

Após preencher todas as suas credenciais, confirme as configurações para continuar. Agora você está conectado ao Adobe Experience Platform.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar [!DNL Tableau] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o guia em [execução de consultas](../best-practices/writing-queries.md).
