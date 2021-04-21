---
keywords: Experience Platform; home; tópicos populares; GDPR; Gdpr; CCPA; ccpa; PDPA; pdpa; LGPD; lgpd; faq; perguntas frequentes; regulamento; regulamentos; regulamentos; privacidade; Privacidade;
solution: Experience Platform
title: Perguntas frequentes sobre regulamentos de privacidade
topic-legacy: troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre regulamentos de privacidade legais suportados e sua implementação no Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Perguntas frequentes sobre regras de privacidade

Este documento fornece respostas a perguntas frequentes sobre regulamentos de privacidade legais suportados e sua implementação no Adobe Experience Cloud.

>[!NOTE]
>
>As definições para os vários termos usados neste documento podem ser encontradas no guia [privacy regulation terminology](terminology.md).

## Questões gerais

As perguntas a seguir estão relacionadas a todas as regras de privacidade suportadas pelo Experience Cloud.

### Com quem as regras de privacidade aceitas afetam?

As [regras de privacidade apoiadas pelo Experience Cloud](./overview.md) aplicam-se a todas as organizações que armazenam e processam os dados pessoais dos cidadãos dentro das respectivas jurisdições, independentemente da localização geográfica da organização.

### O que constitui dados pessoais?

Dados pessoais: qualquer informação relacionada a uma pessoa singular ou a um titular de dados que possa ser usada para identificar direta ou indiretamente tal pessoa. Pode ser qualquer coisa de um nome, uma foto, um endereço de email, detalhes bancários, postagens em sites de redes sociais, informações médicas ou um endereço IP de computador.

Os seguintes identificadores são comumente usados em aplicativos Experience Cloud e podem estar sujeitos aos requisitos de regulamentação de privacidade:

* Nome
* Endereço postal
* Identificador pessoal exclusivo
* Identificador online
* Endereço IP
* Endereço de email
* Nome da conta

As informações pessoais também podem incluir a Internet ou outras informações sobre atividades da rede eletrônica. Isso inclui, mas não se limita a:

* Histórico de navegação
* Histórico de pesquisa
* Informações sobre a interação do consumidor com um site, aplicativo ou anúncio

Embora as regras de privacidade abranjam um amplo conjunto de informações pessoais, os termos padrão do contrato do Adobe exigem que as informações pessoais confidenciais (como SSN, informações de licença do motorista, informações da conta financeira e dados biométricos) sejam geralmente proibidas de importar e usar em aplicativos de Experience Cloud.

### Qual é a diferença entre um controlador de dados e um processador de dados?

Um **controlador de dados** é a entidade que determina as finalidades, condições e meios de processamento de dados pessoais, enquanto o **processador de dados** é uma entidade que processa dados pessoais em nome do controlador de dados.

Um **controlador de dados** é a pessoa ou organização que tem o poder e a responsabilidade de tomar decisões relacionadas à coleta, utilização ou divulgação de dados pessoais. Um **processador de dados** é a pessoa ou organização que opera em relação à coleta, uso ou divulgação dos dados pessoais e a direção do controlador de dados.

### Qual é a diferença entre consentimento explícito e inequívoco do titular dos dados?

**Consentimento explícito** refere-se a um padrão de consentimento que envolve uma indicação específica, informada e inequívoca dos desejos da pessoa em causa, sob forma oral ou escrita. Em termos simples, o titular dos dados deve dizer literalmente e explicitamente &quot;Eu consentimento&quot; ou &quot;Eu concordo&quot; para que o consentimento seja considerado explícito. Além disso, deve ser tão fácil retirar o consentimento como é dar-lhe.

**O** consentimento inequívoco (implícito) refere-se ao consentimento que não foi explicitamente dado pelo titular dos dados, mas que é de natureza inequívoca. Por exemplo, durante o processo de inscrição de um site da empresa, é dado um aviso de que, ao fornecer um endereço de email, o titular dos dados consentiu em receber emails em ofertas especiais. Se o titular dos dados ler o aviso, a ação afirmativa de inserir seu email é suficiente para ser considerada um consentimento inequívoco.

