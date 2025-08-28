---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;unificado;Perfil;rtcp;habilitar perfil;Habilitar perfil;esquema de união;PERFIL DE UNIÃO;perfil de união
title: Guia da interface do usuário do Perfil do cliente em tempo real
description: O Perfil do cliente em tempo real cria uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. Este documento serve como um guia para interagir com o Perfil do cliente em tempo real na interface do usuário do Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: d9fc1fa6a1bbc6b13b2600a5ec9400a0b488056a
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 3%

---

# [!DNL Real-Time Customer Profile] Guia da interface

O [!DNL Real-Time Customer Profile] cria uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. Este documento serve como um guia para interagir com os dados do [!DNL Real-Time Customer Profile] na interface do usuário (UI) do Adobe Experience Platform.

## Introdução

Este guia de interface do usuário requer uma compreensão dos vários serviços do [!DNL Experience Platform] envolvidos no gerenciamento do [!DNL Real-Time Customer Profiles]. Antes de ler este guia ou trabalhar na interface do usuário, consulte a documentação dos seguintes serviços:

* [[!DNL Real-Time Customer Profile] visão geral](../home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] unindo identidades de fontes de dados diferentes conforme elas são assimiladas em [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.

## [!UICONTROL Visão geral]

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Perfis]** na navegação à esquerda para abrir a guia **[!UICONTROL Visão geral]** exibindo o painel de perfil.

>[!NOTE]
>
>Se sua organização for nova no Experience Platform e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, o painel [!UICONTROL Perfis] não estará visível. Em vez disso, a guia [!UICONTROL Visão geral] exibe links e documentação para ajudar você a começar a usar o Perfil do cliente em tempo real.

### Painel do perfil {#profile-dashboard}

O painel de perfil descreve as métricas principais relacionadas aos dados de perfil de sua organização.

Para saber mais, visite o [guia do painel do perfil](../../dashboards/guides/profiles.md).

![O painel Perfil é exibido.](../../dashboards/images/profiles/dashboard-overview.png)

## Métricas da guia [!UICONTROL Procurar]

Selecione a guia **[!UICONTROL Procurar]** para exibir várias métricas relacionadas aos dados de perfil de sua organização. Você também pode usar essa guia para navegar no armazenamento de Perfil usando uma política de mesclagem ou uma identidade, conforme descrito na próxima seção deste guia.

