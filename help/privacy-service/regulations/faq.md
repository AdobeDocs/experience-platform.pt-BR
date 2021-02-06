---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;Regulation;Regulations;Regulations;privacy;Privacy;
solution: Experience Platform
title: Perguntas frequentes sobre os regulamentos de privacidade
topic: troubleshooting
description: Este documento fornece respostas para perguntas frequentes sobre regulamentos de privacidade legais suportados e sua implementação no Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---


# Perguntas frequentes sobre regulamentações de privacidade

Este documento fornece respostas para perguntas frequentes sobre regulamentos de privacidade legais suportados e sua implementação no Adobe Experience Cloud.

>[!NOTE]
>
>As definições para os vários termos usados neste documento podem ser encontradas no guia [terminologia do regulamento de privacidade](terminology.md).

## Questões gerais

As perguntas a seguir estão relacionadas a todas as regulamentações de privacidade suportadas pelo Experience Cloud.

### Quem as regras de privacidade suportadas afetam?

As [regras de privacidade suportadas pelo Experience Cloud](./overview.md) aplicam-se a todas as organizações que armazenam e processam os dados pessoais dos cidadãos dentro das respectivas jurisdições, independentemente da localização geográfica da organização.

### O que constitui dados pessoais?

Dados pessoais, qualquer informação relativa a uma pessoa singular ou a uma pessoa em causa que possa ser utilizada para identificar direta ou indiretamente essa pessoa. Pode ser qualquer coisa de um nome, uma foto, um endereço de email, detalhes bancários, postagens em sites de redes sociais, informações médicas ou um endereço IP do computador.

Os seguintes identificadores são comumente usados em aplicativos Experience Cloud e podem estar sujeitos aos requisitos de regulamentação de privacidade:

* Nome
* Endereço postal
* Identificador pessoal exclusivo
* Identificador online
* Endereço IP
* Endereço de email
* Nome da conta

As informações pessoais também podem incluir a Internet ou outras informações de atividade da rede eletrônica. Isso inclui, mas não se limita a:

* Histórico de navegação
* Histórico de pesquisa
* Informações relacionadas à interação do consumidor com um site, aplicativo ou anúncio

Embora as regras de privacidade abranjam um grande conjunto de informações pessoais, os termos padrão do contrato do Adobe ditam que informações pessoais confidenciais (como SSN, informações de licença do motorista, informações de conta financeira e dados biométricos) são geralmente proibidas de serem importadas e usadas em aplicativos Experience Cloud.

### Qual é a diferença entre um controlador de dados e um processador de dados?

Um **controlador de dados** é a entidade que determina os fins, as condições e os meios de processamento de dados pessoais, enquanto o **processador de dados** é uma entidade que processa dados pessoais em nome do controlador de dados.

Um **controlador de dados** é a pessoa ou organização que tem o poder e a responsabilidade de tomar decisões relacionadas à coleta, uso ou divulgação de dados pessoais. Um **processador de dados** é a pessoa ou organização que opera em relação à coleta, uso ou divulgação dos dados pessoais e a direção do controlador de dados.

### Qual é a diferença entre o consentimento explícito e inequívoco da pessoa em causa?

**Consentimento expresso** refere-se a uma norma de consentimento que envolve uma indicação específica, informada e inequívoca dos desejos da pessoa em causa, sob forma oral ou escrita. Em termos simples, a pessoa em causa tem de dizer, literalmente e explicitamente, &quot;Eu consentimento&quot; ou &quot;Eu concordo&quot; para que o consentimento seja considerado explícito. Além disso, deve ser tão fácil retirar o consentimento como é dar-lhe.

**Consentimento inequívoco (implícito)** refere-se ao consentimento que não foi explicitamente dado pela pessoa em causa, mas que é de natureza inequívoca. Por exemplo, durante o processo de inscrição em um site de empresa, é dado um aviso de que, ao fornecer um endereço de email, a pessoa de dados consente em receber emails em ofertas especiais. Se a pessoa em causa ler a notificação, a ação afirmativa de inserir seu email é suficiente para ser considerada um consentimento inequívoco.

