---
title: Notas de versão da extensão da camada de dados da Google
description: As notas de versão mais recentes para a extensão de tag da Camada de dados da Google no Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Notas de versão da extensão da camada de dados da Google

## Versão 1.0.4

* Versão beta pública da extensão.

## Versão 1.0.6

* Adição de ação para redefinir a camada de dados para o estado calculado.
* Corrija bugs no elemento de dados que impedem a busca de valores do estado calculado.

## Versão 1.1.1

Um aprimoramento significativo e uma versão de correção de bug resultante de comentários de testes beta.

* Corrige um problema no qual um elemento de dados vazio da Extensão da camada de dados do Google usado em uma regra de camada que não é de dados (por exemplo, Biblioteca carregada) retornava o objeto da camada de dados, não o estado calculado.
* Corrige um problema em que a camada de dados do estado computado não era passada do auxiliar nos eventos no momento do acionamento do evento, mas no momento da execução da regra.
* Adiciona um botão na caixa de diálogo do elemento de dados que permite que o usuário escolha se apenas valores de eventos devem ser retornados.
* Corrige um problema no qual o histórico de eventos não foi capturado corretamente pelos ouvintes de eventos da regra.
* Pequenas melhorias na clareza do código.

## Versão 1.2.0

* Adiciona uma ação para encaminhar para a camada de dados usando uma caixa de diálogo de vários campos de valor-chave.
* Corrige um erro que evitava o carregamento da extensão quando as Tags eram implantadas sincronicamente.
* Corrige um erro que causava um erro ao salvar um elemento de dados em algumas circunstâncias.
* Adiciona documentação à caixa de diálogo de evento explicando o uso do objeto de evento Tags.
* Adiciona um aviso sobre loops infinitos na caixa de diálogo do evento.
