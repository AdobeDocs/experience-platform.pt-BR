---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform de outubro de 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: Outubro de 2020**

- [Preparo de dados](#data-prep)
- [Fontes](#sources)

## Preparo de dados {#data-prep}

O Data Prep permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM).

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Função `is_set`  | A `is_set` função permite verificar a presença de um atributo nos dados de origem. `is_set` pode ser usado em combinação com `is_empty` para verificar a presença do atributo e a presença do valor dentro do atributo. |
| Função `get_values`  | A `get_values` função permite obter os valores do mapa de entrada para qualquer tecla. |

Para obter mais informações, leia a visão geral [da Preparação de](../../data-prep/home.md)dados.

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento hierárquico | Você pode pré-visualização um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de ingestão de dados. |
| Suporte de autenticação SSH para SFTP | Você pode conectar sua conta SFTP com [!DNL Platform] chaves SSH abertas RSA/DSA. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Melhorias no UX | Você pode ativar seu conjunto de dados para [!DNL Profile] durante o processo de ingestão de dados. Consulte o tutorial de fluxo de trabalho [de fluxo de dados do armazenamento](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) em nuvem para obter mais informações. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.