---
keywords: móvel, destinos de envolvimento móvel, LINE, destino de envolvimento móvel LINE
title: Conexão LINE
description: O destino LINE permite adicionar perfis ao seu segmento da Platform e fornecer experiências personalizadas a usuários conectados.
source-git-commit: b15ad6339cb342d754e3a78e0d68b232a94a835e
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---


# [!DNL LINE] conexão

## Visão geral {#overview}

[[!DNL LINE]](https://line.me/en/) é uma plataforma de comunicação popular que conecta pessoas, serviços e informações e cresceu de um aplicativo de chat em um hub para atividades de entretenimento, sociais e diárias.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL LINE] API de mensagens](https://developers.line.biz/en/reference/messaging-api/). Você pode ativar perfis de seus segmentos do Experience Platform como conexões em [!DNL LINE] para as suas necessidades comerciais.

[!DNL LINE] O usa tokens de portador como mecanismo de autenticação para se comunicar com o [!DNL LINE] API de mensagens. Instruções para autenticação em seu [!DNL LINE] instâncias estão mais abaixo, dentro de [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como comerciante, você pode direcionar usuários em um destino de envolvimento móvel, com segmentos incorporados [!DNL Adobe Experience Platform]. Além disso, você pode fornecer experiências personalizadas a elas, com base em atributos de seus [!DNL Adobe Experience Platform] assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

## Pré-requisitos {#prerequisites}

### [!DNL LINE] pré-requisitos {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL LINE]para exportar dados da Platform para seu [!DNL LINE] conta:

#### Você precisa ter um [!DNL LINE] account {#prerequisites-account}

Você precisa se registrar e criar um [!DNL LINE] , se você ainda não tiver uma. Para criar uma conta:

1. Navegue até o [!DNL LINE] [logon da conta](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) página
2. Selecionar **[!UICONTROL Criar uma conta]**.

#### Colete a [!DNL LINE channel access token (long-lived)] do [!DNL LINE] console do desenvolvedor {#gather-credentials}

Para permitir que a Platform acesse [!DNL LINE] recursos, você precisará do *[!DNL Channel access token (long-lived)]* da [!DNL LINE] *API de mensagens* canal.

1. Faça logon com seu [!DNL LINE] para [[!DNL LINE] Console do desenvolvedor](https://developers.line.biz/console).
1. Em seguida, acesse o *[!DNL Providers]* e, em seguida, selecione a *[!DNL Provider]* de interesse e, por fim, selecione o *API de mensagens* para acessar suas configurações. Se você estiver acessando o console do desenvolvedor pela primeira vez, siga o [[!DNL LINE] documentação](https://developers.line.biz/en/docs/messaging-api/getting-started/) para concluir as etapas necessárias para criar um provedor.
1. Finalmente, navegue até a ***[!DNL Channel access token]*** e copie a ***[!DNL Channel access token (long-lived)]*** valor exigido em [Autenticar para destino](#authenticate) etapa.

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Seu [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulte a [[!DNL LINE] documentação](https://developers.line.biz/en/docs/messaging-api/getting-started/) para obter orientação sobre como criar um canal ou adicionar um canal ao seu [!DNL LINE] por meio da [!DNL LINE] console desenvolvedores.

## Identidades suportadas {#supported-identities}

[!DNL LINE] O suporta a atualização e exportação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| ID para anunciantes (IFAs) | Selecione a ID da identidade de destino dos anunciantes (IFAs) quando as identidades de origem forem IFA *(Apple ID para anunciantes)* ou GAID *(Google Advertising ID) namespaces. |
| IDs de usuário LINE | Selecione a identidade de destino UserID quando as identidades de origem forem IDs de usuário LINE. |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na [!DNL LINE] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL LINE]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL Engajamento móvel]** categoria .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**.
![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Preencha os campos obrigatórios abaixo.
* **[!UICONTROL Token de portador]**: Seu [!DNL LINE Channel access token (long-lived)] do [!DNL LINE] console do desenvolvedor. Consulte a [coletar credenciais](#gather-credentials) seção.

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** status com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Tipo de público-alvo]**: Selecionar **[!UICONTROL ID para anunciantes (IFAs)]** se as identidades que você deseja exportar forem do tipo *ID para anunciantes (IFAs)*. Selecionar **[!UICONTROL IDs de usuário LINE]** se as identidades que você deseja exportar forem do tipo *IDs de usuário LINE*. Consulte a [Identidades suportadas](#supported-identities) para obter mais informações sobre os tipos de identidade.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Mapear atributos e identidades {#map}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL LINE] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino. Para mapear corretamente os campos XDM para a variável [!DNL LINE] campos de destino, siga estas etapas:

Dependendo da sua identidade de origem, os seguintes namespace de identidade de destino devem ser mapeados: | Identidade do Target | Campo de origem | Campo de destino | | — | — | — | | ID para anunciantes (IFAs) | `IDFA` ou `GAID` | `LineId` | | IDs de usuário LINE | `UserID` | `LineId` |

Se as identidades de destino forem *IDs de usuário LINE* você precisará do seguinte:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Target mapping ao usar IDs de usuário LINE para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Se sua identidade de destino for *ID para anunciantes (IFAs)* você precisará do seguinte:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Target mapping ao usar ID para anunciantes (IFAs) para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validar exportação de dados {#exported-data}

Após uma exportação bem-sucedida de dados do Experience Platform, a [!DNL LINE] o destino cria um novo público-alvo no [!DNL LINE] usando o nome do segmento selecionado.

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Em [!DNL LINE], faça logon no [Console do gerenciador](https://manager.line.biz/).

1. Em seguida, navegue até **[!UICONTROL Controles de dados]** > **[!UICONTROL Públicos-alvo]** e verifique o nome que corresponde ao segmento selecionado no **[!UICONTROL Nome do público]** coluna.

1. O volume atualizado corresponderia à contagem no segmento.

1. O *Tipo* a coluna mencionará **[!UICONTROL UserID]** se as identidades que você exportou forem do tipo *UserID*. Da Mesma Forma, O *Tipo* a coluna mencionará **[!UICONTROL ID de anúncio móvel]** se as identidades que você exportou forem do tipo *IDFA*.

Uma configuração de exemplo em [!DNL LINE] é mostrado abaixo:
![Captura de tela da interface do usuário do LINE que mostra o volume do público-alvo.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).