---
title: Guia de configuração das regras de vinculação do gráfico de identidade
description: Saiba mais sobre as etapas recomendadas a serem seguidas ao implementar seus dados com configurações de regras de vinculação de gráfico de identidade.
badge: Beta
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 5%

---

# Guia de configuração das regras de vinculação do gráfico de identidade

Leia este documento para obter um guia passo a passo que você pode seguir ao implementar seus dados com o Adobe Experience Platform Identity Service.

Estrutura passo a passo:

1. [Criar os namespaces de identidade necessários](#namespace)
2. [Use a ferramenta de simulação de gráficos para se familiarizar com o algoritmo de otimização de identidade](#graph-simulation)
3. [Use a ferramenta de configurações de identidade para designar seus namespaces exclusivos e configurar as classificações de prioridade para seus namespaces](#identity-settings)
4. [Criar um esquema do Experience Data Model (XDM)](#schema)
5. [Criar um conjunto de dados](#dataset)
6. [Assimilar seus dados no Experience Platform](#ingest)

## Pré-requisitos de pré-implementação

Antes de começar, primeiro verifique se os eventos autenticados no sistema sempre contêm um identificador de pessoa.

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## Criar namespaces de identidade {#namespace}

Se os dados exigirem, primeiro crie os namespaces apropriados para sua organização. Para obter etapas sobre como criar um namespace personalizado, leia o guia em [criar um namespace personalizado na interface do usuário](../features/namespaces.md#create-custom-namespaces).

## Usar ferramenta de simulação de gráfico {#graph-simulation}

Em seguida, navegue até o [ferramenta de simulação de gráficos](./graph-simulation.md) no espaço de trabalho da interface do usuário do Serviço de identidade. Você pode usar a ferramenta de simulação de gráficos para simular gráficos de identidade, criados com uma variedade de diferentes configurações de namespace único e prioridade de namespace.

Ao criar configurações diferentes, você pode usar a ferramenta de simulação de gráficos para conhecer e entender melhor como o algoritmo de otimização de identidade e determinadas configurações podem afetar como seu gráfico se comporta.

## Definir configurações de identidade {#identity-settings}

Assim que tiver uma ideia melhor de como deseja que o gráfico se comporte, navegue até o [ferramenta de configurações de identidade](./identity-settings-ui.md) no espaço de trabalho da interface do usuário do Serviço de identidade.

Use a ferramenta de configurações de identidade para designar seus namespaces exclusivos e configurar seus namespaces por ordem de prioridade. Quando terminar de aplicar as configurações, aguarde pelo menos seis horas para continuar a assimilar dados, pois levará pelo menos seis horas para que as novas configurações sejam refletidas no Serviço de identidade.

## Criar um esquema do XDM {#schema}

Com os namespaces exclusivos e as prioridades de namespace estabelecidas, agora é possível prosseguir para a configuração necessária para assimilar seus dados. Primeiro, você deve criar um esquema XDM. Dependendo dos seus dados, talvez seja necessário criar um esquema para o Perfil individual XDM e o ExperienceEvent XDM.

Para assimilar dados no Perfil do cliente em tempo real, você deve garantir que seu esquema contenha pelo menos um campo que tenha sido designado como a identidade principal. Ao configurar uma identidade principal, é possível ativar um determinado esquema para assimilação de perfil.

Para obter instruções sobre como criar um schema, leia o guia em [criação de um esquema XDM na interface do usuário](../../xdm/tutorials/create-schema-ui.md).

## Criar um conjunto de dados {#dataset}

Em seguida, crie um conjunto de dados para fornecer uma estrutura para os dados que você vai assimilar. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados funcionam em conjunto com esquemas e, para assimilar dados no Perfil do cliente em tempo real, seu conjunto de dados deve estar habilitado para assimilação de perfil. Para que seu conjunto de dados seja ativado para o Perfil, ele deve fazer referência a um esquema que esteja ativado para assimilação de Perfil.

Para obter instruções sobre como criar um conjunto de dados, leia o [guia da interface do usuário do conjunto de dados](../../catalog/datasets/user-guide.md).

## Assimilar seus dados {#ingest}

Nesse ponto, você deve ter o seguinte:

* As permissões necessárias para acessar os recursos do Serviço de identidade.
* Namespaces para seus dados.
* Namespaces exclusivos designados e prioridades configuradas para seus namespaces.
* Pelo menos um esquema XDM. (Dependendo dos seus dados e do caso de uso específico, talvez seja necessário criar esquemas de evento de perfil e de experiência.)
* Um conjunto de dados baseado no seu esquema.

Depois de ter todos os itens listados acima, você pode começar a assimilar seus dados no Experience Platform. Você pode realizar a assimilação de dados de várias maneiras diferentes. Você pode usar os seguintes serviços para trazer seus dados para o Experience Platform:

* [Assimilação em lote e por transmissão](../../ingestion/home.md)
* [Coleta de dados no Experience Platform](../../collection/home.md)
* [origens de Experience Platform](../../sources/home.md)

>[!TIP]
>
>Depois que os dados são assimilados, a carga de dados brutos do XDM não é alterada. Você ainda pode ver suas configurações de identidade principais na interface do usuário. No entanto, essas configurações serão substituídas pelas configurações de identidade.

Para qualquer feedback, use o **[!UICONTROL Feedback do Beta]** no espaço de trabalho da interface do usuário do Serviço de identidade.