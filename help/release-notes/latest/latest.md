---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform para 28 de julho de 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: dc01e03975fdda375b31f44edc8459fa32b5a61b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 10%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 28 de julho de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Data Science Workspace](#dsw)
- [Experience Data Model (XDM)](#xdm)
- [Fontes](#sources)

## Data Science Workspace {#dsw}

O Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Atualizações de biblioteca e sistema operacional | O Data Science Workspace fez atualizações significativas de bibliotecas e SOs para melhorar a funcionalidade e usabilidade. Isso inclui o JupyterLab 1.2.20, Python 3.7, Pandas 1.2.4, Tensorflow 2.4.1 com suporte para CUDA 11 e CUDNN 8 e muito mais. Para saber como visualizar as bibliotecas disponíveis no JupyterLab, visite a seção [bibliotecas compatíveis](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) na documentação de visão geral dos notebooks JupyterLab. |

Para obter informações mais gerais sobre o Data Science Workspace, consulte a [Visão geral do Data Science Workspace](../../data-science-workspace/home.md).

## Experience Data Model (XDM) {#xdm}

O Experience Data Model (XDM) é uma especificação de código aberto criada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para dados na forma de schemas, que permitem que qualquer aplicativo se comunique com os serviços da plataforma.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Filtro da indústria das telecomunicações | Ao adicionar grupos de campos a um schema na interface do usuário, agora é possível filtrar pelo setor de telecomunicações. Consulte o [diagrama de relacionamento da entidade do setor de telecomunicações (ERD)](../../xdm/schema/industries/telecom.md) para ver um modelo de dados recomendado para casos de uso de telecom. |

Para obter informações mais gerais sobre XDM na Platform, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Fontes beta movendo-se para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (Beta) | Agora você pode conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [[!DNL Salesforce Marketing Cloud] visão geral do conector](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
