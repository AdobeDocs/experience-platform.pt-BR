---
title: Guia de configuração das regras de vinculação do gráfico de identidade
description: Saiba mais sobre as etapas recomendadas a serem seguidas ao implementar seus dados com configurações de regras de vinculação de gráfico de identidade.
badge: Beta
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: e3568aa925661f4f519daf6572fd2df40b163cb5
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 2%

---

# Guia de configuração das regras de vinculação do gráfico de identidade

>[!AVAILABILITY]
>
>As regras de vinculação do gráfico de identidade estão na versão beta. Entre em contato com a equipe de conta do Adobe para obter informações sobre os critérios de participação. O recurso e a documentação estão sujeitos a alterações.

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

## Definir permissões {#set-permissions}

A primeira etapa do processo de implementação do Serviço de identidade é garantir que sua conta Experience Platform seja adicionada a uma função que esteja provisionada com as permissões necessárias. O administrador pode configurar permissões para sua conta navegando até a interface de permissões no Adobe Experience Cloud. A partir daí, sua conta deve ser adicionada a uma função com as seguintes permissões:

* [!UICONTROL Exibir Configurações de Identidade]: aplique esta permissão para poder exibir namespaces exclusivos e a prioridade de namespace na página de procura de namespace de identidade.
* [!UICONTROL Editar configurações de identidade]: aplique esta permissão para poder editar e salvar suas configurações de identidade.

Para obter mais informações sobre permissões, leia o [guia de permissões](../../access-control/abac/ui/permissions.md).

## Criar namespaces de identidade {#namespace}

