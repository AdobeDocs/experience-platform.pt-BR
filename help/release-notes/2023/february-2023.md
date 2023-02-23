---
title: Notas de versão da Adobe Experience Platform fevereiro de 2023
description: As notas de versão de fevereiro de 2023 para o Adobe Experience Platform.
source-git-commit: 66ca8d3972045cffe4a1614f638546f4e7838680
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de fevereiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Fontes](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados** {#destinations-new-updated-features}

| Recurso | Descrição |
| ----------- | ----------- |
| [Aprimoramento da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) para integrações com o [destinos com base em arquivo (em lote)](/help/destinations/destination-types.md#file-based) | <p> Quando os perfis não estão mais qualificados para uma política de consentimento, o Experience Platform agora comunica proativamente sua saída da política para destinos baseados em arquivos. Isso segue a [lançamento em fevereiro de 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) da mesma funcionalidade para destinos de transmissão. </p> <p> <b>Observação</b>: Essa funcionalidade está disponível somente para clientes do **[!UICONTROL Privacy e Security Shield]**, bem como os **[!UICONTROL Escudo da Saúde]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentação nova ou atualizada** {#destinations-new-updated-documentation}

| Documentação | Descrição |
| ----------- | ----------- |
| Como a documentação de destinos funciona | <p>Publicamos três novos artigos explicadores sobre como os destinos funcionam, com base em perguntas comuns dos usuários:</p> <p><ul><li>[Configurações configuráveis e comuns de exportação em destinos](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento de exportação de perfil para diferentes tipos de destino](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Manuseio de identidade no fluxo de trabalho de ativação de destinos](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**
&#x200B; | Recurso | Descrição | | — | — | | Descontinuação de campo por meio da interface do usuário | Agora você pode [descontinuar campos de seus esquemas depois que os dados forem assimilados](../../xdm/tutorials/field-deprecation-ui.md). A desativação do campo XDM permite remover campos da exibição da interface do usuário, mantendo-os para uso. Se necessário, é possível revelar campos obsoletos, e todos os segmentos, consultas ou soluções de downstream que referenciam os campos serão executados como de costume. |

{style=&quot;table-layout:auto&quot;}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Perfil de Prospecto Individual XDM]](https://github.com/adobe/xdm/pull/1669/files) | A classe Perfil individual de prospecto XDM traz IDs fornecidas por parceiros. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [!UICONTROL Restrições de limite de frequência] | O [!UICONTROL Restrições de limite de frequência] grupo de campos foi [atualizado para suportar eventos repetidos e personalizados](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo de dados | [!UICONTROL Referenciador da Web] | As propriedades do referenciador da Web foram [atualizado para incluir `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivamente, esses são o nome e a região do elemento HTML que foi selecionado na página anterior. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação da mensagem] | [O [!UICONTROL URL do rastreador] campo adicionado](https://github.com/adobe/xdm/pull/1665/files) para [!UICONTROL Adobe CJM ExperienceEvent]. Esse rastreador fornece o URL selecionado pelo usuário. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes da interação da mensagem] | [O vazio `meta:enum` propriedade foi removida](https://github.com/adobe/xdm/pull/1668/files) do URL [!UICONTROL Tipo de rastreamento] campo. |
| Tipo de dados | [!UICONTROL Informações da mídia] | [O padrão de regex da variável `videoSegment` propriedade em [!UICONTROL Informações da mídia] o tipo de dados foi removido](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md)&#x200B;

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados de data lake e capturar os resultados da consulta como um novo conjunto de dados para uso em relatórios, na Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**
&#x200B; | Recurso | Descrição | | — | — | | Habilitar conjuntos de dados para perfil com SQL | Use LABELs em queries CTAS para fazer um &quot;perfil ativado&quot; de conjunto de dados ou use ALTER para atualizar conjuntos de dados existentes para serem habilitados para o perfil. | | Monitorar consultas programadas | Use a guia Consultas agendadas para encontrar informações importantes sobre a execução do query e assinar alertas. Monitore consultas para detalhes de agendamento, status e mensagens/códigos de erro em caso de falha.  | | Alternar recurso de preenchimento automático | Elimine determinados comandos de metadados e melhore os tempos de processamento, alternando o recurso de preenchimento automático do Editor de consultas. Esse recurso sugere automaticamente possíveis palavras-chave SQL e detalhes da tabela para a consulta à medida que você a escreve. | | Amostras do conjunto de dados | Especifique uma taxa de amostragem em sua consulta e use amostras de conjunto de dados para criar uma amostra aleatória uniforme ou crie amostras condicionais com base em critérios específicos. |

{style=&quot;table-layout:auto&quot;} &#x200B; Para obter mais informações sobre os Serviços de Consulta, consulte o [Visão geral do Serviço de query](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time Customer Data Platform B2B Edition {#b2b}

Baseado no Real-time Customer Data Platform (Real-Time CDP), o Real-Time CDP B2B Edition foi desenvolvido para profissionais de marketing que operam em um modelo de serviço de empresa para empresa. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem com precisão públicos-alvo específicos e os envolvam em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Ativar serviço de contas relacionadas | A nova função de alternância permite habilitar o serviço de contas relacionadas em sua conta. Para obter mais informações, leia o guia sobre [habilitando o serviço de contas relacionadas](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre o Real-Time CDP B2B Edition, leia a [Visão geral do Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Designar acesso no nível da assinatura com [!DNL Google PubSub] | Agora você pode definir o acesso a uma assinatura de tópico específica ao usar o [!DNL Google PubSub] fornecendo a ID da assinatura ao autenticar. Para obter mais informações, leia a [!DNL Google PubSub] tutorial de autenticação [usando a API do Serviço de Fluxo](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [Interface do usuário da plataforma](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Assimilar dados de atividade personalizada de [!DNL Marketo] | Agora é possível trazer dados de atividade personalizados da [!DNL Marketo] instância para Experience Platform. Para assimilar dados de atividade personalizados, você deve configurar grupos de campos de atividades personalizadas no esquema Atividades B2B e criar um fluxo de dados usando o conjunto de dados de atividades. Quando o fluxo de dados for concluído, o conjunto de dados assimilado conterá atividades padrão e personalizadas do [!DNL Marketo] instância. Você pode usar [Serviço de query](../../query-service/home.md) para acessar seus registros de atividade personalizados no Platform. Para obter mais informações, leia o guia sobre [criação de um fluxo de dados para dados de atividade personalizados](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Excluir contas não reclamadas do [!DNL Marketo] | Agora é possível configurar se deseja excluir ou incluir contas não reivindicadas da assimilação ao criar um fluxo de dados para dados de empresas. Para obter mais informações, leia o guia sobre [criar uma conexão de origem e um fluxo de dados para [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).