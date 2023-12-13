---
title: Notas da versão de fevereiro de 2023 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2023 da Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 38689125a43ad0b1a12a00efe6800bb310d7557c
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 97%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de fevereiro de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Coleção de dados](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query Service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Fontes](#sources)

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

### Assurance {#assurance}

O Adobe Assurance permite inspecionar, provar, simular e validar a forma como você coleta dados ou fornece experiências em seus aplicativos móveis.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| APIs públicas | As APIs do Adobe Assurance agora estão disponíveis. As APIs do Assurance são uma coleção de APIs que permitem que você teste e depure seus próprios aplicativos móveis e da web, quando equipados com a extensão do Adobe Assurance com SDK móvel. Para saber mais sobre as APIs do Assurance, leia a [Visão geral da API do Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Para obter mais informações sobre o Assurance, leia a [Documentação do Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados** {#destinations-new-updated-features}

| Recurso | Descrição |
| ----------- | ----------- |
| [Aprimoramento da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) para integrações com [destinos baseados em arquivos (lote)](/help/destinations/destination-types.md#file-based) | <p> Quando os perfis não estão mais qualificados para uma política de consentimento, a Experience Platform agora comunica proativamente a saída da política deles para os destinos baseados em arquivos. Isso está de acordo com o [lançamento, em fevereiro de 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality), da mesma funcionalidade para destinos de transmissão. </p> <p> <b>Observação</b>: essa funcionalidade está disponível somente para clientes do **[!UICONTROL Privacy and Security Shield]** e do **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentação nova ou atualizada** {#destinations-new-updated-documentation}

| Documentação | Descrição |
| ----------- | ----------- |
| Documentação Como os destinos funcionam | <p>Publicamos três novos artigos explicativos sobre como os destinos funcionam, com base em perguntas frequentes de usuários:</p> <p><ul><li>[Configurações de exportação comuns e alteráveis em destinos](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento de exportação de perfil para diferentes tipos de destino](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Manuseio de identidade no fluxo de trabalho de ativação de destinos](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Para obter mais informações gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Descontinuação de campo por meio da interface | Agora é possível [descontinuar campos de seus esquemas após a assimilação dos dados](../../xdm/tutorials/field-deprecation-ui.md). A descontinuação dos campos XDM permite remover campos da visualização da interface, enquanto os mantém para uso. Você pode revelar novamente os campos descontinuados, se necessário, e quaisquer segmentos, consultas ou soluções de downstream que façam referência a esses campos serão executados normalmente. |

{style="table-layout:auto"}

**Novos componentes de XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Perfil de cliente potencial individual do XDM]](https://github.com/adobe/xdm/pull/1669/files) | A classe Perfil de cliente potencial individual do XDM traz as IDs fornecidas por parceiros. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [!UICONTROL Restrições de limite de frequência] | O grupo de campos [!UICONTROL Restrições de limite de frequência] foi [atualizado para oferecer suporte a eventos repetidos e personalizados](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo de dados | [!UICONTROL Referenciador da Web] | As propriedades do referenciador da Web foram [atualizadas para incluir `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Esses são o nome e a região do elemento HTML selecionado na página anterior, respectivamente. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação da mensagem] | [O campo [!UICONTROL URL do rastreador] foi adicionado](https://github.com/adobe/xdm/pull/1665/files) ao [!UICONTROL Adobe CJM ExperienceEvent]. Este rastreador fornece o URL selecionado pelo usuário ou usuária. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação da mensagem] | [O propriedade `meta:enum` vazia foi removida](https://github.com/adobe/xdm/pull/1668/files) do campo [!UICONTROL Tipo de rastreamento] do URL. |
| Tipo de dados | [!UICONTROL Informações da mídia] | [O padrão regex da propriedade `videoSegment` no tipo de dados [!UICONTROL Informações da mídia] foi removido](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia a [Visão geral do sistema XDM](../../xdm/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. É possível unir qualquer conjunto de dados do data lake e capturar os resultados de consultas como um novo conjunto de dados para usar em relatórios, no espaço de trabalho de ciência de dados ou para assimilação no perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Habilitar conjuntos de dados para perfil com SQL | [Use LABELs em consultas CTAS para tornar um conjunto de dados &quot;habilitado para perfil&quot;](../../query-service/sql/syntax.md#create-table-as-select) ou use ALTER para atualizar conjuntos de dados já existentes e habilitá-los para perfil. Você pode usar essa construção de SQL estendido para fornecer suporte contínuo a conjuntos de dados derivados para seus casos de uso de negócios do Perfil do cliente em tempo real. Consulte a [Fluxo SQL contínuo para o documento de conjuntos de dados derivados](../../query-service/data-distiller/derived-datasets/seamless-sql-flow.md) para obter mais detalhes. |
| Monitorar consultas programadas | Use a [guia Consultas programadas](../../query-service/ui/monitor-queries.md) para encontrar informações importantes sobre suas consultas e assinar alertas. Monitore consultas para obter detalhes de agendamento, status e mensagens/códigos de erro caso haja falha. |
| Alternar recurso de preenchimento automático | Elimine determinados comandos de metadados e melhore os tempos de processamento ao [ativar o recurso de preenchimento automático do Editor de consultas](../../query-service/ui/user-guide.md#auto-complete). Esse recurso sugere automaticamente possíveis palavras-chave SQL e detalhes da tabela para a consulta à medida que ela é escrita. |
| Amostras de conjunto de dados | Especifique uma taxa de amostragem em sua consulta e [use amostras de conjunto de dados para criar uma amostra aleatória uniforme](../../query-service/key-concepts/dataset-samples.md), ou crie amostras condicionais com base em critérios específicos. |

{style="table-layout:auto"}

Para obter mais informações sobre o Query Service, consulte a [Visão geral do Query Service](../../query-service/home.md).


## Real-Time Customer Data Platform B2B Edition {#b2b}

Criada com base na Real-time Customer Data Platform (Real-Time CDP), a Real-Time CDP B2B Edition foi desenvolvida especificamente para profissionais de marketing que operam em um modelo de serviço B2B. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Habilitar serviço de contas relacionadas | A nova função ativável permite habilitar o serviço de contas relacionadas na sua conta. Para obter mais informações, leia o manual sobre [ativação do serviço de contas relacionadas](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Para saber mais sobre a Real-Time CDP B2B Edition, leia a [Visão geral da Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Origens {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Designar acesso em nível de assinatura com [!DNL Google PubSub] | Agora é possível definir o acesso a uma assinatura de tópico específica ao usar a fonte [!DNL Google PubSub], fornecendo a ID da assinatura ao autenticar. Para obter mais informações, leia o tutorial de autenticação do [!DNL Google PubSub] [usando a API do Serviço de fluxo](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [Interface da Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Assimilar dados de atividade personalizados do [!DNL Marketo] | Agora você pode trazer os dados de atividades personalizadas da sua instância do [!DNL Marketo] para a Experience Platform. Para assimilar dados de atividades personalizadas, será necessário configurar grupos de campos de atividades personalizadas no esquema Atividades B2B e criar um fluxo de dados usando o conjunto de dados de atividades. Quando o fluxo de dados for concluído, o conjunto de dados assimilado conterá tanto as atividades padrão quanto as personalizadas da instância do [!DNL Marketo]. Você poderá então usar o [Query Service](../../query-service/home.md) para acessar seus registros de atividades personalizadas na Platform. Para obter mais informações, leia o manual sobre a [criação de um fluxo de dados para dados de atividades personalizadas](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Excluir contas não reivindicadas do [!DNL Marketo] | Agora é possível configurar se deseja excluir ou incluir contas não reivindicadas na assimilação ao criar um fluxo de dados para dados de empresas. Para obter mais informações, leia o manual sobre a [criação de uma conexão de origem e fluxo de dados para  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