Para muitos regulamentos, como o GDPR, é necessário consentimento explícito para o processamento de dados pessoais confidenciais, onde nada menos que &quot;opt in&quot; será suficiente. No entanto, para dados não confidenciais, o consentimento inequívoco (implícito) é aceitável.

### Os titulares de dados com menos de uma certa idade podem consentir?

Muitas regulamentações de privacidade estipulam que, se um titular de dados tiver menos de uma certa idade, ele não poderá legalmente consentir com a coleta de seus dados pessoais. Alguns regulamentos permitem que, nestes casos, o titular da responsabilidade parental, mas não todos, dê o seu consentimento à pessoa em causa. A tabela a seguir apresenta a idade mínima para as pessoas em causa darem o seu próprio consentimento a cada regulamento, com notas para mais informações:

| Regulamento | Idade do consentimento | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 16 | <ul><li>O consentimento parental só pode ser fornecido para titulares de dados com idade igual ou superior a 13 anos.</li><li>É estritamente proibida a recolha de dados pessoais de pessoas com menos de 13 anos.</li></ul> |
| GDPR (União Europeia) | 16º | <ul><li>Alguns Estados-Membros da UE podem prever uma lei para uma idade inferior para este efeito, mas não inferior a 13 anos.</li><li>Deve ser dado consentimento parental a todos os titulares de dados com idade inferior ao limite.</li></ul> |
| LGPD (Brasil) | 13º | <ul><li>Deve ser dado consentimento parental a todos os titulares de dados com idade inferior ao limite.</li><li>O consentimento pode ser dado por uma pessoa singular de 13 a 18 anos, desde que o tratamento dos seus dados pessoais seja efetuado no seu interesse superior.</li></ul> |
| PDPA (Tailândia) | 10 | <ul><li>Deve ser dado consentimento parental a todos os titulares de dados com idade inferior ao limite.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Quantos dias uma empresa precisa responder a uma solicitação do consumidor para acessar ou excluir informações pessoais?

Supondo que a empresa tenha coletado informações pessoais e que possa autenticar ou verificar a identidade de um determinado consumidor, as regras de privacidade permitem que um período específico seja atendido por uma solicitação do consumidor. O quadro seguinte discrimina os períodos de tempo aplicáveis a cada regulamento, com notas sobre algumas exceções:

| Regulamento | Janela de conformidade | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 45 dias |  |
| GDPR (União Europeia) | 30 dias | Se a solicitação for complexa ou várias solicitações tiverem sido feitas pelo mesmo titular de dados, a solicitação poderá ser estendida para 60 dias. |
| LGPD (Brasil) | 15 dias |  |
| PDPA (Tailândia) | 30 dias | Se uma empresa não puder responder à solicitação de um titular de dados dentro da janela de conformidade, a empresa terá mais 30 dias a partir da data em que não pôde atender à solicitação para responder por escrito ao titular dos dados. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Minha empresa precisa nomear um oficial de proteção de dados?

Se as operações de dados da sua organização estiverem sob as jurisdições legais do GDPR, LGPD ou PDPA, você deverá nomear um responsável pela proteção de dados (DPO) nos seguintes casos:

* Sua organização é uma autoridade pública
* Sua organização realiza um monitoramento sistemático em grande escala
* Sua organização realiza um processamento em grande escala de dados pessoais confidenciais.

>[!IMPORTANT]
>
>Ao contrário de outros regulamentos, a CCPA estipula isso como um requisito. No entanto, é recomendável que, para manter a conformidade com a privacidade, uma empresa tenha atividades qualificadas de monitoramento individual de coleta de dados e armazenamento de dados do consumidor, além de responder a consultas do cliente.

### Como posso oferecer suporte às solicitações de privacidade do consumidor se mantiver dados cobertos pelas regras de privacidade?

