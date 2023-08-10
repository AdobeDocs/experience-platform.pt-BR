---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;identidade;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados de identidade
description: Este documento fornece uma visão geral do tipo de dados XDM de identidade.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 4%

---

# [!UICONTROL Identidade] tipo de dados

[!UICONTROL Identidade] é um tipo de dados XDM padrão usado para distinguir claramente as pessoas que estão interagindo com experiências digitais. A identidade é estabelecida por um provedor de identidade, que é referenciado em uma `namespace` atributo. Em cada `namespace`, a identidade é única.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `namespace` | Objeto | Um objeto que contém um único campo de string (`code`), que indica o namespace associado ao `id` atributo. |
| `authenticatedState` | String | O estado autenticado para esta identidade no momento do Evento de experiência observado. Consulte a [apêndice](#authenticatedState) para obter valores e definições aceitos. |
| `id` | String | A identidade do consumidor no namespace relacionado. |
| `primary` | Booleano | Indica se esta é a identidade principal do indivíduo. Cada indivíduo só pode ter uma identidade principal. |
| `xid` | String | Quando presente, esse valor representa um identificador de namespace cruzado que é exclusivo em todos os identificadores de escopo de namespace em todos os namespaces. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Apêndice

A seção a seguir contém informações adicionais sobre o [!UICONTROL Identidade] tipo de dados.

## Valores aceitos para authenticatedState {#authenticatedState}

A tabela a seguir descreve os valores aceitos para `authenticatedState` e significados associados:

| Valor | Descrição |
| --- | --- |
| `ambiguous` | O estado autenticado é ambíguo. |
| `authenticated` | O usuário foi identificado por um logon ou uma ação semelhante que era válida no momento da observação do evento. |
| `loggedOut` | O usuário foi identificado por uma ação de logon em algum momento anterior, mas não estava conectado no momento da observação do evento. |
