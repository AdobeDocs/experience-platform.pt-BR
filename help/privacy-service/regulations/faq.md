---
keywords: Experience Platform;página inicial;tópicos populares;GDPR;gdpr;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;FAQ;regulamento;regulamentos;Regulamentos;privacidade;Privacidade;
solution: Experience Platform
title: Perguntas frequentes sobre regulamentos de privacidade
description: Este documento fornece respostas a perguntas frequentes sobre as regulamentações legais de privacidade compatíveis e sua implementação no Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 7e86721f6dd6fd280ae7e7e67aca21b4258ffb66
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 1%

---

# Perguntas frequentes sobre regulamentos de privacidade

Este documento fornece respostas a perguntas frequentes sobre as regulamentações legais de privacidade compatíveis e sua implementação no Adobe Experience Cloud.

>[!NOTE]
>
>As definições para os vários termos utilizados neste documento podem ser [terminologia do regulamento de privacidade](terminology.md) guia.

## Perguntas gerais

As perguntas a seguir estão relacionadas a todos os regulamentos de privacidade aceitos pelo Experience Cloud.

### Quem são afetados pelas regulamentações de privacidade aceitas?

A variável [regulamentos de privacidade compatíveis com o Experience Cloud](./overview.md) aplicam-se a todas as organizações que armazenam e processam dados pessoais de cidadãos nas respectivas jurisdições dos regulamentos, independentemente da localização geográfica da organização.

### O que constituem dados pessoais?

Dados pessoais são qualquer informação relacionada a uma pessoa física ou titular de dados que possa ser usada para identificar direta ou indiretamente tal pessoa. Pode ser qualquer coisa, desde um nome, uma foto, um endereço de email, detalhes bancários, publicações em sites de redes sociais, informações médicas ou um endereço IP de computador.

Os seguintes identificadores são comumente usados em aplicativos Experience Cloud e podem estar sujeitos a requisitos de regulamento de privacidade:

* Nome
* Endereço postal
* Identificador pessoal exclusivo
* Identificador online
* Endereço IP
* Endereço de email
* Nome da conta

As informações pessoais também podem incluir informações de atividade da Internet ou de outra rede eletrônica. Isso inclui, mas não está limitado a:

* Histórico de navegação
* Pesquisar histórico
* Informações sobre a interação do consumidor com um site, aplicativo ou anúncio

Embora as regulamentações de privacidade cubram um amplo conjunto de informações pessoais, os termos contratuais padrão do Adobe determinam que informações pessoais confidenciais (como SSN, informações de carteira de motorista, informações de conta financeira e dados biométricos) sejam geralmente proibidas de serem importadas e usadas em aplicativos Experience Cloud.

### Qual é a diferença entre um controlador de dados e um processador de dados?

A **controlador de dados** é a entidade que determina as finalidades, as condições e os meios de tratamento dos dados pessoais, ao passo que **processador de dados** é uma entidade que processa dados pessoais em nome do controlador de dados.

A **controlador de dados** é a pessoa ou organização que tem o poder e a responsabilidade de tomar decisões relacionadas à coleta, ao uso ou à divulgação de dados pessoais. A **processador de dados** é a pessoa ou organização que opera em relação à coleta, utilização ou divulgação dos dados pessoais e à direção do controlador de dados.

### Qual é a diferença entre consentimento explícito e inequívoco do titular dos dados?

**Consentimento explícito** refere-se a um padrão de consentimento que envolve uma indicação específica, informada e inequívoca dos desejos do titular dos dados, oralmente ou por escrito. Em termos simples, o titular dos dados deve dizer literalmente e explicitamente &quot;Eu concordo&quot; ou &quot;Eu concordo&quot; para que o consentimento seja considerado explícito. Além disso, deve ser tão fácil retirar o consentimento como o dar.

**Consentimento inequívoco (implícito)** refere-se ao consentimento que não foi explicitamente dado pelo titular dos dados, mas é, no entanto, de natureza inequívoca. Por exemplo, durante o processo de inscrição em um site de empresa, é dado um aviso de que, ao fornecer um endereço de email, o titular dos dados consente em receber emails sobre ofertas especiais. Se o titular dos dados ler o aviso, a ação afirmativa de inserir seu email é suficiente para ser considerada consentimento inequívoco.

