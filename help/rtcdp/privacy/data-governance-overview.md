---
keywords: controle de dados rtcdp; controle de dados rtcdp; controle de dados de perfil de dados de clientes em tempo real
title: Visão geral da governança de dados
seo-title: Data Governance in Real-time Customer Data Platform
description: 'A Governança de dados permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Governança de dados na CDP em tempo real

[!DNL Real-time Customer Data Platform] (CDP em tempo real) reúne dados de vários sistemas empresariais, permitindo que os profissionais de marketing identifiquem, entendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais. Portanto, é importante garantir que a CDP em tempo real esteja em conformidade com as políticas de uso ao manipular seus dados.

A Governança de dados do Adobe Experience Platform permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função essencial na CDP em tempo real, permitindo definir políticas de uso, categorizar seus dados com base nessas políticas e verificar violações de política ao executar determinadas ações de marketing.

A CDP em tempo real foi criada sobre o Adobe Experience Platform e, portanto, a maioria dos recursos de Governança de dados é abordada no [!DNL Experience Platform] documentação. Este documento destina-se a complementar o [Visão geral da governança de dados](../../data-governance/home.md) para [!DNL Experience Platform]e descreve os recursos de Governança disponíveis na CDP em tempo real. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade de uso de dados](#enforce)

## Aplicar rótulos de uso aos seus dados {#labels}

A Governança de dados permite aplicar rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem categorizar os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configurar ações de marketing para destinos {#destinations}

Você pode definir restrições de uso de dados em um destino definindo ações de marketing (também chamadas de casos de uso de marketing) para esse destino. Uma ação de marketing para um destino indica a intenção dos dados que serão exportados para esse destino.

>[!NOTE]
>
>Para obter mais informações sobre ações de marketing e seu uso em políticas de uso de dados, consulte o [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) no [!DNL Experience Platform] documentação.

A definição de ações de marketing em destinos permite garantir que todos os perfis ou segmentos enviados para esses destinos sejam compatíveis com as políticas de uso de dados. Portanto, você deve adicionar as ações de marketing apropriadas aos destinos com base nas necessidades da organização para impor restrições de política na ativação.

As ações de marketing só podem ser selecionadas ao configurar um destino pela primeira vez. Dependendo do tipo de destino com o qual você está trabalhando, a oportunidade de configurar ações de marketing será exibida em pontos diferentes no fluxo de trabalho de configuração. Consulte a [documentação de destinos](../destinations/overview.md) para obter etapas sobre como configurar seu destino específico.

## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados sejam compatíveis com a conformidade dos dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que você tem permissão para ou tem restrição de executar em dados dentro da CDP em tempo real. Consulte a seção &quot;Políticas de uso de dados&quot; em [!DNL Experience Platform] [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

A Adobe Experience Platform fornece várias políticas principais para casos de uso comuns da experiência do cliente. Essas políticas podem ser visualizadas na interface do usuário navegando até o **[!UICONTROL Políticas]** e selecionar o **[!UICONTROL Procurar]** guia . Consulte a [guia do usuário de políticas](../../data-governance/policies/user-guide.md) no [!DNL Experience Platform] documentação para obter etapas mais detalhadas sobre como trabalhar com políticas na interface do usuário, incluindo como fazer suas próprias políticas personalizadas.

## Impor conformidade de uso de dados {#enforce}

Depois que os dados forem rotulados e as políticas de uso forem definidas, é possível impor a conformidade do uso de dados com as políticas. Ao ativar segmentos de público-alvo para destinos na CDP em tempo real, a Governança de dados aplica automaticamente as políticas de uso em caso de violação.

Consulte o documento em [aplicação automática da política](../../data-governance/enforcement/auto-enforcement.md) para obter mais informações.

## Próximas etapas

Agora que você foi introduzido nos principais recursos de Governança de dados da CDP em tempo real e como [!DNL Experience Platform] habilite-os, continue para o [documentação da Governança de dados no Adobe Experience Platform](../../data-governance/home.md). A documentação fornece visões gerais dos conceitos essenciais de Governança de dados, bem como fluxos de trabalho passo a passo para gerenciar rótulos e políticas de uso de dados.

O vídeo a seguir fornece uma visão geral da Governança de dados na CDP em tempo real, incluindo o uso de casos de uso de marketing em destinos e fluxos de trabalho de exemplo para diferentes cenários:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
