---
title: Visão geral da origem do RainFocus
description: Saiba como transferir dados de gestão de eventos e análise da sua conta RainFocus para o Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 6%

---

# [!DNL RainFocus]

>[!NOTE]
>
>A variável [!DNL RainFocus] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

[!DNL RainFocus] O é uma plataforma que você pode usar para promover seus eventos e criar seus públicos. Você pode usar [!DNL RainFocus] para criar belas páginas promocionais, rastrear o desempenho da campanha e otimizar as conversões de registro.

Use o [!DNL RainFocus] fonte no Adobe Experience Platform e no Real-time Customer Data Platform para enriquecer automaticamente seus perfis de dados do cliente com eventos de experiência do participante em tempo real. Depois de ativados, os eventos de experiência são transmitidos automaticamente para o Real-Time CDP, permitindo uma poderosa segmentação de público, análise de dados e ativação da jornada de participantes com destinos e aplicativos downstream, como Customer Journey Analytics e Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Esse conector de origem e a página de documentação são criados e mantidos pelo [!DNL RainFocus] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente com o atendimento ao cliente<span>@rainfocus.com ou visite o [[!DNL RainFocus] Centro de ajuda](https://help.rainfocus.com/hc/en-us)

## Pré-requisitos

Você deve concluir os seguintes pré-requisitos para poder ativar o [!DNL RainFocus] integração no Experience Platform:

[Criar uma conta de serviço da Adobe (JWT) no portal do Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>O Adobe anunciou recentemente a desativação de tokens JWT em favor do OAuth. Para acomodar essa alteração, a variável [!DNL RainFocus] A origem migrará para OAuth em breve.

### Coletar credenciais necessárias

Para se conectar [!DNL RainFocus] para Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão em [!DNL RainFocus]:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID do cliente | A ID do cliente pode ser obtida da conta de serviço da Adobe no Adobe Developer Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Segredo do cliente | O segredo do cliente pode ser obtido na conta de serviço da Adobe no Adobe Developer Portal. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID da conta técnica | A ID da conta técnica pode ser obtida da conta de serviço da Adobe no Adobe Developer Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID da organização | A ID da organização pode ser obtida da conta de serviço da Adobe no portal do Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Criar um esquema XDM e definir o campo de identidade {#create-an-xdm-schema-and-define-the-identity-field}

Para armazenar os eventos de experiência do [!DNL RainFocus] no Experience Platform, você deve criar um esquema do Experience Data Model (XDM) para descrever um conjunto de dados que pode armazenar os possíveis campos e tipos de dados que serão enviados do [!DNL RainFocus].

[!DNL RainFocus] A recomenda os seguintes campos, que abrangem todos os dados possíveis enviados por padrão.

Os seguintes grupos de campos também são recomendados (indicados pelo prefixo ):

* Participante
* Expositor
* Cliente potencial
* Session
* HoraSessão

**O schema deve conter os seguintes campos:**

| Campo | Tipo | Exemplo | Descrição |
| --- | --- | --- | --- |
| `attendee.registered` | String | Sim | Um sinalizador que determina se o participante deve ser registrado. |
| `attendee.attendeeId` | String | 1619119968857001fvLB | A ID do participante em [!DNL RainFocus]. |
| `attendee.externalId` | String | 1666809456617001wyPj | A ID externa especificada por uma organização. |
| `attendee.clientId` | String | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | A ID do cliente SSO do participante. |
| `attendee.email` | String | usuário<span>@company.com | O endereço de email do participante. |
| `transmissionId` | String | 1680309557133001YHhz | Um identificador exclusivo usado para push de dados. |
| `eventType` | String | SessãoAgendada | O nome do Evento de Experiência do Participante. |
| `timestamp` | DateTime | 2023-04-01T00:41:57,000Z | O carimbo de data e hora do push de dados. |
| `event.name` | String | Adobe Summit 2023 | O nome do evento no qual uma transmissão ocorreu. |
| `exhibitor.exhibitorId` | String | 1680309557133001YHhz | A variável [!DNL RainFocus] identificador do exibidor. |
| `exhibitor.externalId` | String | 1666809514105001lSJN | O identificador do exibidor no sistema cliente. |
| `exhibitor.name` | String | IBM | O nome do expositor. |
| `lead.leadId` | String | 1666809456617001wyPj | A variável [!DNL RainFocus] identificador do cliente potencial. |
| `lead.note` | String | | |
| `session.sessionId` | String | 1666809373585001t4aV | A variável [!DNL RainFocus] identificador da sessão. |
| `session.externalId` | String | 1666809456617001wyPj | O identificador da sessão no sistema cliente. |
| `session.code` | String | GS3 | O código da sessão. |
| `session.title` | String | Palestra de inspiração | O título da sessão. |
| `session.length` | Número inteiro | 90 | A duração da sessão. |
| `sessiontime.sessiontimeId` | String | 1673033149739001OJLZ | A variável [!DNL RainFocus] identificador para o tempo da sessão. |
| `sessiontime.startTime` | String | 2023-03-22 10:00:00 | A hora de início da sessão. |
| `sessiontime.endTime` | String | 2023-03-22 10:00:00 | A hora final da sessão. |
| `sessiontime.room` | String | B32 | A sala usada para a sessão. |

{style="table-layout:auto"}

Para criar seu esquema para [!DNL RainFocus] , leia a documentação a seguir para obter as etapas sobre como criar um esquema usando APIs ou a interface do usuário.

* [Criar o esquema usando a interface](../../../xdm/tutorials/create-schema-ui.md)
* [Criar o esquema usando a API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* O esquema deve estender a variável **Classe XDM ExperienceEvent.**
>* Você deve garantir que o esquema inclua um **identidade principal**, e é **ativado para o Perfil**. Para obter mais informações, leia o guia em [definição de campos de identidade na interface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Você pode substituir o exemplo de identidade (Email) por outro identificador apropriado, como um email sha256 ou ECID.

### Criar um perfil de integração no RainFocus {#create-an-integration-profile-in-rainfocus}

Quando a conta de serviço e o esquema XDM estiverem prontos, você poderá ativar o [!DNL Integration Profile] por meio da [!DNL RainFocus] plataforma. A variável [!DNL Integration Profile] O é responsável pela transmissão de dados para o Experience Platform.

Faça logon na [[!DNL RainFocus] platform](https://app.rainfocus.com). Na navegação principal, selecione **[!DNL Libraries]** e selecione **[!DNL Integration Profiles]**

![A interface do usuário RainFocus com bibliotecas e perfis de integração selecionados.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Para criar um novo perfil, selecione **(`+`)** ícone. Em seguida, selecione **Adobe Real-time Customer Data Platform** e selecione **OK**.

![A janela Criar perfil de integração na interface do usuário do RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Em seguida, forneça as credenciais recuperadas no Projeto do portal do Adobe Developer:

* **ID do cliente**
* **Segredo do cliente**
* **ID da conta técnica**
* **ID da organização**

Após fornecer as credenciais, selecione **[!DNL Save]**. Agora você deve ver o novo [!DNL Integration Profile] listado na [!DNL RainFocus] painel.

Selecione o [!DNL Integration Profile] que você acabou de criar para ver uma lista de eventos **tipos de push** já está configurado. Estas são as [Eventos de experiência](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) que será enviado para o Experience Platform quando ocorrerem.

![Uma lista de tipos de push predefinidos no painel RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Para recuperar uma cópia da carga JSON de amostra, selecione **[!DNL Sample JSON Payload]**. Em seguida, destaque e copie a amostra de carga JSON e **salve-o em um novo arquivo com uma extensão .json**. Isso será usado posteriormente no Experience Platform para [configurações de mapeamento](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Uma amostra de carga JSON no painel RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**A instalação ainda não foi concluída**: depois que o fluxo de dados for criado, será necessário retornar para o [!DNL RainFocus] para concluir o [!DNL Integration Profile] fornecendo suas **URL do ponto de extremidade de transmissão** e **ID do fluxo de dados**.

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para transmitir dados de seu [!DNL RainFocus] conta para Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL RainFocus] para Experience Platform usando a interface do usuário](../../tutorials/ui/create/analytics/rainfocus.md).
