---
title: Visão geral do Oracle NetSuite Source
description: Saiba como conectar o Oracle NetSuite ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2024-01-30T00:00:00Z
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 6%

---

# [!DNL Oracle NetSuite]

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de sistemas de automação de marketing de terceiros. O suporte para provedores de automação de marketing inclui [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) é um conjunto de gerenciamento de negócios baseado em nuvem que abrange soluções de ERP/financeiras, CRM e comércio eletrônico.

Você pode usar duas fontes diferentes para assimilar dados de [!DNL Oracle NetSuite] para o Experience Platform:

* Use a origem [!DNL Oracle NetSuite Activities] para assimilar dados de eventos.
* Use a fonte [!DNL Oracle NetSuite Entities] para assimilar dados de clientes e contatos.

Exiba a tabela a seguir para obter mais informações sobre as duas fontes [!DNL Oracle NetSuite].

| Fonte | Tipo | Descrição |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupere as atividades agendadas adicionadas ao seu calendário. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupere dados específicos do cliente, incluindo detalhes como nomes, endereços e identificadores-chave do cliente. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contato | Recupere nomes de contato, emails, números de telefone e quaisquer campos personalizados relacionados a contatos associados aos clientes. |

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-allow-list}

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes de trazer os dados do [!DNL Oracle NetSuite] para a Experience Platform, primeiro verifique se você tem o seguinte:

* **Uma conta [!DNL Oracle NetSuite]**.
   * Contate [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) se você ainda não tiver uma conta válida.
* Uma **assinatura ativa** para qualquer produto [!DNL Oracle NetSuite].
* Uma **ID de conta**.
   * A origem [!DNL Oracle NetSuite] usa OAuth 2.0 para se comunicar com as APIs [!DNL Oracle NetSuite]. Se você não tiver sua ID de conta, visite a documentação do [!DNL Oracle] em [como recuperar a ID de conta](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Uma combinação de **ID do cliente** e **segredo do cliente**.
   * A ID do cliente e o segredo do cliente são necessários para acessar as APIs [!DNL Oracle NetSuite]. Durante essa etapa, você também deve garantir que o administrador tenha:
      * Ativação do recurso OAuth 2.0 e configuração das funções OAuth 2.0 apropriadas.
      * Usuários atribuídos às funções OAuth 2.0 e registros de integração criados necessários.
* Um **token de acesso** e um **token de atualização**.
   * Consulte o guia [!DNL Oracle] em [Fluxo de Concessão de Código de Autorização OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) para obter informações sobre como gerar os tokens de acesso e atualização.

### Coletar credenciais necessárias {#gather-credentials}

Para conectar [!DNL Oracle NetSuite] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID de cliente | O valor da ID do cliente que é gerada quando você cria o registro de integração em [!DNL Oracle NetSuite]. Leia o guia [!DNL Oracle] sobre como [criar registros de integração](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obter mais informações. | `7fce.....b42f`<br>O valor é uma cadeia de 64 caracteres. |
| Segredo do cliente | O valor do segredo do cliente gerado ao criar o registro de integração. Leia o guia [!DNL Oracle] sobre como [criar registros de integração](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obter mais informações. | `5c98.....1b46`<br>O valor é uma cadeia de 64 caracteres. |
| URL de teste de autorização | (Opcional) Sua URL de teste de autorização [!DNL NetSuite]. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token de acesso | O token de acesso está no formato JSON Web Token (JWT) e é válido por apenas 60 minutos. Para obter mais informações sobre como recuperar o token de acesso, leia o guia do [!DNL Oracle] sobre a autorização do [OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> O valor é uma cadeia de 1024 caracteres formatada como JWT (JSON Web Token). |
| Atualizar token | Use a atualização para gerar um novo token de acesso, após a expiração do token de acesso. O token de atualização é válido por sete dias. Para obter mais informações sobre como recuperar o token de acesso, leia o guia do [!DNL Oracle] sobre a autorização do [OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> O valor é uma cadeia de 1024 caracteres formatada como JWT (JSON Web Token). |
| URL do token de acesso | O ponto de extremidade do token para o qual o aplicativo envia as solicitações de POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Depois que um token de atualização expirar, você deverá criar uma nova conta no Experience Platform com seus tokens atualizados.

## Conectar [!DNL Oracle NetSuite Activities] ao Experience Platform {#oracle-netsuite-activities}

A documentação abaixo fornece informações sobre como conectar o [!DNL Oracle NetSuite Activities] ao Experience Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL Oracle NetSuite Activities] dados para a Experience Platform usando APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Conecte sua conta [!DNL Oracle NetSuite Activities] à Experience Platform usando a interface](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).

## Conectar [!DNL Oracle NetSuite Entities] ao Experience Platform {#oracle-netsuite-entities}

A documentação abaixo fornece informações sobre como conectar o [!DNL Oracle NetSuite Entities] ao Experience Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL Oracle NetSuite Entities] dados para a Experience Platform usando APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Conecte sua conta [!DNL Oracle NetSuite Entities] à Experience Platform usando a interface](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).
