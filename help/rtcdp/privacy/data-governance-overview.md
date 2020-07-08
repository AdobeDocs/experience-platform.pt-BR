---
title: Visão geral do controle de dados
seo-title: Controle de dados na Platform de dados do cliente em tempo real
description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
seo-description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---


# Controle de dados em CDP em tempo real

A Real-time Customer Data Platform (Real-time CDP) reúne dados de vários sistemas corporativos, permitindo que os profissionais de marketing identifiquem, entendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos a restrições de uso definidas pela sua organização ou por regulamentos legais. Portanto, é importante garantir que a CDP em tempo real esteja em conformidade com as políticas de uso ao manipular seus dados.

O controle de dados do Adobe Experience Platform permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na CDP em tempo real, permitindo que você defina políticas de uso, classifique seus dados com base nessas políticas e verifique violações de políticas ao executar determinadas ações de marketing.

A CDP em tempo real foi desenvolvida sobre o Adobe Experience Platform e, portanto, a maioria dos recursos de controle de dados são abordados na documentação do Experience Platform. Este documento é destinado a complementar a visão geral [do controle de](../../data-governance/home.md) dados para o Experience Platform e descreve os recursos de controle disponíveis na CDP em tempo real. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade de uso de dados](#enforce-data-usage-compliance)

## Aplicar rótulos de uso aos seus dados {#labels}

O controle de dados permite que você aplique rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem que você categorize os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte o guia [do usuário de rótulos de uso de](../../data-governance/labels/overview.md) dados para Adobe Experience Platform.

## Configurar casos de uso de marketing para destinos {#destinations}

É possível definir restrições de uso de dados em um destino definindo casos de uso de marketing (também chamados de ações de marketing) para esse destino. Um caso de uso de marketing para um destino indica a intenção dos dados que serão exportados para esse destino.

>[!NOTE]
>
>Para obter mais informações sobre ações de marketing e seu uso em políticas de uso de dados, consulte a visão geral [das políticas de uso de](../../data-governance/policies/overview.md) dados na documentação do Experience Platform.

A definição de casos de uso de marketing em destinos permite garantir que quaisquer perfis ou segmentos enviados para esses destinos sejam compatíveis com as políticas de uso de dados. Portanto, você deve adicionar casos de uso de marketing apropriados aos seus destinos com base nas necessidades de sua organização para aplicar restrições de política à ativação.

Os casos de uso de marketing só podem ser selecionados ao configurar um destino pela primeira vez. Dependendo do tipo de destino com o qual você está trabalhando, a oportunidade de configurar casos de uso de marketing aparecerá em diferentes pontos no fluxo de trabalho da configuração. Consulte a documentação [de](../destinations/destinations-overview.md) destino para obter etapas sobre como configurar seu destino específico.


## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro da CDP em tempo real. Consulte a seção &quot;Políticas de uso de dados&quot; na visão geral [do Experience Platform](../../data-governance/home.md) Data Governance para obter mais informações.

O Adobe Experience Platform fornece várias políticas **** principais para casos comuns de uso da experiência do cliente. Essas políticas podem ser exibidas na interface do usuário navegando até a área de trabalho **[!UICONTROL Políticas]** e selecionando a guia **[!UICONTROL Procurar]** . Consulte o guia [de usuário de](../../data-governance/policies/user-guide.md) políticas na documentação do Experience Platform para obter etapas mais detalhadas sobre como trabalhar com políticas na interface do usuário, incluindo como fazer suas próprias políticas personalizadas.

## (Beta) Reforçar a conformidade de uso de dados {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Este recurso está atualmente em beta e não está disponível para todos os usuários. Ele pode ser ativado mediante solicitação. A documentação e a funcionalidade estão sujeitas a alterações.

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá aplicar a conformidade de uso de dados com as políticas. Ao ativar segmentos de audiência para destinos em CDP em tempo real, o Data Governance automaticamente aplica as políticas de uso caso ocorram violações.

O diagrama a seguir ilustra como a aplicação de políticas é integrada ao fluxo de dados da ativação de segmentos:

![](assets/enforcement-flow.png)

Quando um segmento é ativado pela primeira vez, o Serviço de Política DULE verifica se há violações de política com base nos seguintes fatores:

* Os rótulos de uso de dados aplicados a campos e conjuntos de dados dentro do segmento a ser ativado.
* A finalidade de comercialização do destino.

>[!NOTE]
>
>Se houver rótulos de uso de dados que foram aplicados somente a determinados campos em um conjunto de dados (em vez de todo o conjunto de dados), a imposição desses rótulos de nível de campo na ativação ocorrerá somente sob as seguintes condições:
>* Os campos são usados na definição do segmento.
>* Os campos são configurados como atributos projetados para o destino do público alvo.


### Mensagens de violação de política {#enforcement}

Se ocorrer uma violação de política ao tentar ativar um segmento (ou [fazer edições em um segmento](#policy-enforcement-for-activated-segments)já ativado), a ação será impedida e um fornecedor será exibido indicando que uma ou mais políticas foram violadas. Selecione uma violação de política na coluna esquerda do provedor para exibir detalhes dessa violação.

![](assets/violation-popover.png)

A guia *Detalhes* do fornecedor indica a ação que acionou a violação o motivo da violação e fornece sugestões para como resolver o problema.

Clique em Linhagem **de** dados para rastrear os destinos, segmentos, políticas de mesclagem ou conjuntos de dados cujos rótulos de dados acionaram a violação.

![](assets/data-lineage.png)

Depois que uma violação é acionada, o botão **Salvar** é desativado para a ativação até que os componentes apropriados sejam atualizados para atender às políticas de uso de dados.

### Aplicação de política para segmentos ativados {#policy-enforcement-for-activated-segments}

A imposição de políticas ainda se aplica aos segmentos depois de ativados, restringindo quaisquer alterações a um segmento ou seu destino que resultariam em uma violação de política. Devido aos diversos componentes envolvidos na ativação de segmentos para destinos, qualquer uma das ações a seguir pode possivelmente acionar uma violação:

* Atualização de rótulos de uso de dados
* Alteração de conjuntos de dados para um segmento
* Alteração de predicados de segmento
* Alteração das configurações de destino

Se qualquer uma das ações acima acionar uma violação, essa ação será impedida de ser salva e uma mensagem de violação de política será exibida, garantindo que seus segmentos ativados continuem a seguir as políticas de uso de dados ao serem modificados.

## Próximas etapas

Agora que você foi apresentado aos principais recursos do Data Governance em CDP em tempo real e como o Experience Platform os habilita, continue com a [documentação do Data Governance no Adobe Experience Platform](../../data-governance/home.md). A documentação fornece visões gerais dos conceitos essenciais do Data Governance, bem como workflows passo a passo para gerenciar rótulos e políticas de uso de dados.

O vídeo a seguir fornece uma visão geral do controle de dados na CDP em tempo real, incluindo o uso de casos de uso de marketing em destinos e workflows de exemplo para diferentes cenários:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)