---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: b714a5cf0f4bdf2c0f010664bfef96c5b6641c22
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 7 de março de 2022**

>[!NOTE]
>
>Esta versão foi transferida da data original de 23 de fevereiro para 7 de março.

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [Coleta de dados](#data-collection)
- [[!DNL Identity Service]](#identity)
- [Fontes](#sources)

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
