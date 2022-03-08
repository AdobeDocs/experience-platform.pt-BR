---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 366656346c25cd5206b36c7ff2b9942c5027de17
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 7 de março de 2022**

>[!NOTE]
>
>Esta versão foi transferida da data original de 23 de fevereiro para 7 de março.

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] através da qual você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novos widgets de destinos padrão | Os widgets padrão a seguir permitem visualizar métricas diferentes relacionadas aos destinos.<ul><li>Segmentos ativados recentemente por destino. Esse widget exibe os cinco principais segmentos ativados mais recentemente em ordem decrescente de acordo com o destino escolhido.</li><li>Tendência do tamanho do público-alvo. Este widget descreve o relacionamento da contagem de perfis durante um período de tempo para um segmento que foi mapeado para essa conta de destino.</li><li>Segmentos não mapeados por identidade. Este widget lista os cinco principais segmentos não mapeados classificados por contagem de identidade decrescente para um determinado destino e identidade.</li><li>Segmentos mapeados por identidade. Esse widget lista os cinco principais segmentos mapeados. Os segmentos são ordenados de alto a baixo de acordo com suas respectivas contagens de IDs de origem que correspondem à ID de destino selecionada no menu suspenso do widget.</li><li>Públicos-alvo comuns. Este widget fornece uma lista dos cinco principais segmentos ativados na conta de destino escolhida na parte superior da página, e o destino selecionado na lista suspensa do widget.</li></ul> Para obter mais informações sobre os widgets padrão disponíveis, consulte o [documentação do painel de destinos.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Para obter mais informações sobre [!DNL Dashboards]consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## Coleta de dados {#data-collection}

A Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Fluxo de trabalho de interface do usuário aprimorado para configuração de armazenamento de dados | O fluxo de trabalho para criar um novo armazenamento de dados na interface do usuário da coleta de dados foi atualizado. Ao adicionar serviços a um armazenamento de dados, somente os serviços aos quais você tem acesso serão incluídos na lista de opções. Consulte o guia sobre [configuração de um armazenamento de dados](../../edge/fundamentals/datastreams.md) para obter mais informações. |
| Preparação de dados para coleta de dados | Se você estiver usando o SDK da Web da Adobe Experience Platform, agora poderá aproveitar os recursos de Preparação de dados para mapear seus dados para o Experience Data Model (XDM) no lado do servidor. Consulte a seção sobre [Preparação de dados para coleta de dados](../../edge/fundamentals/datastreams.md#data-prep) no guia datastreams para obter mais informações. |
| IDs de dispositivo próprio | Agora é possível enviar suas próprias IDs de dispositivo para a Adobe Experience Platform Edge Network ao coletar dados do cliente usando o SDK da Web da plataforma, fornecendo uma solução alternativa para as restrições recentes do navegador em relação à duração do cookie de terceiros. Consulte o guia sobre [IDs de dispositivo primário](../../edge/identity/first-party-device-ids.md) para obter mais informações. |

Para obter mais informações sobre a coleta de dados no Platform, consulte o [visão geral da coleta de dados](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Suporte do Destination SDK para destinos com base em arquivos (Beta) | [Suporte do Destination SDK para destinos com base em arquivos](../../destinations/destination-sdk/file-based-destination-configuration.md) no momento, o está em beta privado e só está disponível para um número selecionado de parceiros e clientes. A funcionalidade e a documentação associada estão sujeitas a alterações antes do lançamento da disponibilidade geral.<br><br>Entre em contato com o representante de conta do Adobe para saber como acessar o recurso. Os representantes da conta interna do Adobe devem entrar em contato com as equipes de produtos e engenharia de destinos do Experience Platform para discutir os casos de uso suportados. <br><br> Na fase beta do suporte do Destination SDK para destinos com base em arquivos, os parceiros beta e os clientes podem usar o [Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para criar destinos privados para se beneficiarem da seguinte funcionalidade: <ul><li>Crie um destino (em lote) com base em arquivos via Amazon S3, servidores SFTP, Azure Blob, Armazenamento Azure Data Lake, armazenamento da Zona de Aterrissagem de Dados.</li><li>Configure e defina as opções padrão de programação e frequência da exportação de arquivos.</li><li>Configure e defina opções para formatar os arquivos CSV exportados (delimitadores, caracteres de escape e outras opções).</li><li>Capacidade de definir e editar cabeçalhos de arquivos personalizados.</li><li>Capacidade de receber notificações de eventos sobre a exportação de arquivos e segmentos.</li><li>Capacidade de exportar tipos de arquivos adicionais, como CSV, TSV, JSON, Parquet.</li></ul>  <br>Para começar a usar a nova funcionalidade, leia [(Beta) Use o Destination SDK para configurar um destino baseado em arquivo](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> A funcionalidade para criar conteúdo privado ou produzido *transmissão* os destinos usando o Destination SDK já estão disponíveis para todos os clientes e parceiros do Experience Platform. Leia o guia sobre como [use o Destination SDK para configurar um destino de transmissão](/help/destinations/destination-sdk/configure-destination-instructions.md) para obter detalhes. |

## [!DNL Identity Service] {#identity}

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova permissão para `view-identity-graph` | Agora você pode usar o `view-identity-graph` permissão para controlar se os usuários em sua organização podem exibir dados de gráficos de identidade. Os usuários sem essa permissão serão proibidos de acessar o visualizador de gráfico de identidade na interface do usuário ou ao acessar [!DNL Identity Service] APIs que retornam identidades. Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre permissões. |

Para obter informações mais gerais sobre [!DNL Identity Service], consulte o [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Fontes beta movendo-se para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