Se os dados exigirem, primeiro crie os namespaces apropriados para sua organização. Para obter etapas sobre como criar um namespace personalizado, leia o manual sobre [criação de um namespace personalizado na interface](../features/namespaces.md#create-custom-namespaces).

## Usar ferramenta de simulação de gráfico {#graph-simulation}

Em seguida, navegue até a [ferramenta de simulação de gráficos](./graph-simulation.md), no espaço de trabalho da interface do usuário do Serviço de Identidade. Você pode usar a ferramenta de simulação de gráficos para simular gráficos de identidade, criados com uma variedade de diferentes configurações de namespace único e prioridade de namespace.

Ao criar configurações diferentes, você pode usar a ferramenta de simulação de gráficos para conhecer e entender melhor como o algoritmo de otimização de identidade e determinadas configurações podem afetar como seu gráfico se comporta.

## Definir configurações de identidade {#identity-settings}

Assim que tiver uma ideia melhor de como deseja que o gráfico se comporte, navegue até a [ferramenta de configurações de identidade](./identity-settings-ui.md) no espaço de trabalho da interface do usuário do Serviço de Identidade.

Use a ferramenta de configurações de identidade para designar seus namespaces exclusivos e configurar seus namespaces por ordem de prioridade. Quando terminar de aplicar as configurações, aguarde pelo menos seis horas para continuar a assimilar dados, pois levará pelo menos seis horas para que as novas configurações sejam refletidas no Serviço de identidade.

## Criar um esquema do XDM {#schema}

Com os namespaces exclusivos e as prioridades de namespace estabelecidas, agora é possível prosseguir para a configuração necessária para assimilar seus dados. Primeiro, você deve criar um esquema XDM. Dependendo dos seus dados, talvez seja necessário criar um esquema para o Perfil individual XDM e o ExperienceEvent XDM.

Para assimilar dados no Perfil do cliente em tempo real, você deve garantir que seu esquema contenha pelo menos um campo que tenha sido designado como a identidade principal. Ao configurar uma identidade principal, é possível ativar um determinado esquema para assimilação de perfil.

Para obter instruções sobre como criar um esquema, leia o manual sobre [criação de um esquema XDM na interface](../../xdm/tutorials/create-schema-ui.md).

## Criar um conjunto de dados {#dataset}

Em seguida, crie um conjunto de dados para fornecer uma estrutura para os dados que você vai assimilar. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados funcionam em conjunto com esquemas e, para assimilar dados no Perfil do cliente em tempo real, seu conjunto de dados deve estar habilitado para assimilação de perfil. Para que seu conjunto de dados seja ativado para o Perfil, ele deve fazer referência a um esquema que esteja ativado para assimilação de Perfil.

Para obter instruções sobre como criar um conjunto de dados, leia o [guia da interface do conjunto de dados](../../catalog/datasets/user-guide.md).

## Assimilar seus dados {#ingest}

>[!WARNING]
>
>* Durante o processo de pré-implementação, você deve garantir que os eventos autenticados que seu sistema enviará para o Experience Platform sempre contenham um identificador de pessoa, como CRMID.
>* Durante a implementação, você deve garantir que o namespace exclusivo com a maior prioridade esteja sempre presente em cada perfil. Consulte o [apêndice](#appendix) para obter exemplos de cenários de gráficos que são resolvidos garantindo que cada perfil contenha o namespace exclusivo com a prioridade mais alta.
>* Se você estiver usando o [conector de origem do Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para assimilar dados, deverá dar às ECIDs uma prioridade mais alta do que a AAID, pois o Serviço de Identidade bloqueia a AAID. Ao priorizar a ECID, você pode instruir o Serviço de identidade a armazenar eventos não autenticados na ECID em vez da AAID.

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

Para qualquer comentário, use a opção **[!UICONTROL comentários sobre o Beta]** no espaço de trabalho da interface do usuário do Serviço de Identidade.

## Apêndice {#appendix}

Leia esta seção para obter informações adicionais que você pode consultar ao implementar suas configurações de identidade e namespaces exclusivos.

### Cenário do dispositivo compartilhado {#shared-device-scenario}

Você deve garantir que um único namespace seja usado em todos os perfis que representam uma pessoa. Ao fazer isso, o Serviço de identidade pode detectar o identificador de pessoa apropriado em um determinado gráfico.

>[!BEGINTABS]

>[!TAB Sem um namespace de identificador de pessoa singular]

Sem um namespace exclusivo para representar seus identificadores de pessoa, você pode acabar com um gráfico que se vincula a identificadores de pessoa diferentes para a mesma ECID. Neste exemplo, B2BCRM e B2CCRM estão vinculados à mesma ECID ao mesmo tempo. Este gráfico sugere que Tom, usando sua conta de login B2C, compartilhou um dispositivo com Summer, usando sua conta de login B2B. No entanto, o sistema reconhecerá que este é um perfil (colapso de gráfico).

![Um cenário de gráfico em que dois identificadores de pessoa estão vinculados à mesma ECID.](../images/graph-examples/multi_namespaces.png)

>[!TAB Com um namespace de identificador de pessoa singular]

Dado um namespace exclusivo (neste caso, uma CRMID em vez de dois namespaces diferentes), o Serviço de identidade pode discernir o identificador de pessoa que foi associado pela última vez à ECID. Neste exemplo, como existe uma CRMID exclusiva, o Serviço de identidade pode reconhecer um cenário de &quot;dispositivo compartilhado&quot;, em que duas entidades estão compartilhando o mesmo dispositivo.

![Um cenário de gráfico de dispositivo compartilhado, em que dois identificadores de pessoa são vinculados à mesma ECID, mas o link mais antigo é removido.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

### Perdendo o cenário de ID de logon {#dangling-loginid-scenario}

O gráfico a seguir simula um cenário de ID de logon &quot;pendente&quot;. Neste exemplo, duas IDs de logon diferentes são vinculadas à mesma ECID. No entanto, `{loginID: ID_C}` não está vinculado ao CRMID. Portanto, não há como o Serviço de identidade detectar que essas duas IDs de logon representam duas entidades diferentes.

>[!BEGINTABS]

>[!TAB LoginID ambíguo]

Neste exemplo, `{loginID: ID_C}` é deixado pendente e desvinculado a um CRMID. Assim, a entidade de pessoa à qual essa ID de logon deve ser associada é deixada ambígua.

![Um exemplo de gráfico com um cenário de loginID &quot;pendente&quot;.](../images/graph-examples/dangling_example.png)

>[!TAB loginID está vinculado a um CRMID]

Neste exemplo, `{loginID: ID_C}` está vinculado a `{CRMID: Tom}`. Portanto, o sistema pode discernir que essa ID de logon está associada ao Tom.

![LoginID está vinculado a um CRMID.](../images/graph-examples/id_c_tom.png)

>[!TAB loginID está vinculado a outro CRMID]

Neste exemplo, `{loginID: ID_C}` está vinculado a `{CRMID: Summer}`. Portanto, o sistema pode discernir que essa ID de logon está associada a outra entidade de pessoa, neste caso, o Verão.

Este exemplo também mostra que Tom e Summer são entidades de pessoas diferentes que estão compartilhando um dispositivo, representado por `{ECID: 111}`.

![LoginID está vinculado a outro CRMID.](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]
