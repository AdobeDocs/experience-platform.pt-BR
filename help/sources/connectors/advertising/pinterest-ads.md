---
keywords: Experience Platform;home;popular tópicos;Pinterest Ads;
title: Visão geral do Pinterest Ads Source
description: Saiba como conectar o Pinterest Ads ao Adobe Experience Platform usando APIs ou a interface do usuário.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>A origem [!DNL Pinterest Ads] está na versão beta. Leia a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema de publicidade de terceiros. O suporte para provedores de publicidade inclui [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) é um mecanismo de descoberta visual para encontrar receitas, decoração doméstica, inspiração de estilo e outras ideias na web. Eles são apresentados em pequena escala usando imagens, GIFs animados e vídeos no formato pinboard. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) permite que você expanda sua empresa e alcance 400 milhões de pessoas usando o [!DNL Pinterest].

Com o [!DNL Pinterest Ads], você pode alcançar os usuários através de anúncios direcionados para descobrir e comprar seus produtos. Pins de [!DNL Pinterest Ads] são patrocinados para receber exposição extra em resultados de pesquisa relevantes. Os usuários que assinaram o [!DNL Pinterest Business] podem optar por promover marcadores existentes com melhor desempenho, criar uma nova imagem ou vídeo ou até mesmo promover uma imagem que tenha sido fixada em um site. O [!DNL Pinterest Ads] oferece vários formatos de anúncio para ajudar você a alcançar suas metas específicas de campanha.

## [!DNL Pinterest] APIs {#pinterest-apis}

A origem [!DNL Pinterest Ads] aproveita as APIs [!DNL Pinterest] para recuperar os dados [!DNL Pinterest Ads], juntamente com todo o desempenho e todas as métricas. Os endpoints de API compatíveis são:

