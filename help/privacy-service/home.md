---
keywords: Experience Platform;página inicial;tópicos populares;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Visão geral do Privacy Service
description: O Privacy Service permite facilitar a conformidade automatizada com as normas legais de privacidade em suas operações de dados Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 5%

---

# Visão geral do [!DNL Privacy Service]

Para oferecer melhores experiências aos clientes, é necessário coletar e armazenar os dados pessoais deles. Ao usar esses dados, é importante entender e respeitar a privacidade dos clientes. As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação.

Adobe Experience Platform [!DNL Privacy Service] foi desenvolvido em resposta a uma mudança fundamental na forma como as empresas são obrigadas a gerenciar os dados pessoais de seus clientes. O objetivo central da [!DNL Privacy Service] O é automatizar a conformidade com as regulamentações de privacidade de dados que, quando violadas, podem resultar em multas graves e interromper as operações de dados da sua empresa.

[!DNL Privacy Service] O fornece uma API RESTful e uma interface para ajudar você a gerenciar solicitações de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

## Introdução ao [!DNL Privacy Service] {#getting-started}

A fim de utilizar os [!DNL Privacy Service], várias decisões importantes precisam ser tomadas em termos dos requisitos de privacidade da sua organização, dos tipos de dados de identidade coletados dos clientes e da melhor maneira de interagir seu sistema de CRM com o serviço.

Essas decisões podem ser resumidas através das seguintes perguntas:

