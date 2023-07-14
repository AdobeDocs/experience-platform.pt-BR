---
keywords: móvel;destino do engajamento móvel;LINE;destino do engajamento móvel LINE
title: Conexão LINE
description: O destino LINE permite adicionar perfis ao público-alvo da Platform e fornecer experiências personalizadas aos usuários conectados.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# [!DNL LINE] conexão

## Visão geral {#overview}

[[!DNL LINE]](https://line.me/en/) O é uma plataforma de comunicação popular que conecta pessoas, serviços e informações e cresceu de um aplicativo de bate-papo para um centro de atividades sociais, diárias, de entretenimento.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL LINE] API de mensagens](https://developers.line.biz/en/reference/messaging-api/). Você pode ativar perfis dos públicos-alvo do Experience Platform como conexões no [!DNL LINE] para as necessidades da sua empresa.

[!DNL LINE] O usa Tokens de portador como mecanismo de autenticação para se comunicar com o [!DNL LINE] API de mensagens. Instruções para autenticar em seu [!DNL LINE] instância estão mais abaixo, dentro de [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode direcionar usuários em um destino de engajamento móvel, com públicos-alvo integrados [!DNL Adobe Experience Platform]. Além disso, você pode fornecer experiências personalizadas para eles, com base nos atributos deles [!DNL Adobe Experience Platform] perfis, assim que públicos-alvo e perfis forem atualizados no [!DNL Adobe Experience Platform].

## Pré-requisitos {#prerequisites}

### [!DNL LINE] pré-requisitos {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL LINE], para exportar dados da Platform para o seu [!DNL LINE] conta:

#### Você precisa ter um [!DNL LINE] account {#prerequisites-account}

É necessário registrar-se e criar um [!DNL LINE] conta, se você ainda não tiver uma. Para criar uma conta:

1. Navegue até a [!DNL LINE] [logon na conta](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) página
2. Selecionar **[!UICONTROL Criar uma conta]**.

#### Obtenha os [!DNL LINE channel access token (long-lived)] do [!DNL LINE] console do desenvolvedor {#gather-credentials}

Para permitir que a Platform acesse [!DNL LINE] recursos, você precisará do *[!DNL Channel access token (long-lived)]* do desejado [!DNL LINE] *API de mensagens* canal.

1. Faça logon com o [!DNL LINE] para a conta [[!DNL LINE] Console do desenvolvedor](https://developers.line.biz/console).
1. Em seguida, acesse o *[!DNL Providers]* e selecione a variável *[!DNL Provider]* de interesse e, por fim, selecione o *API de mensagens* para acessar as configurações. Se você estiver acessando o console do desenvolvedor pela primeira vez, siga as [[!DNL LINE] documentação](https://developers.line.biz/en/docs/messaging-api/getting-started/) para concluir as etapas necessárias para criar um provedor.
1. Por fim, navegue até o ***[!DNL Channel access token]*** e copie a ***[!DNL Channel access token (long-lived)]*** valor obrigatório em [Autenticar para destino](#authenticate) etapa.

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Seu [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulte a [[!DNL LINE] documentação](https://developers.line.biz/en/docs/messaging-api/getting-started/) para obter orientação sobre como criar um canal ou adicionar um canal ao seu existente [!DNL LINE] conta por meio da [!DNL LINE] console de desenvolvedores.

## Identidades suportadas {#supported-identities}

[!DNL LINE] O oferece suporte à atualização e exportação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| ID para anunciantes (IFAs) | Selecione a ID da identidade de destino de anunciantes (IFAs) quando as identidades de origem forem IFA *(Apple ID para anunciantes)* ou namespaces GAID *(Google Advertising ID). |
| IDs de usuário LINE | Selecione a identidade de destino da ID de usuário quando as identidades de origem forem IDs de usuário LINE. |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no [!DNL LINE] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar [!DNL LINE]. Como alternativa, você pode localizá-lo na **[!UICONTROL Engajamento móvel]** categoria.

### Autenticar para destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Preencha os campos obrigatórios abaixo.
* **[!UICONTROL Token de portador]**: Seu [!DNL LINE Channel access token (long-lived)] do [!DNL LINE] console do desenvolvedor. Consulte a [coletar credenciais](#gather-credentials) seção.

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Tipo de público-alvo]**: Selecionar **[!UICONTROL ID para anunciantes (IFAs)]** se as identidades que você deseja exportar forem do tipo *ID para anunciantes (IFAs)*. Selecionar **[!UICONTROL IDs de usuário LINE]** se as identidades que você deseja exportar forem do tipo *IDs de usuário LINE*. Consulte a [Identidades suportadas](#supported-identities) para obter mais informações sobre os tipos de identidade.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos e identidades {#map}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL LINE] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino. Para mapear corretamente os campos XDM para o [!DNL LINE] campos de destino, siga estas etapas:

Dependendo da sua identidade de origem, os seguintes namespaces de identidade de destino devem ser mapeados: | Identidade do público alvo | Campo de origem | Campo de destino | | — | — | — | | ID para anunciantes (IFAs) | `IDFA` ou `GAID` | `LineId` | | IDs de usuário do LINE | `UserID` | `LineId` |

Se suas identidades de público-alvo forem *IDs de usuário LINE* você precisará do seguinte:
![Exemplo de captura de tela da interface do usuário da plataforma mostrando o Target mapping ao usar IDs de usuário LINE para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Se sua identidade de público alvo for *ID para anunciantes (IFAs)* você precisará do seguinte:
![Exemplo de captura de tela da interface do usuário da plataforma mostrando o mapeamento do Target ao usar ID para anunciantes (IFAs) para identidades de destino.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validar exportação de dados {#exported-data}

Após uma exportação de dados bem-sucedida fora do Experience Platform, a variável [!DNL LINE] o destino cria um novo público-alvo no [!DNL LINE] usando o nome de público-alvo selecionado.

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Entrada [!DNL LINE], faça logon na [Console do gerenciador](https://manager.line.biz/).

1. Em seguida, acesse **[!UICONTROL Controles de dados]** > **[!UICONTROL Públicos-alvo]** e verifique o nome correspondente ao público selecionado na variável **[!UICONTROL Nome do público]** coluna.

1. O volume atualizado corresponderia à contagem no segmento.

1. A variável *Tipo* a coluna mencionará **[!UICONTROL UserID]** se as identidades exportadas forem do tipo *UserID*. Do Mesmo Modo, A *Tipo* a coluna mencionará **[!UICONTROL ID de anúncio móvel]** se as identidades exportadas forem do tipo *IDFA*.

Um exemplo de configuração em [!DNL LINE] é mostrado abaixo:
![Captura de tela da interface do usuário LINE mostrando o volume de público-alvo.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
