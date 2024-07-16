---
keywords: Experience Platform;página inicial;tópicos populares;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Visão geral do Privacy Service
description: Descubra como o Privacy Service pode facilitar a conformidade automatizada com as normas legais de privacidade em suas operações de dados Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 5%

---

# Visão geral do Privacy Service

Para oferecer melhores experiências aos clientes, é necessário coletar e armazenar os dados pessoais deles. Ao usar esses dados, é importante entender e respeitar a privacidade dos clientes. As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação.

O Adobe Experience Platform Privacy Service foi desenvolvido em resposta a uma mudança fundamental na forma como as empresas são obrigadas a gerenciar os dados pessoais de seus clientes. O objetivo central do Privacy Service é automatizar a conformidade com as regulamentações de privacidade de dados que, quando violadas, podem resultar em multas graves e interromper as operações de dados da sua empresa.

O Privacy Service fornece uma API RESTful e uma interface para ajudar você a gerenciar solicitações de dados do cliente. Você pode usar o Privacy Service para enviar solicitações para acessar e excluir dados pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

>[!IMPORTANT]
>
>O Privacy Service se destina apenas a solicitações de titulares de dados e de direitos do consumidor. Qualquer outro uso do Privacy Service para limpeza ou manutenção de dados não é suportado ou permitido. A Adobe tem a obrigação legal de os cumprir em tempo útil. Dessa forma, o teste de carga no Privacy Service não é permitido, pois é um ambiente somente de produção e cria um backlog desnecessário de solicitações de privacidade válidas.
>
>Um limite rígido de upload diário está em vigor para ajudar a evitar o abuso do serviço. Os usuários que abusam do sistema terão o acesso ao serviço desativado. Uma reunião subsequente será realizada com eles para abordar suas ações e discutir o uso aceitável do Privacy Service.

## Introdução ao Privacy Service {#getting-started}

Para fazer uso ideal do Privacy Service, várias decisões importantes devem ser tomadas em termos dos requisitos de privacidade da sua organização, os tipos de dados de identidade coletados dos clientes e a melhor maneira de interagir o sistema de CRM com o serviço.

Essas decisões podem ser resumidas através das seguintes perguntas:

