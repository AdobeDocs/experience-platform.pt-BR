---
title: setDebug
description: Ative ou desative a configuração de depuração do SDK da Web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

A variável `setDebug` permite entrar ou sair do modo de depuração no SDK da Web. É uma das várias opções disponíveis para [depuração](../use-cases/debugging.md). O Adobe aconselha ativar o modo de depuração em ambientes de desenvolvimento ou apenas em sua máquina local em ambientes de produção.

## Definir a depuração usando a extensão de tag do SDK da Web

A extensão de tag não oferece a capacidade de alternar opções de depuração na interface do usuário. Você pode usar o editor de código personalizado usando a sintaxe JavaScript ou inserir o código JavaScript no console do navegador enquanto estiver no site.

## Definir a depuração usando a biblioteca JavaScript do SDK da Web

Execute o `setDebug` ao chamar a instância configurada do SDK da Web. A única opção no objeto de configuração é `enabled`, que é um booleano que determina se o modo de depuração está ativado.

```js
alloy("setDebug", {"enabled": true});
```
