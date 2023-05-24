---
title: Notas de versão da Adobe Experience Platform de fevereiro de 2023
description: As notas de versão de fevereiro de 2023 do Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de fevereiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

### Assurance {#assurance}

O Adobe Assurance permite inspecionar, testar, simular e validar como você coleta dados ou veicula experiências em seu aplicativo móvel.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| APIs públicas | As APIs do Adobe Assurance agora estão disponíveis. As APIs do Assurance são uma coleção de APIs que capacitam os usuários a testar e depurar seus próprios aplicativos móveis e da Web, quando equipados com a extensão Adobe Assurance com SDK móvel. Para saber mais sobre as APIs do Assurance, leia o [Visão geral da API do Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Para obter mais informações sobre o Assurance, leia o [Documentação de garantia](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados** {#destinations-new-updated-features}

| Recurso | Descrição |
| ----------- | ----------- |
| [Aprimoramento da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) para integrações com a [destinos com base em arquivo (lote)](/help/destinations/destination-types.md#file-based) | <p> Quando os perfis não estão mais qualificados para uma política de consentimento, o Experience Platform agora comunica proativamente a saída da política para destinos baseados em arquivo. Segue-se a [lançamento em fevereiro de 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) da mesma funcionalidade para destinos de transmissão. </p> <p> <b>Nota</b>: essa funcionalidade está disponível somente para clientes do **[!UICONTROL Escudo de Proteção e Privacidade]** e as de **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentação nova ou atualizada** {#destinations-new-updated-documentation}

| Documentação | Descrição |
| ----------- | ----------- |
| Como a documentação de destinos funciona | <p>Publicamos três novos artigos explicativos sobre como os destinos funcionam, com base em perguntas comuns dos usuários:</p> <p><ul><li>[Configurações de exportação configuráveis e comuns em destinos](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamento de exportação de perfil para diferentes tipos de destino](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Manuseio de identidade no workflow de ativação de destinos](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Descontinuação de campo por meio da interface | Agora você pode [descontinuar campos de seus esquemas após a assimilação de dados](../../xdm/tutorials/field-deprecation-ui.md). A desativação do campo XDM permite remover campos da visualização da interface do usuário, além de mantê-los para uso. Você pode revelar campos obsoletos novamente, se necessário, e quaisquer segmentos, consultas ou soluções downstream que referenciem os campos serão executados como de costume. |

{style="table-layout:auto"}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Perfil de cliente potencial individual XDM]](https://github.com/adobe/xdm/pull/1669/files) | A classe Perfil de cliente potencial individual XDM traz IDs fornecidas pelo parceiro. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [!UICONTROL Restrições de limite de frequência] | A variável [!UICONTROL Restrições de limite de frequência] o grupo de campos foi [atualização para oferecer suporte a eventos repetidos e personalizados](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo de dados | [!UICONTROL Referenciador da Web] | As propriedades do referenciador da Web foram [atualizado para incluir `xdm:linkName` e `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Esses são o nome e a região do elemento HTML selecionado na página anterior, respectivamente. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação da mensagem] | [A variável [!UICONTROL URL do rastreador] o campo foi adicionado](https://github.com/adobe/xdm/pull/1665/files) para o [!UICONTROL Adobe CJM ExperienceEvent]. Este rastreador fornece o URL selecionado pelo usuário. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação de mensagens] | [O vazio `meta:enum` propriedade removida](https://github.com/adobe/xdm/pull/1668/files) do URL [!UICONTROL Tipo de rastreamento] campo. |
| Tipo de dados | [!UICONTROL Informações da mídia] | [O padrão regex do `videoSegment` propriedade no [!UICONTROL Informações da mídia] o tipo de dados foi removido](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md)&#x200B;

## Serviço de query {#query-service}

O Serviço de consulta permite usar o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. Você pode unir qualquer conjunto de dados do data lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Habilitar conjuntos de dados para perfil com SQL | [Use LABELs em consultas CTAS para tornar um conjunto de dados &quot;perfil ativado&quot;](../../query-service/sql/syntax.md#create-table-as-select)ou use ALTER para atualizar conjuntos de dados existentes para serem habilitados para o perfil. Você pode usar essa construção de SQL estendido para fornecer suporte contínuo a atributos derivados para seus casos de uso de negócios do Perfil do cliente em tempo real. Consulte a [Fluxo SQL contínuo para o documento de atributos derivados](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) para obter mais detalhes. |
| Monitorar consultas programadas | Use o [Guia Consultas programadas](../../query-service/ui/monitor-queries.md) para encontrar informações importantes sobre as execuções de consulta e assinar alertas. Monitore consultas para obter detalhes de agendamento, status e mensagens/códigos de erro caso haja falha. |
| Alternar recurso de preenchimento automático | Eliminar determinados comandos de metadados e melhorar os tempos de processamento ao [alternar o recurso de preenchimento automático do Editor de consultas](../../query-service/ui/user-guide.md#auto-complete). Esse recurso sugere automaticamente possíveis palavras-chave SQL e detalhes da tabela para a consulta à medida que ela é gravada. |
| Amostras de conjunto de dados | Especifique uma taxa de amostragem em seu query e [usar amostras de conjunto de dados para criar uma amostra aleatória uniforme](../../query-service/essential-concepts/dataset-samples.md)ou criar amostras condicionais com base em critérios específicos. |

{style="table-layout:auto"}

Para obter mais informações sobre os Serviços de consulta, consulte [Visão geral do Serviço de consulta](../../query-service/home.md).


## Real-Time Customer Data Platform B2B Edition {#b2b}

Criado no Real-time Customer Data Platform (Real-Time CDP), o Real-Time CDP B2B Edition foi desenvolvido especificamente para profissionais de marketing que operam em um modelo de serviço business-to-business. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem públicos específicos com precisão e envolvam esses públicos em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Habilitar serviço de contas relacionadas | A nova função de alternância permite habilitar o serviço de contas relacionadas na sua conta. Para obter mais informações, leia o guia em [habilitando o serviço de contas relacionado](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Para saber mais sobre o Real-Time CDP B2B Edition, leia o [Visão geral da Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Designar acesso em nível de assinatura com [!DNL Google PubSub] | Agora você pode definir o acesso a uma assinatura de tópico específica ao usar o [!DNL Google PubSub] fonte fornecendo a ID de assinatura ao autenticar. Para obter mais informações, leia a [!DNL Google PubSub] tutorial de autenticação [uso da API do Serviço de fluxo](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [Interface do Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Assimilar dados de atividade personalizados do [!DNL Marketo] | Agora você pode trazer os dados de atividade personalizados de sua [!DNL Marketo] instância para Experience Platform. Para assimilar dados de atividades personalizadas, você deve configurar grupos de campos de atividades personalizadas no esquema Atividades B2B e criar um fluxo de dados usando o conjunto de dados de atividades. Quando o fluxo de dados for concluído, o conjunto de dados assimilado conterá atividades padrão e personalizadas do [!DNL Marketo] instância. Você pode então usar [Serviço de consulta](../../query-service/home.md) para acessar seus registros de atividade personalizados na Platform. Para obter mais informações, leia o guia em [criação de um fluxo de dados para dados de atividade personalizados](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Excluir contas não solicitadas de [!DNL Marketo] | Agora é possível configurar se deseja excluir ou incluir contas não solicitadas da assimilação ao criar um fluxo de dados para dados de empresas. Para obter mais informações, leia o guia em [criação de uma conexão de origem e fluxo de dados para [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
