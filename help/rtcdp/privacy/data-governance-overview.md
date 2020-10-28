---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Visão geral do controle de dados
seo-title: Controle de dados na plataforma de dados do cliente em tempo real
description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
seo-description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
translation-type: tm+mt
source-git-commit: 66042cb9397b9c7b507fc063f33e92f4f4c381c7
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 0%

---


# [!DNL Data Governance] em CDP em tempo real

[!DNL Real-time Customer Data Platform] (CDP em tempo real) reúne dados de vários sistemas corporativos, permitindo que os profissionais de marketing identifiquem, entendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos às restrições de uso definidas pela sua organização ou por regulamentos legais. Portanto, é importante garantir que a CDP em tempo real esteja em conformidade com as políticas de uso ao manipular seus dados.

A Adobe Experience Platform [!DNL Data Governance] permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na CDP em tempo real, permitindo que você defina políticas de uso, classifique seus dados com base nessas políticas e verifique violações de políticas ao executar determinadas ações de marketing.

A CDP em tempo real foi desenvolvida sobre a Adobe Experience Platform e, portanto, a maioria dos [!DNL Data Governance] recursos são abordados na [!DNL Experience Platform] documentação. Este documento é destinado a complementar a visão geral [do](../../data-governance/home.md) Data Governance para [!DNL Experience Platform]e descreve os recursos de controle disponíveis na CDP em tempo real. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade de uso de dados](#enforce-data-usage-compliance)

## Aplicar rótulos de uso aos seus dados {#labels}

[!DNL Data Governance] permite que você aplique rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem que você categorize os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte o guia [do usuário de rótulos de uso de](../../data-governance/labels/overview.md) dados para Adobe Experience Platform.

## Configurar casos de uso de marketing para destinos {#destinations}

É possível definir restrições de uso de dados em um destino definindo casos de uso de marketing (também chamados de ações de marketing) para esse destino. Um caso de uso de marketing para um destino indica a intenção dos dados que serão exportados para esse destino.

>[!NOTE]
>
>Para obter mais informações sobre ações de marketing e seu uso em políticas de uso de dados, consulte a visão geral [das políticas de uso de](../../data-governance/policies/overview.md) dados na [!DNL Experience Platform] documentação.

A definição de casos de uso de marketing em destinos permite garantir que quaisquer perfis ou segmentos enviados para esses destinos sejam compatíveis com as políticas de uso de dados. Portanto, você deve adicionar casos de uso de marketing apropriados aos seus destinos com base nas necessidades de sua organização para aplicar restrições de política à ativação.

Os casos de uso de marketing só podem ser selecionados ao configurar um destino pela primeira vez. Dependendo do tipo de destino com o qual você está trabalhando, a oportunidade de configurar casos de uso de marketing aparecerá em diferentes pontos no fluxo de trabalho da configuração. Consulte a documentação [de](../destinations/destinations-overview.md#data-governance) destinos para obter etapas sobre como configurar seu destino específico.

## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro da CDP em tempo real. Consulte a seção &quot;Políticas de uso de dados&quot; na visão geral [!DNL Experience Platform] do [](../../data-governance/home.md) Data Governance para obter mais informações.

A Adobe Experience Platform fornece várias políticas principais para casos comuns de uso da experiência do cliente. Essas políticas podem ser exibidas na interface do usuário navegando até a área de trabalho **[!UICONTROL Políticas]** e selecionando a guia **[!UICONTROL Procurar]** . Consulte o guia [de usuário de](../../data-governance/policies/user-guide.md) [!DNL Experience Platform] políticas na documentação para obter etapas mais detalhadas sobre como trabalhar com políticas na interface do usuário, incluindo como fazer suas próprias políticas personalizadas.

## Impor conformidade de uso de dados {#enforce-data-usage-compliance}

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá aplicar a conformidade de uso de dados com as políticas. Ao ativar segmentos de audiência para destinos em CDP em tempo real, [!DNL Data Governance] aplica automaticamente as políticas de uso caso ocorram violações.

O diagrama a seguir ilustra como a aplicação de políticas é integrada ao fluxo de dados da ativação de segmentos:

<img src="assets/governance/enforcement-flow.png" width="650">

Quando um segmento é ativado pela primeira vez, [!DNL Policy Service] verifica se há violações de política com base nos seguintes fatores:

* Os rótulos de uso de dados aplicados a campos e conjuntos de dados dentro do segmento a ser ativado.
* A finalidade de comercialização do destino.

>[!NOTE]
>
>Se houver rótulos de uso de dados que foram aplicados somente a determinados campos em um conjunto de dados (em vez de todo o conjunto de dados), a imposição desses rótulos de nível de campo na ativação ocorrerá somente sob as seguintes condições:
>* Os campos são usados na definição do segmento.
>* Os campos são configurados como atributos projetados para o destino do público alvo.


### Linhagem de dados {#lineage}

Na CDP em tempo real, a linha de dados desempenha um papel fundamental na forma como as políticas são aplicadas. Em termos gerais, a linhagem de dados se refere à origem de um conjunto de dados, e o que acontece a ele (ou onde ele se move) ao longo do tempo.

No contexto de [!DNL Data Governance], a linhagem permite que as etiquetas de uso de dados se propaguem de conjuntos de dados para serviços de downstream que consomem seus dados, como Perfil e destinos do cliente em tempo real. Isso permite que as políticas sejam avaliadas e aplicadas em vários pontos-chave na jornada dos dados pela Plataforma, e fornece contexto aos consumidores de dados sobre o porquê de uma violação de política ter ocorrido.

Na CDP em tempo real, a aplicação da política está relacionada com a seguinte linha:

1. Os dados são ingeridos em CDP em tempo real e armazenados em **conjuntos de dados**.
1. Os perfis do cliente são identificados e construídos a partir desses conjuntos de dados, unindo fragmentos de dados de acordo com a política **de** mesclagem.
1. Grupos de perfis são divididos em **segmentos** com base em atributos comuns.
1. Os segmentos são ativados para **destinos** downstream.

Cada estágio na linha do tempo acima representa uma entidade que pode contribuir para que uma política seja violada, conforme descrito na tabela abaixo:

| Fase da linhagem de dados | Papel na execução das políticas |
| --- | --- |
| Conjunto de dados | Os conjuntos de dados contêm rótulos de uso de dados (aplicados no nível do conjunto de dados ou do campo) que definem para quais casos o conjunto de dados inteiro ou campos específicos podem ser usados. Violações de política ocorrerão se um conjunto de dados ou campo que contém determinados rótulos for usado para uma finalidade que uma política restringe. |
| Política de mesclagem | As políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados ao mesclar fragmentos de vários conjuntos de dados. Violações de políticas ocorrerão se suas políticas de mesclagem estiverem configuradas para que os conjuntos de dados com rótulos restritos sejam ativados para um destino. Consulte o guia sobre políticas [de](../../profile/ui/merge-policies.md) mesclagem para obter mais informações. |
| Segmento | As regras do segmento definem quais atributos devem ser incluídos nos perfis do cliente. Dependendo de quais campos uma definição de segmento inclui, o segmento herdará quaisquer rótulos de uso aplicados para esses campos. As violações de política ocorrerão se você ativar um segmento cujos rótulos herdados são restritos pelas políticas aplicáveis do destino do público alvo, com base em seu caso de uso de marketing. |
| Destino | Ao configurar um destino, uma ação de marketing (às vezes chamada de caso de uso de marketing) pode ser definida. Esse caso de uso correlaciona-se a uma ação de marketing, conforme definido em uma política de uso de dados. Em outras palavras, o caso de uso de marketing definido para um destino determina quais políticas de uso de dados são aplicáveis a esse destino. Violações de política ocorrerão se você ativar um segmento cujos rótulos de uso são restritos pelas políticas aplicáveis do destino do público alvo. |

Quando ocorrem violações de política, as mensagens resultantes exibidas na interface do usuário fornecem ferramentas úteis para explorar a linha de dados de contribuição da violação para ajudar a resolver o problema. Mais detalhes são fornecidos na próxima seção.

### Mensagens de violação de política {#enforcement}

Se ocorrer uma violação de política ao tentar ativar um segmento (ou [fazer edições em um segmento](#policy-enforcement-for-activated-segments)já ativado), a ação será impedida e um fornecedor será exibido indicando que uma ou mais políticas foram violadas. Depois que uma violação é acionada, o botão **[!UICONTROL Salvar]** é desativado para a entidade que você está modificando até que os componentes apropriados sejam atualizados para atender às políticas de uso de dados.

Selecione uma violação de política na coluna esquerda do provedor para exibir detalhes dessa violação.

![](assets/governance/violation-policy-select.png)

A mensagem de violação fornece um resumo da política violada, incluindo as condições que a política está configurada para verificar, a ação específica que disparou a violação e uma lista de possíveis resoluções para o problema.

![](assets/governance/violation-summary.png)

Um gráfico de linhagem de dados é exibido abaixo do resumo da violação, permitindo visualizar quais conjuntos de dados, políticas de mesclagem, segmentos e destinos estavam envolvidos na violação de política. A entidade que você está alterando está realçada no gráfico, indicando qual ponto no fluxo está causando a ocorrência da violação. Você pode selecionar um nome de entidade no gráfico para abrir a página de detalhes da entidade em questão.

![](assets/governance/data-lineage.png)

Você também pode usar o ícone **[!UICONTROL Filtrar]** (![](./assets/governance/filter.png)) para filtrar as entidades exibidas por categoria. Pelo menos duas categorias devem ser selecionadas para que os dados sejam exibidos.

![](assets/governance/lineage-filter.png)

Selecione visualização **[!UICONTROL de]** Lista para exibir a linha de dados como uma lista. Para voltar ao gráfico visual, selecione visualização **** do caminho.

![](assets/governance/list-view.png)

### Aplicação de política para segmentos ativados {#policy-enforcement-for-activated-segments}

A imposição de políticas ainda se aplica aos segmentos depois de ativados, restringindo quaisquer alterações a um segmento ou seu destino que resultariam em uma violação de política. Devido ao modo como a linhagem [de](#lineage) dados funciona na aplicação de políticas, qualquer uma das ações a seguir pode possivelmente acionar uma violação:

* Atualização de rótulos de uso de dados
* Alteração de conjuntos de dados para um segmento
* Alteração de predicados de segmento
* Alteração das configurações de destino

Se qualquer uma das ações acima acionar uma violação, essa ação será impedida de ser salva e uma mensagem de violação de política será exibida, garantindo que seus segmentos ativados continuem a seguir as políticas de uso de dados ao serem modificados.

## Próximas etapas

Agora que você foi apresentado aos principais [!DNL Data Governance] recursos da CDP em tempo real e como [!DNL Experience Platform] os habilita, continue com a [documentação do Data Governance no Adobe Experience Platform](../../data-governance/home.md). A documentação fornece visões gerais de [!DNL Data Governance] conceitos essenciais, bem como workflows passo a passo para gerenciar rótulos e políticas de uso de dados.

O vídeo a seguir fornece uma visão geral da CDP em tempo real, incluindo o uso de casos de uso de marketing em destinos e workflows de exemplo para diferentes cenários: [!DNL Data Governance]

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)