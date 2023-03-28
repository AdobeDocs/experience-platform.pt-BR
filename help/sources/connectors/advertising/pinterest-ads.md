---
keywords: Experience Platform; home; tópicos populares; Pinterest Ads;
title: Visão geral da fonte de anúncios do pinterest
description: Saiba como conectar Pinterest Ads ao Adobe Experience Platform usando APIs ou a interface do usuário.
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>O [!DNL Pinterest Ads] A fonte está em beta. Leia o [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um sistema de publicidade de terceiros. O suporte para provedores de publicidade inclui [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) O é um mecanismo de descoberta visual para encontrar receitas, decoração doméstica, inspiração de estilo e outras ideias em toda a Web. Eles são apresentados em pequena escala usando imagens, GIF animados e vídeos no formato de pinboard. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) permite que você expanda sua empresa e alcance 400 milhões de pessoas usando [!DNL Pinterest].

Com [!DNL Pinterest Ads], você pode alcançar os usuários por meio de anúncios direcionados para descobrir e comprar seus produtos. Pinos de [!DNL Pinterest Ads] são patrocinadas para receber exposição extra em resultados de pesquisa relevantes. Usuários inscritos em [!DNL Pinterest Business] O pode optar por promover os pinos de melhor desempenho existentes, criar uma nova imagem ou vídeo ou até mesmo promover uma imagem que tenha sido fixada em um site. [!DNL Pinterest Ads] O oferece vários formatos de publicidade para ajudar você a atingir suas metas específicas de campanha.

## [!DNL Pinterest] APIs {#pinterest-apis}

O [!DNL Pinterest Ads] a fonte usa o [!DNL Pinterest] APIs para recuperar [!DNL Pinterest Ads] , juntamente com todo o desempenho e métricas. Os endpoints de API compatíveis são:

