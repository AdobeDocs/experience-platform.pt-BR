---
title: Informações confidenciais e pessoais no XDM
description: Saiba mais sobre as principais considerações relacionadas a informações pessoais confidenciais (SPI) e informações de identificação pessoal (PII) no Experience Data Model (XDM).
source-git-commit: 76815389a1c87fbf908e499c50594a4b356a11a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Informações confidenciais e pessoais no XDM

O Experience Data Model (XDM) fornece estruturas de dados padrão para uso no Adobe Experience Platform, permitindo coletar dados sobre as experiências do cliente. Esses dados podem incluir informações pessoais confidenciais (SPI) e informações de identificação pessoal (PII), como endereço de email de um cliente, nome, ID da conta e outros campos de dados.

Regras organizacionais e regulamentos legais de privacidade como o Regulamento Geral sobre a Proteção de Dados (GDPR) impõem restrições sobre como a SPI e a PII podem ser coletadas, armazenadas, usadas e compartilhadas. Dessa forma, é importante considerar quais campos representam informações confidenciais ou pessoais no modelo de dados e garantir que suas operações estejam dentro das diretrizes organizacionais e legais.

Este documento aborda as principais considerações relacionadas aos dados confidenciais e pessoais no XDM.

## Determinar quais campos contêm dados confidenciais ou pessoais

O que constitui SPI e PII é muito específico do contexto, e, portanto, cabe a você compreender o modelo de dados, as operações comerciais e as regulamentações aplicáveis para determinar quais campos de esquema representam dados confidenciais ou pessoais.

Por exemplo, a jurisdição legal dos clientes tem um efeito direto nas informações consideradas confidenciais. O GDPR fornece definições sólidas para os IPC e os PII, mas os clientes fora do Espaço Econômico Europeu (EEE) podem estar sujeitos a diferentes definições e restrições.

## Tratamento de dados pessoais e confidenciais

Semelhante às definições para os próprios dados confidenciais e pessoais, as restrições para lidar com esses dados também são específicas do contexto.

O consentimento do cliente geralmente é um fator essencial em termos de quais dados podem ser coletados e processados e para quais fins. Dependendo da jurisdição legal sob a qual seus clientes estão, pode ser necessário consentimento explícito para que seus dados confidenciais e pessoais sejam coletados. Mesmo nos casos em que o consentimento explícito não é obrigatório, as restrições de tratamento de dados ainda são aplicáveis, dependendo do que o aviso de privacidade disser ao cliente.

Consulte sua equipe jurídica para determinar como os dados confidenciais e pessoais devem ser tratados em seus casos de uso comercial.

## Restrição do uso de dados confidenciais e pessoais

O XDM fornece uma variedade de grupos de campos e tipos de dados padrão para descrever estruturas de dados relevantes e comumente usadas para potencializar as experiências do cliente. Se um recurso padrão recomendado contiver campos restritos que você não deseja incluir em seus esquemas, no entanto, não é necessário usar esse recurso.

A Platform permite definir seus próprios grupos de campos e tipos de dados personalizados, fornecendo controle total sobre como seus dados são estruturados se algum recurso padrão disponível não atender às suas necessidades. Consulte a documentação a seguir para obter mais informações sobre como definir esses recursos personalizados:

* [Criar um grupo de campos personalizado](../ui/resources/field-groups.md#create)
* [Criar um tipo de dados personalizado](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## Próximas etapas

Este documento cobriu considerações importantes sobre dados confidenciais e pessoais no XDM. Para obter mais informações sobre como modelar seus esquemas para atender melhor seus casos de uso da empresa, consulte o guia em [práticas recomendadas para modelagem de dados](./best-practices.md).

Para obter mais informações sobre o controle de dados e os recursos de privacidade no Experience Platform, consulte a visão geral em [governança, privacidade e segurança](../../landing/governance-privacy-security/overview.md).
