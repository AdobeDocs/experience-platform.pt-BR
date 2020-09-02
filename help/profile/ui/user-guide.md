---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
solution: Adobe Experience Platform
title: Guia do usuário do Perfil do cliente em tempo real
topic: guide
description: O Perfil de cliente em tempo real cria uma visualização holística de cada um de seus clientes individuais, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros. Este documento serve como um guia para interagir com o Perfil Cliente em tempo real na interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 31166ddf8afbe13874be66b29c89501bd6ce1e51
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] guia do usuário

[!DNL Real-time Customer Profile] cria uma visualização holística de cada um de seus clientes individuais, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros.

Este documento serve como um guia para interagir com [!DNL Real-time Customer Profile] dados na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos no gerenciamento [!DNL Real-time Customer Profiles]. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

* [[!DNL Perfil do cliente em tempo real]](../home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-time Customer Profile] a ponte de identidades de fontes de dados diferentes à medida que são assimiladas [!DNL Platform].
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.

## Visão geral

Na [[!DNL Experience Platform] interface](http://platform.adobe.com)do usuário, selecione **[!UICONTROL Perfis]** na navegação à esquerda para abrir a guia **[!UICONTROL Visão geral]** . Esta guia fornece links para a documentação e vídeos para ajudá-lo a entender e começar a trabalhar com perfis.

![](../images/user-guide/profiles-overview.png)

## Procurar

Selecione a guia **[!UICONTROL Procurar]** para procurar perfis por identidade.

![](../images/user-guide/profiles-browse.png)

### Métricas de perfil {#profile-metrics}

No lado direito da guia [!UICONTROL Procurar] estão várias métricas importantes relacionadas aos dados do seu perfil, incluindo a contagem [total de](#profile-count) perfis, bem como uma lista de [perfis por namespace](#profiles-by-namespace).

Essas métricas de perfil são avaliadas usando a política de mesclagem padrão de sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem, incluindo como definir uma política de mesclagem padrão, consulte o guia [do usuário](merge-policies.md)Mesclar políticas.

Além dessas métricas, a seção de métricas de perfil também fornece uma data e hora [!UICONTROL última atualização] , mostrando quando as métricas foram avaliadas pela última vez.

![](../images/user-guide/profiles-profile-metrics.png)

### contagem de perfis {#profile-count}

A contagem de perfis exibe o número total de perfis que sua organização tem dentro [!DNL Experience Platform], depois que a política de mesclagem padrão da sua organização unir fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em canais diferentes, mas esses fragmentos seriam unidos (de acordo com a política de mesclagem padrão) e retornariam uma contagem de perfis &quot;1&quot;, pois estão todos relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de séries cronológicas (eventos), como perfis Adobe Analytics. A contagem de perfis é atualizada regularmente para fornecer um número total atualizado de perfis na Plataforma.

Quando a ingestão de registros na [!DNL Profile] loja aumenta ou diminui a contagem em mais de 5%, uma tarefa é acionada para atualizar a contagem. Para workflows de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se o tiver feito, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote no repositório de Perfis, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem de perfis.

### Perfis por namespace {#profiles-by-namespace}

A métrica **[!UICONTROL Perfis por namespace]** exibe a contagem total e o detalhamento das namespaces em todos os perfis unidos na Loja de Perfis. O número total de perfis por namespace (em outras palavras, adicionar os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis porque um perfil pode ter várias namespaces associadas a ela. Por exemplo, se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual.

Semelhante à métrica de contagem [de](#profile-count) perfis, quando a ingestão de registros na [!DNL Profile] loja aumenta ou diminui a contagem em mais de 5%, uma tarefa é acionada para atualizar as métricas de namespace. Para workflows de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se o tiver feito, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote na [!DNL Profile] loja, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar as métricas.

### Política de mesclagem

O seletor de política **[!UICONTROL de]** mesclagem seleciona automaticamente a política de mesclagem padrão para sua organização. Se você não quiser usar essa política de mesclagem, poderá selecionar a política `X` ao lado da política de mesclagem padrão para abrir a caixa de diálogo **[!UICONTROL Selecionar política]** de mesclagem, onde poderá escolher outra política de mesclagem. Para saber mais sobre as políticas de mesclagem e sua função na Plataforma, consulte o guia [do usuário das políticas de](merge-policies.md)mesclagem.

![](../images/user-guide/profiles-search-merge-policy.png)

### Namespace de identidade

O seletor de namespace **[!UICONTROL de]** identidade abre uma caixa de diálogo onde você pode escolher a namespace de identidade pela qual deseja pesquisar, e você pode personalizar os atributos exibidos em sua pesquisa selecionando o ícone de filtro e escolhendo quais atributos você gostaria de adicionar ou remover.

![](../images/user-guide/profiles-search-filter.png)

Na caixa de diálogo **[!UICONTROL Selecionar namespace]** de identidade, escolha a namespace pela qual deseja pesquisar ou use a barra de pesquisa na caixa de diálogo para começar a digitar o nome de uma namespace. Você pode selecionar uma namespace para visualização com mais detalhes e, depois de encontrar a namespace que gostaria de usar, pode selecionar o botão de opção e pressionar **[!UICONTROL Select (Selecionar]** ) para continuar.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valor de identidade

Depois de selecionar uma namespace [!UICONTROL de]identidade, você retorna à guia [!UICONTROL Procurar] , onde pode inserir um valor **[!UICONTROL de]** Identidade. Esse valor é específico para um perfil de cliente individual e deve ser uma entrada válida para a namespace fornecida. Por exemplo, a seleção da namespace [!UICONTROL de] identidade &quot;Email&quot; exigiria um valor [!UICONTROL de] identidade na forma de um endereço de email válido.

![](../images/user-guide/profiles-show-profile.png)

Depois que um valor for inserido, selecione **[!UICONTROL Mostrar perfil]** e um único perfil que corresponda ao valor será retornado. Selecione a ID **[!UICONTROL do]** Perfil para visualização dos detalhes do perfil.

![](../images/user-guide/profiles-display-profile.png)

### Detalhes do perfil {#profile-detail}

Ao selecionar a ID [!UICONTROL do]Perfil, a guia **[!UICONTROL Detalhe]** é aberta. As informações do perfil exibidas na guia [!UICONTROL Detalhe] foram unidas de vários fragmentos de perfil para formar uma única visualização do cliente individual. Isso inclui detalhes do cliente, como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados também podem ser alterados em nível organizacional para exibir os atributos de Perfil preferenciais. Para saber mais sobre como personalizar esses campos, incluindo instruções passo a passo para adicionar e remover atributos e redimensionar painéis de painéis, leia o guia [de personalização dos detalhes do](profile-customization.md)perfil.

![](../images/user-guide/profiles-profile-detail.png)

Você pode visualização informações adicionais relacionadas ao perfil individual selecionando outra das guias disponíveis. Essas guias incluem [!UICONTROL Atributos], [!UICONTROL Eventos]e associação [!UICONTROL de]segmento, que mostra os [!UICONTROL segmentos] para os quais o perfil está qualificado no momento.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Mesclar políticas

No menu principais [!UICONTROL Perfis] , selecione a guia **[!UICONTROL Mesclar políticas]** para visualização de uma lista de políticas de mesclagem pertencentes à sua organização. Cada política listada exibe seu nome, seja ela a política de mesclagem padrão ou não, e o schema ao qual ela se aplica.

Para obter mais informações sobre políticas de mesclagem, consulte o guia [do usuário das políticas de](merge-policies.md)mesclagem.

![](../images/user-guide/profiles-merge-policies.png)

## Schema união {#union-schema}

No menu principal [!UICONTROL Perfis] , selecione a guia Schema **[!UICONTROL de]** União para visualização dos schemas de união dos dados do Perfil. Um schema de união é uma combinação de todos os campos [!DNL Experience Data Model] (XDM) na mesma classe, cujos schemas foram habilitados para uso em [!DNL Real-time Customer Profile]. Ao selecionar uma classe da lista [!UICONTROL Classe] no lado esquerdo, é possível visualização a estrutura de seu schema na tela. Por exemplo, selecionar &quot;[!DNL XDM Profile]&quot; exibe o schema de união da [!DNL XDM Individual Profile] classe.

Para obter mais informações sobre schemas de união e sua função no Adobe Experience Platform, consulte a seção sobre schemas de união no guia [de composição do](../../xdm/schema/composition.md)schema.

![](../images/user-guide/profiles-union-schema.png)

## Próximas etapas

Ao ler este guia, agora você sabe como visualização e gerenciar seus [!DNL Profile] dados usando a [!DNL Experience Platform] interface do usuário. Para obter informações sobre como trabalhar com dados de Perfil usando a API Perfil do cliente em tempo real, consulte o guia [do desenvolvedor do](../api/overview.md)Perfil.