* [Análise de campanha](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análise do grupo de anúncios](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Análise de anúncios](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Use o [!DNL Pinterest Ads] fonte para trazer seus dados de [!DNL Pinterest] para o Experience Platform, onde é possível executar análises de dados. Os dados são retornados a partir da data de assimilação para um intervalo pré-datado de 90 dias. [!DNL Pinterest Ads] O usa os tokens do portador como um mecanismo de autenticação para se comunicar com o [!DNL Pinterest] APIs.

## Pré-requisitos {#prerequisites}

A primeira etapa na criação de um [!DNL Pinterest Ads] a conexão de origem é garantir que você tenha uma conta de desenvolvedor do Pinterest. Se você ainda não tiver um, visite o [inscrever-se](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) para registrar e criar sua conta.

### Configuração [!DNL Pinterest] aplicativo e gerar token de acesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>É recomendável usar a variável [!DNL Pinterest] As APIs para gerar seu token de acesso, pois a geração do token de acesso na interface do usuário fornece um acesso limitado. Por meio da interface do usuário, você só poderá acessar os seguintes escopos: `pins:read`, `boards:read` e `user_accounts:read`. Essa limitação não é adequada para uso com os endpoints de análise do [!DNL Pinterest] API.

Para gerar seu token de acesso, leia a [!DNL Pinterest] guias em [configuração do seu aplicativo](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticação usando o OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Obter credenciais necessárias {#gather-required-credentials}

Para se conectar [!DNL Pinterest Ads] para Plataforma, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| Token de acesso | O [!DNL Pinterest Ads] token de acesso para sua conta de usuário. A conta de usuário do token deve ser o proprietário do [!DNL Pinterest Ad] ou ter uma das funções necessárias concedidas a eles por meio do Business Access: Administrador, analista ou gerente de campanha. Para obter mais informações sobre o token de acesso, consulte o [[!DNL Pinterest] guia sobre como gerar seu token de acesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID da conta do anúncio | Os [!DNL Pinterest Ads] ID da conta do anúncio para a unidade comercial. Para obter informações sobre como recuperar a ID da conta do anúncio. Visite o [[!DNL Pinterest] guia sobre encontrar IDs no Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campanha, grupo de publicidade ou ID de publicidade | O `campaign`, `ad group`ou `ad` IDs que correspondem à ID da conta de publicidade. Para obter as IDs necessárias, navegue até o [!DNL Pinterest] página para **Hub de negócios da pinterest** > **Resumo da conta do anúncio** > **Campanhas** / **Grupos de anúncios** / **Anúncios** e copie as IDs necessárias mencionadas logo abaixo de cada um de seus nomes. |

>[!NOTE]
>
>O [!DNL Pinterest] A API fornece APIs individuais para recuperar dados associados a cada ID. Dessa forma, é necessário transmitir somente as IDs correspondentes para o tipo de ID em que você está interessado.

## Medidas de proteção {#guardrails}

As seções a seguir fornecem informações sobre medidas de proteção de dados para [!DNL Pinterest].

### [!DNL Pinterest] intervalo de datas {#pinterest-date-range}

O [!DNL Pinterest] A API suporta `start_date` e um `end_date` para recuperar os dados do analytics entre um determinado intervalo de datas.

* O `start_date` não pode ser superior a 90 dias antes da data atual.
* O `end_date` não pode ser superior a 90 dias após a `start_date`.

Ao agendar seu fluxo de dados, você deve definir uma das seguintes configurações de frequência e intervalo:

| Frequência | Intervalo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por exemplo, se a assimilação estiver definida em 15 de março de 2023 com uma configuração de frequência e intervalo configurada para `Day=1` ou `Hour=24`, em seguida, o [!DNL Pinterest] A API recuperaria apenas dados de até 15 de dezembro de 2022, pois o cálculo é pré-datado por 90 dias.

### [!DNL Pinterest] intervalo de tempo {#pinterest-time-range}

O [!DNL Pinterest] A API suporta diferentes tipos de granularidade de tempo para como os dados podem ser recuperados:

| Granularidade de tempo | Descrição |
| --- | --- |
| **TOTAL** | As métricas de dados são agregadas em um intervalo de datas especificado. |
| **DIA** | As métricas de dados são analisadas diariamente. |
| **HORA** | As métricas de dados são analisadas a cada hora. |
| **SEMANAL** | As métricas de dados são analisadas semanalmente. |
| **MENSAL** | As métricas de dados são divididas mensalmente. |

Para Platform, a variável [!DNL Pinterest Ads] a origem está configurada internamente para `Day`, o que significa que os dados serão agregados diariamente. Por exemplo, usando `impressions recorded` como uma métrica, já que a granularidade é configurada como uma `DAY`, você obteria `xx` impressões em `day 1`, `yy` impressões em `day 2` e assim por diante.

>[!IMPORTANT]
>
>O pinterest impõe um limite de taxa de 1.000 chamadas de API diariamente em sua API para ler informações de anúncios, grupos de anúncios ou campanhas de anúncios. Para obter informações sobre limites de taxa aplicáveis a chamadas de API subjacentes, consulte [[!DNL Pinterest] documentação sobre limites de taxa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connect [!DNL Pinterest Ads] para a plataforma {#connect-to-platform}

A documentação abaixo fornece informações sobre como se conectar [!DNL Pinterest Ads] para Plataforma usando APIs ou a interface do usuário:

### Connect [!DNL Pinterest Ads] para Plataforma usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão base do Pinterest usando a API do Serviço de fluxo](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorar tabelas de dados usando a API do Serviço de fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de publicidade usando a API do Serviço de fluxo](../../tutorials/api/collect/advertising.md)

### Connect [!DNL Pinterest Ads] para Plataforma usando a interface do usuário {#connect-to-platform-using-ui}

* [Criar uma conexão de origem do Pinterest na interface do usuário](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Criar um fluxo de dados para uma conexão de fonte de publicidade na interface do usuário](../../tutorials/ui/dataflow/advertising.md)