* [Análise de campanha](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análise de Grupo de Anúncios](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Anúncios de análise](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Use a fonte [!DNL Pinterest Ads] para trazer seus dados do [!DNL Pinterest] para a Experience Platform, onde você pode executar a análise de dados. Os dados são retornados a partir da data de assimilação para um intervalo retroativo de 90 dias. [!DNL Pinterest Ads] usa tokens de portador como um mecanismo de autenticação para se comunicar com as APIs [!DNL Pinterest].

## Pré-requisitos {#prerequisites}

A primeira etapa na criação de uma conexão de origem [!DNL Pinterest Ads] é garantir que você tenha uma conta de desenvolvedor do Pinterest. Se você ainda não tiver uma, visite a página [inscreva-se](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) para se registrar e criar sua conta.

### Configurar o aplicativo [!DNL Pinterest] e gerar o token de acesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>É recomendável usar as APIs do [!DNL Pinterest] para gerar seu token de acesso, pois gerar seu token de acesso na interface fornece um acesso limitado. Por meio da interface, você só poderá acessar os seguintes escopos: `pins:read`, `boards:read` e `user_accounts:read`. Essa limitação não é adequada para uso com os pontos de extremidade de análise da API [!DNL Pinterest].

Para gerar seu token de acesso, leia os guias do [!DNL Pinterest] sobre [configuração do aplicativo](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticação usando OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Coletar credenciais necessárias {#gather-required-credentials}

Para conectar [!DNL Pinterest Ads] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| Token de acesso | O token de acesso [!DNL Pinterest Ads] para sua conta de usuário. A conta de usuário do token deve ser o proprietário da conta [!DNL Pinterest Ad] especificada ou ter uma das funções necessárias concedidas a ele por meio do Business Access: Administrador, Analista ou Gerente de Campanha. Para obter mais informações sobre o token de acesso, consulte o [[!DNL Pinterest] manual sobre como gerar o token de acesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID da conta de anúncio | A ID da conta de anúncio [!DNL Pinterest Ads] relacionada à sua unidade de negócios. Para obter informações sobre como recuperar a ID da conta de anúncio. Visite o [[!DNL Pinterest] guia sobre como encontrar IDs no Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campanha, grupo de publicidade ou ID de publicidade | As IDs do `campaign`, `ad group` ou `ad` que correspondem à ID da conta do anúncio. Para obter as IDs necessárias, navegue até a página [!DNL Pinterest] do **Pinterest Business Hub** > **Resumo da Conta de Anúncios** > **Campanhas** / **Grupos de Anúncios** / **Anúncios** e copie as IDs necessárias mencionadas logo abaixo de cada um de seus nomes. |

>[!NOTE]
>
>A API [!DNL Pinterest] fornece APIs individuais para recuperar dados associados a cada ID. Portanto, é necessário transmitir somente as IDs correspondentes ao tipo de ID em que você está interessado.

## Medidas de proteção {#guardrails}

As seções a seguir fornecem informações sobre medidas de proteção de dados para [!DNL Pinterest].

### Intervalo de datas [!DNL Pinterest] {#pinterest-date-range}

A API [!DNL Pinterest] é compatível com os parâmetros `start_date` e `end_date` para recuperar dados de análise entre um determinado intervalo de datas.

* O `start_date` não pode ser mais de 90 dias antes da data atual.
* O `end_date` não pode ser mais de 90 dias após o `start_date`.

Ao agendar seu fluxo de dados, você deve definir uma das seguintes configurações de frequência e intervalo:

| Frequência | Intervalo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por exemplo, se a assimilação for definida em 15 de março de 2023 com uma configuração de frequência e intervalo definida como `Day=1` ou `Hour=24`, a API [!DNL Pinterest] só recuperará dados de até 15 de dezembro de 2022, pois o cálculo tem data retroativa de 90 dias.

### [!DNL Pinterest] intervalo de tempo {#pinterest-time-range}

A API [!DNL Pinterest] oferece suporte a diferentes tipos de granularidade de tempo para a forma como os dados podem ser recuperados:

| Granularidade de tempo | Descrição |
| --- | --- |
| **TOTAL** | As métricas de dados são agregadas em um intervalo de datas especificado. |
| **DIA** | As métricas de dados são detalhadas diariamente. |
| **HORA** | As métricas de dados são detalhadas de hora em hora. |
| **SEMANAL** | As métricas de dados são detalhadas semanalmente. |
| **MENSALMENTE** | As métricas de dados são detalhadas mensalmente. |

Para o Experience Platform, a origem [!DNL Pinterest Ads] é configurada internamente para `Day`, o que significa que os dados serão agregados diariamente. Por exemplo, usando `impressions recorded` como métrica, já que a granularidade está configurada como `DAY`, você obteria `xx` impressões sobre `day 1`, `yy` impressões sobre `day 2` e assim por diante.

>[!IMPORTANT]
>
>O Pinterest impõe um limite de taxa de 1.000 chamadas de API diariamente em sua API para ler informações de anúncios, grupos de anúncios ou campanhas de anúncios. Para obter informações sobre limites de taxa aplicáveis a chamadas de API subjacentes, consulte a [[!DNL Pinterest] documentação sobre limites de taxa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Conectar [!DNL Pinterest Ads] ao Experience Platform {#connect-to-platform}

A documentação abaixo fornece informações sobre como conectar o [!DNL Pinterest Ads] ao Experience Platform usando APIs ou a interface do usuário:

### Conectar o [!DNL Pinterest Ads] ao Experience Platform usando APIs {#connect-to-platform-using-api}

* [Criar uma conexão básica do Pinterest usando a API do serviço de fluxo](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de publicidade usando a API do serviço de fluxo](../../tutorials/api/collect/advertising.md)

### Conectar o [!DNL Pinterest Ads] ao Experience Platform usando a interface {#connect-to-platform-using-ui}

* [Criar uma conexão de origem do Pinterest na interface](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Criar um fluxo de dados para uma conexão de origem de anúncio na interface](../../tutorials/ui/dataflow/advertising.md)
