---
title: A conexão Trade Desk - CRM
description: Ative perfis para sua conta da Trade Desk para direcionamento e supressão de público com base nos dados do CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 5%

---

# A conexão [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Com o lançamento da EUID (European Unified ID), você verá agora dois destinos do [!DNL The Trade Desk - CRM] no [catálogo de destinos](/help/destinations/catalog/overview.md).
>
>* Se seus dados se originarem da UE, use o destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Se seus dados se originarem das regiões da Ásia-Pacífico ou América do Norte, use o destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe *[!DNL Trade Desk]*. Para qualquer consulta ou solicitação de atualização, contate o representante do [!DNL Trade Desk].

## Visão geral {#overview}

Entenda como você pode ativar perfis para sua conta do [!DNL Trade Desk] para direcionamento e supressão de público com base nos dados do CRM.

Este conector envia dados para o ponto de extremidade primário [!DNL The Trade Desk]. A integração entre o Adobe Experience Platform e o [!DNL The Trade Desk] não oferece suporte à exportação de dados para o ponto de extremidade de terceiros [!DNL The Trade Desk].

O [!DNL The Trade Desk(TTD)] não lida diretamente com o arquivo de carregamento de endereços de email a qualquer momento, nem armazena seus emails brutos (sem hash).[!DNL The Trade Desk]

>[!TIP]
>
>Use os destinos do CRM [!DNL The Trade Desk] para o mapeamento de dados do CRM, como email ou endereço de email com hash. Use o [outro destino da Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) no catálogo do Adobe Experience Platform para cookies e mapeamentos de ID de dispositivo.

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Antes de poder ativar públicos para a Trade Desk, você deve entrar em contato com o gerente de conta do [!DNL Trade Desk] para assinar o contrato de integração do CRM. O [!DNL The Trade Desk] habilitará o uso de UID2/EUID e compartilhará outros detalhes para ajudá-lo a configurar seu destino.

## Requisitos de correspondência de ID {#id-matching-requirements}

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes. Leia a [visão geral do Namespace de Identidade](/help/identity-service/features/namespaces.md) para obter mais informações.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções na seção Requisitos de correspondência de ID e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | Endereços de email (texto não criptografado) | Insira `email` como identidade de destino quando sua identidade de origem for um atributo ou namespace de email. |
| Email_LC_SHA256 | Os endereços de email precisam ser transformados em hash usando SHA256 e em minúsculas. Você não poderá alterar essa configuração posteriormente. | Insira `hashed_email` como identidade de destino quando sua identidade de origem for um namespace ou atributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisitos de hash de email {#hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email brutos.

Para saber mais sobre como assimilar endereços de email no Experience Platform, leia a [visão geral de assimilação em lote](/help/ingestion/batch-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Remova espaços à esquerda e à direita.
* Converta todos os caracteres ASCII em minúsculas.
* Em `gmail.com` endereços de email, remova os seguintes caracteres da parte do nome de usuário do endereço de email:
   * O ponto (. (código ASCII 46). Por exemplo, normalize `jane.doe@gmail.com` para `janedoe@gmail.com`.
   * O sinal de mais (+ (código ASCII 43)) e todos os caracteres subsequentes. Por exemplo, normalize `janedoe+home@gmail.com` para `janedoe@gmail.com`.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (email ou email com hash) usados no destino da Trade Desk. |
| Frequência de exportação | **[!UICONTROL Daily Batch]** | Como um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o perfil (identidades) é atualizado uma vez por dia downstream para a plataforma de destino. Leia mais sobre [exportações de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

### Autenticar no destino {#authenticate}

O Destino do CRM [!DNL The Trade Desk] é um carregamento diário de arquivo em lotes e não requer autenticação do usuário.

### Preencher Detalhes do Destino {#fill-in-details}

Antes de enviar ou ativar dados de público-alvo para um destino, você deve configurar uma conexão com sua própria plataforma de destino. Ao [configurar](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=pt-BR) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Account Type]**: Escolha a opção **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Advertiser ID]**: seu [!DNL Trade Desk Advertiser ID], que pode ser compartilhado pelo seu Gerente de Conta do [!DNL Trade Desk] ou ser encontrado em [!DNL Advertiser Preferences] na interface do usuário do [!DNL Trade Desk].

![Captura de tela da interface do Experience Platform mostrando como preencher os detalhes do destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Ao se conectar ao destino, definir uma política de governança de dados é totalmente opcional. Revise a [visão geral da governança de dados](/help/data-governance/policies/overview.md) da Experience Platform para obter mais detalhes.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para um destino.

Na página **[!UICONTROL Scheduling]**, é possível configurar o agendamento e os nomes de arquivo para cada público-alvo que você está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

![Captura de tela da interface do Experience Platform para agendar a ativação de públicos-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todos os públicos-alvo ativados para o Destino do CRM [!DNL The Trade Desk] são definidos automaticamente para uma frequência diária e uma exportação de arquivo completa.

![Captura de tela da interface do Experience Platform para agendar a ativação de públicos-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Na página **[!UICONTROL Mapping]**, você deve selecionar atributos ou namespaces de identidade na coluna de origem e mapear para a coluna de destino.

![Captura de tela da interface do Experience Platform para mapear a ativação de público-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Veja abaixo um exemplo de mapeamento de identidade correto ao ativar públicos para o destino do CRM [!DNL The Trade Desk].

>[!IMPORTANT]
>
> O Destino do CRM [!DNL The Trade Desk] não aceita endereços de email brutos e com hash como identidades no mesmo fluxo de ativação. Crie fluxos de ativação separados para endereços de email brutos e com hash.

Selecionar campos de origem:

* Selecione o namespace ou atributo `Email` como identidade de origem se estiver usando o endereço de email bruto na assimilação de dados.
* Selecione o namespace ou atributo `Email_LC_SHA256` como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados na Experience Platform.

Selecionar campos de destino:

* Insira `email` como identidade de destino quando o namespace ou atributo de origem for `Email`.
* Insira `hashed_email` como identidade de destino quando o namespace ou atributo de origem for `Email_LC_SHA256`.

## Validar exportação de dados {#validate}

Para validar se os dados foram exportados corretamente do Experience Platform para o [!DNL The Trade Desk], localize os públicos-alvo no bloco de dados Adobe 1PD na Plataforma de Gerenciamento de Dados (DMP) do [!DNL The Trade Desk]. Estas são as etapas para encontrar a ID correspondente na interface do usuário do [!DNL Trade Desk]:

1. Primeiro, selecione a guia **[!UICONTROL Data]** e revise a seção **[!UICONTROL First-Party]**.
2. Role a página para baixo, em **[!UICONTROL Imported Data]**, você encontrará a **[!UICONTROL Adobe 1PD Tile]**.
3. Clique no bloco **[!UICONTROL Adobe 1PD]** e ele listará todos os públicos ativados para o destino [!DNL Trade Desk] do seu anunciante. Você também pode usar a função de pesquisa.
4. O Nº de ID de segmento do Experience Platform será exibido como o Nome do segmento na interface do usuário do [!DNL Trade Desk].

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).
