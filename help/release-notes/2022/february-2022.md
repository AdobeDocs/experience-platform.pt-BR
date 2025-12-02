---
title: Notas da versão de fevereiro de 2022 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2022 da Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 17%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: terça-feira, 7 de março de 2022**

>[!NOTE]
>
>Essa versão foi transferida da data original de 23 de fevereiro para 7 de março.

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] através dos quais você pode visualizar insights importantes sobre os dados da sua organização, conforme capturados durante os instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novos widgets de destinos padrão | Os widgets padrão a seguir permitem visualizar diferentes métricas relacionadas aos seus destinos.<ul><li>Segmentos ativados recentemente por destino. Este widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido.</li><li>Tendência de tamanho do público. Este widget descreve a relação da contagem de perfis durante um período de tempo para um segmento que foi mapeado para essa conta de destino.</li><li>Segmentos não mapeados por identidade. Este widget lista os cinco principais segmentos não mapeados classificados por contagem decrescente de identidades para um determinado destino e identidade.</li><li>Segmentos mapeados por identidade. Este widget lista os cinco principais segmentos mapeados. Os segmentos são ordenados de cima para baixo de acordo com suas respectivas contagens de IDs de origem que correspondem à ID de destino selecionada no menu suspenso do widget.</li><li>Públicos comuns. Este widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget.</li></ul> Para obter mais informações sobre widgets padrão disponíveis, consulte a [documentação do painel de destinos.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=pt-BR#standard-widgets). |

Para obter mais informações sobre [!DNL Dashboards], consulte a [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## Coleção de dados {#data-collection}

O Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los para o Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou que não sejam da Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Fluxo de trabalho de interface do usuário aprimorado para configuração de sequência de dados | O fluxo de trabalho para criar um novo fluxo de dados na interface da Coleção de dados foi atualizado. Ao adicionar serviços a um fluxo de dados, somente os serviços aos quais você tem acesso serão incluídos na lista de opções. Consulte o manual sobre [configuração de uma sequência de dados](../../datastreams/overview.md) para obter mais informações. |
| Preparo de dados para a coleção de dados | Se você estiver usando o Adobe Experience Platform Web SDK, agora é possível aproveitar os recursos de Preparo de dados para mapear seus dados para o Experience Data Model (XDM) no lado do servidor. Consulte a seção sobre [Preparação de dados para coleção de dados](../../datastreams/data-prep.md) no guia de sequências de dados para obter mais informações. |
| IDs próprias para dispositivos | Agora é possível enviar suas próprias IDs de dispositivo para o Adobe Experience Platform Edge Network ao coletar dados do cliente usando o Experience Platform Web SDK, fornecendo uma solução alternativa para as restrições recentes do navegador sobre a duração dos cookies de terceiros. Consulte o manual sobre [IDs de dispositivo próprio](/help/collection/use-cases/identity/first-party-device-ids.md) para obter mais informações. |

Para obter mais informações sobre a coleta de dados no Experience Platform, consulte a [visão geral da coleta de dados](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| (Beta) Suporte do Destination SDK para destinos baseados em arquivo | [O suporte da Destination SDK para destinos baseados em arquivo](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) está atualmente em beta privado e só está disponível para um número selecionado de parceiros e clientes. A funcionalidade e a documentação associada estão sujeitas a alterações antes do lançamento de disponibilidade geral.<br><br>Entre em contato com o representante de conta da Adobe para saber como acessar o recurso. Os representantes de contas internas da Adobe devem entrar em contato com as equipes de produtos e engenharia de destinos da Experience Platform para discutir os casos de uso compatíveis. <br><br> Na fase beta do suporte do Destination SDK para destinos baseados em arquivo, os parceiros beta e clientes podem usar o [Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md) para criar destinos privados que se beneficiem das seguintes funcionalidades: <ul><li>Crie um destino baseado em arquivo (em lote) por meio do Amazon S3, servidores SFTP, Azure Blob, Armazenamento do Azure Data Lake, Armazenamento da Data Landing Zone.</li><li>Configure e defina o agendamento de exportação de arquivos padrão e as opções de frequência.</li><li>Configure e defina opções para formatar seus arquivos CSV exportados (delimitadores, caracteres de escape e outras opções).</li><li>Capacidade de definir e editar cabeçalhos de arquivos personalizados.</li><li>Capacidade de receber notificações de eventos sobre a exportação de arquivos e segmentos.</li><li>Capacidade de exportar tipos de arquivos adicionais, como CSV, TSV, JSON, Parquet.</li></ul>  <br>Para começar a usar a nova funcionalidade, leia [(Beta) Usar o Destination SDK para configurar um destino baseado em arquivo](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> A funcionalidade de criar destinos de *transmissão* privados ou de produção usando o Destination SDK já está disponível para todos os clientes e parceiros da Experience Platform. Leia o guia sobre como [usar o Destination SDK para configurar um destino de streaming](../../destinations/destination-sdk/guides/configure-destination-instructions.md) para obter detalhes. |

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O Adobe Experience Platform [!DNL Identity Service] ajuda você a ter uma melhor visão do seu cliente e do comportamento dele ao unir as identidades de vários dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova permissão para `view-identity-graph` | Agora você pode usar a permissão `view-identity-graph` para controlar se os usuários em sua organização podem exibir dados do gráfico de identidade. Os usuários sem essa permissão serão proibidos de acessar o visualizador de gráficos de identidade na interface do usuário ou ao acessar as APIs [!DNL Identity Service] que retornam identidades. Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre permissões. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte a [visão geral do Serviço de Identidade](../../identity-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Origens do Beta migrando para o GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li></ul> |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).