Para muitos regulamentos, como o RGPD, é necessário consentimento explícito para o processamento de dados pessoais sensíveis, onde nada menos do que &quot;opt in&quot; será suficiente. No entanto, para dados não sensíveis, é aceitável um consentimento inequívoco (implícito).

### As pessoas com menos de uma certa idade podem dar consentimento?

Muitas regulamentações de privacidade estipulam que, se uma pessoa de dados tiver menos de uma certa idade, não poderá legalmente dar consentimento para a coleta de seus dados pessoais. Alguns regulamentos permitem que, nestes casos, o titular da responsabilidade parental relativamente a essa pessoa de dados, mas não todos. O quadro seguinte lista a idade mínima para que as pessoas em causa possam dar o seu próprio consentimento a cada regulamento, com notas para mais informações:

| regulamento | Idade do consentimento | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 16 | <ul><li>O consentimento parental só pode ser dado a pessoas com 13 anos ou mais de idade.</li><li>A recolha de dados pessoais de pessoas com menos de 13 anos é estritamente proibida.</li></ul> |
| RGPD (União Europeia) | 16 | <ul><li>Alguns Estados-Membros da UE podem prever uma lei para uma idade inferior, mas não inferior a 13 anos.</li><li>Deve ser dado consentimento parental a todas as pessoas com menos de idade.</li></ul> |
| LGPD (Brasil) | 13 | <ul><li>Deve ser dado consentimento parental a todas as pessoas com menos de idade.</li><li>O consentimento pode ser dado por uma pessoa singular de 13 a 18 anos, desde que o tratamento dos seus dados pessoais seja efetuado no seu interesse.</li></ul> |
| PDPA (Tailândia) | 10 | <ul><li>Deve ser dado consentimento parental a todas as pessoas com menos de idade.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Quantos dias uma empresa tem que responder a uma solicitação do consumidor para acessar ou excluir informações pessoais?

Supondo que a empresa tenha coletado informações pessoais e que possa autenticar ou verificar a identidade de um consumidor específico, as regras de privacidade permitem um período específico para que uma solicitação do consumidor seja atendida. O quadro seguinte apresenta os períodos de tempo aplicáveis a cada regulamento, com algumas notas sobre algumas exceções:

| regulamento | Janela de conformidade | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 45 dias |  |
| RGPD (União Europeia) | 30 dias | Se a solicitação for complexa ou várias solicitações tiverem sido feitas pela mesma pessoa de dados, a solicitação poderá ser estendida para 60 dias. |
| LGPD (Brasil) | 15 dias |  |
| PDPA (Tailândia) | 30 dias | Se uma empresa não puder responder à solicitação de uma pessoa de dados dentro da janela de conformidade, ela terá mais 30 dias a partir da data em que não pôde atender à solicitação para responder por escrito à pessoa de dados. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Minha empresa precisa nomear um oficial de proteção de dados?

Se as operações de dados da sua organização forem da competência legal do RGPD, LGPD ou PDPA, você deverá nomear um responsável pela proteção de dados (DPO) nos seguintes casos:

* Sua organização é uma autoridade pública
* Sua organização se envolve em monitoramento sistemático em grande escala
* Sua organização trabalha com processamento em grande escala de dados pessoais confidenciais.

>[!IMPORTANT]
>
>Ao contrário de outros regulamentos, a CCPA estimula isso como um requisito. No entanto, geralmente é recomendável que, para manter a conformidade com a privacidade, uma empresa tenha atividades qualificadas de coleta de dados de monitoramento individual e o armazenamento de dados do consumidor, além de responder a consultas do cliente.

### Como posso dar suporte a solicitações de privacidade do consumidor se mantiver dados cobertos por regulamentos de privacidade?

