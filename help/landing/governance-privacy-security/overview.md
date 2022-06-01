---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Visão geral de governança, privacidade e segurança
topic-legacy: overview
description: A Adobe Experience Platform fornece vários serviços e ferramentas que permitem controlar com segurança seus dados de experiência coletados para cumprir suas práticas comerciais, obrigações legais e processo de desenvolvimento.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f456b28016af6d2978933deac68f45c2f8d37f80
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Governança, privacidade e segurança no Adobe Experience Platform

O Adobe Experience Platform permite assimilar, analisar, otimizar e agir seus dados para aprimorar bastante as experiências dos clientes. Esses dados são vastos, complexos e incrivelmente valiosos. Dependendo da natureza de suas operações de dados, das jurisdições legais em que sua empresa opera e de suas políticas organizacionais relacionadas ao uso de dados, você deve controlar e monitorar cuidadosamente a coleta e o uso dos dados de experiência do cliente para proteger seus interesses comerciais.

O Experience Platform fornece vários serviços e ferramentas que permitem controlar com segurança seus dados de experiência coletados para cumprir suas práticas comerciais, obrigações legais e processos de desenvolvimento. As seções abaixo apresentam uma introdução a cada um desses serviços, juntamente com links para a documentação, para obter mais informações.

Os serviços podem ser categorizados em três domínios:

* [Governança de dados](#governance)
* [Privacidade](#privacy)
* [Segurança](#security)

## Governança de dados {#governance}

A governança de dados é um conceito essencial que está interligado a todos os recursos do Experience Platform. O controle de dados representa sua capacidade de controlar e compreender seus dados em toda a jornada por meio da Platform. Isso envolve a manutenção da qualidade dos dados, da linhagem dos dados, da catalogação de dados e muito mais.

### Governança de dados do Adobe Experience Platform {#data-governance}

Como um serviço da plataforma, a Governança de dados da Adobe Experience Platform permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função essencial no Experience Platform em vários níveis, incluindo rotulagem de uso de dados, políticas de uso de dados, aplicação de políticas e linhagem de dados.

Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

### Catálogo e conjuntos de dados {#catalog}

O Serviço de Catálogo é o sistema de registro para localização e linhagem de dados na Plataforma. Embora todos os dados assimilados no Experience Platform sejam armazenados no Data Lake como arquivos e diretórios, o Catalog retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

O Catálogo organiza os dados assimilados em conjuntos de dados, com cada conjunto de dados contendo metadados que podem ser usados para rotular e categorizar os dados que ele contém.

Consulte a [Visão geral do serviço de catálogo](../../catalog/home.md) para obter mais informações sobre o serviço. Para saber como gerenciar conjuntos de dados no Experience Platform, consulte o [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).

## Privacidade {#privacy}

A privacidade é um problema crítico para seus negócios, legisladores e clientes. Como os dados pessoais coletados de seus clientes estão no centro de quase todos os fluxos de trabalho do Experience Platform, a Platform fornece serviços para dar suporte a essas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

Regulamentos legais de privacidade como o Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia e a California Consumer Privacy Act (CCPA) concedem aos cidadãos de suas jurisdições o direito de acessar e excluir os dados pessoais que você coletar e armazenar a partir deles.

O Adobe Experience Platform Privacy Service fornece uma RESTful API e interface do usuário para ajudar a gerenciar essas solicitações. Com o Privacy Service, você pode enviar solicitações para acessar ou excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

Consulte a [Visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações.

### Processamento de consentimento {#consent}

Muitas regulamentações legais de privacidade introduziram requisitos de consentimento ativo e específico quando se trata de coleta de dados, personalização e outros casos de uso de marketing. Para atender a esses requisitos, o Experience Platform permite capturar informações de consentimento em perfis de clientes individuais e usar essas preferências como um fator determinante de como os dados de cada cliente são usados em workflows da plataforma downstream.

Para saber como processar os dados de consentimento e preferência do cliente usando o Adobe standard, consulte a visão geral em [processamento de consentimento no Experience Platform](./consent/adobe/overview.md).

Para obter informações sobre como processar os dados de consentimento do cliente de acordo com a Estrutura de transparência e consentimento (TCF) 2.0 do IAB, consulte a visão geral em [Suporte ao IAB TCF 2.0 na plataforma](./consent/iab/overview.md).

## Segurança {#security}

A integridade e a segurança de seus dados são indispensáveis para sua empresa e esse risco requer recursos de segurança líderes do setor. Para enfrentar esse desafio, a Platform fornece várias ferramentas para ajudar a proteger suas operações de dados.

### Criptografia de dados

Todos os dados da plataforma são criptografados em trânsito e em repouso. Consulte o documento em [criptografia de dados no Platform](./encryption.md) para obter mais informações.

### Controle de acesso {#access-control}

O Experience Platform usa o Adobe Admin Console para fornecer controle de acesso baseado em funções a vários recursos da plataforma. Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.

Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações.

### Sandboxes {#sandboxes}

O Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional.

Para atender à necessidade de flexibilidade de desenvolvimento, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudá-lo a desenvolver seus aplicativos de experiência digital com base em seu próprio ciclo de vida de desenvolvimento.

Consulte a [visão geral das sandboxes](../../sandboxes/home.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma visão geral dos vários serviços e ferramentas da plataforma envolvidos com governança, privacidade e segurança de dados. Consulte a documentação vinculada a este guia para saber mais sobre esses recursos.