Depois de tomar as medidas necessárias para autenticar consumidores que estejam nas jurisdições legais apropriadas, o Adobe Experience Platform Privacy Service permite enviar solicitações de privacidade do consumidor para aplicativos Experience Cloud compatíveis. Consulte a [[!DNL Privacy Service] visão geral](../home.md) para obter mais informações. Para obter informações sobre como seus aplicativos Experience Cloud específicos podem atender às solicitações de privacidade, consulte o guia em [Privacy Service and Experience Cloud applications](../experience-cloud-apps.md).

>[!NOTE]
>
>Ainda há mais orientações do regulador da Califórnia sobre quais tipos de dados estão qualificados para solicitações de privacidade do consumidor.

## Perguntas sobre a CCPA

As seguintes questões estão especificamente relacionadas com a CCPA.

### Como as diferentes funções e responsabilidades da CCPA se aplicam ao Experience Cloud?

Conforme definido pela CCPA, as seguintes funções se aplicam ao Adobe e seus clientes:

* Os clientes do Adobe (a parte que solicita a coleta e o uso de informações pessoais dos residentes da Califórnia) seriam considerados um **Business**.
* O Adobe, na sua função de fornecer o serviço, seria considerado um **Provedor de serviços**.

Como Provedor de serviços, a Adobe coleta e processa informações pessoais em nome da empresa e está contratualmente obrigada a usar essas informações apenas para os fins específicos estabelecidos no contrato.

Tendo em conta esta relação e a linguagem do contrato de Adobe, as divulgações de informações não seriam provavelmente consideradas uma &quot;venda&quot; para a qual as empresas precisariam de informar e solicitar consentimento.

No entanto, os serviços Adobe podem ser utilizados para permitir o compartilhamento de dados e transferências para terceiros. Essas transferências de terceiros podem ser consideradas uma &quot;venda&quot; e exigem legalmente a divulgação e o consentimento. Os clientes devem trabalhar com seus advogados para avaliar casos de uso específicos, a fim de avaliar os requisitos aplicáveis.

### O Adobe oferece outras ferramentas que podem ser úteis para atender aos requisitos da CCPA?

Os aplicativos Adobe Experience Cloud oferecem funções de gerenciamento e controle de dados que podem ser úteis para as necessidades de privacidade das empresas. Entre essas ferramentas estão a rotulagem de uso de dados, controles de acesso com base em funções, ofuscação de IP e recursos de hash.

A Adobe recebeu várias certificações de suas práticas de privacidade e segurança, como uma certificação ISO 27001 e uma validação TrustArc GDPR.

## Perguntas sobre o RGPD

As perguntas a seguir estão relacionadas especificamente com o GDPR.

### Qual é a diferença entre um regulamento e uma diretiva?

Um **regulamento** é um ato legislativo vinculativo e deve ser aplicado na sua totalidade em toda a UE. Uma **diretiva** é um ato legislativo que define um objetivo que todos os países da UE devem alcançar, mas cabe a cada um deles decidir como.

É importante observar que o GDPR é um regulamento, ao contrário da legislação anterior (a Diretiva Proteção de Dados), que é uma diretiva.

### Como o GDPR afeta as políticas relacionadas às violações de dados?

Os regulamentos propostos relativos às violações de dados estão relacionados principalmente com as políticas de notificação das empresas que foram violadas. As violações de dados que possam constituir um risco para os indivíduos devem ser notificadas à autoridade responsável pela proteção de dados no prazo de 72 horas e às pessoas afetadas sem demora injustificada.

## Perguntas sobre PDPA

As seguintes questões estão especificamente relacionadas com o PDPA.

### O que são dados pessoais confidenciais?

O PDPA prevê requisitos rigorosos para a recolha e armazenamento de dados pessoais sensíveis, incluindo dados pessoais relativos a: origem racial ou étnica, opiniões políticas, crenças religiosas ou filosóficas, registros criminais, associações sindicais, dados genéticos, dados biométricos, registros de saúde e orientação ou preferências sexuais.
