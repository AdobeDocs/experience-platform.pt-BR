---
title: Exclusões no serviço de identidade
description: Este documento fornece uma visão geral dos vários mecanismos que você pode usar para excluir os dados de identidade no Experience Platform e para esclarecer como os gráficos de identidade podem ser afetados.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 576b17842ee1c5722332ba49e26b037537ec96ed
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# Exclusões no serviço de identidade

O Serviço de identidade da Adobe Experience Platform gera gráficos de identidade ao vincular deterministicamente identidades em dispositivos e sistemas para uma pessoa individual. Os vínculos entre gráficos de identidade são estabelecidos quando duas ou mais identidades marcadas são recebidas na mesma linha de dados.

Os gráficos de identidade são aproveitados pelo Perfil do cliente em tempo real para criar uma visualização abrangente e singular dos atributos e comportamentos do cliente, permitindo que você forneça experiências digitais impactantes e pessoais em tempo real, para pessoas, e não para dispositivos.

Este documento fornece uma visão geral dos vários mecanismos que você pode usar para excluir os dados de identidade no Experience Platform e para esclarecer como os gráficos de identidade podem ser afetados.

## Introdução

O documento abaixo faz referência aos seguintes recursos do Experience Platform:

* [Serviço de identidade](../home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
   * [Gráfico de identidade](./identity-graph-viewer.md): um gráfico de identidade é um mapa dos relacionamentos entre identidades diferentes para um cliente específico, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais.
   * [Namespaces de identidade](./namespaces.md): os namespaces de identidade são um componente do Serviço de identidade que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.
* [Serviço de catálogo](../../catalog/home.md): explore a linhagem de dados, os metadados, as descrições dos arquivos, os diretórios e os conjuntos de dados no data lake.
* [Higiene de dados](../../hygiene/home.md): gerencie os dados do consumidor armazenados agendando expirações automáticas do conjunto de dados ou excluindo registros individuais de um conjunto de dados ou de todos os conjuntos de dados.
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md): gerencie solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais nos aplicativos da Adobe Experience Cloud.
* [Perfil do cliente em tempo real](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.

## Exclusões de identidade única

As solicitações de exclusão de identidade únicas permitem excluir uma identidade em um gráfico, resultando na remoção de links vinculados a uma única identidade de usuário associada a um namespace de identidade. Você pode usar mecanismos fornecidos pelo [Privacy Service](../../privacy-service/home.md) para casos de uso como solicitações de exclusão de dados do cliente e conformidade com regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR).

As seções abaixo descrevem os mecanismos que podem ser usados para solicitações de exclusão de identidade única no Experience Platform.

### Exclusão de identidade única no Privacy Service

O Privacy Service processa solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e a Lei de Privacidade do Consumidor da Califórnia (CCPA). Com o Privacy Service, você pode enviar solicitações de trabalho usando a API ou a interface do usuário. Quando o Experience Platform recebe uma solicitação de exclusão do Privacy Service, a Platform envia uma confirmação para o Privacy Service de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. A exclusão da identidade individual baseia-se no namespace e/ou valor de ID fornecido. Além disso, a exclusão ocorre para todas as sandboxes associadas a uma determinada organização. Para obter mais informações, leia o guia em [processamento de solicitação de privacidade no Serviço de identidade](../privacy.md).

A tabela abaixo fornece um detalhamento da exclusão de identidade única no Privacy Service:

| Exclusão de identidade única | Privacy Service |
| --- | --- |
| Casos de uso aceitos | Somente solicitações de privacidade de dados (GDPR, CCPA). |
| Latência estimada | Dias a semanas |
| Serviços afetados | A exclusão de identidade única no Privacy Service permite selecionar se os dados serão excluídos do Serviço de identidade, do Perfil do cliente em tempo real ou do data lake. |
| Padrões de exclusão | Excluir uma identidade do Serviço de identidade. |

{style="table-layout:auto"}

## Exclusão do conjunto de dados

As seções a seguir descrevem os mecanismos que podem ser usados para excluir conjuntos de dados e links de identidade associados no Experience Platform.

### Exclusão de conjunto de dados no serviço de catálogo

