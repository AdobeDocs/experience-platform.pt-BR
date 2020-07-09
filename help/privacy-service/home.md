---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Visão geral do Adobe Experience Platform Privacy Service

Para oferecer melhores experiências aos clientes, é necessário coletar e armazenar os dados pessoais dos clientes. Ao usar esses dados, é importante entender e respeitar a privacidade dos clientes. As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação.

A Adobe Experience Platform Privacy Service foi desenvolvida em resposta a uma mudança fundamental na forma como as empresas são obrigadas a gerir os dados pessoais dos seus clientes. O objetivo central do Privacy Service é automatizar a conformidade com as regulamentações de privacidade de dados que, quando violadas, podem resultar em multas importantes e interromper as operações de dados para sua empresa.

O Privacy Service fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar as solicitações de dados do cliente. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais do cliente dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

## Introdução ao Privacy Service {#getting-started}

Para usar o Privacy Service, várias decisões importantes precisam ser tomadas em termos de requisitos de privacidade da sua organização, os tipos de dados de identidade coletados dos seus clientes e a melhor maneira de interligar seu sistema CRM com o serviço.

Estas decisões podem ser resumidas através das seguintes questões:

1. **Que informações estou coletando de meus clientes?**
   * Para usar o Privacy Service da melhor forma, é necessário conhecer detalhadamente os tipos de dados coletados pelos clientes e quais deles estão sujeitos às regras de privacidade. Consulte a seção sobre como [determinar os requisitos](#requirements) de privacidade para obter mais informações.
1. **Eu rotulei corretamente meus dados?**
   * Os dados devem ser rotulados corretamente para que o serviço determine quais campos devem ser acessados ou excluídos durante trabalhos de privacidade. Consulte a seção sobre dados [de](#label) rotulagem para obter mais informações.
1. **Eu sei quais IDs enviar para a Privacy Service?**
   * Ao enviar solicitações de privacidade, as IDs individuais do cliente específicas para determinados aplicativos da Adobe devem ser fornecidas. Consulte as seções sobre como [fornecer dados](#identity) de identidade e [fazer solicitações](#requests) de privacidade para obter mais informações.
1. **Como estou rastreando meus trabalhos de privacidade?**
   * Depois de fazer solicitações de privacidade, há várias opções para rastrear o status e os resultados. Consulte a seção sobre [monitoramento de trabalhos](#monitor) de privacidade para obter mais informações.

As seções abaixo fornecem orientações gerais sobre essas etapas importantes de pré-requisito e também fornecem links para a documentação adicional do Privacy Service para obter mais detalhes.

### Determine os requisitos de privacidade de sua organização {#requirements}

Dependendo da natureza de sua empresa e das jurisdições sob as quais ela opera, suas operações de dados podem estar sujeitas a regulamentos legais de privacidade. Esses regulamentos muitas vezes concedem aos clientes o direito de solicitar acesso aos dados coletados e o direito de solicitar a exclusão desses dados armazenados. Essas solicitações do cliente para seus dados pessoais são chamadas de &quot;solicitações de privacidade&quot; em toda a documentação.

A tabela a seguir descreve as regras legais de privacidade que a Privacy Service gerencia solicitações, incluindo links para a documentação para obter mais informações:

| regulamento | Descrição |
| --- | --- |
| CCPA (Califórnia) | A Lei de Privacidade do Consumidor da Califórnia (California Consumer Privacy Act, ou CCPA) aprimora os direitos de privacidade e a proteção do consumidor para os moradores da Califórnia, nos Estados Unidos. A CCPA fornece novos direitos de privacidade de dados aos residentes da Califórnia, incluindo o direito de acessar e excluir seus dados pessoais, saber se seus dados pessoais são vendidos ou divulgados (e a quem) e o direito de opt out a venda de seus dados a terceiros.<br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://oag.ca.gov/privacy/ccpa)</li><li>[Perguntas frequentes sobre CCPA](ccpa/faq.md)</li></ul> |
| RGPD (União Europeia) | O Regulamento Geral sobre a Proteção de Dados (GDPR) introduziu vários novos direitos de privacidade de dados para os membros da União Europeia, incluindo o **Direito de acesso** e o **Direito de ser esquecido**. Isso significa que qualquer cidadão da UE cujos dados pessoais tenham sido coletados pela sua empresa pode solicitar acesso ou apagar os dados a qualquer momento. <br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://gdpr-info.eu/)</li><li>[Perguntas frequentes sobre o GDPR](gdpr/faq.md)</li><li>[Terminologia do GDPR](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Tailândia) | A Lei de Proteção de Dados Pessoais da Tailândia (PDPA) foi introduzida para proteger os proprietários de dados tailandeses da coleta, uso ou divulgação ilegais de seus dados pessoais. Inspirado no RGPD da União Europeia, o regulamento concede aos cidadãos tailandeses o direito de solicitarem o acesso ou a supressão dos seus dados pessoais armazenados.<br/><br/>Links para documentação adicional: <ul><li>[Visão geral jurídica](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Perguntas frequentes sobre PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologia PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Se suas operações de dados forem da competência de qualquer uma das regulamentações acima, consulte sua documentação para obter informações importantes, como os direitos de privacidade específicos que eles oferecem aos seus clientes, e as janelas de conformidade para atender às solicitações de privacidade. Essas informações devem ser levadas em conta ao determinar como integrar o Privacy Service ao seu sistema CRM e como os clientes devem interagir com seu site para fazer solicitações de privacidade.

Além dos regulamentos legais, quaisquer normas organizacionais ou do setor aplicáveis à sua organização também devem ser consideradas ao tomar essas decisões.

### Dados de etiqueta para solicitações de privacidade {#label}

Dependendo dos aplicativos de Experience Cloud que você estiver usando, você deve rotular os campos de dados específicos que devem ser acessados ou excluídos em resposta às solicitações de privacidade. O processo de etiquetagem de dados varia entre os aplicativos. Para saber como rotular os dados para cada aplicativo da Adobe suportado, consulte o documento nos aplicativos [do](./experience-cloud-apps.md)Experience Cloud.

### Determine os tipos de dados de identidade a serem enviados para o Privacy Service {#identity}

Para que o Privacy Service processe uma solicitação de privacidade de um cliente, pelo menos um valor de identidade exclusivo para esse cliente deve ser fornecido na própria solicitação. Um valor de identidade exclusivo é qualquer informação que pode ser usada para identificar uma pessoa individual e seus dados pessoais armazenados em seus armazenamentos de dados de Experience Cloud. O Privacy Service usa essas informações de identidade para localizar e processar os dados pessoais do cliente de acordo com a natureza da solicitação (acesso, exclusão ou não).

Dependendo dos aplicativos de Experience Cloud que seu sistema CRM utiliza, o tipo e o número de valores de identidade que você deve fornecer para cada cliente variam. Alguns aplicativos utilizam seus próprios valores internos de ID do cliente (como Adobe Target IDs), enquanto outras soluções dependem de identificadores globais do Adobe Experience Cloud Identity Service (ECID) que rastreiam a atividade do cliente em todos os aplicativos Experience Cloud. Além disso, informações pessoais genéricas, como um endereço de email ou número de telefone, também podem servir como dados de identidade válidos.

O documento sobre dados de [identidade para solicitações](./identity-data.md) de privacidade fornece informações mais detalhadas sobre os tipos de informações de identidade aceitas para o Privacy Service. O documento também fornece orientação sobre como aproveitar as tecnologias da Adobe para recuperar com eficácia as informações de identidade apropriadas de seus clientes à medida que interagem com seu site, e enviar esses dados para solicitações de API do Privacy Service.

### Start fazendo solicitações de privacidade {#requests}

Depois de determinar as necessidades de privacidade de sua empresa e decidir quais valores de identidade enviar para o Privacy Service, você poderá fazer solicitações de privacidade do start. O Privacy Service permite enviar solicitações de privacidade por meio da API ou da interface do usuário.

>[!IMPORTANT]
>
>As seções abaixo fornecem links para a documentação que abordam como fazer solicitações de privacidade genéricas na API ou na interface do usuário. No entanto, dependendo dos aplicativos de Experience Cloud que você estiver usando, os campos que devem ser enviados na carga da solicitação podem ser diferentes dos exemplos mostrados nesses guias.
>
>Conforme você segue os guias da API ou da interface do usuário, consulte o documento nos aplicativos [de](./experience-cloud-apps.md) Privacy Service e Experience Cloud para obter mais documentação sobre como formatar solicitações de privacidade para seus aplicativos Experience Cloud.

#### Uso da API

A API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service fornece vários pontos de extremidade para criar e gerenciar trabalhos de privacidade usando chamadas RESTful API, permitindo que você adote uma abordagem programática da conformidade com a regulamentação de privacidade para seus aplicativos Experience Cloud. Para obter etapas detalhadas sobre como usar a API, consulte o guia [do desenvolvedor da API de](api/getting-started.md)Privacy Service.

#### Uso da interface

>[!NOTE]
>
>Atualmente, a interface do usuário do Privacy Service suporta apenas solicitações de acesso e exclusão. Todas as solicitações de não participação devem ser feitas por meio da API.

A interface do usuário do Privacy Service permite que você crie e monitore trabalhos de privacidade usando uma interface gráfica. A interface do usuário inclui um widget Relatório **de** status que fornece uma representação visual do status de todas as solicitações ativas e permite que você crie novas solicitações usando o Construtor **de** solicitações integrado ou fazendo upload de arquivos JSON. Para obter mais informações sobre como usar a interface do usuário, consulte o guia [do usuário do](ui/overview.md)Privacy Service.

### Monitorar trabalhos de privacidade {#monitor}

Depois de realizar trabalhos de privacidade, você tem várias opções para monitorar seu status e resultados:

| Método de monitorização | Descrição |
| --- | --- |
| UI Privacy Service | A interface do usuário do Privacy Service fornece um painel de monitoramento que permite que você visualização uma representação visual do status de todas as solicitações ativas. Consulte o guia [do usuário do](ui/overview.md) Privacy Service para obter mais informações. |
| API Privacy Service | Você pode monitorar programaticamente o status dos trabalhos de Privacidade usando os pontos de extremidade de pesquisa fornecidos pela API do Privacy Service. Consulte o guia [do desenvolvedor do](./api/getting-started.md) Privacy Service para obter as etapas detalhadas sobre como usar a API. |
| Eventos de privacidade | Os Eventos de privacidade aproveitam Eventos de E/S da Adobe enviados para um webhook configurado, a fim de facilitar a automação eficiente das solicitações de trabalho. Eles reduzem ou eliminam a necessidade de pesquisar a API Privacy Service para verificar se um trabalho foi concluído ou se um determinado marco em um fluxo de trabalho foi atingido. Consulte o tutorial sobre como [assinar Eventos](./privacy-events.md) de privacidade para obter mais informações. |

## Próximas etapas

Este documento fornece uma visão geral de alto nível do Privacy Service e as principais etapas necessárias para o start usando os recursos do serviço. Consulte a documentação relacionada à visão geral para obter informações mais aprofundadas sobre os vários aspectos do trabalho com o Privacy Service.
