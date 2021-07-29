---
title: Notas de versão da extensão do Adobe Target
description: As notas de versão mais recentes para a extensão de tag do Adobe Target no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 74%

---

# Notas de versão do Adobe Target

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 24 de julho de 2020

### Extensão do Adobe Target 0.11.3

* Correção de um erro quando a extensão falhava se um script ou código adicionasse uma propriedade `default` ao `window` ou `document`

## 15 de junho de 2020

### Extensão do Adobe Target 0.11.2

* Correção de um problema ao usar a substituição de CNAME e borda, em que o at.js 1.x poderia criar incorretamente o domínio do servidor, resultando na falha da solicitação do Target.

## 25 de março de 2020

### Extensão do Adobe Target 0.11.1

* Atualização do at.js para v1.8.1.
* Correção de um problema em que os parâmetros e os parâmetros de carregamento de página não eram processados corretamente.

## 10 de outubro de 2019

### Extensão do Adobe Target 0.11.0

* Atualização do at.js para v1.8.
* Desempenho aprimorado para integrações entre a biblioteca da Experience Cloud ID (ECID) v4.4 e o at.js 1.8.
* Anteriormente, a biblioteca ECID fez duas chamadas de bloqueio antes que o at.js pudesse buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.

>[!NOTE]
>Atualize sua extensão de tag da ECID para Adobe Experience Platform para v4.4.1 para aproveitar esse aprimoramento de desempenho.

## 31 de julho de 2019

### Extensão do Adobe Target 0.10.1

* Hotfix de parâmetros que manipulam a extensão de tag para Adobe Target

## 4 de maio de 2019

### Extensão do Adobe Target 0.10.0

* Correção de um problema em elementos de dados causado pelas alterações mais recentes do Google Chrome.

## 14 de março de 2019

### Extensão do Adobe Target 0.9.3

* Versão de extensão atualizada para usar at.js 1.7.1.

## 20 de fevereiro de 2019

### Extensão do Adobe Target 0.9.2

* Condições de corrida entre as extensões do Target e do Analytics corrigidas.

## 12 de fevereiro de 2019

### Extensão do Adobe Target 0.9.1

#### **Recursos**

* Extensão atualizada para usar a at.js 1.7.0, que tem funcionalidade de privacidade de Opt-in compatível por meio de tags para controlar como e quando a tag do Target é acionada. Verifique a documentação das tags sobre como configurar a implementação do Opt-in. Adicionada a possibilidade de personalizar se um parâmetro de mBox com valor vazio deve ser enviado para o Target ou não.

## 23 de janeiro de 2019

### Extensão do Adobe Target 0.8.4

* Atualização do at.js para a versão 1.6.4.
* A interface de usuário da extensão migrada para o Adobe Spectrum.

## 15 de novembro de 2018

### Extensão do Adobe Target 0.8.2

* Atualização do at.js para a versão 1.6.3.

## 24 de outubro de 2018

### Extensão do Adobe Target 0.8.1

* Atualização do at.js para a versão 1.6.2.

## 23 de agosto de 2018

### Extensão do Adobe Target 0.8.0

* Atualização do at.js para a versão 1.6.0.

## 10 de agosto de 2018

### Extensão do Adobe Target 0.7.2

* Pequenas alterações
* Atualização da `exchangeUrl` propriedade no `extension.json` arquivo.

## 1 de agosto de 2018

### Extensão do Adobe Target 0.7.1

* Correções secundárias.

## 18 de junho de 2018

### Extensão do Adobe Target 0.7.0

* Atualização da versão do at.js para 1.5.0.
* Corrigido um problema no qual o Media Optimizer exibia um erro de referência nula no IE 11.

## 15 de junho de 2018

### Extensão do Adobe Target 0.6.0

#### **Recursos**

* A extensão do Target foi atualizada para usar o at.js v1.3.1. Quando você implanta o Target com o Analytics, agora aguardamos até que todas as chamadas do Target tenham sida resolvidas (incluindo ofertas de redirecionamento) antes que o Analytics seja acionado, solucionando a condição de corrida que existia anteriormente.

## 22 de fevereiro de 2018

### Extensão do Adobe Target 0.4.1

#### **Recursos**

* Adição da listagem do Adobe Exchange ao extension.json.
* Adicionamos verificações para ver se o Target está desativado e se a Autoria está ativada.

#### **Correções de erros**

* Correção de um erro na extensão Adobe Target que impedia o Visual Experience Composer de mostrar a página quando implantada por meio de tags.

## 8 de fevereiro de 2018

### Extensão do Adobe Target 0.4.0

#### **Recursos**

* Exibições atualizadas nas telas de configuração de extensão.
* O at.js foi atualizado para a versão 1.2.3 (adiciona suporte para ofertas JSON).
