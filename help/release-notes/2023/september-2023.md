---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de setembro de 2023 para o Adobe Experience Platform.
source-git-commit: 1bfd5e05642e0ac8f80af5502878eaee0b33c704
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 26%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 28 de setembro de 2023**

Novos recursos na Adobe Experience Platform:

- [Atributos computados](#computed-attributes)

Atualizações dos recursos já existentes na Experience Platform:

- [Alertas](#alerts)
- [Coleção de dados](#data-collection)
- [Identity Service](#identity-service)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Atributos computados {#computed-attributes}

Os atributos computados permitem resumir facilmente os dados do evento em atributos de perfil por meio de uma interface intuitiva para segmentação, personalização e ativação avançadas com base em comportamento. Com esse recurso, você pode criar atributos computados de maneira automatizada, gerenciá-los e usá-los na segmentação, destinos do Real-Time CDP ou Adobe Journey Optimizer. Além disso, os atributos computados simplificam a segmentação e os fluxos de trabalho de jornada para ajudá-lo a fornecer experiências relevantes de maneira contínua. Para saber mais sobre atributos computados, leia a [visão geral dos atributos computados](../../profile/computed-attributes/overview.md).

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da Platform. É possível assinar diferentes regras de alerta por meio da [!UICONTROL Alertas] na interface do usuário da Platform e podem optar por receber mensagens de alerta na própria interface ou por notificações por email.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Guia Histórico de alertas | Os alertas [!UICONTROL Histórico] A guia agora incluirá todos os eventos, incluindo atrasos, inicializações, sucesso e falhas. Leia o [documentação da interface de alertas](../../observability/alerts/ui.md) para obter mais informações sobre a guia histórico. |

{style="table-layout:auto"}

Para saber mais sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Sequências de dados | Suporte à pesquisa de dispositivo | Ao configurar um fluxo de dados, agora é possível selecionar o nível de informações de pesquisa de dispositivo a serem coletadas. As informações de pesquisa do dispositivo incluem dados sobre o dispositivo, hardware, sistema operacional e navegador usados para interagir com a página. <br>  As informações de pesquisa de dispositivo não podem ser coletadas junto com o agente do usuário e as dicas do cliente. Optar por coletar informações do dispositivo desativará a coleta de agentes do usuário e dicas do cliente, e vice-versa. Todas as informações de pesquisa do dispositivo são armazenadas no `xdm:device` grupo de campos. Saiba mais na documentação sobre [configurando sequências de dados](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensões | [!DNL TikTok] extensão da API de eventos da web | A variável [[!DNL TikTok] API de eventos da Web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) permite que você aproveite os dados capturados na Rede de borda da Adobe Experience Platform e os envie para [!DNL TikTok] na forma de eventos do lado do servidor usando o [!DNL TikTok] API de eventos da Web. |

{style="table-layout:auto"}

Para saber mais sobre a coleta de dados, leia o [visão geral da coleção de dados](../../tags/home.md).

## Identity Service {#identity-service}

O Identity Service da Adobe Experience Platform fornece uma visão abrangente dos clientes e seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais de impacto em tempo real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos na interface do usuário do serviço de identidade | Use a ferramenta aprimorada de criação de namespace personalizado na interface do usuário do Experience Platform para gerenciar melhor seus namespaces personalizados e seus tipos de identidade correspondentes. A interface aprimorada do serviço de identidade fornece: <ul><li>Experiência contextual: dicas visuais, clareza e contexto para o que é um namespace de identidade e os tipos de identidade.</li><li>Precisão: melhor tratamento de erros, sem mais nomes de identidade duplicados.</li><li>Capacidade de descoberta: acesso à documentação por meio de uma caixa de diálogo no produto.</li></ul> Para obter mais informações, leia o guia em [criação de namespaces personalizados](../../identity-service/namespaces.md#create-namespaces). |
| Alterações nos limites do gráfico de identidade | O limite do gráfico de identidade foi alterado de 150 identidades para 50 identidades. Quando uma nova identidade é assimilada em um gráfico completo, a identidade mais antiga com base no carimbo de data e hora de assimilação e no tipo de identidade é excluída. Os tipos de identidade de cookie são priorizados para exclusão. Entre em contato com a equipe de conta do Adobe para solicitar uma alteração no tipo de identidade se a sandbox de produção contiver: <ul><li>um namespace personalizado em que os identificadores de pessoa (como IDs de CRM) são configurados como tipo de identidade de cookie/dispositivo.</li><li>um namespace personalizado em que os identificadores de cookie/dispositivo são configurados como tipo de identidade entre dispositivos.</li></ul> A engenharia de Adobe processará manualmente essas solicitações. Para obter mais informações, leia a [medidas de proteção para dados do serviço de identidade](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Para saber mais sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../../identity-service/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Colunas personalizáveis | Agora é possível personalizar o layout do Audience Portal com colunas redimensionáveis. Para obter mais informações sobre esse recurso, leia a [guia da interface de segmentação](../../segmentation/ui/overview.md#customize). |
| Atualizar detalhamento de frequência | Agora você pode ver um detalhamento das frequências de atualização dos públicos-alvo em sua organização. Para obter mais informações sobre esse recurso, leia a [guia da interface de segmentação](../../segmentation/ui/overview.md#browse). |

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).

Para saber mais sobre o Serviço de segmentação, leia o [Visão geral do serviço de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Novos parâmetros para o `offset` paginação em fontes de autoatendimento (SDK em lote) | Agora você pode especificar um `endConditionName` e `endConditionValue` para sua origem ao usar `offset` paginação. Esses parâmetros permitem indicar a condição que encerrará o loop de paginação na próxima solicitação HTTP. Para obter mais informações, leia a [guia de paginação para Fontes de autoatendimento (SDK em lote)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).