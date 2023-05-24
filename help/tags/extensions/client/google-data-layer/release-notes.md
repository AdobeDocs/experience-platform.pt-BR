---
title: Notas de versão da extensão de camada de dados do Google
description: As notas de versão mais recentes da extensão de tag da Camada de dados da Google na Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Notas de versão da extensão da Camada de dados do Google

## Versão 1.0.4

* Versão beta pública da extensão.

## Versão 1.0.6

* Adição de ação para redefinir a camada de dados para o estado calculado.
* Corrigir bugs no elemento de dados que impedem a busca de valores do estado calculado.

## Versão 1.1.1

Um aprimoramento significativo e uma versão de correção de erros resultante do feedback de teste beta.

* Correção de um problema em que um elemento de dados vazio da Extensão de camada de dados do Google usado em uma regra de camada que não seja de dados (por exemplo, Biblioteca carregada) retornava o objeto da camada de dados, não o estado calculado.
* Correção de um problema em que o estado calculado da camada de dados não era transmitido pelo auxiliar nos eventos no momento do acionamento do evento, mas sim no momento da execução da regra.
* Adiciona um botão à caixa de diálogo Elemento de dados, que permite ao usuário escolher se somente os valores dos eventos devem ser retornados.
* Corrige um problema em que o histórico de eventos não era capturado corretamente pelos ouvintes de eventos da regra.
* Pequenas melhorias na clareza do código.

## Versão 1.2.0

* Adiciona uma ação para encaminhar para a camada de dados usando uma caixa de diálogo de vários campos de valor chave.
* Correção de um erro que impedia o carregamento da extensão quando as tags eram implantadas de forma síncrona.
* Correção de um erro que causava um erro ao salvar um elemento de dados em algumas circunstâncias.
* Adiciona documentação à caixa de diálogo do evento explicando o uso do objeto de evento Tags.
* Adiciona um aviso sobre loops infinitos à caixa de diálogo de eventos.
