---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Governança, privacidade e segurança no Adobe Experience Platform
topic: overview
description: O Experience Platform fornece vários serviços e ferramentas que permitem controlar com confiança seus dados de experiência coletados para atender às práticas comerciais, obrigações legais e processo de desenvolvimento.
translation-type: tm+mt
source-git-commit: 6ec317dd790b6ad77d8181c1398934f9636c5f5f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---


# Governança, privacidade e segurança no Adobe Experience Platform

A Adobe Experience Platform permite que você ingira, analise, otimize e aja seus dados para aprimorar consideravelmente as experiências dos clientes. Estes dados são vastos, complexos e incrivelmente valiosos. Dependendo da natureza de suas operações de dados, das jurisdições legais sob as quais sua empresa opera e de suas políticas organizacionais relacionadas ao uso de dados, você deve controlar e monitorar cuidadosamente a coleta e o uso dos dados de experiência do cliente para proteger seus interesses comerciais.

O Experience Platform fornece vários serviços e ferramentas que permitem controlar com confiança seus dados de experiência coletados para atender às práticas comerciais, obrigações legais e processos de desenvolvimento. As seções abaixo apresentam uma introdução a cada um desses serviços, juntamente com links para a documentação para obter mais informações.

Os serviços podem ser classificados em três domínios:

* [Governação de dados](#governance)
* [Privacidade](#privacy)
* [Segurança](#security)

## Controle de dados {#governance}

A governança de dados é um conceito essencial que está interligado com todos os recursos do Experience Platform. O controle de dados representa sua capacidade de controlar e compreender seus dados por toda a jornada por meio da plataforma. Isso envolve a manutenção da qualidade dos dados, da linhagem dos dados, da catalogação de dados e muito mais.

### Adobe Experience Platform Data Governance {#data-governance}

Como um serviço de plataforma, o Adobe Experience Platform Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental dentro do Experience Platform em vários níveis, incluindo rotulagem de uso de dados, políticas de uso de dados, aplicação de políticas e linhagem de dados.

Consulte [Visão geral do Data Governance](../../data-governance/home.md) para obter mais informações.

### Catálogo e conjuntos de dados {#catalog}

O serviço de catálogo é o sistema de registro para localização e linhagem de dados na Plataforma. Enquanto todos os dados ingeridos no Experience Platform são armazenados no Data Lake como arquivos e diretórios, o Catálogo armazena os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

O Catálogo organiza os dados ingeridos em conjuntos de dados, com cada conjunto de dados contendo metadados que podem ser usados para rotular e categorizar os dados que ele contém.

Consulte a [visão geral do serviço de catálogo](../../catalog/home.md) para obter mais informações sobre o serviço. Para saber como gerenciar conjuntos de dados no Experience Platform, consulte a [visão geral dos conjuntos de dados](../../catalog/datasets/overview.md).

## Privacidade {#privacy}

A privacidade é um problema crítico para seus negócios, legisladores e clientes. Como os dados pessoais coletados de seus clientes estão no centro de quase todos os workflows de Experience Platform, a Plataforma fornece serviços para dar suporte a essas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

As regulamentações legais de privacidade, como o Regulamento Geral de Proteção de Dados da União (RGPD) e a Lei de Privacidade do Consumidor da Califórnia (CCPA), concedem aos cidadãos de suas jurisdições o direito de acessar e excluir os dados pessoais que você coleta e armazena deles.

A Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário para ajudar a gerenciar essas solicitações. Com o Privacy Service, você pode enviar solicitações para acessar ou excluir dados de clientes particulares ou pessoais de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

Consulte a [visão geral do Privacy Service](../../privacy-service/home.md) para obter mais informações.

### Coleção de consentimento {#consent}

Muitas regulamentações legais de privacidade introduziram requisitos para consentimento ativo e específico quando se trata de coleta de dados, personalização e outros casos de uso de marketing. Para atender a esses requisitos, o Experience Platform permite capturar informações de consentimento em perfis individuais de clientes e usar essas preferências como um fator determinante na forma como os dados de cada cliente são usados em workflows de plataforma downstream.

Para saber como coletar e processar dados de consentimento do cliente de acordo com o IAB Transparency and Consent Framework (TCF) 2.0, consulte a visão geral sobre o suporte do IAB TCF 2.0 na Platform](./consent/iab/overview.md).[

<!-- For more information on the consent collection process using the Adobe standard, see the [consent collection overview]. -->

## Segurança {#security}

A integridade e a segurança dos seus dados são indispensáveis para a sua empresa, e esse risco requer recursos de segurança líderes do setor. Para enfrentar esse desafio, a Platform fornece várias ferramentas para ajudar a proteger suas operações de dados.

### Controle de acesso {#access-control}

O Experience Platform usa o Adobe Admin Console para fornecer controle de acesso baseado em funções para vários recursos da plataforma. Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção.

Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações.

### Sandboxes {#sandboxes}

O Experience Platform foi desenvolvido para enriquecer aplicativos de experiência digital em escala global. O Empresa geralmente executa vários aplicativos de experiência digital em paralelo e precisa atender ao desenvolvimento, teste e implantação desses aplicativos, garantindo a conformidade operacional.

Para atender à necessidade de flexibilidade de desenvolvimento, o Experience Platform fornece caixas de proteção que particionam uma única instância da plataforma em ambientes virtuais separados para ajudá-lo a desenvolver seus aplicativos de experiência digital com base no seu próprio ciclo de vida de desenvolvimento.

Consulte [sandboxes overview](../../sandboxes/home.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma visão geral dos vários serviços e ferramentas da plataforma envolvidos com controle de dados, privacidade e segurança. Consulte a documentação vinculada a este guia para saber mais sobre esses recursos.