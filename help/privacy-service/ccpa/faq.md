---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Perguntas frequentes sobre CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Perguntas frequentes sobre CCPA

Este documento fornece respostas para perguntas frequentes sobre a CCPA [!DNL California Consumer Protection Act] (CCPA) e sua implementação na Adobe Experience Cloud.

## O que é CCPA?

A [!DNL California Consumer Privacy Act] (CCPA) é a nova lei de privacidade da Califórnia que confere aos seus residentes novos direitos em relação às suas informações pessoais, e impõe responsabilidades de proteção de dados a determinadas entidades que fazem negócios na Califórnia.

>[!NOTE]
>
>Embora tecnicamente em vigor em Janeiro de 2020, a CCPA ainda está a ser aperfeiçoada pelos legisladores. Além disso, são apresentados detalhes importantes sobre a implementação e outras orientações nas regras que ainda não foram elaboradas pelo regulador da Califórnia.

Embora a CCPA partilhe de alguns conceitos fornecidos ao abrigo do Regulamento Geral sobre a Proteção de Dados das Uniões Europeias (RGPD), como o direito de acesso e apagamento de informações pessoais, existem várias formas principais de a CCPA diferir do RGPD. Por exemplo, a CCPA fornece aos consumidores um direito de opção de não participação de determinadas atividades de compartilhamento de dados que qualificam como &quot;venda&quot; de informações pessoais a terceiros, em vez de exigir o consentimento prévio.

## Qual é a definição de informações pessoais no âmbito da CCPA?

A informação pessoal é a informação que &quot;identifica, relaciona, descreve, é susceptível de ser associada a, ou pode razoavelmente estar ligada, direta ou indiretamente, a um consumidor ou a um agregado familiar&quot;.

## Quais tipos de informações pessoais ou identificadores usados na Adobe Experience Cloud estão sujeitos a esses novos requisitos?

Os seguintes identificadores são comumente usados em [!DNL Experience Cloud] aplicativos e podem estar sujeitos aos requisitos do CCPA:

- Nome
- Endereço postal
- Identificador pessoal exclusivo
- Identificador online
- Endereço IP
- Endereço de email
- Nome da conta

As informações pessoais também podem incluir a Internet ou outras informações de atividade da rede eletrônica. Isso inclui, mas não se limita a:

- Histórico de navegação
- Histórico de pesquisa
- Informações relacionadas à interação do consumidor com um site, aplicativo ou anúncio

Embora o CCPA cubra um grande conjunto de informações pessoais, os termos padrão do contrato da Adobe determinam que informações pessoais confidenciais (como SSN, informações sobre a licença do motorista, informações sobre a conta financeira e dados biométricos) sejam geralmente proibidas de importar e usar em [!DNL Experience Cloud] aplicativos.

## Como se aplicam as diferentes funções e responsabilidades da CCPA [!DNL Experience Cloud]?

Conforme definido pelo CCPA, as seguintes funções se aplicam à Adobe e a seus clientes:

- Os clientes da Adobe (a parte que solicita a coleta e o uso de informações pessoais de residentes na Califórnia) seriam considerados uma **Empresa**.
- A Adobe, na sua função de fornecer o serviço, seria considerada um **Provedor de serviço**.

Dado esse relacionamento e a linguagem de contrato da Adobe, as divulgações à Adobe provavelmente não seriam consideradas uma &quot;venda&quot; para a qual as empresas precisariam fornecer um aviso e oferta de uma opção de não participação.

No entanto, os serviços da Adobe podem ser usados para permitir o compartilhamento de determinados dados e transferências para terceiros. Estas transferências de terceiros podem ser consideradas uma &quot;venda&quot; e exigem legalmente a divulgação e a não participação.  Os clientes devem trabalhar com seus consultores jurídicos para avaliar casos de uso específicos, a fim de avaliar os requisitos aplicáveis.

## Quantos dias uma empresa tem que responder a uma solicitação do consumidor para acessar ou excluir informações pessoais?

Supondo que a empresa tenha coletado informações pessoais e que possa autenticar ou verificar a identidade de um consumidor californiano específico, a CCPA permite que as solicitações do consumidor sejam atendidas dentro de 45 dias (com algumas exceções).

## Qual é a função da Adobe no CCPA?

Como um Provedor de serviço, a Adobe coleta e processa informações pessoais em nome da Empresa e está contratualmente obrigada a usar essas informações apenas para os fins específicos estabelecidos no contrato.

Considerando esse relacionamento e a linguagem de contrato da Adobe, as divulgações à Adobe se enquadram nas disposições da lei para Provedores de serviço, e provavelmente não seriam consideradas uma &quot;venda&quot; para a qual as empresas precisariam fornecer aviso e oferta e uma opção de não participação.

Os serviços da Adobe podem ser usados para permitir o compartilhamento de determinados dados e transferências para terceiros. Estas transferências de terceiros podem ser consideradas uma &quot;venda&quot; e exigem legalmente a divulgação e a não participação.  Os clientes devem trabalhar com seus consultores jurídicos para avaliar casos de uso específicos, a fim de avaliar os requisitos aplicáveis.

## Como posso suportar os requisitos de privacidade do consumidor na CCPA se eu mantiver certos tipos de dados que são cobertos pelos requisitos?

Depois que você tiver tomado as etapas necessárias para autenticar os consumidores da CA, o Adobe Experience Platform [!DNL Privacy Service] permitirá que você envie solicitações de privacidade do consumidor para [!DNL Experience Cloud] aplicativos compatíveis. Consulte a visão geral [do](../home.md) Privacy Service para obter mais informações. Para obter informações sobre como seus aplicativos específicos podem atender às solicitações de privacidade, consulte o guia sobre aplicativos [!DNL Experience Cloud] Privacy Service e Experience Cloud [](../experience-cloud-apps.md).

>[!NOTE]
>
>Ainda há outras orientações da autoridade reguladora da Califórnia sobre quais tipos de dados são elegíveis para solicitações de privacidade do consumidor.

## A Adobe oferta outras ferramentas que podem ser úteis para atender aos requisitos de CCPA?

Os aplicativos da Adobe Experience Cloud oferecem funções de gestão de dados e controle que podem ser úteis para as necessidades de privacidade da empresa. Entre essas ferramentas estão a rotulagem de uso de dados, controles de acesso baseados em funções, ofuscação de IP e recursos de hash.

A Adobe recebeu várias certificações de suas práticas de privacidade e segurança, como uma certificação ISO 27001 e uma validação TrustArc GDPR.