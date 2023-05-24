---
keywords: Experience Platform;página inicial;tópicos populares;Pinterest Ads;
title: Visão geral da origem dos anúncios da pinterest
description: Saiba como conectar o Pinterest Ads ao Adobe Experience Platform usando APIs ou a interface do usuário.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>A variável [!DNL Pinterest Ads] a fonte está na versão beta. Leia o [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema de publicidade de terceiros. O suporte para provedores de publicidade inclui [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) O é um mecanismo de descoberta visual para encontrar receitas, decoração doméstica, inspiração de estilo e outras ideias na web. Eles são apresentados em pequena escala usando imagens, GIF animados e vídeos no formato pinboard. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) permite expandir sua empresa e alcançar 400 milhões de pessoas usando [!DNL Pinterest].

Com [!DNL Pinterest Ads], você pode alcançar os usuários por meio de anúncios direcionados para descobrir e comprar seus produtos. Fixar de [!DNL Pinterest Ads] são patrocinados para receber exposição extra em resultados de pesquisa relevantes. Usuários inscritos [!DNL Pinterest Business] O pode optar por promover pins de melhor desempenho existentes, criar uma nova imagem ou vídeo ou até mesmo promover uma imagem que foi fixada a partir de um site. [!DNL Pinterest Ads] O oferece vários formatos de anúncio para ajudar você a atingir suas metas específicas do campaign.

## [!DNL Pinterest] APIs {#pinterest-apis}

A variável [!DNL Pinterest Ads] a origem utiliza o [!DNL Pinterest] APIs para recuperar o [!DNL Pinterest Ads] dados, juntamente com todos os dados de desempenho e métricas. Os endpoints de API compatíveis são:

* [Análise de campanha](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análise de grupo de anúncios](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Anúncios do Analytics](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Use o [!DNL Pinterest Ads] fonte da qual seus dados serão transferidos [!DNL Pinterest] para Experience Platform, onde é possível executar a análise de dados. Os dados são retornados a partir da data de assimilação para um intervalo retroativo de 90 dias. [!DNL Pinterest Ads] O usa tokens de portador como um mecanismo de autenticação para se comunicar com a [!DNL Pinterest] APIs.

## Pré-requisitos {#prerequisites}

A primeira etapa na criação de um [!DNL Pinterest Ads] a conexão de origem é para garantir que você tenha uma conta de desenvolvedor do Pinterest. Se ainda não tiver um, visite o [inscrever-se](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) página para registrar e criar sua conta.

### Configuração [!DNL Pinterest] aplicativo e gerar token de acesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>É recomendável usar a variável [!DNL Pinterest] APIs para gerar o token de acesso, pois gerar o token de acesso na interface do usuário fornece um acesso limitado. Por meio da interface do usuário do, você só poderá acessar os seguintes escopos: `pins:read`, `boards:read` e `user_accounts:read`. Essa limitação não é adequada para uso com os endpoints de análise do [!DNL Pinterest] API.

Para gerar o token de acesso, leia o [!DNL Pinterest] guias sobre [configuração do seu aplicativo](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticação usando o OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Coletar credenciais necessárias {#gather-required-credentials}

Para se conectar [!DNL Pinterest Ads] Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| Token de acesso | A variável [!DNL Pinterest Ads] token de acesso para sua conta de usuário. A conta de usuário do token deve ser o proprietário do [!DNL Pinterest Ad] ou ter uma das funções necessárias concedidas a eles por meio do Business Access: Administrador, Analista ou Gerente de campanha. Para obter mais informações sobre o token de acesso, consulte o [[!DNL Pinterest] guia sobre como gerar seu token de acesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID da conta de anúncio | Os [!DNL Pinterest Ads] ID da conta de publicidade da sua unidade de negócios. Para obter informações sobre como recuperar a ID da conta de anúncio. Visite o [[!DNL Pinterest] guia sobre como encontrar IDs no Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campanha, grupo de publicidade ou ID de publicidade | A variável `campaign`, `ad group`ou `ad` IDs que correspondem à ID da conta de anúncio. Para obter as IDs necessárias, navegue até a [!DNL Pinterest] página para **Hub de negócios pinterest** > **Resumo da conta de anúncio** > **Campanhas** / **Grupos de anúncios** / **Anúncios** e copie as IDs necessárias mencionadas logo abaixo de cada um de seus nomes. |

>[!NOTE]
>
>A variável [!DNL Pinterest] A API fornece APIs individuais para recuperar dados associados a cada ID. Portanto, é necessário transmitir somente as IDs correspondentes ao tipo de ID em que você está interessado.

## Medidas de proteção {#guardrails}

As seções a seguir fornecem informações sobre as medidas de proteção de dados para [!DNL Pinterest].

### [!DNL Pinterest] intervalo de datas {#pinterest-date-range}

A variável [!DNL Pinterest] A API oferece suporte a uma `start_date` e uma `end_date` parâmetro para recuperar dados de análise entre um determinado intervalo de datas.

* A variável `start_date` não pode ser mais de 90 dias antes da data atual.
* A variável `end_date` não pode ser superior a 90 dias após a `start_date`.

Ao agendar seu fluxo de dados, você deve definir uma das seguintes configurações de frequência e intervalo:

| Frequência | Interval |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por exemplo, se a assimilação for definida em 15 de março de 2023 com uma configuração de frequência e intervalo definida como `Day=1` ou `Hour=24`, depois o [!DNL Pinterest] A API só recuperaria dados de até 15 de dezembro de 2022, pois o cálculo tem data retroativa de 90 dias.

### [!DNL Pinterest] intervalo de tempo {#pinterest-time-range}

A variável [!DNL Pinterest] A API oferece suporte a diferentes tipos de granularidade de tempo para como os dados podem ser recuperados:

| Granularidade de tempo | Descrição |
| --- | --- |
| **TOTAL** | As métricas de dados são agregadas em um intervalo de datas especificado. |
| **DIA** | As métricas de dados são detalhadas diariamente. |
| **HORA** | As métricas de dados são detalhadas de hora em hora. |
| **SEMANALMENTE** | As métricas de dados são detalhadas semanalmente. |
| **MENSAL** | As métricas de dados são detalhadas mensalmente. |

Para a Platform, a variável [!DNL Pinterest Ads] a origem está configurada internamente para `Day`, o que significa que os dados serão agregados diariamente. Por exemplo, usando `impressions recorded` como uma métrica, já que a granularidade é configurada como uma `DAY`, você obteria `xx` impressões em `day 1`, `yy` impressões em `day 2` e assim por diante.

>[!IMPORTANT]
>
>O pinterest impõe um limite de taxa de 1.000 chamadas de API diariamente em sua API para ler informações de anúncios, grupos de anúncios ou campanhas de anúncios. Para obter informações sobre limites de taxa aplicáveis às chamadas de API subjacentes, consulte o [[!DNL Pinterest] documentação sobre limites de taxa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Conectar [!DNL Pinterest Ads] para a Platform {#connect-to-platform}

A documentação abaixo fornece informações sobre como se conectar [!DNL Pinterest Ads] para a Platform usando APIs ou a interface do usuário:

### Conectar [!DNL Pinterest Ads] para a Platform usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão básica do Pinterest usando a API do serviço de fluxo](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de publicidade usando a API do serviço de fluxo](../../tutorials/api/collect/advertising.md)

### Conectar [!DNL Pinterest Ads] para a Platform usando a interface {#connect-to-platform-using-ui}

* [Criar uma conexão de origem do Pinterest na interface](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Criar um fluxo de dados para uma conexão de origem de anúncio na interface](../../tutorials/ui/dataflow/advertising.md)
