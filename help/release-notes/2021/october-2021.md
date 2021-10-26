---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 14%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de outubro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Fontes](#sources)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Amazon S3] melhorias na fonte | Agora você pode usar o `s3SessionToken` para conectar seu [!DNL Amazon S3] conta para a Platform usando credenciais de segurança temporárias. Esse token permite que você forneça acesso temporário e de curto prazo ao seu [!DNL Amazon S3] recursos para usuários em ambientes não confiáveis. Consulte a [[!DNL Amazon S3] documentação](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obter mais informações. |
| [!DNL Generic REST API] (Beta) | Agora você pode criar um [!DNL Generic REST API] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) ou [interface do usuário](../../sources/tutorials/ui/create/protocols/generic-rest.md) para trazer dados de um aplicativo REST genérico para a plataforma. Consulte a [[!DNL Generic REST API] visão geral](../../sources/connectors/protocols/generic-rest.md) para obter mais informações. |
| [!DNL Zoho CRM] (Beta) | Agora você pode criar um [!DNL Zoho CRM] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) ou [interface do usuário](../../sources/tutorials/ui/create/crm/zoho.md) para trazer dados do [!DNL Zoho CRM] para a Platform. Consulte a [[!DNL Zoho CRM] visão geral](../../sources/connectors/crm/zoho.md) para obter mais informações. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
