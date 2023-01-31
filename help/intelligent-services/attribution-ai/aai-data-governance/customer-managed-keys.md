---
keywords: insights, ai de atribuição, insights do ai de atribuição, serviço de consulta AAI, consultas de atribuição, pontuações de atribuição; chaves gerenciadas pelo cliente na AAI
feature: Customer-Managed Keys in Attribution AI
title: Chaves gerenciadas pelo cliente
description: Saiba como configurar Chaves gerenciadas pelo cliente para o Attribution AI.
source-git-commit: 3b1cc7ca710071df9de06428f7eed2993219ae1a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 24%

---

# Chaves gerenciadas pelo cliente

O Attribution AI fornece a opção para [Escudo da Saúde](https://www.adobe.com/trust/compliance/hipaa-ready.html) e clientes do Privacy &amp; Security Shield para utilizar o Azure Customer Managed Keys (CMK) para ser aplicado aos dados do Attribution AI. O processo de configuração é igual ao [Configuração do Adobe Experience Platform CMK](../../../landing/governance-privacy-security/customer-managed-keys.md) e você pode seguir as etapas descritas aqui.

Você pode ler a documentação em [Chaves gerenciadas pelo cliente no Adobe Experience Platform](../../../landing/governance-privacy-security/encryption.md) e siga as etapas descritas para passar pelo processo de configuração.

>[!NOTE]
>
>[!DNL Customer Managed Keys] estão disponíveis no momento somente para organizações que compraram a variável [[!DNL Healthcare Shield or Privacy & Security Shield]](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/vertical-blueprints/healthcare-vertical.html%3Flang%3Den) oferta complementar.

Todos os dados utilizados pela Platform são criptografados em trânsito e em repouso para manter seus dados protegidos, com ou sem CMK. Para obter informações sobre criptografia do Adobe Experience Platform, leia a documentação em [Criptografia de dados](../../../landing/governance-privacy-security/encryption.md).