No lado direito da guia **[!UICONTROL Procurar]** está a [contagem de perfis](#profile-count) e uma listagem de [perfis por namespace](#profiles-by-namespace).

>[!NOTE]
>
>Estas métricas de perfil podem ser diferentes das métricas exibidas no [painel de perfil](#profile-dashboard), pois são avaliadas usando a política de mesclagem padrão de sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem, incluindo como definir uma política de mesclagem padrão, consulte a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

Além dessas métricas, esta seção fornece uma data e hora da última atualização, mostrando quando as métricas foram avaliadas pela última vez.

![As métricas do Perfil são exibidas e destacadas.](../images/user-guide/browse-metrics.png)

### Contagem de perfis {#profile-count}

A contagem de perfis exibe o número total de perfis que sua organização tem na Experience Platform, depois que a política de mesclagem padrão da organização se mescla com fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em diferentes canais, mas esses fragmentos seriam mesclados (de acordo com a política de mesclagem padrão) e retornariam uma contagem de &quot;1&quot; perfil, pois todos estão relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de série temporal (evento), como perfis do Adobe Analytics. A contagem de perfis é atualizada regularmente para fornecer um número total de perfis atualizado no Experience Platform.

#### Atualização da métrica de contagem de perfis

Quando a assimilação de registros no armazenamento [!DNL Profile] aumenta ou diminui a contagem em mais de 3%, um trabalho é acionado para atualizar a contagem. Para workflows de dados de transmissão, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 3% foi atingido. Se tiver sido, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para assimilação em lote, dentro de 15 minutos após a assimilação bem-sucedida de um lote no Armazenamento de perfis, se o limite de aumento ou diminuição de 3% for atingido, um trabalho será executado para atualizar a contagem de perfis.

### [!UICONTROL Perfis por namespace] {#profiles-by-namespace}

A métrica **[!UICONTROL Perfis por namespace]** exibe a contagem total e o detalhamento de namespaces em todos os perfis mesclados no repositório de perfis. O número total de perfis por namespace (em outras palavras, somando os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

#### Atualizando a métrica [!UICONTROL Perfis por namespace]

Semelhante à métrica [contagem de perfis](#profile-count), quando a assimilação de registros no repositório [!DNL Profile] aumenta ou diminui a contagem em mais de 5%, um trabalho é acionado para atualizar as métricas de namespace. Para workflows de dados de transmissão, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para assimilação em lote, dentro de 15 minutos após a assimilação bem-sucedida de um lote no repositório [!DNL Profile], se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar as métricas.

## Use a guia [!UICONTROL Procurar] para exibir perfis

Na guia **[!UICONTROL Procurar]**, é possível exibir perfis de exemplo usando uma política de mesclagem ou pesquisar perfis específicos usando um valor e um namespace de identidade.

![Os perfis que pertencem à organização são exibidos.](../images/user-guide/none-selected.png)

### Procurar por [!UICONTROL Política de mesclagem]

Por padrão, a guia **[!UICONTROL Procurar]** está definida como a política de mesclagem padrão para sua organização. Para escolher uma política de mesclagem diferente, selecione `X` ao lado do nome da política de mesclagem e use o seletor para abrir a caixa de diálogo **[!UICONTROL Selecionar política de mesclagem]**.

>[!NOTE]
>
>Se não houver política de mesclagem selecionada, use o botão seletor ao lado do campo **[!UICONTROL Política de mesclagem]** para abrir a caixa de diálogo de seleção.

![O seletor de política de mesclagem está realçado.](../images/user-guide/browse-by-merge-policy.png)

Para escolher uma política de mesclagem na caixa de diálogo **[!UICONTROL Selecionar política de mesclagem]**, selecione o botão de opção ao lado do nome da política e use **[!UICONTROL Selecionar]** para retornar à guia [!UICONTROL Procurar]. Você pode selecionar **[!UICONTROL Exibir]** para atualizar os perfis de exemplo e ver uma amostragem de perfis com a nova política de mesclagem aplicada.

![Uma caixa de diálogo na qual você pode selecionar a política de mesclagem para filtrar é exibida.](../images/user-guide/select-merge-policy.png)

Os perfis exibidos representam uma amostra de até 20 perfis do armazenamento de perfis da sua organização, depois que a política de mesclagem selecionada é aplicada. Os perfis de exemplo para a política de mesclagem selecionada são atualizados quando novos dados são adicionados ao armazenamento de perfis da sua organização.

Para exibir os detalhes de um dos perfis de exemplo, selecione a **[!UICONTROL ID do Perfil]**. Para obter mais informações, consulte a seção mais adiante neste guia em [exibindo detalhes do perfil](#profile-detail).

![Perfis de exemplo que correspondem à política de mesclagem são exibidos.](../images/user-guide/sample-profiles.png)

Para saber mais sobre as políticas de mesclagem e sua função na Experience Platform, consulte a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

### Procurar por [!UICONTROL Identidade] {#browse-identity}

Na guia **[!UICONTROL Procurar]**, você pode usar um namespace de identidade para procurar um perfil específico por um valor de identidade. A navegação por uma identidade exige que você forneça uma política de mesclagem, um namespace de identidade e um valor de identidade.

![O seletor de política de mesclagem está realçado.](../images/user-guide/browse-by-merge-policy.png)

Se necessário, use o seletor de **[!UICONTROL Política de mesclagem]** para abrir a caixa de diálogo **[!UICONTROL Selecionar política de mesclagem]** e escolher a política de mesclagem que deseja usar.

![Uma caixa de diálogo na qual você pode selecionar a política de mesclagem para filtrar é exibida.](../images/user-guide/select-merge-policy.png)

Em seguida, use o seletor de **[!UICONTROL Namespace de identidade]** para abrir a caixa de diálogo **[!UICONTROL Selecionar namespace de identidade]** e escolha o namespace pelo qual deseja pesquisar. Se sua organização tiver muitos namespaces, você poderá usar a barra de pesquisa na caixa de diálogo para começar a digitar o nome de um namespace.

Você pode selecionar um namespace para exibir detalhes adicionais ou selecionar o botão de opção para escolher um namespace. Você pode usar **[!UICONTROL Selecionar]** para continuar.

![É exibida uma caixa de diálogo na qual você pode selecionar o namespace de identidade pelo qual filtrar.](../images/user-guide/select-identity-namespace.png)

Depois de selecionar um [!UICONTROL namespace de identidade] e retornar à guia [!UICONTROL Procurar], você pode inserir um **[!UICONTROL valor de identidade]** relacionado ao namespace selecionado.

>[!NOTE]
>
>Esse valor é específico para um perfil de cliente individual e deve ser uma entrada válida para o namespace fornecido. Por exemplo, selecionar o namespace de identidade &quot;Email&quot; exigiria um valor de identidade na forma de um endereço de email válido.

![O valor de identidade pelo qual você deseja filtrar está realçado.](../images/user-guide/filter-identity-value.png)

Depois que um valor for inserido, selecione **[!UICONTROL Exibir]** e um único perfil correspondente ao valor será retornado. Selecione a **[!UICONTROL ID do Perfil]** para exibir os detalhes do perfil.

![O perfil que corresponde ao valor de identidade está realçado.](../images/user-guide/filtered-identity-value.png)

## Exibir detalhes do perfil {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Entidade não encontrada"
>abstract="Isso significa que a Experience Platform não encontrou a entidade solicitada. Para resolver esse erro, tente uma das seguintes soluções:<ul><li>Verifique se a ID do perfil correta está listada no URL da entidade que você está tentando acessar.</li><li>Verifique se você tem a combinação correta de Organização e sandbox para a entidade que está tentando acessar.</li></ul>"

Depois de selecionar uma **[!UICONTROL ID de perfil]**, a guia **[!UICONTROL Detalhes]** é aberta. As informações do perfil exibidas na guia **[!UICONTROL Detalhes]** foram mescladas de vários fragmentos de perfil para formar uma única visualização do cliente individual. Isso inclui detalhes do cliente, como atributos básicos, identidades vinculadas e preferências de canal.

Os campos padrão mostrados também podem ser alterados em um nível organizacional para exibir atributos de perfil preferenciais. Para saber mais sobre como personalizar esses campos, incluindo instruções passo a passo para adicionar e remover atributos e redimensionar painéis de painel, leia o [guia de personalização de detalhes do perfil](profile-customization.md).

![A guia Detalhes está realçada. Os detalhes do perfil são exibidos.](../images/user-guide/profile-detail-row-name.png)

Você também pode optar por alternar entre visualizar os nomes de atributo como seus nomes de exibição e os nomes de caminho do campo. Para alternar entre essas duas exibições, selecione a opção **[!UICONTROL Mostrar nomes para exibição]**.

![A opção Mostrar nomes para exibição está realçada e os nomes para exibição são mostrados sob os atributos.](../images/user-guide/profile-detail.png)

Para exibir informações adicionais relacionadas ao perfil de cliente individual, selecione uma das outras guias disponíveis. Essas guias incluem atributos, eventos e a guia de associação de público-alvo que mostra os públicos para os quais o perfil está qualificado no momento.

### Guia Atributos

A guia **[!UICONTROL Atributos]** fornece uma exibição de lista resumindo todos os atributos relacionados a um único perfil, após a política de mesclagem especificada ser aplicada.

Esses atributos também podem ser exibidos como um objeto JSON ao selecionar **[!UICONTROL Exibir JSON]**. Isso é útil para qualquer usuário que deseje entender melhor como os atributos de perfil são assimilados na Experience Platform.

![A guia Atributos está realçada. Os atributos do perfil são exibidos.](../images/user-guide/attributes.png)

Para exibir os atributos disponíveis na Edge, selecione **[!UICONTROL Edge]** no seletor de local de dados.

![O seletor de local de dados na guia de atributos está realçado.](../images/user-guide/attributes-select.png)

Para obter mais informações sobre perfis de borda, leia a [documentação sobre perfis de borda](../edge-profiles.md).

### Guia Eventos

A guia **[!UICONTROL Eventos]** contém dados dos 100 Eventos de Experiência mais recentes associados ao cliente. Esses dados podem incluir aberturas de email, atividades de carrinho e exibições de página. Selecionar **[!UICONTROL Exibir todos]** para qualquer evento individual fornece campos e valores adicionais para capturas como parte do evento.

Os eventos também podem ser exibidos como um objeto JSON ao selecionar **[!UICONTROL Exibir JSON]**. Isso é útil para entender como os eventos são capturados no Experience Platform.

![A guia Eventos está realçada. Os eventos de perfil são exibidos.](../images/user-guide/events.png)

### Guia Associação de público

A guia **[!UICONTROL Associação de público-alvo]** exibe uma lista com o nome e a descrição dos públicos-alvo aos quais o perfil de cliente individual pertence atualmente. Essa lista é atualizada automaticamente conforme o perfil se qualifica ou expira dos públicos-alvo. A contagem total de públicos para os quais o perfil está qualificado no momento é mostrada no lado direito da guia.

Para obter mais informações sobre segmentação no Experience Platform, consulte a [documentação do Serviço de segmentação do Experience Platform](../../segmentation/home.md).

![A guia Associação de público-alvo está realçada. Os detalhes de associação de público do perfil são exibidos.](../images/user-guide/audience-membership.png)

Para exibir a associação de público-alvo dos perfis disponíveis na Edge, selecione **[!UICONTROL Edge]** no seletor de local de dados. Mais informações sobre a segmentação de borda podem ser encontradas no [guia de segmentação de borda](../../segmentation/methods/edge-segmentation.md).

![O seletor de local de dados na guia de associação de público-alvo está realçado.](../images/user-guide/audience-membership-select.png)

## Mesclar políticas

No menu principal **[!UICONTROL Perfis]**, selecione a guia **[!UICONTROL Políticas de mesclagem]** para exibir uma lista de políticas de mesclagem que pertencem à sua organização. Cada política listada exibe seu nome, seja ela a política de mesclagem padrão e a classe de esquema à qual se aplica.

Para obter mais informações sobre políticas de mesclagem, consulte a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

![A guia Políticas de Mesclagem está realçada. Políticas de mesclagem pertencentes à organização são exibidas.](../images/user-guide/merge-policies.png)

## Esquema de união {#union-schema}

No menu principal **[!UICONTROL Perfis]**, selecione a guia **[!UICONTROL Esquema de união]** para exibir os esquemas de união disponíveis para seus dados assimilados. Um esquema de união é uma combinação de todos os campos [!DNL Experience Data Model] (XDM) na mesma classe, cujos esquemas foram habilitados para uso em [!DNL Real-Time Customer Profile].

Para obter mais informações sobre esquemas de união, visite o [guia da interface do esquema de união](union-schema.md).

![A guia Esquema de união está realçada. Esquemas de união pertencentes à organização são exibidos.](../images/user-guide/union-schema.png)

## Atributos computados {#computed-attributes}

No menu principal **[!UICONTROL Perfis]**, selecione a guia **[!UICONTROL Atributos computados]** para exibir uma lista de atributos computados que pertencem à sua organização.

![A guia Atributos computados está realçada.](../images/user-guide/computed-attributes.png)

Para obter mais informações sobre atributos computados, leia a [visão geral sobre atributos computados](../computed-attributes/overview.md). Para obter mais informações sobre como usar atributos computados na interface do Experience Platform, leia o [guia da interface do usuário de atributos computados](../computed-attributes/ui.md).

## Próximas etapas

Ao ler este guia, você sabe como visualizar e gerenciar os dados de perfil de sua organização usando a interface do usuário do Experience Platform. Para obter informações sobre como trabalhar com dados de perfil usando APIs do Experience Platform, consulte o [Guia da API de perfil do cliente em tempo real](../api/overview.md).
