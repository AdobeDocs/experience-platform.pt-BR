---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do usuário do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: 59dff7687f8a0c5b5084eb1ce7dd222cc18d8dbf
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# Guia do usuário do Perfil do cliente em tempo real

O Perfil de cliente em tempo real cria uma visualização holística de cada um de seus clientes individuais, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros.

Este documento serve como um guia para interagir com o Perfil Cliente em tempo real na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão dos vários serviços de Experience Platform envolvidos com o gerenciamento de Perfis de clientes em tempo real. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

* [Perfil](../home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Serviço](../../identity-service/home.md)de identidade: Habilita o Perfil do cliente em tempo real, conectando identidades de diferentes fontes de dados à medida que são ingeridas no Platform.
* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

## Visão geral

Na interface do usuário do [Experience Platform](http://platform.adobe.com), clique em **Perfis** na navegação à esquerda para abrir a guia _Visão geral_ . Esta guia fornece links para a documentação e vídeos para ajudá-lo a entender e começar a trabalhar com perfis.

![](../images/user-guide/profiles-overview.png)

## Procurar

Selecione a guia *Procurar* para procurar perfis por identidade.

![](../images/user-guide/profiles-browse.png)

### Métricas de Perfil {#profile-metrics}

No lado direito da guia *Procurar* estão várias métricas importantes relacionadas aos dados do seu perfil, incluindo a contagem [total de](#profile-count) perfis, bem como uma lista de [perfis por namespace](#profiles-by-namespace).

Essas métricas de perfil são avaliadas usando a política de mesclagem padrão de sua organização. Para obter mais informações sobre como trabalhar com políticas de mesclagem, incluindo como definir uma política de mesclagem padrão, consulte o guia [do usuário](merge-policies.md)Mesclar políticas.

Além dessas métricas, a seção de métricas de perfil também fornece uma data e hora *última atualização* , mostrando quando as métricas foram avaliadas pela última vez.

![](../images/user-guide/profiles-profile-metrics.png)

### contagem de Perfis {#profile-count}

A contagem de perfis exibe o número total de perfis que sua organização tem dentro do Experience Platform, depois que a política de mesclagem padrão da sua organização unir fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em canais diferentes, mas esses fragmentos seriam unidos (de acordo com a política de mesclagem padrão) e retornariam uma contagem de perfis &quot;1&quot;, pois estão todos relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de séries cronológicas (eventos), como perfis Analytics da Adobe. A contagem de perfis é atualizada regularmente para fornecer um número total atualizado de perfis no Platform.

Quando a ingestão de registros na Loja de Perfis aumenta ou diminui a contagem em mais de 5%, uma tarefa é acionada para atualizar a contagem. Para workflows de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se o tiver feito, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote no Perfil Store, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem de perfis.

### Perfis por namespace {#profiles-by-namespace}

A métrica *Perfis por namespace* exibe a contagem total e o detalhamento das namespaces em todos os perfis unidos na Loja de Perfis. O número total de perfis por namespace (em outras palavras, adicionar os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis porque um perfil pode ter várias namespaces associadas a ela. Por exemplo, se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual.

Semelhante à métrica de contagem [de](#profile-count) perfis, quando a ingestão de registros na Loja de Perfis aumenta ou diminui a contagem em mais de 5%, uma tarefa é acionada para atualizar as métricas de namespace. Para workflows de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se o tiver feito, uma tarefa será automaticamente acionada para atualizar a contagem de perfis. Para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote no Perfil Store, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar as métricas.

### Política de mesclagem

O seletor de política **de** mesclagem seleciona automaticamente a política de mesclagem padrão para sua organização. Se você não quiser usar essa política de mesclagem, poderá selecionar a política `X` ao lado da política de mesclagem padrão para abrir uma caixa de diálogo *Selecionar política* de mesclagem, onde poderá escolher outra política de mesclagem. Para saber mais sobre as políticas de mesclagem, consulte o guia [do usuário](merge-policies.md)Mesclar políticas.

![](../images/user-guide/profiles-search-merge-policy.png)

### namespace de identidade

O seletor de namespace **de** identidade abre uma caixa de diálogo onde você pode escolher a namespace de identidade pela qual deseja pesquisar, e você pode personalizar os atributos exibidos em sua pesquisa selecionando o ícone de filtro e escolhendo quais atributos você gostaria de adicionar ou remover.

![](../images/user-guide/profiles-search-filter.png)

Na caixa de diálogo *Selecionar namespace* de identidade, escolha a namespace pela qual deseja pesquisar ou use a barra **Pesquisar** na caixa de diálogo para começar a digitar o nome de uma namespace. Você pode selecionar uma namespace para visualização com mais detalhes e, depois de encontrar a namespace que deseja pesquisar, pode selecionar o botão de opção e pressionar **Select (Selecionar** ) para continuar.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valor de identidade

Depois de selecionar uma namespace **de** identidade, você retorna à guia *Procurar* , onde pode inserir um valor **de** Identidade. Esse valor é específico para um perfil de cliente individual e deve ser uma entrada válida para a namespace fornecida. Por exemplo, a seleção da namespace **de** identidade &quot;Email&quot; exigiria um valor **de** identidade na forma de um endereço de email válido.

![](../images/user-guide/profiles-show-profile.png)

Depois que um valor for inserido, selecione **Mostrar perfil** e um único perfil que corresponda ao valor será retornado. Selecione a ID **do** Perfil para visualização dos detalhes do perfil.

![](../images/user-guide/profiles-display-profile.png)

### Detalhes do Perfil

Ao selecionar a ID **do** Perfil, a guia _Detalhe_ é aberta. Esta página exibe informações sobre o perfil selecionado, incluindo atributos básicos, identidades vinculadas e canais de contato disponíveis. As informações de perfil exibidas foram unidas de vários fragmentos de perfil para formar uma única visualização do cliente individual.

![](../images/user-guide/profiles-profile-detail.png)

Você pode visualização informações adicionais relacionadas ao perfil, incluindo *Atributos*, *Eventos* e *Segmentos* aos quais o perfil é membro.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Mesclar políticas

Selecione a guia *Mesclar políticas* para visualização de uma lista de políticas de mesclagem pertencentes à sua organização. Cada política listada exibe seu nome, seja ela a política de mesclagem padrão ou não, e o schema ao qual ela se aplica.

Para obter mais informações sobre políticas de mesclagem, consulte o guia [do usuário](merge-policies.md)Mesclar políticas.

![](../images/user-guide/profiles-merge-policies.png)

## schema União

Selecione a guia Schema *da* União para visualização dos schemas da união da Loja de Perfis. Um schema de união é uma combinação de todos os campos do Modelo de Dados de Experiência (XDM) na mesma classe, cujos schemas foram habilitados para uso no Perfil do Cliente em tempo real. Selecione uma classe na lista esquerda para visualização da estrutura de sua schema de união na tela.

Por exemplo, selecionar &quot;Perfil XDM&quot; exibe o schema de união para a classe de Perfil Individual XDM.

Consulte a seção sobre schemas de união no guia [de composição do](../../xdm/schema/composition.md) schema para obter mais informações sobre schemas de união e sua função no Perfil do cliente em tempo real.

![](../images/user-guide/profiles-union-schema.png)

## Próximas etapas

Ao ler este guia, agora você sabe como visualização e gerenciar seus dados de Perfil usando a interface do usuário do Experience Platform. Para obter informações sobre como aproveitar os dados de Perfil do cliente em tempo real para gerar segmentos de audiência, consulte a documentação [de](../../segmentation/home.md)segmentação.