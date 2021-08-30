---
keywords: Experience Platform; home; tópicos populares; GDPR; gdpr; ccpa:CCPA; pdpa; PDPA; pdpa_que; PDPA_THA; lgpd; LGPD; lgpd_bra; LGPD_BRA;
solution: Experience Platform
title: Visão geral do Privacy Service
topic-legacy: overview
description: O Privacy Service permite facilitar a conformidade automatizada com as normas legais de privacidade em suas operações de dados do Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 2%

---

# [!DNL Privacy Service] visão geral

Para oferecer melhores experiências ao cliente, é necessário coletar e armazenar os dados pessoais dos clientes. Ao usar esses dados, é importante entender e respeitar a privacidade de seus clientes. As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação.

O Adobe Experience Platform [!DNL Privacy Service] foi desenvolvido em resposta a uma mudança fundamental em como as empresas são necessárias para gerenciar os dados pessoais dos clientes. O objetivo central do [!DNL Privacy Service] é automatizar a conformidade com as regulamentações de privacidade de dados, que, quando violadas, podem resultar em multas importantes e interromper as operações de dados para sua empresa.

[!DNL Privacy Service] O fornece uma RESTful API e interface do usuário para ajudar você a gerenciar solicitações de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

## Introdução a [!DNL Privacy Service] {#getting-started}

Para utilizar [!DNL Privacy Service], várias decisões importantes precisam ser tomadas em termos de requisitos de privacidade de sua organização, os tipos de dados de identidade coletados de seus clientes e a melhor maneira de fazer interface do seu sistema CRM com o serviço.

Estas decisões podem ser resumidas através das seguintes questões:

1. **Quais informações estou coletando de meus clientes?**
   * Para fazer o melhor uso de [!DNL Privacy Service], você deve ter uma compreensão detalhada dos tipos de dados coletados de seus clientes e quais deles estão sujeitos às regras de privacidade. Consulte a seção [determinando requisitos de privacidade](#requirements) para obter mais informações.
1. **Os dados foram rotulados corretamente?**
   * Os dados devem ser rotulados corretamente para que o serviço determine quais campos devem ser acessados ou excluídos durante as tarefas de privacidade. Consulte a seção [rotulando dados](#label) para obter mais informações.
1. **Eu sei para quais IDs enviar  [!DNL Privacy Service]?**
   * Ao enviar solicitações de privacidade, as IDs individuais do cliente específicas para determinados aplicativos do Adobe devem ser fornecidas. Consulte as seções em [fornecendo dados de identidade](#identity) e [fazendo solicitações de privacidade](#requests) para obter mais informações.
1. **Como estou rastreando meus trabalhos de privacidade?**
   * Depois de fazer solicitações de privacidade, há várias opções para rastrear o status e os resultados. Consulte a seção sobre [monitoramento de tarefas de privacidade](#monitor) para obter mais informações.

As seções abaixo fornecem orientação geral sobre essas etapas importantes de pré-requisito e também fornecem links para a documentação adicional [!DNL Privacy Service] para obter mais detalhes.

### Determine os requisitos de privacidade da sua organização {#requirements}

Dependendo da natureza da sua empresa e das jurisdições sob as quais ela opera, suas operações de dados podem estar sujeitas a regulamentos legais de privacidade. Essas regulamentações geralmente dão aos clientes o direito de solicitar acesso aos dados coletados deles e o direito de solicitar a exclusão desses dados armazenados. Essas solicitações de clientes para seus dados pessoais são chamadas de &quot;solicitações de privacidade&quot; em toda a documentação.

Para obter detalhes sobre as diferentes regulamentações legais de privacidade que [!DNL Privacy Service] gerencia solicitações de, incluindo termos e respostas importantes a perguntas frequentes, consulte a [documentação de regulamentos de privacidade](./regulations/overview.md).

Se suas operações de dados estiverem sob o objetivo de qualquer uma das regulamentações compatíveis, revise a documentação para obter informações importantes, como os direitos específicos de privacidade que oferecem aos clientes, e as janelas de conformidade para atender às solicitações de privacidade. Essas informações devem ser consideradas ao determinar como integrar [!DNL Privacy Service] ao seu sistema CRM e como os clientes devem interagir com seu site para fazer solicitações de privacidade.

Além dos regulamentos legais, quaisquer normas organizacionais ou do setor aplicáveis à sua organização também devem ser consideradas ao tomar essas decisões.

### Rotular dados para solicitações de privacidade {#label}

Dependendo dos aplicativos [!DNL Experience Cloud] que você está usando, é necessário rotular os campos de dados específicos que devem ser acessados ou excluídos em resposta às solicitações de privacidade. O processo de rotulagem de dados varia de acordo com os aplicativos. Para saber como rotular dados para cada aplicativo do Adobe suportado, consulte o documento em [Experience Cloud applications](./experience-cloud-apps.md).

### Determine os tipos de dados de identidade para enviar para [!DNL Privacy Service] {#identity}

Para que [!DNL Privacy Service] processe uma solicitação de privacidade de um cliente, pelo menos um valor de identidade exclusivo para esse cliente deve ser fornecido na própria solicitação. Um valor de identidade exclusivo é qualquer parte das informações que podem ser usadas para identificar uma pessoa individual e seus dados pessoais armazenados em seus armazenamentos de dados [!DNL Experience Cloud]. [!DNL Privacy Service] O usa essas informações de identidade para localizar e processar os dados pessoais do cliente de acordo com a natureza da solicitação (acesso, exclusão ou recusa).

Dependendo dos aplicativos [!DNL Experience Cloud] que seu sistema CRM utiliza, o tipo e o número de valores de identidade que você deve fornecer para cada cliente variam. Alguns aplicativos utilizam seus próprios valores internos de ID do cliente (como Adobe Target IDs), enquanto outras soluções dependem de identificadores globais do Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastreiam a atividade do cliente em todos os aplicativos [!DNL Experience Cloud]. Além disso, informações pessoais genéricas, como um endereço de email ou número de telefone, também podem servir como dados de identidade válidos.

O documento em [dados de identidade para solicitações de privacidade](./identity-data.md) fornece informações mais detalhadas sobre os tipos de informações de identidade que são aceitas para [!DNL Privacy Service]. O documento também fornece orientação sobre como aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas de seus clientes à medida que interagem com seu site e enviar esses dados para [!DNL Privacy Service] em solicitações de API.

### Começar a fazer solicitações de privacidade {#requests}

Depois de determinar as necessidades de privacidade da sua empresa e decidir quais valores de identidade enviar para [!DNL Privacy Service], você pode começar a fazer solicitações de privacidade. [!DNL Privacy Service] O permite enviar solicitações de privacidade por meio da API ou da interface do usuário.

>[!IMPORTANT]
>
>As seções abaixo fornecem links para a documentação que abordam como fazer solicitações de privacidade genéricas na API ou na interface do usuário. No entanto, dependendo dos aplicativos [!DNL Experience Cloud] que você está usando, os campos que você deve enviar na carga da solicitação podem ser diferentes dos exemplos mostrados nesses guias.
>
>Conforme você segue junto com os guias da API ou da interface do usuário, consulte o documento em [Privacy Service and Experience Cloud applications](./experience-cloud-apps.md) para obter mais documentação sobre como formatar solicitações de privacidade para seus aplicativos específicos [!DNL Experience Cloud].
>
>Também é importante observar que as solicitações de privacidade são processadas de forma assíncrona em todos os aplicativos Experience Cloud. Depois que uma solicitação é recebida pelo Privacy Service, cada aplicativo pode levar de minutos a semanas para concluir a solicitação. O tempo necessário para concluir cada solicitação é específico para o aplicativo com o qual você está trabalhando e a quantidade de dados que precisa ser processada.

#### Uso da API

O [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) fornece vários endpoints para criar e gerenciar tarefas de privacidade usando chamadas RESTful API, permitindo que você aborde programaticamente a conformidade do regulamento de privacidade para seus aplicativos [!DNL Experience Cloud]. Para obter etapas detalhadas sobre como usar a API, consulte o [Guia do desenvolvedor da API do Privacy Service](api/getting-started.md).

#### Uso da interface do usuário

>[!NOTE]
>
>No momento, a interface do usuário [!DNL Privacy Service] suporta apenas solicitações de acesso e exclusão. Todas as solicitações de recusa devem ser feitas por meio da API .

A interface [!DNL Privacy Service] permite criar e monitorar tarefas de privacidade usando uma interface gráfica. A interface do usuário inclui um widget **[!UICONTROL Relatório de status]** que fornece uma representação visual do status de todas as solicitações ativas e permite criar novas solicitações usando o **[!UICONTROL Construtor de solicitações]** incorporado ou carregando arquivos JSON. Para obter mais informações sobre como usar a interface do usuário, consulte o [guia do usuário do Privacy Service](ui/overview.md).

### Monitorar trabalhos de privacidade {#monitor}

Depois de fazer tarefas de privacidade, você tem várias opções para monitorar seu status e resultados:

| Método de monitorização | Descrição |
| --- | --- |
| [!DNL Privacy Service] Interface | A interface [!DNL Privacy Service] fornece um painel de monitoramento que permite visualizar uma representação visual do status de todas as solicitações ativas. Consulte o [guia do usuário do Privacy Service](ui/overview.md) para obter mais informações. |
| [!DNL Privacy Service] API | Você pode monitorar programaticamente o status de tarefas de Privacidade usando os endpoints de pesquisa fornecidos pela API [!DNL Privacy Service]. Consulte o [Guia do desenvolvedor do Privacy Service](./api/getting-started.md) para obter etapas detalhadas sobre como usar a API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveite os Adobe I/O Events enviados para um webhook configurado para facilitar a automação eficiente de solicitações de trabalhos. Eles reduzem ou eliminam a necessidade de pesquisar a API [!DNL Privacy Service] para verificar se uma tarefa foi concluída ou se um determinado marco em um workflow foi atingido. Consulte o tutorial em [subscrição de Eventos de privacidade](./privacy-events.md) para obter mais informações. |

## Próximas etapas

Este documento forneceu uma visão geral de alto nível de [!DNL Privacy Service] e as principais etapas necessárias para começar a usar os recursos do serviço. Consulte a documentação vinculada em toda a visão geral para obter informações mais detalhadas sobre os vários aspectos do trabalho com [!DNL Privacy Service].