Para muitos regulamentos como o GDPR, o consentimento explícito é necessário para processar dados pessoais confidenciais, onde nada menos que &quot;aceitar&quot; será suficiente. No entanto, para dados não confidenciais, o consentimento inequívoco (implícito) é aceitável.

### Os titulares de dados com menos de uma determinada idade podem consentir?

Muitas regulamentações de privacidade estipulam que, se um titular de dados tiver menos de uma determinada idade, não poderá legalmente fornecer consentimento para a coleta de seus dados pessoais. Alguns regulamentos permitem que o consentimento seja dado pelo titular da responsabilidade parental por esse titular de dados nesses casos, mas não em todos. A tabela a seguir lista a idade mínima para que os titulares de dados forneçam seu próprio consentimento para cada regulamento, com notas para obter mais informações:

| Regulação | Idade do consentimento | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 16 | <ul><li>O consentimento dos pais só pode ser fornecido para titulares de dados com 13 anos ou mais.</li><li>A coleta de dados pessoais de indivíduos com menos de 13 anos é estritamente proibida.</li></ul> |
| GDPR (União Europeia) | 16 | <ul><li>Alguns Estados-Membros da UE podem prever uma lei para uma idade mais baixa para este efeito, mas não inferior a 13 anos.</li><li>O consentimento dos pais deve ser fornecido para todos os titulares de dados abaixo do limite de idade.</li></ul> |
| LGPD (Brasil) | 13 | <ul><li>O consentimento dos pais deve ser fornecido para todos os titulares de dados abaixo do limite de idade.</li><li>O consentimento pode ser dado por uma pessoa singular de 13 a 18 anos, desde que o tratamento dos seus dados pessoais seja efetuado no seu interesse.</li></ul> |
| PDPA (Tailândia) | 10 | <ul><li>O consentimento dos pais deve ser fornecido para todos os titulares de dados abaixo do limite de idade.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Quantos dias uma empresa tem para responder a uma solicitação do consumidor para acessar ou excluir informações pessoais?

Supondo que a empresa tenha coletado informações pessoais e possa autenticar ou verificar a identidade de um consumidor específico, as regulamentações de privacidade permitem que uma janela de tempo específica seja atendida para uma solicitação do consumidor. A tabela a seguir detalha as janelas de tempo aplicáveis para cada regulamento, com observações sobre algumas exceções:

>[!NOTE]
>
>O prazo de resposta em &quot;dias&quot; reflete os prazos obrigatórios de cada lei regulatória para concluir uma solicitação dos consumidores.

| Regulação | Prazo de resposta | Notas |
| --- | --- | --- |
| CCPA (Califórnia) | 45 dias |  |
| GDPR (União Europeia) | 30 dias | Se a solicitação for complexa ou se várias solicitações tiverem sido feitas pelo mesmo titular dos dados, ela poderá ser estendida para 60 dias. |
| LGPD (Brasil) | 15 dias |  |
| PDPA (Tailândia) | 30 dias | Se uma empresa não puder responder a uma solicitação do titular dos dados dentro da janela de conformidade, a empresa terá 30 dias adicionais a partir da data em que não pôde atender à solicitação para responder por escrito ao titular dos dados. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Minha empresa precisa nomear um responsável pela proteção de dados?

Se as operações de dados da sua organização estiverem sob as jurisdições legais do GDPR, LGPD ou PDPA, você deverá nomear um responsável pela proteção de dados (DPO) nos seguintes casos:

* Sua organização é uma autoridade pública
* Sua organização se envolve em monitoramento sistemático em larga escala
* Sua organização se envolve no processamento em larga escala de dados pessoais confidenciais.

>[!IMPORTANT]
>
>Ao contrário de outros regulamentos, a CCPA estipula isso como um requisito. No entanto, geralmente recomenda-se que, para manter a conformidade com a privacidade, uma empresa tenha de ter atividades qualificadas de monitoramento de dados individuais e de armazenamento de dados do consumidor, bem como de resposta a consultas dos clientes.

