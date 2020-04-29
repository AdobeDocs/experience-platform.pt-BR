---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do usuário do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: ab289f07475abcbe966c723423825fd392eb3615

---


# Guia do usuário do Perfil do cliente em tempo real

O Perfil de cliente em tempo real cria uma visualização holística de cada um de seus clientes individuais, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros.

Este documento serve como um guia para interagir com o Perfil Cliente em tempo real na interface do usuário da plataforma Adobe Experience.

## Introdução

Este guia do usuário requer uma compreensão dos vários serviços da plataforma de experiência envolvidos no gerenciamento do Perfil do cliente em tempo real. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

* [Perfil](../home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Serviço](../../identity-service/home.md)de identidade: Habilita o Perfil do cliente em tempo real, fazendo a ponte entre identidades de diferentes fontes de dados que estão sendo assimiladas na Plataforma.
* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

## Visão geral do Perfil

Na interface do usuário [da plataforma de](http://platform.adobe.com)experiência, clique em **Perfis** na navegação à esquerda para abrir a guia _Visão geral_ na área de trabalho _Perfis_ . Esta guia exibe vários widgets que fornecem informações de alto nível sobre a loja de Perfis, incluindo o total de audiências endereçáveis, o número de registros de Perfis que foram ingeridos na última semana, bem como estatísticas relacionadas a registros bem-sucedidos e com falha no mesmo período.

![](../images/user-guide/profile-overview.png)

## Amostras de perfil de Visualização

Clique em **Procurar** para visualização de uma lista de amostra de perfis disponíveis. Esta amostra inclui até 50 perfis da contagem [total de](#profile-count)perfis. As amostras são atualizadas por um trabalho automático que coleta novos dados de perfil à medida que são ingeridos. Cada perfil listado exibe sua ID, nome, sobrenome e email pessoal. Clicar na ID de um perfil listado exibe seus detalhes no Visualizador do [Perfil](#profile-viewer).

![](../images/user-guide/profile-samples.png)

Você pode personalizar os atributos exibidos na lista clicando no ícone do seletor de colunas. Isso exibe uma lista suspensa contendo atributos comuns de perfil que você pode adicionar ou remover.

![](../images/user-guide/column-selector.png)

### contagem de Perfis {#profile-count}

A contagem de perfis exibe o número total de perfis que sua organização tem na Experience Platform, depois que a política de mesclagem padrão da sua organização unir fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em canais diferentes, mas esses fragmentos seriam unidos (de acordo com a política de mesclagem padrão) e retornariam uma contagem de perfis &quot;1&quot;, pois estão todos relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro) e perfis (como perfis do Adobe Analytics) que contêm apenas dados de séries cronológicas (eventos). A contagem é atualizada regularmente para fornecer um número total atualizado de perfis na Plataforma. Sempre que uma ingestão de perfis aumenta ou diminui a contagem em mais de 5%, uma tarefa é acionada automaticamente para atualizar a contagem. Se sua organização estiver usando assimilação de fluxo contínuo, os trabalhos serão executados a cada hora para coletar dados ingeridos recentemente.

![](../images/user-guide/profile-count.png)

### Pesquisa de Perfis

Se você souber uma identidade vinculada para um determinado perfil (como seu endereço de email), poderá procurar esse perfil clicando em **Localizar um perfil**. Essa é a maneira mais confiável de acessar um perfil específico, independentemente de ele aparecer na lista de amostras.

![](../images/user-guide/find-a-profile.png)

Na caixa de diálogo exibida, selecione uma namespace de ID apropriada na lista suspensa (&quot;Email&quot; neste exemplo) e insira o valor de ID abaixo antes de clicar em **OK**. Se encontrado, os detalhes do perfil direcionado aparecem no visualizador de perfis, conforme descrito na próxima seção.

![](../images/user-guide/find-a-profile-details.png)

### Visualizador de Perfis {#profile-viewer}

Ao selecionar ou pesquisar um perfil específico, a tela _Detalhe_ do visualizador do perfil é aberta. Esta página exibe informações sobre o perfil selecionado, como os atributos básicos do perfil, as identidades vinculadas e os canais de contato disponíveis. As informações de perfil exibidas foram unidas de vários fragmentos de perfil para formar uma única visualização do cliente individual.

![](../images/user-guide/profile-viewer-detail.png)

O visualizador de perfis também fornece guias que permitem a visualização de eventos e associações de segmentos associadas a esse perfil, se houver.

![](../images/user-guide/profile-viewer-events-seg.png)

## Mesclar políticas

Clique em **Mesclar políticas** para visualização de uma lista de políticas de mesclagem pertencentes à sua organização. Cada política listada exibe seu nome, seja ela a política de mesclagem padrão ou não, e o schema ao qual ela se aplica.

![](../images/user-guide/profile-merge-policies.png)

Para obter mais informações sobre como trabalhar com políticas de mesclagem na interface do usuário, consulte o guia [do usuário](merge-policies.md)Mesclar políticas.

## schema União

Clique em Schema **de** União para visualização dos schemas de união para o armazenamento de dados do perfil. Um schema de união é uma combinação de todos os campos do Modelo de Dados de Experiência (XDM) na mesma classe, cujos schemas foram habilitados para uso no Perfil do Cliente em tempo real. Clique em uma classe na lista esquerda para visualização da estrutura de sua schema de união na tela.

![](../images/user-guide/profile-union-schema.png)

Consulte a seção sobre schemas de união no guia [de composição do](../../xdm/schema/composition.md) schema para obter mais informações sobre schemas de união e sua função no Perfil do cliente em tempo real.

## Próximas etapas

Ao ler este guia, agora você sabe como visualização e gerenciar seus dados de Perfil usando a interface do usuário da plataforma de experiência. Para obter informações sobre como aproveitar os dados de Perfil do cliente em tempo real para gerar segmentos de audiência, consulte a documentação [de](../../segmentation/home.md)segmentação.