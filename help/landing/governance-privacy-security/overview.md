---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Visão geral de governança, privacidade e segurança
description: A Adobe Experience Platform fornece vários serviços e ferramentas que permitem controlar com confiança os dados de experiência coletados para estar em conformidade com as práticas comerciais, as obrigações legais e o processo de desenvolvimento.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 8%

---

# Governança, privacidade e segurança no Adobe Experience Platform

O Adobe Experience Platform permite assimilar, analisar, otimizar e agir com seus dados para melhorar muito a experiência do cliente. Esses dados são vastos, complexos e incrivelmente valiosos. Dependendo da natureza das operações de dados, das jurisdições legais sob as quais sua empresa opera e das políticas organizacionais relacionadas ao uso de dados, você deve controlar e monitorar cuidadosamente a coleta e o uso de dados da experiência do cliente para proteger os interesses comerciais.

O Experience Platform fornece vários serviços e ferramentas que permitem controlar com confiança os dados de experiência coletados para estar em conformidade com as práticas comerciais, as obrigações legais e os processos de desenvolvimento. As seções abaixo fornecem uma introdução a cada um desses serviços, juntamente com links para a documentação para obter mais informações.

Os serviços podem ser classificados em três domínios:

* [Governança de dados](#governance)
* [Privacidade](#privacy)
* [Segurança](#security)

## Governança de dados {#governance}

A governança de dados é um conceito essencial que está interligado a todos os recursos do Experience Platform. A governança de dados representa sua capacidade de controlar e compreender seus dados em toda a jornada por meio da Plataforma. Isso envolve a manutenção da qualidade dos dados, da linhagem de dados, da catalogação de dados e muito mais.

### Governança de dados do Adobe Experience Platform {#data-governance}

Como um serviço de plataforma, o Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no Experience Platform em vários níveis, incluindo rotulagem de uso de dados, políticas de uso de dados, aplicação de políticas e linhagem de dados.

Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

### Catálogo e conjuntos de dados {#catalog}

O Serviço de catálogo é o sistema de registro para localização e linhagem de dados na Platform. Embora todos os dados assimilados na Experience Platform sejam armazenados no Data Lake como arquivos e diretórios, o Catálogo retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

O catálogo organiza dados assimilados em conjuntos de dados, com cada conjunto de dados contendo metadados que podem ser usados para rotular e categorizar os dados que ele contém.

Consulte a [Visão geral do Serviço de catálogo](../../catalog/home.md) para obter mais informações sobre o serviço. Para saber como gerenciar conjuntos de dados no Experience Platform, consulte a [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).

## Privacidade {#privacy}

A privacidade é um problema crítico para sua empresa, legisladores e clientes. Como os dados pessoais coletados de seus clientes estão no centro de quase todos os fluxos de trabalho do Experience Platform, a Platform fornece serviços para dar suporte a essas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

Regulamentos legais de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia e a Lei de Privacidade do Consumidor da Califórnia (CCPA), concedem aos cidadãos em suas jurisdições o direito de acessar e excluir os dados pessoais coletados e armazenados neles.

O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface para ajudar a gerenciar essas solicitações. Com o Privacy Service, você pode enviar solicitações para acessar ou excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

Consulte a [visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações.

### Processamento de consentimento {#consent}

Muitas regulamentações legais de privacidade introduziram requisitos para consentimento ativo e específico quando se trata de coleta de dados, personalização e outros casos de uso de marketing. Para atender a esses requisitos, o Experience Platform permite capturar informações de consentimento em perfis de clientes individuais e usar essas preferências como um fator determinante em como os dados de cada cliente são usados nos workflows downstream da plataforma.

Para saber como processar os dados de consentimento e preferência do cliente usando o padrão Adobe, consulte a visão geral em [processamento de consentimento no Experience Platform](./consent/adobe/overview.md).

Para obter informações sobre como processar dados de consentimento do cliente em conformidade com a Estrutura de transparência e consentimento (TCF) do IAB 2.0, consulte a visão geral sobre [Suporte IAB TCF 2.0 na plataforma](./consent/iab/overview.md).

## Segurança {#security}

A integridade e a segurança de seus dados são indispensáveis para seus negócios, e esse risco requer recursos de segurança líderes do setor. Para enfrentar esse desafio, a Platform fornece várias ferramentas para ajudar a proteger suas operações de dados.

### Criptografia de dados

Todos os dados da plataforma são criptografados em trânsito e em repouso. Consulte o documento sobre [criptografia de dados na Platform](./encryption.md) para obter mais informações.

### Controle de acesso {#access-control}

O Experience Platform usa o Adobe Admin Console para fornecer controle de acesso baseado em funções a vários recursos da plataforma. Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.

Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações.

### Sandboxes {#sandboxes}

O Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

Para atender à necessidade de flexibilidade de desenvolvimento, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar você a desenvolver seus aplicativos de experiência digital com base em seu próprio ciclo de vida de desenvolvimento.

Consulte a [visão geral das sandboxes](../../sandboxes/home.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma visão geral dos vários serviços e ferramentas da Platform envolvidos com governança, privacidade e segurança de dados. Consulte a documentação vinculada a este guia para saber mais sobre esses recursos.
