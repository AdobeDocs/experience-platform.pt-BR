---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;unificado;Perfil;rtcp;habilitar perfil;Habilitar perfil;esquema de união;PERFIL DE UNIÃO;perfil de união
title: Guia da interface do usuário do Perfil do cliente em tempo real
description: O Perfil do cliente em tempo real cria uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. Este documento serve como um guia para interagir com o Perfil do cliente em tempo real na interface do usuário do Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2008'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] Guia da interface do usuário

[!DNL Real-Time Customer Profile] O cria uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. Este documento serve como um guia para interagir com o [!DNL Real-Time Customer Profile] na interface do usuário (UI) do Adobe Experience Platform.

## Introdução

Este guia de interface do usuário requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos no gerenciamento [!DNL Real-Time Customer Profiles]. Antes de ler este guia ou trabalhar na interface do usuário, consulte a documentação dos seguintes serviços:

* [[!DNL Real-Time Customer Profile] visão geral](../home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] identidades de diferentes fontes de dados à medida que são assimiladas na [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a [!DNL Platform] organiza os dados de experiência do cliente.

## [!UICONTROL Visão geral]

Na interface do Experience Platform, selecione **[!UICONTROL Perfis]** na navegação à esquerda, para abrir a **[!UICONTROL Visão geral]** exibindo o painel do perfil.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, a variável [!UICONTROL Perfis] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e documentação para ajudar você a começar a usar o Perfil do cliente em tempo real.

### Painel do perfil {#profile-dashboard}

O painel de perfil descreve as métricas principais relacionadas aos dados de perfil de sua organização.

Para saber mais, visite o [guia do painel de perfis](../../dashboards/guides/profiles.md).

![O painel Perfil é exibido.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Procurar] métricas de guia

Selecione o **[!UICONTROL Procurar]** para exibir várias métricas relacionadas aos dados de perfil de sua organização. Você também pode usar essa guia para navegar no armazenamento de perfis usando uma política de mesclagem ou uma identidade, conforme descrito na próxima seção deste guia.

No lado direito do **[!UICONTROL Procurar]** é a guia [contagem de perfis](#profile-count) bem como uma lista de [perfis por namespace](#profiles-by-namespace).

>[!NOTE]
>
>Essas métricas de perfil podem ser diferentes das métricas exibidas no [painel de perfil](#profile-dashboard) porque são avaliadas usando a política de mesclagem padrão da sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem, incluindo como definir uma política de mesclagem padrão, consulte o [visão geral das políticas de mesclagem](../merge-policies/overview.md).

Além dessas métricas, esta seção fornece uma data e hora da última atualização, mostrando quando as métricas foram avaliadas pela última vez.

![As métricas de Perfil são exibidas e destacadas.](../images/user-guide/browse-metrics.png)

### Contagem de perfis {#profile-count}

A contagem de perfis exibe o número total de perfis que sua organização tem no Experience Platform, depois que a política de mesclagem padrão da organização mescla fragmentos de perfis para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em diferentes canais, mas esses fragmentos seriam mesclados (de acordo com a política de mesclagem padrão) e retornariam uma contagem de &quot;1&quot; perfil, pois todos estão relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de série temporal (evento), como perfis do Adobe Analytics. A contagem de perfis é atualizada regularmente para fornecer um número total de perfis atualizado na Platform.

#### Atualização da métrica de contagem de perfis

Quando a assimilação de registros na variável [!DNL Profile] A loja aumenta ou diminui a contagem em mais de 5%. um trabalho é acionado para atualizar a contagem. Para workflows de dados de transmissão, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para assimilação em lote, dentro de 15 minutos após a assimilação bem-sucedida de um lote no Armazenamento de perfis, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem de perfis.

### [!UICONTROL Perfis por namespace] {#profiles-by-namespace}

A variável **[!UICONTROL Perfis por namespace]** Esta métrica exibe a contagem total e o detalhamento dos namespaces em todos os perfis mesclados na Loja de perfis. O número total de perfis por namespace (em outras palavras, somando os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

#### Atualização do [!UICONTROL Perfis por namespace] métrica

Semelhante ao [contagem de perfis](#profile-count) quando a assimilação de registros na variável [!DNL Profile] A loja aumenta ou diminui a contagem em mais de 5%. um trabalho é acionado para atualizar as métricas de namespace. Para workflows de dados de transmissão, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para assimilação em lote, dentro de 15 minutos após a assimilação bem-sucedida de um lote na [!DNL Profile] armazenamento, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar as métricas.

## Uso [!UICONTROL Procurar] guia para visualizar perfis

No **[!UICONTROL Procurar]** guia é possível visualizar perfis de amostra usando uma política de mesclagem ou pesquisar perfis específicos usando um namespace de identidade e valor.

![Os Perfis que pertencem à organização são exibidos.](../images/user-guide/none-selected.png)

### Procurar por [!UICONTROL Política de mesclagem]

A variável **[!UICONTROL Procurar]** é definida como a política de mesclagem padrão para sua organização por padrão. Para escolher uma política de mesclagem diferente, selecione a `X` ao lado do nome da política de mesclagem e use o seletor para abrir o **[!UICONTROL Selecionar política de mesclagem]** diálogo.

>[!NOTE]
>
>Se não houver política de mesclagem selecionada, use o botão seletor ao lado da guia **[!UICONTROL Política de mesclagem]** para abrir a caixa de diálogo de seleção.

![O seletor de política de mesclagem é realçado.](../images/user-guide/browse-by-merge-policy.png)

Para escolher uma política de mesclagem na **[!UICONTROL Selecionar política de mesclagem]** selecione o botão de opção ao lado do nome da política e, em seguida, use **[!UICONTROL Selecionar]** para retornar ao [!UICONTROL Procurar] guia. É possível selecionar **[!UICONTROL Exibir]** para atualizar os perfis de amostra e ver uma amostra de perfis com a nova política de mesclagem aplicada.

![Uma caixa de diálogo na qual você pode selecionar a política de mesclagem para filtrar é exibida.](../images/user-guide/select-merge-policy.png)

Os perfis mostrados representam uma amostra de até 20 perfis do armazenamento de perfis da sua organização, depois que a política de mesclagem selecionada é aplicada. Os perfis de exemplo para a política de mesclagem selecionada são atualizados quando novos dados são adicionados ao armazenamento de perfil da organização.

Para exibir os detalhes de um dos perfis de amostra, selecione o **[!UICONTROL ID do perfil]**. Para obter mais informações, consulte a seção mais adiante neste guia sobre [exibição de detalhes do perfil](#profile-detail).

![Perfis de amostra que correspondem à política de mesclagem são exibidos.](../images/user-guide/sample-profiles.png)

Para saber mais sobre as políticas de mesclagem e sua função na Platform, consulte o [visão geral das políticas de mesclagem](../merge-policies/overview.md).

### Procurar por [!UICONTROL Identidade] {#browse-identity}

No **[!UICONTROL Procurar]** você pode usar um namespace de identidade para procurar um perfil específico por um valor de identidade. A navegação por uma identidade exige que você forneça uma política de mesclagem, um namespace de identidade e um valor de identidade.

![O seletor de política de mesclagem é realçado.](../images/user-guide/browse-by-merge-policy.png)

Se necessário, use o **[!UICONTROL Política de mesclagem]** seletor para abrir o **[!UICONTROL Selecionar política de mesclagem]** e escolha a política de mesclagem que deseja usar.

![Uma caixa de diálogo na qual você pode selecionar a política de mesclagem para filtrar é exibida.](../images/user-guide/select-merge-policy.png)

Em seguida, use o **[!UICONTROL Namespace de identidade]** seletor para abrir o **[!UICONTROL Selecionar namespace de identidade]** e escolha o namespace pelo qual deseja pesquisar. Se sua organização tiver muitos namespaces, você poderá usar a barra de pesquisa na caixa de diálogo para começar a digitar o nome de um namespace.

Você pode selecionar um namespace para exibir detalhes adicionais ou selecionar o botão de opção para escolher um namespace. Você pode então usar **[!UICONTROL Selecionar]** para continuar.

![Uma caixa de diálogo na qual você pode selecionar o namespace de identidade pelo qual filtrar é exibida.](../images/user-guide/select-identity-namespace.png)

Após selecionar um [!UICONTROL Namespace de identidade] e retornando ao [!UICONTROL Procurar] você pode inserir um **[!UICONTROL Valor de identidade]** relacionado ao namespace selecionado.

>[!NOTE]
>
>Esse valor é específico para um perfil de cliente individual e deve ser uma entrada válida para o namespace fornecido. Por exemplo, selecionar o namespace de identidade &quot;Email&quot; exigiria um valor de identidade na forma de um endereço de email válido.

![O valor de identidade pelo qual você deseja filtrar é realçado.](../images/user-guide/filter-identity-value.png)

Depois que um valor é inserido, selecione **[!UICONTROL Exibir]** e um único perfil correspondente ao valor é retornado. Selecione o **[!UICONTROL ID do perfil]** para exibir os detalhes do perfil.

![O perfil que corresponde ao valor de identidade é realçado.](../images/user-guide/filtered-identity-value.png)

## Exibir detalhes do perfil {#profile-detail}

Depois de selecionar um **[!UICONTROL ID do perfil]**, o **[!UICONTROL Detalhe]** é aberta. As informações do perfil exibidas na guia **[!UICONTROL Detalhe]** A guia foi mesclada de vários fragmentos de perfil para formar uma única visualização do cliente individual. Isso inclui detalhes do cliente, como atributos básicos, identidades vinculadas e preferências de canal.

Os campos padrão mostrados também podem ser alterados em um nível organizacional para exibir atributos de perfil preferenciais. Para saber mais sobre como personalizar esses campos, incluindo instruções passo a passo para adicionar e remover atributos e redimensionar painéis de painel, leia o [guia de personalização de detalhes do perfil](profile-customization.md).

![A guia Details (Detalhes) é realçada. Os detalhes do perfil são exibidos.](../images/user-guide/profile-detail.png)

Você pode exibir informações adicionais relacionadas ao perfil de cliente individual selecionando outra das guias disponíveis. Essas guias incluem atributos, eventos e a guia de associação de público-alvo que mostra os públicos para os quais o perfil está qualificado no momento.

### Guia Atributos

A variável **[!UICONTROL Atributos]** A guia fornece uma exibição de lista resumindo todos os atributos relacionados a um único perfil após a política de mesclagem especificada ser aplicada.

Esses atributos também podem ser exibidos como um objeto JSON ao selecionar para **[!UICONTROL Exibir JSON]**. Isso é útil para qualquer usuário que deseje entender melhor como os atributos do perfil são assimilados na Platform.

![A guia Atributos é realçada. Os atributos do perfil são exibidos.](../images/user-guide/attributes.png)

### Guia Eventos

A variável **[!UICONTROL Eventos]** A guia contém dados dos 100 ExperienceEvents mais recentes associados ao cliente. Esses dados podem incluir aberturas de email, atividades de carrinho e exibições de página. Selecionar **[!UICONTROL Exibir todos]** para qualquer evento individual fornece campos adicionais e capturas de valores como parte do evento.

Os eventos também podem ser exibidos como um objeto JSON ao selecionar: **[!UICONTROL Exibir JSON]**. Isso é útil para entender como os eventos são capturados na Platform.

![A guia Eventos é realçada. Os eventos de perfil são exibidos.](../images/user-guide/events.png)

### Guia Associação de público

A variável **[!UICONTROL associação de público]** A guia exibe uma lista com o nome e a descrição dos públicos-alvo aos quais o perfil de cliente individual pertence atualmente. Essa lista é atualizada automaticamente conforme o perfil se qualifica ou expira dos públicos-alvo. A contagem total de públicos para os quais o perfil está qualificado no momento é mostrada no lado direito da guia.

Para obter mais informações sobre segmentação em Experience Platform, consulte a [Documentação do Adobe Experience Platform Segmentation Service](../../segmentation/home.md).

![A guia Associação de público-alvo é realçada. Os detalhes de associação do público-alvo do perfil são exibidos.](../images/user-guide/segment-membership.png)

## Políticas de mesclagem

A partir do principal **[!UICONTROL Perfis]** selecione o **[!UICONTROL Políticas de mesclagem]** para exibir uma lista de políticas de mesclagem pertencentes à sua organização. Cada política listada exibe seu nome, seja ela a política de mesclagem padrão e a classe de esquema à qual se aplica.

Para obter mais informações sobre políticas de mesclagem, consulte [visão geral das políticas de mesclagem](../merge-policies/overview.md).

![A guia Merge Policies (Políticas de mesclagem) é realçada. As políticas de mesclagem pertencentes à organização são exibidas.](../images/user-guide/merge-policies.png)

## Esquema de união {#union-schema}

A partir do principal **[!UICONTROL Perfis]** selecione o **[!UICONTROL Esquema de união]** para visualizar os esquemas de união disponíveis para seus dados assimilados. Um esquema de união é uma combinação de todos [!DNL Experience Data Model] (XDM) campos na mesma classe, cujos esquemas foram ativados para uso no [!DNL Real-Time Customer Profile].

Para obter mais informações sobre esquemas de união, visite o [guia da interface do esquema de união](union-schema.md).

![A guia Esquema de união é realçada. Esquemas de união pertencentes à organização são exibidos.](../images/user-guide/union-schema.png)

## Atributos computados {#computed-attributes}

A partir do principal **[!UICONTROL Perfis]** selecione o **[!UICONTROL Atributos computados]** para exibir uma lista de atributos computados que pertencem à sua organização.

Para obter mais informações sobre atributos computados, leia a [visão geral dos atributos computados](../computed-attributes/overview.md). Para obter mais informações sobre como usar atributos computados na interface do usuário da Platform, leia a [guia da interface de atributos computados](../computed-attributes/ui.md).

IMAGEM

## Próximas etapas

Ao ler este guia, você sabe como visualizar e gerenciar os dados de perfil de sua organização usando a interface do usuário do Experience Platform. Para obter informações sobre como trabalhar com dados de perfil usando APIs de Experience Platform, consulte [Guia da API do Perfil do cliente em tempo real](../api/overview.md).
