---
description: Para usar o Destination SDK, uma empresa parceira deve atender aos pré-requisitos listados neste documento.
title: Pré-requisitos de integração
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Pré-requisitos de integração

Para usar o Destination SDK, verifique se você atende aos pré-requisitos técnicos e de parceria listados nas seções abaixo.

## Pré-requisitos técnicos / de API para destinos de transmissão {#streaming-prerequisites}

1. Você tem um terminal de API REST para que o Adobe Experience Platform forneça os seguintes tipos de dados:
   * Informações de associação de segmento;
   * Informações sobre a identidade do perfil;
   * (Opcional) Atributos adicionais para o enriquecimento do perfil.
2. O ponto de extremidade da API REST oferece suporte à autenticação do portador de token da API ou ao protocolo de autenticação OAuth 2.0.
3. (Opcional) Você tem uma API de criação/atualização/exclusão de segmento ou um terminal de API para o gerenciamento de metadados programático.

## Pré-requisitos técnicos para destinos em lote {#batch-prerequisites}

1. Você tem um local de destino hospedado em [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], SFTP, [!DNL Google Cloud]ou privado [!DNL Data Landing Zone], onde você pode receber arquivos exportados do Experience Platform.
2. A plataforma de destino pode assimilar arquivos no formato configurado por meio do [opções de formatação de arquivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) em Destination SDK para destinos de lote.
3. (Opcional) Você tem uma API de criação/recuperação/atualização/exclusão (CRUD) de segmento ou um terminal de API para o gerenciamento de metadados programático.

## Pré-requisitos da parceria {#partnership-prerequisites}

Se você for um Fornecedor Independente de Software (ISV) ou Integrador de Sistema (SI) que deseja usar o Destination SDK, leia os requisitos de parceria para ISVs e SIs no [seção obtendo acesso](./overview.md#get-access).
