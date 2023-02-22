---
title: Notas de versão da Adobe Experience Platform fevereiro de 2023
description: As notas de versão de fevereiro de 2023 para o Adobe Experience Platform.
source-git-commit: 1c2b7f291d0f8c0845a76ba4c863a9558da1bb4f
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 3%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de fevereiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Contas relacionadas no Real-Time CDP B2B Edition](#related-accounts)
- [Fontes](#sources)

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**
&#x200B; | Recurso | Descrição | | — | — | | Descontinuação de campo por meio da interface do usuário | Agora é possível descontinuar os campos dos seus esquemas depois que os dados forem assimilados. A desativação do campo XDM permite remover campos da exibição da interface do usuário, mantendo-os para uso. Se necessário, é possível revelar campos obsoletos, e todos os segmentos, consultas ou soluções de downstream que referenciam os campos serão executados como de costume. |

{style=&quot;table-layout:auto&quot;} &#x200B; Para obter mais informações sobre o XDM na plataforma, leia o [Visão geral do sistema XDM](../../xdm/home.md). &#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

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

## Contas relacionadas no Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>O recurso Contas relacionadas está disponível somente para clientes do Real-Time CDP B2B Edition.

Contas relacionadas, [!DNL Real-Time CDP B2B] O permite visualizar uma lista de contas semelhantes à conta que você está navegando. É possível incluir as contas relacionadas nas definições de segmento para ampliar o alcance ou aplicar critérios mais amplos em seus segmentos.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Ativar serviço de contas relacionadas | A nova função de alternância permite habilitar o serviço de contas relacionadas em sua conta. Para obter mais informações, leia o guia sobre [habilitando o serviço de contas relacionadas](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Leia mais sobre recursos de contas relacionadas nas seguintes páginas de documentação:

- [Contas relacionadas na visão geral do Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Guia contas relacionadas no guia da interface do usuário do perfil da conta](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Como usar contas relacionadas em definições de segmento](../../rtcdp/segmentation/b2b.md#related-accounts)

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