1. **Quais informações estou coletando de meus clientes?**
   * Para tirar o melhor partido possível do [!DNL Privacy Service], você deve ter uma compreensão detalhada dos tipos de dados coletados de seus clientes e quais deles estão sujeitos a regulamentos de privacidade. Consulte a seção sobre [determinação dos requisitos de privacidade](#requirements) para obter mais informações.
1. **Os dados estão corretamente rotulados?**
   * Os dados devem ser rotulados corretamente para que o serviço determine quais campos acessar ou excluir durante trabalhos de privacidade. Consulte a seção sobre [rotulagem de dados](#label) para obter mais informações.
1. **Sei quais IDs enviar para o [!DNL Privacy Service]?**
   * Ao enviar solicitações de privacidade, as IDs individuais do cliente específicas para aplicativos Adobe específicos devem ser fornecidas. Consulte as seções sobre [fornecimento de dados de identidade](#identity)  e [fazer solicitações de privacidade](#requests) para obter mais informações.
1. **Como estou rastreando meus trabalhos de privacidade?**
   * Depois de fazer solicitações de privacidade, há várias opções para rastrear o status e os resultados. Consulte a seção sobre [monitoramento de processos de privacidade](#monitor) para obter mais informações.

As seções abaixo fornecem orientações gerais sobre essas importantes etapas de pré-requisitos e também fornecem links para outras [!DNL Privacy Service] para obter mais detalhes.

### Determine os requisitos de privacidade de sua organização {#requirements}

Dependendo da natureza da sua empresa e das jurisdições sob as quais ela opera, suas operações de dados podem estar sujeitas a regulamentos legais de privacidade. Esses regulamentos geralmente oferecem aos clientes o direito de solicitar acesso aos dados coletados deles e o direito de solicitar a exclusão desses dados armazenados. Essas solicitações de dados pessoais feitas pelos clientes são chamadas de &quot;solicitações de privacidade&quot; em toda a documentação.

Para obter detalhes sobre os diferentes regulamentos legais de privacidade que [!DNL Privacy Service] gerencia solicitações de, incluindo termos principais e respostas a perguntas frequentes, consulte a [documentação de regulamentos de privacidade](./regulations/overview.md).

Se suas operações de dados se enquadrarem no escopo de qualquer um dos regulamentos compatíveis, consulte sua documentação para obter informações importantes, como os direitos de privacidade específicos que eles concedem aos clientes e as janelas de conformidade para atender a solicitações de privacidade. Estas informações devem ser tidas em conta na determinação da forma de integração [!DNL Privacy Service] no sistema CRM e como os clientes devem interagir com seu site para fazer solicitações de privacidade.

Além de regulamentos legais, quaisquer padrões organizacionais ou do setor aplicáveis à sua organização também devem ser considerados ao tomar essas decisões.

### Rotular dados para solicitações de privacidade {#label}

Dependendo do [!DNL Experience Cloud] aplicativos que você está usando, é necessário rotular os campos de dados específicos que devem ser acessados ou excluídos em resposta às solicitações de privacidade. O processo de rotulação de dados varia entre os aplicativos. Para saber como rotular dados para cada aplicativo Adobe compatível, consulte o documento em [aplicativos Experience Cloud](./experience-cloud-apps.md).

### Determine os tipos de dados de identidade para enviar [!DNL Privacy Service] {#identity}

A fim de [!DNL Privacy Service] para processar uma solicitação de privacidade de um cliente, pelo menos um valor de identidade exclusivo para esse cliente deve ser fornecido na própria solicitação. Um valor de identidade exclusivo é qualquer informação que possa ser usada para identificar uma pessoa individual e seus dados pessoais armazenados em seu [!DNL Experience Cloud] armazenamentos de dados. [!DNL Privacy Service] O usa essas informações de identidade para localizar e processar os dados pessoais do cliente de acordo com a natureza da solicitação (acesso, exclusão ou recusa).

Dependendo do [!DNL Experience Cloud] aplicativos que seu sistema de CRM utiliza, o tipo e o número de valores de identidade que você deve fornecer para cada cliente variam. Alguns aplicativos utilizam seus próprios valores internos de IDs do cliente (como Adobe Target IDs), enquanto outras soluções dependem de identificadores globais do Adobe [!DNL Experience Cloud Identity Service] (ECID) que controlam a atividade do cliente em todas as [!DNL Experience Cloud] aplicativos. Além disso, informações pessoais genéricas, como um endereço de email ou número de telefone, também podem servir como dados de identidade válidos.

O documento sobre [dados de identidade para solicitações de privacidade](./identity-data.md) fornece informações mais detalhadas sobre os tipos de informações de identidade aceitas para [!DNL Privacy Service]. O documento também fornece orientação sobre como aproveitar as tecnologias Adobe para recuperar efetivamente as informações de identidade apropriadas de seus clientes à medida que eles interagem com seu site e enviar esses dados para o [!DNL Privacy Service] em solicitações de API.

### Comece a fazer solicitações de privacidade {#requests}

Depois de determinar as necessidades de privacidade de sua empresa e decidir a quais valores de identidade enviar [!DNL Privacy Service], você pode começar a fazer solicitações de privacidade. [!DNL Privacy Service] O permite enviar solicitações de privacidade por meio da API ou da interface.

>[!IMPORTANT]
>
>As seções abaixo fornecem links para a documentação que aborda como fazer solicitações de privacidade genéricas na API ou na interface do usuário. No entanto, dependendo da [!DNL Experience Cloud] aplicativos que você está usando, os campos que você deve enviar na carga da solicitação podem ser diferentes dos exemplos mostrados nesses guias.
>
>Conforme você seguir os guias da API ou da interface do usuário, consulte o documento em [aplicativos Privacy Service e Experience Cloud](./experience-cloud-apps.md) para obter mais documentação sobre como formatar solicitações de privacidade para sua [!DNL Experience Cloud] aplicativo(s).
>
>Também é importante observar que as solicitações de privacidade são processadas de forma assíncrona nos aplicativos do Experience Cloud. Depois que uma solicitação é recebida pelo Privacy Service, cada aplicativo pode levar de minutos a semanas para concluir a solicitação. O tempo necessário para concluir cada solicitação é específico para o aplicativo com o qual você está trabalhando e a quantidade de dados que precisam ser processados.

#### Uso da API

A variável [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) O fornece vários endpoints para criar e gerenciar trabalhos de privacidade usando chamadas RESTful API, permitindo que você aborde programaticamente a conformidade com o regulamento de privacidade para suas [!DNL Experience Cloud] aplicativos. Para obter etapas detalhadas sobre como usar a API, consulte [Guia da API do Privacy Service](api/overview.md).

#### Uso da interface

>[!NOTE]
>
>A variável [!DNL Privacy Service] Atualmente, a interface do usuário só oferece suporte a solicitações de acesso e exclusão. Todas as solicitações de recusa devem ser feitas por meio da API.

A variável [!DNL Privacy Service] A interface permite criar e monitorar processos de privacidade usando uma interface gráfica. A interface do usuário inclui uma **[!UICONTROL Relatório de Status]** widget que fornece uma representação visual do status de todas as solicitações ativas e permite que você crie novas solicitações usando o recurso interno **[!UICONTROL Construtor de solicitações]** ou carregando arquivos JSON. Para obter mais informações sobre o uso da interface, consulte a [guia do usuário do Privacy Service](ui/overview.md).

### Monitorar trabalhos de privacidade {#monitor}

Depois de realizar os trabalhos de privacidade, você terá várias opções para monitorar o status e os resultados:

| Método de monitoramento | Descrição |
| --- | --- |
| [!DNL Privacy Service] Interface do usuário | A variável [!DNL Privacy Service] A interface do usuário fornece um painel de monitoramento que permite visualizar uma representação visual do status de todas as solicitações ativas. Consulte a [guia do usuário do Privacy Service](ui/overview.md) para obter mais informações. |
| [!DNL Privacy Service] API | Você pode monitorar programaticamente o status de processos de privacidade usando os pontos de extremidade de pesquisa fornecidos pela [!DNL Privacy Service] API. Consulte a [Guia da API do Privacy Service](./api/overview.md) para obter etapas detalhadas sobre como usar a API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveite os Adobe I/O Events enviados para um webhook configurado para facilitar a automação eficiente da solicitação de trabalho. Elas reduzem ou eliminam a necessidade de pesquisar o [!DNL Privacy Service] para verificar se um trabalho foi concluído ou se uma determinada etapa em um fluxo de trabalho foi atingida. Veja o tutorial sobre [assinatura de eventos de privacidade](./privacy-events.md) para obter mais informações. |

## Próximas etapas

Este documento forneceu uma visão geral de alto nível sobre [!DNL Privacy Service] e as principais etapas necessárias para começar a usar os recursos do serviço. Consulte a documentação ligada a toda a visão geral para obter informações mais detalhadas sobre os vários aspectos do trabalho com o [!DNL Privacy Service].
