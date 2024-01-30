---
title: Visão geral da origem do Oracle NetSuite
description: Saiba como conectar o Oracle NetSuite ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>A variável [!DNL Oracle NetSuite] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de sistemas de automação de marketing de terceiros. O suporte para provedores de automação de marketing inclui [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) O é um pacote de gerenciamento de negócios baseado em nuvem que abrange soluções de ERP/financeiras, CRM e comércio eletrônico.

Você pode usar duas fontes diferentes para assimilar dados do [!DNL Oracle NetSuite] para Experience Platform:

* Use o [!DNL Oracle NetSuite Activities] fonte para assimilar dados de eventos.
* Use o [!DNL Oracle NetSuite Entities] fonte para assimilar dados do cliente e de contato.

Consulte a tabela a seguir para obter mais informações sobre os dois [!DNL Oracle NetSuite] fontes.

| Fonte | Tipo | Descrição |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupere as atividades agendadas adicionadas ao seu calendário. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupere dados específicos do cliente, incluindo detalhes como nomes, endereços e identificadores-chave do cliente. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contato | Recupere nomes de contato, emails, números de telefone e quaisquer campos personalizados relacionados a contatos associados aos clientes. |

## LISTA DE PERMISSÕES de endereço IP {#ip-allow-list}

Pode ser necessário adicionar uma lista de endereços IP a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes que você possa trazer seu [!DNL Oracle NetSuite] dados para o Experience Platform, você deve primeiro garantir que tenha o seguinte:

* **Um [!DNL Oracle NetSuite] account**.
   * Contato [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) se você ainda não tiver uma conta válida.
* Um **assinatura ativa** a qualquer [!DNL Oracle NetSuite] produto.
* Um **ID da conta**.
   * A variável [!DNL Oracle NetSuite] A fonte usa o OAuth 2.0 para se comunicar com o [!DNL Oracle NetSuite] APIs. Se você não tiver a ID da conta, visite o [!DNL Oracle] documentação sobre [como recuperar a ID da conta](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **ID do cliente** e **segredo do cliente** combinação.
   * A ID do cliente e o segredo do cliente são necessários para acessar o [!DNL Oracle NetSuite] APIs. Durante essa etapa, você também deve garantir que o administrador tenha:
      * Ativação do recurso OAuth 2.0 e configuração das funções OAuth 2.0 apropriadas.
      * Usuários atribuídos às funções OAuth 2.0 e registros de integração criados necessários.
* Um **token de acesso** e uma **atualizar token**.
   * Consulte a [!DNL Oracle] guia sobre [Fluxo de concessão de código de autorização OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) para obter informações sobre como gerar os tokens de acesso e atualização.

### Coletar credenciais necessárias {#gather-credentials}

Para se conectar [!DNL Oracle NetSuite] Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID do cliente | O valor da ID do cliente que é gerado ao criar o registro de integração no [!DNL Oracle NetSuite]. Leia o [!DNL Oracle] guia sobre como [criar registros de integração](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obter mais informações. | `7fce.....b42f`<br>O valor é uma cadeia de 64 caracteres. |
| Client secret | O valor do segredo do cliente gerado ao criar o registro de integração. Leia o [!DNL Oracle] guia sobre como [criar registros de integração](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obter mais informações. | `5c98.....1b46`<br>O valor é uma cadeia de 64 caracteres. |
| URL de teste de autorização | (Opcional) Seu [!DNL NetSuite] URL do teste de autorização. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token de acesso | O token de acesso está no formato JSON Web Token (JWT) e é válido por apenas 60 minutos. Para obter mais informações sobre como recuperar o token de acesso, leia a [!DNL Oracle] guia sobre [Autorização OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> O valor é uma string de 1024 caracteres formatada como um JSON Web Token (JWT). |
| Atualizar token | Use a atualização para gerar um novo token de acesso, após a expiração do token de acesso. O token de atualização é válido por sete dias. Para obter mais informações sobre como recuperar o token de acesso, leia a [!DNL Oracle] guia sobre [Autorização OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> O valor é uma string de 1024 caracteres formatada como um JSON Web Token (JWT). |
| URL do token de acesso | O ponto de extremidade do token para o qual o aplicativo envia as solicitações de POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Depois que um token de atualização expirar, você deverá criar uma nova conta no Experience Platform com seus tokens atualizados.

## Conectar [!DNL Oracle NetSuite Activities] para a Platform {#oracle-netsuite-activities}

A documentação abaixo fornece informações sobre como se conectar [!DNL Oracle NetSuite Activities] para a Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL Oracle NetSuite Activities] dados para a Platform usando APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Conecte seu [!DNL Oracle NetSuite Activities] conta para Experience Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).

## Conectar [!DNL Oracle NetSuite Entities] para a Platform {#oracle-netsuite-entities}

A documentação abaixo fornece informações sobre como se conectar [!DNL Oracle NetSuite Entities] para a Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL Oracle NetSuite Entities] dados para a Platform usando APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Conecte seu [!DNL Oracle NetSuite Entities] conta para Experience Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).
