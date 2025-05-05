---
title: Visão geral da origem do RainFocus
description: Saiba como transferir dados de gestão de eventos e análise da sua conta RainFocus para o Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>A origem [!DNL RainFocus] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O [!DNL RainFocus] é uma plataforma que você pode usar para promover seus eventos e criar seus públicos. Você pode usar o [!DNL RainFocus] para criar belas páginas promocionais, acompanhar o desempenho da campanha e otimizar as conversões de registro.

Use a fonte [!DNL RainFocus] no Adobe Experience Platform e no Real-time Customer Data Platform para enriquecer automaticamente seus perfis de dados do cliente com eventos de experiência do participante em tempo real. Depois de ativados, os eventos de experiência são transmitidos automaticamente para o Real-Time CDP, permitindo uma poderosa segmentação de público, análise de dados e ativação da jornada de participantes com destinos e aplicativos downstream, como Customer Journey Analytics e Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Este conector de origem e página de documentação são criados e mantidos pela equipe [!DNL RainFocus]. Para fazer consultas ou solicitações de atualização, entre em contato diretamente com o clientcare<span>@rainfocus.com ou visite a [[!DNL RainFocus] Central de ajuda](https://help.rainfocus.com/hc/en-us)

## Pré-requisitos

Você deve atender aos seguintes pré-requisitos para ativar a integração do [!DNL RainFocus] no Experience Platform:

[Criar uma Conta de Serviço (JWT) da Adobe no Portal do Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>O Adobe anunciou recentemente a desativação de tokens JWT em favor do OAuth. Para acomodar essa alteração, a origem [!DNL RainFocus] será migrada para OAuth em breve.

### Coletar credenciais necessárias

Para conectar [!DNL RainFocus] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão em [!DNL RainFocus]:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID de cliente | A ID do cliente pode ser obtida da conta de serviço da Adobe no Adobe Developer Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Segredo do cliente | O segredo do cliente pode ser obtido na conta de serviço da Adobe no Adobe Developer Portal. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID da conta técnica | A ID da conta técnica pode ser obtida da conta de serviço da Adobe no Adobe Developer Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID da organização | A ID da organização pode ser obtida da conta de serviço da Adobe no portal do Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Criar um esquema XDM e definir o campo de identidade {#create-an-xdm-schema-and-define-the-identity-field}

Para armazenar os Eventos de Experiência de [!DNL RainFocus] no Experience Platform, você deve criar um esquema do Experience Data Model (XDM) para descrever um conjunto de dados que pode armazenar os possíveis campos e tipos de dados que serão enviados de [!DNL RainFocus].

O [!DNL RainFocus] recomenda os seguintes campos, que abrangem todos os dados possíveis enviados por padrão.

Os seguintes grupos de campos também são recomendados (indicados pelo prefixo ):

* Participante
* Expositor
* Lead
* Session
* HoraSessão

**O esquema deve conter os seguintes campos:**

| Campo | Tipo | Exemplo | Descrição |
| --- | --- | --- | --- |
| `attendee.registered` | String | Sim | Um sinalizador que determina se o participante deve ser registrado. |
| `attendee.attendeeId` | String | 1619119968857001fvLB | A ID de participante em [!DNL RainFocus]. |
| `attendee.externalId` | String | 1666809456617001wyPj | A ID externa especificada por uma organização. |
| `attendee.clientId` | String | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | A ID do cliente SSO do participante. |
| `attendee.email` | String | usuário<span>@company.com | O endereço de email do participante. |
| `transmissionId` | String | 1680309557133001YHhz | Um identificador exclusivo usado para push de dados. |
| `eventType` | String | SessãoAgendada | O nome do Evento de Experiência do Participante. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000Z | O carimbo de data e hora do push de dados. |
| `event.name` | String | Adobe Summit 2023 | O nome do evento no qual uma transmissão ocorreu. |
| `exhibitor.exhibitorId` | String | 1680309557133001YHhz | O identificador [!DNL RainFocus] do exibidor. |
| `exhibitor.externalId` | String | 1666809514105001lSJN | O identificador do exibidor no sistema cliente. |
| `exhibitor.name` | String | IBM | O nome do expositor. |
| `lead.leadId` | String | 1666809456617001wyPj | O identificador [!DNL RainFocus] do cliente potencial. |
| `lead.note` | String | | |
| `session.sessionId` | String | 1666809373585001t4aV | O identificador [!DNL RainFocus] da sessão. |
| `session.externalId` | String | 1666809456617001wyPj | O identificador da sessão no sistema cliente. |
| `session.code` | String | GS3 | O código da sessão. |
| `session.title` | String | Palestra de inspiração | O título da sessão. |
| `session.length` | Número inteiro | 90 | A duração da sessão. |
| `sessiontime.sessiontimeId` | String | 1673033149739001OJLZ | O identificador [!DNL RainFocus] para o tempo de sessão. |
| `sessiontime.startTime` | String | 22/03/2023 10:00:00 | A hora de início da sessão. |
| `sessiontime.endTime` | String | 22/03/2023 10:00:00 | A hora final da sessão. |
| `sessiontime.room` | String | B32 | A sala usada para a sessão. |

{style="table-layout:auto"}

Para criar seu esquema para dados do [!DNL RainFocus], leia a documentação a seguir para obter as etapas sobre como criar um esquema usando APIs ou a interface do usuário.

* [Criar o esquema usando a interface](../../../xdm/tutorials/create-schema-ui.md)
* [Criar o esquema usando a API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* O esquema deve estender a classe **XDM ExperienceEvent.**
>* Você deve garantir que o esquema inclua uma **identidade primária** e esteja **habilitado para o Perfil**. Para obter mais informações, leia o manual sobre [definição de campos de identidade na interface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=pt-BR)
>* Você pode substituir o exemplo de identidade (Email) por outro identificador apropriado, como um email sha256 ou ECID.

### Criar um perfil de integração no RainFocus {#create-an-integration-profile-in-rainfocus}

Quando a conta de serviço e o esquema XDM estiverem prontos, você poderá ativar o [!DNL Integration Profile] por meio da plataforma [!DNL RainFocus]. O [!DNL Integration Profile] é responsável pela transmissão de dados para o Experience Platform.

Faça logon na [[!DNL RainFocus] plataforma](https://app.rainfocus.com). Na navegação principal, selecione **[!DNL Libraries]** e, em seguida, **[!DNL Integration Profiles]**

![A interface do usuário RainFocus com Bibliotecas e Perfis de Integração selecionados.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Para criar um novo perfil, selecione o ícone **(`+`)**. Em seguida, selecione **Adobe Real-time Customer Data Platform** e **OK**.

![A janela Criar perfil de integração na interface do usuário do RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Em seguida, forneça as credenciais recuperadas no Projeto do portal do Adobe Developer:

* **ID do cliente**
* **Segredo do cliente**
* **ID da Conta Técnica**
* **ID da organização**

Depois que as credenciais forem fornecidas, selecione **[!DNL Save]**.Agora você deve ver o novo [!DNL Integration Profile] listado no painel [!DNL RainFocus].

Selecione o [!DNL Integration Profile] que você acabou de criar para ver uma lista de **tipos de push** predefinidos já configurados. Estes são os [Eventos de Experiência](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=pt-BR) que serão enviados para o Experience Platform quando ocorrerem.

![Uma lista de tipos de push predefinidos no painel RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Para recuperar uma cópia da carga JSON de amostra, selecione **[!DNL Sample JSON Payload]**. Em seguida, destaque e copie a amostra de carga JSON e **salve-a em um novo arquivo com uma extensão .json**. Isso será usado posteriormente no Experience Platform para [configurações de mapeamento](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Uma amostra de carga JSON no painel RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**A instalação ainda não foi concluída**: depois que o fluxo de dados for criado, você precisará retornar ao painel [!DNL RainFocus] para concluir o [!DNL Integration Profile] fornecendo a **URL do ponto de extremidade de streaming** e a **ID do fluxo de dados**.

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para transmitir dados da sua conta do [!DNL RainFocus] para o Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL RainFocus] ao Experience Platform usando a interface de usuário](../../tutorials/ui/create/analytics/rainfocus.md).