Você pode usar o Serviço de catálogo para enviar solicitações de exclusão do conjunto de dados. Para obter mais informações sobre como excluir conjuntos de dados com o Serviço de catálogo, leia o guia em [exclusão de objetos usando a API do Serviço de Catálogo](../../catalog/api/delete-object.md). Como alternativa, você pode usar a interface do usuário da Platform para enviar solicitações de exclusão do conjunto de dados. Para obter mais informações, leia a [guia do usuário de conjuntos de dados](../../catalog/datasets/user-guide.md#delete-a-dataset).

### Expirações do conjunto de dados na higiene de dados

A variável [[!UICONTROL Higiene de dados] espaço de trabalho](../../hygiene/ui/overview.md) na interface do Adobe Experience Platform, permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o data lake, o serviço de identidade e o perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Para obter mais informações, leia o guia em [gerenciar expirações de conjunto de dados usando o [!UICONTROL Higiene de dados] espaço de trabalho](../../hygiene/ui/dataset-expiration.md).

A tabela abaixo fornece um detalhamento das diferenças entre a exclusão do conjunto de dados no Serviço de catálogo e na Higiene de dados:

| Exclusão do conjunto de dados | Serviço de catálogo | Higiene de dados |
| --- | --- | --- |
| Casos de uso aceitos | Excluir conjuntos de dados completos e suas informações de identidade associadas na Platform. | Gestão de dados armazenados no Experience Platform. |
| Latência estimada | Days | Days |
| Serviços afetados | A exclusão de conjunto de dados por meio do Serviço de catálogo exclui os dados do Serviço de identidade, do Perfil do cliente em tempo real e do data lake. | A exclusão de conjuntos de dados por meio da higiene de dados exclui os dados do Serviço de identidade, do Perfil do cliente em tempo real e do data lake. |
| Padrão de exclusão | Excluir identidades vinculadas do Serviço de identidade estabelecido por um conjunto de dados específico. | Excluir identidades vinculadas do Serviço de identidade estabelecido por um conjunto de dados específico, com base no agendamento de expiração. |

{style="table-layout:auto"}

## Diferentes estados dos gráficos de identidade após a exclusão

Todas as exclusões de gráficos de identidade resultam na remoção de vínculos entre duas ou mais identidades, conforme especificado pela solicitação de exclusão. Para solicitações de exclusão do conjunto de dados, todos os vínculos de identidade estabelecidos pelo conjunto de dados especificado são removidos e podem ou não remover identidades dos gráficos. Para solicitações de exclusão de identidade únicas, os vínculos de identidade são removidos para a identidade especificada e, consequentemente, o próprio valor de identidade é removido de todos os gráficos de identidade. As identidades sem um vínculo único com outra identidade não são armazenadas no Serviço de identidade.

Abaixo está um esboço dos possíveis impactos que as exclusões podem ter no estado dos gráficos de identidade.

| Estado do gráfico de identidade | Descrição |
| --- | --- |
| Atualização parcial | Uma atualização parcial de um gráfico acontece quando pelo menos duas identidades permanecem vinculadas em um gráfico depois que uma solicitação de exclusão é processada com êxito. Após a exclusão, os links de identidade restantes podem permanecer conectados uns aos outros ou podem ser divididos em dois ou mais gráficos separados, dependendo das identidades que foram excluídas. |
| Remoção completa | Um gráfico deve ter pelo menos duas identidades vinculadas para que possa existir. Portanto, se uma solicitação de exclusão resultar na remoção de todos os links existentes em um gráfico, o gráfico será completamente removido. |
| Sem alterações | Um gráfico não será afetado se uma solicitação de exclusão específica contiver uma identidade ou um conjunto de dados que não esteja associado a nenhum membro do gráfico. Além disso, um gráfico não é atualizado mesmo que a solicitação de exclusão remova um link entre um conjunto de dados ou uma combinação identidade-conjunto de dados, visto que o link foi estabelecido por outro link que não foi excluído. Isso significa que, se um link existir em dois conjuntos de dados diferentes, o gráfico não será atualizado porque apenas um dos conjuntos de dados será removido. |

{style="table-layout:auto"}

## Próximas etapas

Esse documento abordou os vários mecanismos que você pode usar para excluir identidades e conjuntos de dados no Experience Platform. Este documento também descreve como as exclusões de identidade e conjunto de dados podem afetar os gráficos de identidade. Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