Depois que você tiver tomado as medidas necessárias para autenticar os consumidores que se enquadram nas jurisdições legais apropriadas, a Adobe Experience Platform Privacy Service permitirá que você envie solicitações de privacidade do consumidor para aplicativos Experience Cloud compatíveis. Consulte a [[!DNL Privacy Service] visão geral](../home.md) para obter mais informações. Para obter informações sobre como seus aplicativos Experience Cloud específicos podem atender às solicitações de privacidade, consulte o guia em [aplicativos Privacy Service e Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Ainda há outras orientações da autoridade reguladora da Califórnia sobre quais tipos de dados são elegíveis para solicitações de privacidade do consumidor.

## Perguntas sobre CCPA

As perguntas que se seguem dizem especificamente respeito à CCPA.

### Como as diferentes funções e responsabilidades do CCPA se aplicam ao Experience Cloud?

Conforme definido pelo CCPA, as seguintes funções se aplicam ao Adobe e seus clientes:

* Os clientes do Adobe (a parte que solicita a coleta e o uso de informações pessoais de residentes na Califórnia) seriam considerados **Business**.
* O Adobe, na sua função de fornecer o serviço, seria considerado um **Provedor de serviço**.

Como Provedor de serviço, a Adobe coleta e processa informações pessoais em nome da Empresa e está contratualmente obrigada a usá-las apenas para os fins específicos estabelecidos no acordo.

Tendo em conta esta relação e a linguagem do contrato de Adobe, as divulgações à Adobe provavelmente não seriam consideradas uma &quot;venda&quot; para a qual as empresas teriam de fornecer um aviso e solicitar o consentimento.

No entanto, os serviços de Adobe podem ser utilizados para permitir o compartilhamento de determinados dados e transferências para terceiros. Estas transferências de terceiros podem ser consideradas uma &quot;venda&quot; e exigem legalmente a divulgação e o consentimento. Os clientes devem trabalhar com seus consultores jurídicos para avaliar casos de uso específicos, a fim de avaliar os requisitos aplicáveis.

### A Adobe oferta  outras ferramentas que podem ser úteis para atender aos requisitos do CCPA?

Os aplicativos Adobe Experience Cloud oferecem funções de gestão de dados e controle que podem ser úteis para as necessidades de privacidade das empresas. Entre essas ferramentas estão a rotulagem de uso de dados, controles de acesso baseados em funções, ofuscação de IP e recursos de hash.

A Adobe recebeu várias certificações de suas práticas de privacidade e segurança, como uma certificação ISO 27001 e uma validação TrustArc GDPR.

## Perguntas sobre o RGPD

As questões que se seguem dizem especificamente respeito ao RGPD.

### Qual é a diferença entre um regulamento e uma diretiva?

Um **regulamento** é um ato legislativo vinculativo e deve ser aplicado na sua totalidade em toda a UE. Uma **diretiva** é um ato legislativo que estabelece um objetivo que todos os países da UE devem atingir, mas cabe a cada um deles decidir como.

É importante notar que o RGPD é um regulamento, em contraste com a legislação anterior (a Diretiva Proteção de Dados), que é uma diretiva.

### Como o RGPD afeta as políticas relacionadas às violações de dados?

A regulamentação proposta relativa às violações de dados relaciona-se principalmente com as políticas de notificação de empresas que foram violadas. As violações de dados que possam constituir um risco para as pessoas devem ser notificadas à autoridade de proteção de dados no prazo de 72 horas e às pessoas afetadas sem demora injustificada.

## Perguntas sobre PDPA

As perguntas a seguir estão relacionadas especificamente ao PDPA.

### O que constitui dados pessoais sensíveis?

O PDPA prevê requisitos rigorosos para a recolha e armazenamento de dados pessoais sensíveis, que incluem dados pessoais relativos a: origens racial ou étnica, opiniões políticas, crenças religiosas ou filosóficas, registros criminais, associações de uniões comerciais, dados genéticos, dados biométricos, registros de saúde e orientação ou preferências sexuais.