---
keywords: Experience Platform;home;popular topics;Aplicação automática;Aplicação baseada em API;controle de dados
solution: Experience Platform
title: Aplicação automática de política
topic: guide
description: Este documento aborda como as políticas de uso de dados são aplicadas automaticamente ao ativar segmentos para destinos no Experience Platform.
translation-type: tm+mt
source-git-commit: acc4fa59a4808ed9a32c2aaf664039e0d12dc1d8
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---


# Aplicação automática de política

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá aplicar a conformidade de uso de dados com as políticas. Ao ativar segmentos de audiência para destinos, a Adobe Experience Platform aplica automaticamente as políticas de uso caso ocorram violações.

## Pré-requisitos

Este guia exige uma compreensão de trabalho dos serviços da plataforma envolvidos na aplicação automática. Consulte a documentação a seguir para saber mais antes de continuar com este guia:

* [Adobe Experience Platform Data Governance](../home.md): A estrutura pela qual a Plataforma aplica a conformidade de uso de dados por meio do uso de rótulos e políticas.
* [Perfil](../../profile/home.md) do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Serviço](../../segmentation/home.md) de segmentação do Adobe Experience Platform: O mecanismo de segmentação dentro do qual você  [!DNL Platform] usa para criar segmentos de audiência a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.
* [Destinos](../../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação contínua de dados da Plataforma para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muito maisY.

## Fluxo de imposição {#flow}

O diagrama a seguir ilustra como a aplicação de políticas é integrada ao fluxo de dados da ativação de segmentos:

![](../images/enforcement/enforcement-flow.png)

Quando um segmento é ativado pela primeira vez, [!DNL Policy Service] verifica se há violações de política com base nos seguintes fatores:

* Os rótulos de uso de dados aplicados a campos e conjuntos de dados dentro do segmento a ser ativado.
* A finalidade de comercialização do destino.

>[!NOTE]
>
>Se houver rótulos de uso de dados que foram aplicados somente a determinados campos em um conjunto de dados (em vez de todo o conjunto de dados), a imposição desses rótulos de nível de campo na ativação ocorrerá somente sob as seguintes condições:
>
>* Os campos são usados na definição do segmento.
>* Os campos são configurados como atributos projetados para o destino do público alvo.


## Linha de dados {#lineage}

A linhagem de dados desempenha um papel fundamental na forma como as políticas são aplicadas na Plataforma. Em termos gerais, a linhagem de dados se refere à origem de um conjunto de dados, e o que acontece a ele (ou onde ele se move) ao longo do tempo.

No contexto de [!DNL Data Governance], a linhagem permite que os rótulos de uso de dados se propaguem de conjuntos de dados para serviços de downstream que consomem seus dados, como Perfil e destinos do cliente em tempo real. Isso permite que as políticas sejam avaliadas e aplicadas em vários pontos-chave na jornada dos dados por meio da Plataforma, e fornece contexto aos consumidores de dados sobre o porquê de uma violação de política ter ocorrido.

Na Experience Platform, a aplicação da política está relacionada com a seguinte linhagem:

1. Os dados são ingeridos na plataforma e armazenados em **conjuntos de dados**.
1. Os perfis do cliente são identificados e construídos a partir desses conjuntos de dados ao mesclar fragmentos de dados de acordo com a **política de mesclagem**.
1. Grupos de perfis são divididos em **segmentos** com base em atributos comuns.
1. Os segmentos são ativados para **destinos downstream**.

Cada estágio na linha do tempo acima representa uma entidade que pode contribuir para que uma política seja violada, conforme descrito na tabela abaixo:

| Fase da linhagem de dados | Papel na execução das políticas |
| --- | --- |
| Conjunto de dados | Os conjuntos de dados contêm rótulos de uso de dados (aplicados no nível do conjunto de dados ou do campo) que definem para quais casos o conjunto de dados inteiro ou campos específicos podem ser usados. Violações de política ocorrerão se um conjunto de dados ou campo que contém determinados rótulos for usado para uma finalidade que uma política restringe. |
| Política de mesclagem | As políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados ao mesclar fragmentos de vários conjuntos de dados. Violações de políticas ocorrerão se suas políticas de mesclagem estiverem configuradas para que os conjuntos de dados com rótulos restritos sejam ativados para um destino. Consulte o guia em [políticas de mesclagem](../../profile/ui/merge-policies.md) para obter mais informações. |
| Segmento | As regras do segmento definem quais atributos devem ser incluídos nos perfis do cliente. Dependendo de quais campos uma definição de segmento inclui, o segmento herdará quaisquer rótulos de uso aplicados para esses campos. As violações de política ocorrerão se você ativar um segmento cujos rótulos herdados são restritos pelas políticas aplicáveis do destino do público alvo, com base em seu caso de uso de marketing. |
| Destino | Ao configurar um destino, uma ação de marketing (às vezes chamada de caso de uso de marketing) pode ser definida. Esse caso de uso correlaciona-se a uma ação de marketing, conforme definido em uma política de uso de dados. Em outras palavras, o caso de uso de marketing definido para um destino determina quais políticas de uso de dados são aplicáveis a esse destino. Violações de política ocorrerão se você ativar um segmento cujos rótulos de uso são restritos pelas políticas aplicáveis do destino do público alvo. |

Quando ocorrem violações de política, as mensagens resultantes exibidas na interface do usuário fornecem ferramentas úteis para explorar a linha de dados de contribuição da violação para ajudar a resolver o problema. Mais detalhes são fornecidos na próxima seção.

## Mensagens de violação de política {#enforcement}

Se ocorrer uma violação de política ao tentar ativar um segmento (ou [fazendo edições em um segmento já ativado](#policy-enforcement-for-activated-segments)), a ação será impedida e um provedor será exibido indicando que uma ou mais políticas foram violadas. Depois que uma violação é acionada, o botão **[!UICONTROL Salvar]** é desativado para a entidade que você está modificando até que os componentes apropriados sejam atualizados para atender às políticas de uso de dados.

Selecione uma violação de política na coluna esquerda do provedor para exibir detalhes dessa violação.

![](../images/enforcement/violation-policy-select.png)

A mensagem de violação fornece um resumo da política violada, incluindo as condições que a política está configurada para verificar, a ação específica que disparou a violação e uma lista de possíveis resoluções para o problema.

![](../images/enforcement/violation-summary.png)

Um gráfico de linhagem de dados é exibido abaixo do resumo da violação, permitindo visualizar quais conjuntos de dados, políticas de mesclagem, segmentos e destinos estavam envolvidos na violação de política. A entidade que você está alterando está realçada no gráfico, indicando qual ponto no fluxo está causando a ocorrência da violação. Você pode selecionar um nome de entidade no gráfico para abrir a página de detalhes da entidade em questão.

![](../images/enforcement/data-lineage.png)

Você também pode usar o ícone **[!UICONTROL Filter]** (![](../images/enforcement/filter.png)) para filtrar as entidades exibidas por categoria. Pelo menos duas categorias devem ser selecionadas para que os dados sejam exibidos.

![](../images/enforcement/lineage-filter.png)

Selecione **[!UICONTROL visualização de Lista]** para exibir a linha de dados como uma lista. Para voltar ao gráfico visual, selecione **[!UICONTROL visualização do caminho]**.

![](../images/enforcement/list-view.png)

## Aplicação de política para segmentos ativados {#policy-enforcement-for-activated-segments}

A imposição de políticas ainda se aplica aos segmentos depois de ativados, restringindo quaisquer alterações a um segmento ou seu destino que resultariam em uma violação de política. Devido ao modo como [linha de dados](#lineage) funciona na aplicação de políticas, qualquer uma das ações a seguir pode possivelmente acionar uma violação:

* Atualização de rótulos de uso de dados
* Alteração de conjuntos de dados para um segmento
* Alteração de predicados de segmento
* Alteração das configurações de destino

Se qualquer uma das ações acima acionar uma violação, essa ação será impedida de ser salva e uma mensagem de violação de política será exibida, garantindo que seus segmentos ativados continuem a seguir as políticas de uso de dados ao serem modificados.

## Próximas etapas

Este documento cobriu como a aplicação automática de política funciona no Experience Platform. Para obter etapas sobre como integrar de forma programática a aplicação de políticas em seus aplicativos usando chamadas de API, consulte o guia em [imposição baseada em API](./api-enforcement.md).