### Como posso aceitar solicitações de privacidade do consumidor se mantenho dados cobertos por regulamentos de privacidade?

Depois de tomar as medidas necessárias para autenticar consumidores que se enquadram nas jurisdições legais apropriadas, a Adobe Experience Platform Privacy Service permite enviar solicitações de privacidade do consumidor para aplicativos compatíveis com o Experience Cloud. Consulte a [[!DNL Privacy Service] visão geral das ](../home.md) para obter mais informações. Para obter informações sobre como seus aplicativos Experience Cloud específicos podem atender às solicitações de privacidade, consulte o manual no [aplicativos Privacy Service e Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Outras orientações do regulador da Califórnia ainda estão disponíveis sobre quais tipos de dados são elegíveis para solicitações de privacidade do consumidor.

## Perguntas da CCPA

As questões seguintes dizem especificamente respeito à CCPA.

### Como as diferentes funções e responsabilidades da CCPA se aplicam ao Experience Cloud?

Conforme definido pela CCPA, as seguintes funções se aplicam ao Adobe e seus clientes:

* Adobe clientes (a parte que solicita a coleta e o uso de informações pessoais de residentes da Califórnia) seriam considerados uma **Empresas**.
* Adobe, no seu papel de prestação do serviço, seria considerada uma **Provedor de serviços**.

Como Provedor de Serviços, a Adobe coleta e processa informações pessoais em nome da Empresa e está contratualmente obrigada a usar essas informações apenas para os fins específicos estabelecidos no contrato.

Dada esta relação e a linguagem do contrato de Adobe, as divulgações ao Adobe provavelmente não seriam consideradas uma &quot;venda&quot; para a qual as empresas precisariam de fornecer um aviso e solicitar consentimento.

No entanto, os serviços da Adobe podem ser usados para permitir determinado compartilhamento de dados e transferências para terceiros. Essas transferências de terceiros podem ser consideradas uma &quot;venda&quot; e exigem legalmente divulgação e consentimento. Os clientes devem trabalhar com seu departamento jurídico para avaliar casos de uso específicos e avaliar os requisitos aplicáveis.

### O Adobe oferece outras ferramentas que podem ser úteis no atendimento dos requisitos da CCPA?

Os aplicativos da Adobe Experience Cloud fornecem funções de gerenciamento e governança de dados que podem ser úteis para as necessidades de privacidade das empresas. Entre essas ferramentas estão a rotulagem de uso de dados, controles de acesso com base em função, ofuscação de IP e recursos de hash.

A Adobe recebeu várias certificações de suas práticas de privacidade e segurança, como uma certificação ISO 27001 e uma validação do GDPR TrustArc.

## Perguntas sobre o GDPR

As perguntas a seguir estão relacionadas especificamente ao GDPR.

### Qual é a diferença entre um regulamento e uma diretiva?

A **regulamento** é um ato legislativo vinculativo e deve ser aplicado na sua totalidade em toda a UE. A **diretiva** é um ato legislativo que estabelece um objetivo que todos os países da UE devem alcançar, mas cabe a cada país decidir como.

É importante observar que o GDPR é um regulamento, em contraste com a legislação anterior (a Diretiva de Proteção de Dados), que é uma diretiva.

### Como o GDPR afeta a política em relação às violações de dados?

As regulamentações propostas em relação às violações de dados estão relacionadas principalmente às políticas de notificação das empresas que foram violadas. As violações de dados que possam constituir um risco para as pessoas devem ser notificadas à autoridade responsável pela proteção de dados no prazo de 72 horas e às pessoas afetadas sem demora injustificada.

## Perguntas sobre PDPA

As perguntas a seguir apresentadas referem-se especificamente ao PDPA.

### O que constituem dados pessoais confidenciais?

O PDPA prevê requisitos rigorosos para a coleta e o armazenamento de dados pessoais sensíveis, que incluem dados pessoais relacionados a: origem racial ou étnica, opiniões políticas, crenças religiosas ou filosóficas, registros criminais, associações a sindicatos, dados genéticos, dados biométricos, registros de saúde e orientação ou preferências sexuais.
