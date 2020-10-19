---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de identidade
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de identidade.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---


# [!UICONTROL Tipo de dados de identidade]

[!UICONTROL A identidade] é um tipo de dados XDM padrão que é usado para distinguir claramente as pessoas que estão interagindo com experiências digitais. A identidade é estabelecida por um provedor de identidade, que é referenciado em um `namespace` atributo. Dentro de cada `namespace`, a identidade é única.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `namespace` | Objeto | Um objeto que contém um único campo de string (`code`), que indica a namespace associada ao `id` atributo fornecido. |
| `authenticatedState` | String | O estado autenticado para essa identidade no momento do Evento de experiência observado. Consulte o [apêndice](#authenticatedState) para ver os valores e definições aceites. |
| `id` | String | A identidade do consumidor na namespace relacionada. |
| `primary` | Booleano | Indica se esta é a identidade primária do indivíduo. Cada indivíduo só pode ter uma identidade primária. |
| `xid` | String | Quando presente, esse valor representa um identificador de namespace cruzada que é exclusivo em todos os identificadores com escopo de namespace em todas as namespaces. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados de [!UICONTROL Identidade] .

## Valores aceitos para authenticatedState {#authenticatedState}

A tabela a seguir descreve os valores aceitos para `authenticatedState` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `ambiguous` | O estado autenticado é ambíguo. |
| `authenticated` | O usuário foi identificado por um logon ou ação semelhante válida no momento da observação do evento. |
| `loggedOut` | O usuário foi identificado por uma ação de logon em algum momento anterior, mas não estava conectado no momento da observação do evento. |