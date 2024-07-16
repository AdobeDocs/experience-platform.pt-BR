---
title: setDebug
description: Ative ou desative a configuração de depuração do SDK da Web.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

O comando `setDebug` permite entrar ou sair do modo de depuração no SDK da Web. É uma das várias opções disponíveis para [depuração](../use-cases/debugging.md). O Adobe aconselha ativar o modo de depuração em ambientes de desenvolvimento ou apenas em sua máquina local em ambientes de produção.

## Definir a depuração usando a extensão de tag do SDK da Web

A extensão de tag não oferece a capacidade de alternar opções de depuração na interface do usuário. Você pode usar o editor de código personalizado usando a sintaxe do JavaScript ou inserir o código JavaScript no console do navegador enquanto estiver no site.

## Definir a depuração usando a biblioteca JavaScript do SDK da Web

Execute o comando `setDebug` ao chamar a instância configurada do SDK da Web. A única opção no objeto de configuração é `enabled`, que é um booleano que determina se o modo de depuração está habilitado.

```js
alloy("setDebug", {"enabled": true});
```
