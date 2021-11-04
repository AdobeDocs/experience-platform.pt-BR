---
keywords: Experience Platform; home; tópicos populares; Aplicação de políticas; Aplicação automática; Aplicação baseada em API; governança de dados
solution: Experience Platform
title: Visão geral da aplicação de políticas
topic-legacy: guide
description: Depois que os rótulos de uso de dados tiverem sido aplicados aos conjuntos de dados do Adobe Experience Platform e as políticas de uso de dados tiverem sido definidas para ações de marketing em relação a esses rótulos, os recursos de Governança de dados permitirão aplicar essas políticas e evitar operações de dados que constituam violações de política. Há dois métodos de aplicação de política fornecidos pelos recursos da Governança de dados na Plataforma, na aplicação baseada em API e na aplicação automática.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Visão geral da aplicação de políticas

Depois que os rótulos de uso de dados tiverem sido aplicados aos conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing em relação a esses rótulos, os recursos de Governança de dados do Adobe Experience Platform permitirão aplicar essas políticas e evitar operações de dados que constituam violações de política.

Há dois métodos de aplicação de política fornecidos pelos recursos da Governança de dados em [!DNL Platform]: Aplicação baseada em API e aplicação automática.

## Aplicação baseada em API

O [!DNL Policy Service] A API fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos no aplicativo de experiência para impor adequadamente a conformidade da política de uso de dados.

Veja o tutorial em [Aplicação baseada em API](./api-enforcement.md) para obter etapas sobre como avaliar políticas usando a API.

## Aplicação automática

O Experience Platform aproveita a linhagem de dados, a classificação de dados e os recursos de gerenciamento de políticas para avaliar e exibir automaticamente as violações de políticas. Consulte a visão geral em [aplicação automática da política](./auto-enforcement.md) para obter mais informações.
