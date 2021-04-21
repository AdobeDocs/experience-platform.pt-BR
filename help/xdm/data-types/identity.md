---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, identidade, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados de identidade
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de identidade.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 3%

---

# [!UICONTROL Identity] tipo de dados

[!UICONTROL Identity] é um tipo de dados XDM padrão usado para distinguir claramente as pessoas que interagem com experiências digitais. A identidade é estabelecida por um provedor de identidade, que é referenciado em um atributo `namespace`. Em cada `namespace`, a identidade é exclusiva.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `namespace` | Objeto | Um objeto que contém um único campo de string (`code`), que indica o namespace associado ao atributo `id` fornecido. |
| `authenticatedState` | String | O estado autenticado dessa identidade no momento do evento de experiência observado. Consulte o [apêndice](#authenticatedState) para obter os valores e as definições aceitos. |
| `id` | String | A identidade do consumidor no namespace relacionado. |
| `primary` | Booleano | Indica se esta é a identidade primária do indivíduo. Cada indivíduo só pode ter uma identidade primária. |
| `xid` | String | Quando presente, esse valor representa um identificador de namespace cruzado que é exclusivo em todos os identificadores de escopo de namespace em todos os namespaces. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o tipo de dados [!UICONTROL Identity] .

## Valores aceitos para authenticationState {#authenticatedState}

A tabela a seguir descreve os valores aceitos para `authenticatedState` e seus significados associados:

| Valor | Descrição |
| --- | --- |
| `ambiguous` | O estado autenticado é ambíguo. |
| `authenticated` | O usuário foi identificado por um login ou ação semelhante que era válida no momento da observação do evento. |
| `loggedOut` | O usuário foi identificado por uma ação de logon em algum ponto anterior, mas não foi conectado no momento da observação do evento. |
