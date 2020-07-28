---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 2%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Para oferecer melhores experiências aos clientes, é necessário coletar e armazenar os dados pessoais dos clientes. Ao usar esses dados, é importante entender e respeitar a privacidade dos clientes. As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação.

O Adobe Experience Platform [!DNL Privacy Service] foi desenvolvido em resposta a uma mudança fundamental na forma como as empresas são obrigadas a gerir os dados pessoais dos seus clientes. O objetivo central do é automatizar [!DNL Privacy Service] a conformidade com os regulamentos de privacidade de dados que, quando violados, podem resultar em multas importantes e interromper as operações de dados para sua empresa.

[!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar solicitações de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

## Getting started with [!DNL Privacy Service] {#getting-started}

Para fazer uso do [!DNL Privacy Service], várias decisões importantes precisam ser tomadas em termos de requisitos de privacidade da sua organização, os tipos de dados de identidade coletados de seus clientes e a melhor maneira de interagir com o sistema CRM com o serviço.

Estas decisões podem ser resumidas através das seguintes questões:

1. **Que informações estou coletando de meus clientes?**
   * Para aproveitar ao máximo [!DNL Privacy Service], é necessário conhecer detalhadamente os tipos de dados coletados pelos clientes e quais deles estão sujeitos às regras de privacidade. Consulte a seção sobre como [determinar os requisitos](#requirements) de privacidade para obter mais informações.
1. **Eu rotulei corretamente meus dados?**
   * Os dados devem ser rotulados corretamente para que o serviço determine quais campos devem ser acessados ou excluídos durante trabalhos de privacidade. Consulte a seção sobre dados [de](#label) rotulagem para obter mais informações.
1. **Eu sei para quais IDs enviar[!DNL Privacy Service]?**
   * Ao enviar solicitações de privacidade, é necessário fornecer IDs individuais do cliente específicas para determinados aplicativos de Adobe. Consulte as seções sobre como [fornecer dados](#identity) de identidade e [fazer solicitações](#requests) de privacidade para obter mais informações.
1. **Como estou rastreando meus trabalhos de privacidade?**
   * Depois de fazer solicitações de privacidade, há várias opções para rastrear o status e os resultados. Consulte a seção sobre [monitoramento de trabalhos](#monitor) de privacidade para obter mais informações.

As seções abaixo fornecem orientações gerais sobre essas etapas importantes de pré-requisito e também fornecem links para [!DNL Privacy Service] documentação adicional para obter mais detalhes.

### Determine os requisitos de privacidade de sua organização {#requirements}

Dependendo da natureza de sua empresa e das jurisdições sob as quais ela opera, suas operações de dados podem estar sujeitas a regulamentos legais de privacidade. Esses regulamentos muitas vezes concedem aos clientes o direito de solicitar acesso aos dados coletados e o direito de solicitar a exclusão desses dados armazenados. Essas solicitações do cliente para seus dados pessoais são chamadas de &quot;solicitações de privacidade&quot; em toda a documentação.

A tabela a seguir descreve as regras legais de privacidade que [!DNL Privacy Service] gerenciam solicitações de, incluindo links para a documentação, para obter mais informações:

| regulamento | Descrição |
| --- | --- |
| CCPA (Califórnia) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. A CCPA fornece novos direitos de privacidade de dados aos residentes da Califórnia, incluindo o direito de acessar e excluir seus dados pessoais, saber se seus dados pessoais são vendidos ou divulgados (e a quem) e o direito de opt out a venda de seus dados a terceiros.<br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://oag.ca.gov/privacy/ccpa)</li><li>[Perguntas frequentes sobre CCPA](ccpa/faq.md)</li></ul> |
| RGPD (União Europeia) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. Isso significa que qualquer cidadão da UE cujos dados pessoais tenham sido coletados pela sua empresa pode solicitar acesso ou apagar os dados a qualquer momento. <br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://gdpr-info.eu/)</li><li>[Perguntas frequentes sobre o GDPR](gdpr/faq.md)</li><li>[Terminologia do GDPR](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Tailândia) | A Lei de Proteção de Dados Pessoais da Tailândia (PDPA) foi introduzida para proteger os proprietários de dados tailandeses da coleta, uso ou divulgação ilegais de seus dados pessoais. Inspirado no RGPD da União Europeia, o regulamento concede aos cidadãos tailandeses o direito de solicitarem o acesso ou a supressão dos seus dados pessoais armazenados.<br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Perguntas frequentes sobre PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologia PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Se suas operações de dados forem da competência de qualquer uma das regulamentações acima, consulte sua documentação para obter informações importantes, como os direitos de privacidade específicos que eles oferecem aos seus clientes, e as janelas de conformidade para atender às solicitações de privacidade. Essas informações devem ser levadas em conta ao determinar como se integrar [!DNL Privacy Service] ao seu sistema CRM e como os clientes devem interagir com seu site para fazer solicitações de privacidade.

Além dos regulamentos legais, quaisquer normas organizacionais ou do setor aplicáveis à sua organização também devem ser consideradas ao tomar essas decisões.

### Dados de etiqueta para solicitações de privacidade {#label}

Dependendo dos [!DNL Experience Cloud] aplicativos usados, você deve rotular os campos de dados específicos que devem ser acessados ou excluídos em resposta às solicitações de privacidade. O processo de etiquetagem de dados varia entre os aplicativos. Para saber como rotular dados para cada aplicativo de Adobe suportado, consulte o documento nos aplicativos [de](./experience-cloud-apps.md)Experience Cloud.

### Determine os tipos de dados de identidade para os quais enviar [!DNL Privacy Service] {#identity}

Para [!DNL Privacy Service] processar uma solicitação de privacidade de um cliente, pelo menos um valor de identidade exclusivo para esse cliente deve ser fornecido na própria solicitação. Um valor de identidade exclusivo é qualquer informação que pode ser usada para identificar uma pessoa individual e seus dados pessoais armazenados em seus armazenamentos de [!DNL Experience Cloud] dados. [!DNL Privacy Service] usa essas informações de identidade para localizar e processar os dados pessoais do cliente de acordo com a natureza da solicitação (acesso, exclusão ou recusa).

Dependendo dos [!DNL Experience Cloud] aplicativos que seu sistema CRM utiliza, o tipo e o número de valores de identidade que você deve fornecer para cada cliente variam. Alguns aplicativos utilizam seus próprios valores internos de ID do cliente (como IDs de Adobe Target), enquanto outras soluções dependem de identificadores globais da Adobe [!DNL Experience Cloud Identity Service] (ECID) que rastreiam a atividade do cliente em todos os [!DNL Experience Cloud] aplicativos. Além disso, informações pessoais genéricas, como um endereço de email ou número de telefone, também podem servir como dados de identidade válidos.

O documento sobre dados de [identidade para solicitações](./identity-data.md) de privacidade fornece informações mais detalhadas sobre os tipos de informações de identidade aceitas para [!DNL Privacy Service]. O documento também fornece orientação sobre como aproveitar as tecnologias de Adobe para recuperar efetivamente as informações de identidade apropriadas de seus clientes à medida que interagem com seu site, e enviar esses dados para [!DNL Privacy Service] solicitações de API.

### Start fazendo solicitações de privacidade {#requests}

Depois de determinar as necessidades de privacidade de sua empresa e decidir para quais valores de identidade enviar, você poderá fazer solicitações de privacidade em start. [!DNL Privacy Service] [!DNL Privacy Service] permite enviar solicitações de privacidade por meio da API ou da interface do usuário.

>[!IMPORTANT]
>
>As seções abaixo fornecem links para a documentação que abordam como fazer solicitações de privacidade genéricas na API ou na interface do usuário. No entanto, dependendo dos [!DNL Experience Cloud] aplicativos que você está usando, os campos que você deve enviar na carga da solicitação podem ser diferentes dos exemplos mostrados nesses guias.
>
>Conforme você segue os guias da API ou da interface do usuário, consulte o documento nos aplicativos [de](./experience-cloud-apps.md) Privacy Service e Experience Cloud para obter mais documentação sobre como formatar solicitações de privacidade para seus [!DNL Experience Cloud] aplicativos específicos.

#### Uso da API

O [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) fornece vários endpoints para criar e gerenciar trabalhos de privacidade usando chamadas RESTful API, permitindo que você adote uma abordagem programática da conformidade com a regulamentação de privacidade para seus [!DNL Experience Cloud] aplicativos. Para obter etapas detalhadas sobre como usar a API, consulte o guia [do desenvolvedor da API de](api/getting-started.md)Privacy Service.

#### Uso da interface

>[!NOTE]
>
>Atualmente, a [!DNL Privacy Service] interface de usuário suporta apenas solicitações de acesso e exclusão. Todas as solicitações de não participação devem ser feitas por meio da API.

A [!DNL Privacy Service] interface do usuário permite que você crie e monitore trabalhos de privacidade usando uma interface gráfica. A interface do usuário inclui um widget Relatório **[!UICONTROL de]** status que fornece uma representação visual do status de todas as solicitações ativas e permite que você crie novas solicitações usando o Construtor **[!UICONTROL de]** solicitações integrado ou fazendo upload de arquivos JSON. Para obter mais informações sobre como usar a interface do usuário, consulte o guia [do usuário do](ui/overview.md)Privacy Service.

### Monitorar trabalhos de privacidade {#monitor}

Depois de realizar trabalhos de privacidade, você tem várias opções para monitorar seu status e resultados:

| Método de monitorização | Descrição |
| --- | --- |
| [!DNL Privacy Service] Interface | A [!DNL Privacy Service] interface do usuário fornece um painel de monitoramento que permite que você visualização uma representação visual do status de todas as solicitações ativas. Consulte o guia [do usuário do](ui/overview.md) Privacy Service para obter mais informações. |
| [!DNL Privacy Service] API | Você pode monitorar programaticamente o status dos trabalhos de Privacidade usando os pontos de extremidade de pesquisa fornecidos pela [!DNL Privacy Service] API. Consulte o guia [do desenvolvedor do](./api/getting-started.md) Privacy Service para obter as etapas detalhadas sobre como usar a API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] aproveite Eventos de E/S de Adobe enviados para um webhook configurado, a fim de facilitar a automação eficiente das solicitações de trabalho. Eles reduzem ou eliminam a necessidade de pesquisar a [!DNL Privacy Service] API para verificar se um trabalho foi concluído ou se um determinado marco em um fluxo de trabalho foi atingido. Consulte o tutorial sobre como [assinar Eventos](./privacy-events.md) de privacidade para obter mais informações. |

## Próximas etapas

Este documento fornece uma visão geral de alto nível sobre [!DNL Privacy Service] os principais passos necessários para o start usando os recursos do serviço. Consulte a documentação relacionada ao longo de toda a visão geral para obter informações mais aprofundadas sobre os vários aspectos do trabalho com [!DNL Privacy Service].
