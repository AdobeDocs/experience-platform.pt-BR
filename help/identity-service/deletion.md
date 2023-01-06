---
title: Exclusões no serviço de identidade
description: Este documento fornece uma visão geral dos vários mecanismos que podem ser usados para excluir seus dados de identidade no Experience Platform e para esclarecer como os gráficos de identidade podem ser afetados.
source-git-commit: 17e39f6e9d6e62e22f867de91d571593ba945c71
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 1%

---

# Exclusões no serviço de identidade

O Adobe Experience Platform Identity Service gera gráficos de identidade ao vincular deterministicamente identidades entre dispositivos e sistemas de uma pessoa individual. Os links de gráficos de identidade são estabelecidos quando duas ou mais identidades marcadas são recebidas na mesma linha de dados.

Os gráficos de identidade são aproveitados pelo Perfil do cliente em tempo real para criar uma visão abrangente e singular dos atributos e comportamentos do cliente, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real, para pessoas e não dispositivos.

Este documento fornece uma visão geral dos vários mecanismos que podem ser usados para excluir seus dados de identidade no Experience Platform e para esclarecer como os gráficos de identidade podem ser afetados.

## Introdução

O documento abaixo faz referência aos seguintes recursos do Experience Platform:

* [Serviço de identidade](home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
   * [Gráfico de identidade](./ui/identity-graph-viewer.md): Um gráfico de identidade é um mapa de relacionamentos entre diferentes identidades para um cliente específico, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais.
   * [Namespaces de identidade](namespaces.md): Os namespaces de identidade são um componente do Serviço de identidade que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.
* [Serviço de catálogo](../catalog/home.md): Explore a linhagem de dados, os metadados, as descrições dos arquivos, os diretórios e os conjuntos de dados no lago de dados.
* [Higiene dos dados](../hygiene/home.md): Gerencie os dados do consumidor armazenados agendando expirações automatizadas do conjunto de dados ou excluindo registros individuais de um conjunto de dados ou de todos os conjuntos de dados.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Gerencie solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais nos aplicativos Adobe Experience Cloud.
* [Perfil do cliente em tempo real](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.

## Exclusões de identidade única

Solicitações de exclusão de identidade única permitem excluir uma identidade em um gráfico, resultando na remoção de links vinculados a uma única identidade de usuário associada a um namespace de identidade. Você pode usar [Higiene dos dados](../hygiene/home.md) para limpeza de dados, remoção de dados anônimos ou minimização de dados dos dados coletados. Para casos de uso, como solicitações de clientes para exclusão de dados e conformidade com as regras de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR), é possível usar os mecanismos fornecidos pelo [Privacy Service](../privacy-service/home.md).

As seções abaixo destacam os mecanismos que podem ser usados para solicitações de exclusão de identidade única no Experience Platform.

### Exclusão de identidade única no Privacy Service

O Privacy Service processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme delineado por regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e a Lei de Privacidade do Consumidor da Califórnia (CCPA). Com o Privacy Service, você pode enviar solicitações de trabalho usando a API ou a interface do usuário. Quando o Experience Platform recebe uma solicitação de exclusão do Privacy Service, a Platform envia uma confirmação para o Privacy Service de que a solicitação foi recebida e os dados afetados foram marcados para exclusão. A exclusão da identidade individual é baseada no namespace e/ou no valor de ID fornecidos. Além disso, a exclusão ocorre para todas as sandboxes associadas a uma determinada organização. Para obter mais informações, leia o guia sobre [processamento de solicitação de privacidade no Identity Service](privacy.md).

### Exclusão de identidade única no [!UICONTROL Higiene de dados] espaço de trabalho

O [[!UICONTROL Higiene de dados] espaço de trabalho](../hygiene/ui/overview.md) na interface do usuário da plataforma, é possível excluir registros do consumidor que estão participando do Serviço de identidade e do Perfil do cliente em tempo real. Para obter um guia abrangente sobre como usar o [!UICONTROL Higiene de dados] no workspace, consulte o tutorial em [exclusão de registros de consumidor](../hygiene/ui/record-delete.md).

A tabela abaixo fornece um detalhamento das diferenças entre a exclusão de identidade única no Privacy Service e a higiene dos dados:

| Exclusão de identidade única | Privacy Service | Higiene dos dados |
| --- | --- | --- |
| Casos de uso aceitos | Somente solicitações de privacidade de dados (GDPR, CCPA). | Gestão dos dados armazenados no Experience Platform. |
| Latência estimada | Dias até semanas | Days |
| Serviços afetados | A exclusão de identidade única no Privacy Service permite selecionar se os dados serão excluídos do Serviço de identidade, do Perfil do cliente em tempo real ou do lago de dados. | A exclusão de identidade única na higiene de dados exclui os dados selecionados no Serviço de identidade, no Perfil do cliente em tempo real e no lago de dados. |
| Padrões de exclusão | Exclua uma identidade do Serviço de identidade. | Exclua uma identidade do Serviço de identidade. |

{style=&quot;table-layout:auto&quot;}

## Exclusão do conjunto de dados

As seções a seguir descrevem os mecanismos que podem ser usados para excluir conjuntos de dados e os links de identidade associados no Experience Platform.

### Exclusão do conjunto de dados no serviço de catálogo

Você pode usar o Serviço de catálogo para enviar solicitações para exclusão do conjunto de dados. Para obter mais informações sobre como excluir conjuntos de dados com o Serviço de catálogo, leia o guia sobre [exclusão de objetos usando a API do Serviço de catálogo](../catalog/api/delete-object.md). Como alternativa, você pode usar a interface do usuário do Platform para enviar solicitações para exclusão do conjunto de dados. Para obter mais informações, leia a [guia do usuário de conjuntos de dados](../catalog/datasets/user-guide.md#delete-a-dataset).

### Expirações do conjunto de dados na higiene dos dados

O [[!UICONTROL Higiene de dados] espaço de trabalho](../hygiene/ui/overview.md) na interface do usuário do Adobe Experience Platform permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o lago de dados, o Serviço de identidade e o Perfil do cliente em tempo real começam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Para obter mais informações, leia o guia sobre [gerenciar as expirações do conjunto de dados usando o [!UICONTROL Higiene de dados] espaço de trabalho](../hygiene/ui/dataset-expiration.md).

A tabela abaixo fornece um detalhamento das diferenças entre a exclusão do conjunto de dados no Serviço de catálogo e na Higiene de dados:

| Exclusão do conjunto de dados | Serviço de catálogo | Higiene dos dados |
| --- | --- | --- |
| Casos de uso aceitos | Exclua conjuntos completos de dados e suas informações de identidade associadas na Plataforma. | Gestão dos dados armazenados no Experience Platform. |
| Latência estimada | Days | Days |
| Serviços afetados | A exclusão do conjunto de dados por meio do Serviço de catálogo exclui os dados do Serviço de identidade, do Perfil do cliente em tempo real e do lago de dados. | A exclusão do conjunto de dados por meio da higiene de dados exclui os dados do Serviço de identidade, do Perfil do cliente em tempo real e do lago de dados. |
| Padrão de exclusão | Exclua identidades vinculadas do Serviço de identidade estabelecidas por um conjunto de dados específico. | Exclua identidades vinculadas do Serviço de identidade estabelecidas por um conjunto de dados específico, com base no cronograma de expiração. |

{style=&quot;table-layout:auto&quot;}

## Diferentes estados dos gráficos de identidade após exclusão

Todas as exclusões de gráficos de identidade resultam na remoção de links entre duas ou mais identidades, conforme especificado pela solicitação de exclusão. Para solicitações de exclusão do conjunto de dados, todos os links de identidade estabelecidos pelo conjunto de dados especificado são removidos e podem ou não remover identidades dos gráficos. Para solicitações de exclusão de identidade única, os links de identidade são removidos para a identidade especificada e, consequentemente, o próprio valor de identidade é removido de todos os gráficos de identidade. Identidades sem um único link para outra identidade não são armazenadas no Serviço de identidade.

Abaixo está um esboço dos possíveis impactos que as exclusões podem ter no estado dos gráficos de identidade.

| Estado do gráfico de identidade | Descrição |
| --- | --- |
| Atualização parcial | Uma atualização parcial de um gráfico acontece quando pelo menos duas identidades permanecem vinculadas em um gráfico depois que uma solicitação de exclusão é processada com êxito. Após a exclusão, os links de identidade restantes poderão permanecer conectados entre si ou podem ser divididos em dois ou mais gráficos separados, dependendo das identidades excluídas. |
| Remoção completa | Um gráfico deve ter pelo menos duas identidades vinculadas para existir. Portanto, se uma solicitação de exclusão resultar na remoção de todos os links existentes em um gráfico, o gráfico será completamente removido. |
| Sem alterações | Um gráfico não será afetado se uma determinada solicitação de exclusão contiver uma identidade ou um conjunto de dados que não esteja associado a nenhum membro do gráfico. Além disso, um gráfico não é atualizado mesmo se a solicitação de exclusão remover um link entre um conjunto de dados ou uma combinação de conjunto de dados de identidade, visto que o link foi estabelecido por outro link que não foi excluído. Isso significa que, se um link existir em dois conjuntos de dados diferentes, o gráfico não será atualizado porque apenas um dos conjuntos de dados foi removido. |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Este documento cobriu os vários mecanismos que podem ser usados para excluir identidades e conjuntos de dados no Experience Platform. Este documento também descreve como as exclusões de identidade e conjunto de dados podem afetar os gráficos de identidade. Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do Serviço de identidade](home.md).