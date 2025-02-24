---
keywords: governança de dados rtcdp;governança de dados rtcdp;governança de dados do perfil de dados do cliente em tempo real
title: Visão geral da governança de dados
description: O controle de dados permite gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Governança de dados no Real-Time CDP

O [!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) reúne dados de vários sistemas corporativos, permitindo que os profissionais de marketing identifiquem, compreendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais. Portanto, é importante garantir que o Real-Time CDP esteja em conformidade com as políticas de uso ao manipular seus dados.

O Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no Real-Time CDP, permitindo definir políticas de uso, categorizar seus dados com base nessas políticas e verificar violações de política ao executar determinadas ações de marketing.

O Real-Time CDP foi criado com base no Adobe Experience Platform e, portanto, a maioria dos recursos de Governança de dados é abordada na documentação do [!DNL Experience Platform]. Este documento complementa a [Visão geral da Governança de Dados](../../data-governance/home.md) para [!DNL Experience Platform] e descreve os recursos de Governança disponíveis no Real-Time CDP. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade com o uso de dados](#enforce)

## Aplicar rótulos de uso aos seus dados {#labels}

A Governança de dados permite aplicar rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem categorizar os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configurar ações de marketing para destinos {#destinations}

É possível definir restrições de uso de dados em um destino definindo ações de marketing (também chamadas de casos de uso de marketing) para esse destino. Uma ação de marketing para um destino indica a intenção dos dados que serão exportados para esse destino.

>[!NOTE]
>
>Para obter mais informações sobre ações de marketing e seu uso em políticas de uso de dados, consulte a [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) na documentação de [!DNL Experience Platform].

Definir ações de marketing em destinos permite garantir que todos os perfis ou públicos enviados para esses destinos estejam em conformidade com as políticas de uso de dados. Portanto, você deve adicionar as ações de marketing apropriadas aos seus destinos com base nas necessidades da sua organização para aplicar restrições de política na ativação.

As ações de marketing só podem ser selecionadas ao configurar um destino pela primeira vez. Dependendo do tipo de destino com o qual você está trabalhando, a oportunidade de configurar ações de marketing aparecerá em diferentes pontos do fluxo de trabalho de configuração. Consulte a [documentação de destinos](../destinations/overview.md) para obter etapas sobre como configurar seu destino específico.

## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados estejam de acordo com a conformidade de dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados dentro do Real-Time CDP. Consulte a seção &quot;Políticas de uso de dados&quot; na [!DNL Experience Platform] [Visão geral da Governança de dados](../../data-governance/home.md) para obter mais informações.

A Adobe Experience Platform fornece várias políticas principais para casos de uso comuns de experiência do cliente. Essas políticas podem ser exibidas na interface navegando até o espaço de trabalho **[!UICONTROL Políticas]** e selecionando a guia **[!UICONTROL Procurar]**. Consulte o [guia do usuário de políticas](../../data-governance/policies/user-guide.md) na documentação do [!DNL Experience Platform] para obter etapas mais detalhadas sobre como trabalhar com políticas na interface, incluindo como criar suas próprias políticas personalizadas.

## Impor conformidade com o uso de dados {#enforce}

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá impor a conformidade do uso de dados com as políticas. Ao ativar públicos para destinos na Real-Time CDP, a Governança de dados impõe automaticamente políticas de uso caso ocorram violações.

Consulte o documento sobre [aplicação automática de política](../../data-governance/enforcement/auto-enforcement.md) para obter mais informações.

## Próximas etapas

Agora que você foi apresentado aos principais recursos de Governança de dados no Real-Time CDP e como o [!DNL Experience Platform] os habilita, continue com a [documentação sobre Governança de dados no Adobe Experience Platform](../../data-governance/home.md). A documentação fornece visões gerais de conceitos essenciais de governança de dados, bem como fluxos de trabalho passo a passo para gerenciar rótulos e políticas de uso de dados.

O vídeo a seguir fornece uma visão geral da Governança de dados no Real-Time CDP, incluindo o uso de casos de uso de marketing em destinos e fluxos de trabalho de exemplo para diferentes cenários:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