1. **Que informações estou coletando dos meus clientes?**
   * Para aproveitar ao máximo o Privacy Service, você deve ter uma compreensão detalhada dos tipos de dados coletados de seus clientes e quais deles estão sujeitos a regulamentos de privacidade. Consulte a seção sobre [determinando os requisitos de privacidade](#requirements) para obter mais informações.
1. **Os meus dados foram rotulados corretamente?**
   * Os dados devem ser rotulados corretamente para que o serviço determine quais campos acessar ou excluir durante trabalhos de privacidade. Consulte a seção sobre [rotulando dados](#label) para obter mais informações.
1. **Eu sei quais IDs enviar para o Privacy Service?**
   * Ao enviar solicitações de privacidade, as IDs individuais do cliente específicas para aplicativos Adobe específicos devem ser fornecidas. Consulte as seções em [fornecendo dados de identidade](#identity) e [fazendo solicitações de privacidade](#requests) para obter mais informações.
1. **Como estou rastreando meus trabalhos de privacidade?**
   * Depois de fazer solicitações de privacidade, há várias opções para rastrear o status e os resultados. Consulte a seção sobre [monitoramento de trabalhos de privacidade](#monitor) para obter mais informações.

As seções abaixo fornecem orientação geral sobre essas etapas importantes de pré-requisitos e também fornecem links para a documentação adicional do Privacy Service para obter mais detalhes.

### Determine os requisitos de privacidade de sua organização {#requirements}

Dependendo da natureza da sua empresa e das jurisdições sob as quais ela opera, suas operações de dados podem estar sujeitas a regulamentos legais de privacidade. Esses regulamentos geralmente oferecem aos clientes o direito de solicitar acesso aos dados coletados deles e o direito de solicitar a exclusão desses dados armazenados. Essas solicitações de dados pessoais feitas pelos clientes são chamadas de &quot;solicitações de privacidade&quot; em toda a documentação.

Para obter detalhes sobre os diferentes regulamentos legais de privacidade que o Privacy Service gerencia solicitações de, incluindo termos importantes e respostas a perguntas frequentes, consulte a [documentação de regulamentos de privacidade](./regulations/overview.md).

Se suas operações de dados se enquadrarem no escopo de qualquer um dos regulamentos compatíveis, consulte sua documentação para obter informações importantes, como os direitos de privacidade específicos que eles concedem aos clientes e as janelas de conformidade para atender a solicitações de privacidade. Essas informações devem ser consideradas ao determinar como integrar o Privacy Service ao seu sistema de CRM e como os clientes devem interagir com seu site para fazer solicitações de privacidade.

Além de regulamentos legais, quaisquer padrões organizacionais ou do setor aplicáveis à sua organização também devem ser considerados ao tomar essas decisões.

### Rotular dados para solicitações de privacidade {#label}

Dependendo dos aplicativos do [!DNL Experience Cloud] que você estiver usando, será necessário rotular os campos de dados específicos que devem ser acessados ou excluídos em resposta às solicitações de privacidade. O processo de rotulação de dados varia entre os aplicativos. Para saber como rotular dados para cada aplicativo Adobe suportado, consulte o documento em [aplicativos Experience Cloud](./experience-cloud-apps.md).

### Determine os tipos de dados de identidade a serem enviados para o Privacy Service {#identity}

Para que o Privacy Service processe uma solicitação de privacidade de um cliente, pelo menos um valor de identidade exclusivo para esse cliente deve ser fornecido na própria solicitação. Um valor de identidade exclusivo é qualquer informação que possa ser usada para identificar uma pessoa individual e seus dados pessoais armazenados nos armazenamentos de dados do [!DNL Experience Cloud]. O Privacy Service usa essas informações de identidade para localizar e processar os dados pessoais do cliente de acordo com a natureza da solicitação (acesso, exclusão ou recusa).

Dependendo dos aplicativos do [!DNL Experience Cloud] que seu sistema de CRM usa, o tipo e o número de valores de identidade que você deve fornecer para cada cliente variam. Alguns aplicativos usam seus próprios valores internos de IDs do cliente (como Adobe Target IDs), enquanto outras soluções dependem de identificadores globais do Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastreiam a atividade do cliente em todos os aplicativos [!DNL Experience Cloud]. Além disso, informações pessoais genéricas, como um endereço de email ou número de telefone, também podem servir como dados de identidade válidos.

Leia o documento em [dados de identidade para solicitações de privacidade](./identity-data.md) para obter informações mais detalhadas sobre os tipos de informações de identidade aceitas para o Privacy Service. O documento também fornece orientação sobre como aplicar as tecnologias de Adobe para recuperar efetivamente as informações de identidade apropriadas de seus clientes à medida que eles interagem com seu site e enviar esses dados para o Privacy Service em solicitações de API.

### Comece a fazer solicitações de privacidade {#requests}

Depois de determinar as necessidades de privacidade de sua empresa e decidir quais valores de identidade enviar para o Privacy Service, você pode começar a fazer solicitações de privacidade. Use o Privacy Service para enviar solicitações de privacidade por meio da API ou da interface do usuário.

>[!IMPORTANT]
>
>As seções abaixo fornecem links para a documentação que aborda como fazer solicitações de privacidade genéricas na API ou na interface do usuário. No entanto, dependendo dos aplicativos do [!DNL Experience Cloud] que você está usando, os campos que você deve enviar na carga da solicitação podem ser diferentes dos exemplos mostrados nesses guias.
>
>À medida que seguir os guias da API ou da interface do usuário, consulte o documento em [Privacy Service e aplicativos Experience Cloud](./experience-cloud-apps.md) para obter mais documentação sobre como formatar solicitações de privacidade para seus aplicativos [!DNL Experience Cloud] específicos.
>
>Também é importante observar que as solicitações de privacidade são processadas de forma assíncrona nos aplicativos do Experience Cloud. Depois que uma solicitação é recebida pelo Privacy Service, cada aplicativo pode levar de minutos a semanas para concluir a solicitação. O tempo necessário para concluir cada solicitação é específico para o aplicativo com o qual você está trabalhando e a quantidade de dados que precisam ser processados.

#### Uso da API {#api}

Para abordar programaticamente a conformidade com as regulamentações de privacidade para seus aplicativos do [!DNL Experience Cloud], você pode usar chamadas de API RESTful para [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) pontos de extremidade para criar e gerenciar trabalhos de privacidade. Para obter etapas detalhadas sobre como usar a API, consulte o [guia da API do Privacy Service](api/overview.md).

#### Uso da interface {#ui}

>[!NOTE]
>
>Atualmente, a interface do usuário do Privacy Service só oferece suporte a solicitações de acesso e exclusão. Todas as solicitações de recusa devem ser feitas por meio da API.

Você pode criar e monitorar processos de privacidade usando uma interface gráfica com a interface de usuário do Privacy Service. A interface do usuário inclui um widget do **[!UICONTROL Relatório de status]** que fornece uma representação visual do status de todas as solicitações ativas, e você pode criar solicitações com o **[!UICONTROL Construtor de solicitações]** interno ou carregando arquivos JSON. Para obter mais informações sobre como usar a interface, consulte o [guia do usuário do Privacy Service](ui/overview.md).

### Monitorar trabalhos de privacidade {#monitor}

Depois de realizar os trabalhos de privacidade, você terá várias opções para monitorar o status e os resultados:

| Método de monitoramento | Descrição |
| --- | --- |
| IU DO PRIVACY SERVICE | Você pode visualizar uma representação visual do status de todas as solicitações ativas com o painel de monitoramento da interface do Privacy Service. Consulte o [guia do usuário do Privacy Service](ui/overview.md) para obter mais informações. |
| API PRIVACY SERVICE | Você pode monitorar programaticamente o status de processos de privacidade usando os pontos de extremidade de pesquisa fornecidos pela API Privacy Service. Consulte o [guia da API de Privacy Service](./api/overview.md) para obter etapas detalhadas sobre como usar a API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] use Eventos Adobe I/O que são enviados para um webhook configurado para facilitar a automação eficiente da solicitação de trabalho. Eles reduzem ou eliminam a necessidade de pesquisar a API de Privacy Service para verificar se um trabalho foi concluído ou se uma determinada etapa em um fluxo de trabalho foi atingida. Consulte o tutorial sobre [assinatura de eventos de privacidade](./privacy-events.md) para obter mais informações. |

## Próximas etapas

Este documento forneceu uma visão geral de alto nível do Privacy Service e as principais etapas necessárias para começar a usar os recursos do serviço. Consulte a documentação relacionada à visão geral para obter informações mais detalhadas sobre os vários aspectos do trabalho com o Privacy Service.
