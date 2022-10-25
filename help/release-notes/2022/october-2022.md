---
title: Notas de versão da Adobe Experience Platform de outubro de 2022
description: As notas de versão de outubro de 2022 para o Adobe Experience Platform.
source-git-commit: 098b4b7a0dcd3ddfcd13f7dd473c4fa6832d23df
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de outubro de 2022**

Novos recursos no Adobe Experience Platform:

- [Chaves gerenciadas pelo cliente](#cmk)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Fontes](#sources)

## Chaves gerenciadas pelo cliente {#cmk}

Todos os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado na plataforma, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

Consulte a visão geral em [chaves gerenciadas pelo cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obter detalhes sobre o recurso.

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Tratamento de dados confidenciais para conjuntos de dados | Os datastreams agora usam várias tecnologias da plataforma para lidar adequadamente com dados confidenciais, conforme empregado por regulamentos, como o Health Insurance Portability and Accountability Act (HIPAA). Consulte a seção sobre [tratamento de dados confidenciais em fluxos de dados](../../edge/datastreams/overview.md#sensitive) para obter mais informações. |
| [!DNL Splunk] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Splunk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Splunk] visão geral da extensão](../../tags/extensions/web/splunk/overview.md) para obter mais informações. |
| [!DNL Zendesk] extensão para encaminhamento de eventos | Agora é possível enviar dados para o [!DNL Zendesk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Zendesk] visão geral da extensão](../../tags/extensions/web/zendesk/overview.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Atualização do `authorized` de um tipo booleano a uma string. `season` e `episode` foram alteradas de números inteiros para sequências. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` foi renomeado para `friendlyName`e `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | A `ID` foi renomeada como `name`.  |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- | 
| Disponibilidade beta da origem do Adobe Workfront | Use o [Origem do Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para trazer seus dados do Workfront para o Experience Platform e executar casos de uso, como combinar seus registros de trabalho com dados de terceiros, aplicar análises históricas e de séries de tempo em registros de trabalho e consultar dados de trabalho usando o SQL padrão. Para obter mais informações, leia o guia sobre [criação de uma conexão de origem do Workfront na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Disponibilidade beta da origem da nuvem do Oracle Service | Use a fonte da nuvem do Oracle Service para assimilar dados da sua conta da Oracle Service Cloud para o Experience Platform. Para obter mais informações, leia a documentação sobre o [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).
