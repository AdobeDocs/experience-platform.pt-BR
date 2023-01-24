---
title: Notas de versão da Adobe Experience Platform em janeiro de 2023
description: As notas de versão de janeiro de 2023 para o Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de janeiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Fontes](#sources)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Permitir acesso do usuário às subpastas de fontes de armazenamento na nuvem | Agora é possível definir o acesso a uma subpasta específica da fonte de armazenamento na nuvem ao criar uma nova conta. Depois de criados, os usuários só poderão acessar dados da subpasta permitida. Esse recurso está disponível nas seguintes fontes de armazenamento em nuvem: [Armazenamento Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Armazenamento em nuvem Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidade beta de [!DNL SugarCRM] | [!DNL SugarCRM] Agora, as fontes estão disponíveis em beta. Use o [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] fontes para trazer dados de [!DNL SugarCRM] para o Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |