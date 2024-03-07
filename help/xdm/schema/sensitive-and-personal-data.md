---
title: Informações confidenciais e pessoais no XDM
description: Saiba mais sobre as principais considerações sobre informações pessoais confidenciais (SPI) e informações de identificação pessoal (PII) no Experience Data Model (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Informações confidenciais e pessoais no XDM

O Experience Data Model (XDM) fornece estruturas de dados padrão para uso no Adobe Experience Platform, permitindo coletar dados sobre as experiências do cliente. Esses dados podem incluir informações pessoais confidenciais (SPI) e informações de identificação pessoal (PII), como endereço de email, nome, ID da conta e outros campos de dados do cliente.

Regras organizacionais e regulamentos legais de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR), impõem restrições sobre como as SPI e PII podem ser coletadas, armazenadas, usadas e compartilhadas. Dessa forma, é importante considerar quais campos representam informações confidenciais ou pessoais em seu modelo de dados e garantir que suas operações estejam dentro das diretrizes organizacionais e legais.

Este documento aborda as principais considerações relacionadas a dados confidenciais e pessoais no XDM.

## Determinar quais campos contêm dados confidenciais ou pessoais

O que constitui SPI e PII é muito específico do contexto e, portanto, depende de você entender seu modelo de dados, as operações de negócios e os regulamentos aplicáveis para determinar quais campos de esquema representam dados confidenciais ou pessoais.

Por exemplo, a jurisdição legal de seus clientes tem um efeito direto sobre quais informações são consideradas confidenciais. O GDPR fornece definições robustas de SPI e PII, mas os clientes fora do Espaço Econômico Europeu (EEE) podem estar sujeitos a definições e restrições diferentes.

## Tratamento de dados sensíveis e pessoais

À semelhança das próprias definições de dados sensíveis e pessoais, as restrições ao tratamento destes dados são também específicas do contexto.

O consentimento do cliente geralmente é um fator crítico em termos de quais dados podem ser coletados e processados e para quais finalidades. Dependendo da jurisdição legal sob a qual seus clientes estão sob, pode ser necessário consentimento explícito para que seus dados confidenciais e pessoais sejam coletados. Mesmo nos casos em que o consentimento explícito não é necessário, as restrições de tratamento de dados ainda são aplicáveis, dependendo do que a notificação de privacidade informa ao cliente.

Consulte sua equipe jurídica para determinar como dados confidenciais e pessoais devem ser tratados para os casos de uso de sua empresa.

## Restrição do uso de dados confidenciais e pessoais

O XDM fornece uma variedade de grupos de campos padrão e tipos de dados para descrever estruturas de dados relevantes e usadas com frequência para potencializar as experiências do cliente. No entanto, se um recurso padrão recomendado contiver campos restritos que você não deseja incluir em seus esquemas, não será necessário usar esse recurso.

A Platform permite definir seus próprios grupos de campos personalizados e tipos de dados, fornecendo controle total sobre como seus dados são estruturados se algum recurso padrão disponível não atender às suas necessidades. Consulte a documentação a seguir para obter mais informações sobre como definir esses recursos personalizados:

* [Criar um grupo de campos personalizado](../ui/resources/field-groups.md#create)
* [Criar um tipo de dados personalizado](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI e PII só devem ser salvas na variável [Perfil individual XDM](../classes/individual-profile.md) e [XDM ExperienceEvent](../classes/experienceevent.md) classes. Como prática recomendada para fins de exclusão de dados e privacidade e governança, não salve a SPI e a PII em nenhuma outra classe XDM personalizada ou padrão.

## Próximas etapas

Esse documento abordou as principais considerações relacionadas a dados confidenciais e pessoais no XDM. Para obter mais informações sobre como modelar seus esquemas para melhor atender aos casos de uso da empresa, consulte o guia em [práticas recomendadas para modelagem de dados](./best-practices.md).

Para obter mais informações sobre os recursos de governança de dados e privacidade no Experience Platform, consulte a visão geral no [governança, privacidade e segurança](../../landing/governance-privacy-security/overview.md).
