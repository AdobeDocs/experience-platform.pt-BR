---
description: Para usar o Destination SDK, uma empresa parceira deve atender aos pré-requisitos listados neste documento.
title: Pré-requisitos de integração
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Pré-requisitos de integração

Para usar o Destination SDK, certifique-se de atender aos pré-requisitos técnicos e de parceria listados nas seções abaixo.

## Pré-requisitos técnicos/de API para destinos de transmissão {#streaming-prerequisites}

1. Você tem um endpoint da REST API para o Adobe Experience Platform fornecer os seguintes tipos de dados para:
   * Informações sobre associação de público-alvo;
   * Informações sobre a identidade do perfil;
   * (Opcional) Atributos adicionais para enriquecimento de perfil.
2. O ponto de extremidade da REST API é compatível com token de portador básico ou protocolos de autenticação OAuth 2.0.
3. (Opcional) Você tem um endpoint de API ou API de criação/atualização/exclusão de público-alvo para gerenciamento de metadados programáticos.

## Pré-requisitos técnicos para destinos em lote {#batch-prerequisites}

1. Você tem um local de destino hospedado em [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud], ou um [!DNL Data Landing Zone] privado, onde você pode receber arquivos exportados de Experience Platform.
2. Sua plataforma de destino pode assimilar arquivos no formato configurado através das [opções de formatação de arquivo](functionality/destination-server/file-formatting.md) no Destination SDK para destinos em lote.
3. (Opcional) Você tem um ponto de extremidade de API ou API de criação/recuperação/atualização/exclusão de público-alvo ([!DNL CRUD]) para gerenciamento de metadados programáticos.

## Pré-requisitos da parceria {#partnership-prerequisites}

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistemas (SI) que pretende usar o Destination SDK, leia os requisitos de parceria para ISVs e SIs na [seção obter acesso](overview.md#get-access).
