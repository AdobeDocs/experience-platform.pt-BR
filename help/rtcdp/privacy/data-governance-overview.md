---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Visão geral do controle de dados
seo-title: Controle de dados na plataforma de dados do cliente em tempo real
description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
seo-description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# [!DNL Data Governance] em CDP em tempo real

[!DNL Real-time Customer Data Platform] (CDP em tempo real) reúne dados de vários sistemas corporativos, permitindo que os profissionais de marketing identifiquem, entendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos às restrições de uso definidas pela sua organização ou por regulamentos legais. Portanto, é importante garantir que a CDP em tempo real esteja em conformidade com as políticas de uso ao manipular seus dados.

A Adobe Experience Platform [!DNL Data Governance] permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na CDP em tempo real, permitindo que você defina políticas de uso, classifique seus dados com base nessas políticas e verifique violações de políticas ao executar determinadas ações de marketing.

A CDP em tempo real foi criada sobre a Adobe Experience Platform e, portanto, a maioria dos recursos [!DNL Data Governance] são abordados na documentação [!DNL Experience Platform]. Este documento é destinado a complementar a [visão geral do Data Governance](../../data-governance/home.md) para [!DNL Experience Platform] e descreve os recursos de controle disponíveis na CDP em tempo real. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade de uso de dados](#enforce)

## Aplique rótulos de uso aos seus dados {#labels}

[!DNL Data Governance] permite que você aplique rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem que você categorize os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configurar casos de uso de marketing para destinos {#destinations}

É possível definir restrições de uso de dados em um destino definindo casos de uso de marketing (também chamados de ações de marketing) para esse destino. Um caso de uso de marketing para um destino indica a intenção dos dados que serão exportados para esse destino.

>[!NOTE]
>
>Para obter mais informações sobre ações de marketing e seu uso em políticas de uso de dados, consulte a [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) na documentação [!DNL Experience Platform].

A definição de casos de uso de marketing em destinos permite garantir que quaisquer perfis ou segmentos enviados para esses destinos sejam compatíveis com as políticas de uso de dados. Portanto, você deve adicionar casos de uso de marketing apropriados aos seus destinos com base nas necessidades de sua organização para aplicar restrições de política à ativação.

Os casos de uso de marketing só podem ser selecionados ao configurar um destino pela primeira vez. Dependendo do tipo de destino com o qual você está trabalhando, a oportunidade de configurar casos de uso de marketing aparecerá em diferentes pontos no fluxo de trabalho da configuração. Consulte a [documentação de destinos](../destinations/overview.md) para obter etapas sobre como configurar seu destino específico.

## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro da CDP em tempo real. Consulte a seção &quot;Políticas de uso de dados&quot; em [!DNL Experience Platform] [Visão geral do Data Governance](../../data-governance/home.md) para obter mais informações.

A Adobe Experience Platform fornece várias políticas principais para casos comuns de uso da experiência do cliente. Essas políticas podem ser visualizadas na interface do usuário navegando até a área de trabalho **[!UICONTROL Policies]** e selecionando a guia **[!UICONTROL Procurar]**. Consulte o [guia do usuário de políticas](../../data-governance/policies/user-guide.md) na documentação [!DNL Experience Platform] para obter etapas mais detalhadas sobre como trabalhar com políticas na interface do usuário, incluindo como fazer suas próprias políticas personalizadas.

## Impor conformidade de uso de dados {#enforce}

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá aplicar a conformidade de uso de dados com as políticas. Ao ativar segmentos de audiência para destinos em CDP em tempo real, [!DNL Data Governance] aplica automaticamente as políticas de uso caso ocorram violações.

Consulte o documento em [aplicação automática de política](../../data-governance/enforcement/auto-enforcement.md) para obter mais informações.

## Próximas etapas

Agora que você foi apresentado aos principais recursos [!DNL Data Governance] em CDP em tempo real e como [!DNL Experience Platform] os habilita, continue com a documentação [para o Data Governance no Adobe Experience Platform](../../data-governance/home.md). A documentação fornece visões gerais dos conceitos [!DNL Data Governance] essenciais, bem como workflows passo a passo para gerenciar rótulos e políticas de uso de dados.

O vídeo a seguir fornece uma visão geral de [!DNL Data Governance] no CDP em tempo real, incluindo o uso de casos de uso de marketing em destinos e workflows de exemplo para diferentes cenários:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)