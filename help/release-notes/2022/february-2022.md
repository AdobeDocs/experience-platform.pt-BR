---
title: Notas de versão da Adobe Experience Platform de fevereiro de 2022
description: As notas de versão de fevereiro de 2022 do Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 23%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 7 de março de 2022**

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

O Adobe Experience Platform fornece vários [!DNL dashboards] por meio do qual você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novos widgets de destinos padrão | Os widgets padrão a seguir permitem visualizar diferentes métricas relacionadas aos seus destinos.<ul><li>Segmentos ativados recentemente por destino. Este widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido.</li><li>Tendência de tamanho do público-alvo. Este widget descreve a relação da contagem de perfis durante um período de tempo para um segmento que foi mapeado para essa conta de destino.</li><li>Segmentos não mapeados por identidade. Esse widget lista os cinco principais segmentos não mapeados classificados por contagem de identidade decrescente para um determinado destino e identidade.</li><li>Segmentos mapeados por identidade. Este widget lista os cinco principais segmentos mapeados. Os segmentos são ordenados de cima para baixo de acordo com suas respectivas contagens de IDs de origem que correspondem à ID de destino selecionada no menu suspenso do widget.</li><li>Públicos comuns. Esse widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget.</li></ul> Para obter mais informações sobre widgets padrão disponíveis, consulte [documentação do painel de destinos.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Para obter mais informações sobre [!DNL Dashboards], consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Fluxo de trabalho de interface do usuário aprimorado para configuração de sequência de dados | O fluxo de trabalho para criar um novo fluxo de dados na interface da Coleção de dados foi atualizado. Ao adicionar serviços a um fluxo de dados, somente os serviços aos quais você tem acesso serão incluídos na lista de opções. Consulte o guia sobre [configurar um fluxo de dados](../../datastreams/overview.md) para obter mais informações. |
| Preparação de dados para coleção de dados | Se você estiver usando o SDK da Web da Adobe Experience Platform, agora é possível aproveitar os recursos de Preparo de dados para mapear seus dados para o Experience Data Model (XDM) no lado do servidor. Consulte a seção sobre [Preparação de dados para coleção de dados](../../datastreams/data-prep.md) no guia datastreams para obter mais informações. |
| IDs de dispositivo próprio | Agora é possível enviar suas próprias IDs de dispositivo para a Rede de borda da Adobe Experience Platform ao coletar dados do cliente usando o SDK da Web da plataforma, fornecendo uma solução alternativa para as restrições recentes do navegador sobre a duração dos cookies de terceiros. Consulte o guia sobre [IDs de dispositivo primário](../../edge/identity/first-party-device-ids.md) para obter mais informações. |

Para obter mais informações sobre a coleta de dados na Platform, consulte a [visão geral da coleção de dados](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| (Beta) Suporte para Destination SDK para destinos baseados em arquivo | [Suporte para Destination SDK para destinos baseados em arquivo](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) no momento, o está na versão beta privada e só está disponível para um número selecionado de parceiros e clientes. A funcionalidade e a documentação associada estão sujeitas a alterações antes do lançamento de disponibilidade geral.<br><br>Entre em contato com o representante de conta do Adobe para saber como acessar o recurso. Os representantes de conta interna do Adobe devem entrar em contato com as equipes de produtos e engenharia de destinos do Experience Platform para discutir os casos de uso compatíveis. <br><br> Na fase beta do suporte para Destination SDK para destinos baseados em arquivo, os parceiros e clientes beta podem usar o [Destination SDK Experience Platform](../../destinations/destination-sdk/overview.md) para criar destinos privados que se beneficiem da seguinte funcionalidade: <ul><li>Crie um destino baseado em arquivo (em lote) por meio do Amazon S3, servidores SFTP, Azure Blob, Armazenamento do Azure Data Lake, Armazenamento da Data Landing Zone.</li><li>Configure e defina o agendamento de exportação de arquivos padrão e as opções de frequência.</li><li>Configure e defina opções para formatar seus arquivos CSV exportados (delimitadores, caracteres de escape e outras opções).</li><li>Capacidade de definir e editar cabeçalhos de arquivos personalizados.</li><li>Capacidade de receber notificações de eventos sobre a exportação de arquivos e segmentos.</li><li>Capacidade de exportar tipos de arquivos adicionais, como CSV, TSV, JSON, Parquet.</li></ul>  <br>Para começar a usar a nova funcionalidade, leia [(Beta) Usar o Destination SDK para configurar um destino baseado em arquivo](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> A funcionalidade para criar propriedades privadas ou *transmissão* destinos com o uso do Destination SDK já está disponível para todos os clientes e parceiros do Experience Platform. Leia o guia sobre como [usar o Destination SDK para configurar um destino de transmissão](../../destinations/destination-sdk/guides/configure-destination-instructions.md) para obter detalhes. |

## [!DNL Identity Service] {#identity}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova permissão para `view-identity-graph` | Agora você pode usar o `view-identity-graph` permissão para controlar se os usuários em sua organização podem exibir dados do gráfico de identidade. Os usuários sem essa permissão serão proibidos de acessar o visualizador de gráficos de identidade na interface ou ao acessar [!DNL Identity Service] APIs que retornam identidades. Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre permissões. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte o [Visão geral do serviço de identidade](../../identity-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Origens beta migrando para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).