---
title: Notas de versão da extensão do Adobe Target v2
description: As notas de versão mais recentes para a extensão de tag Adobe Target v2 no Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 78%

---

# Notas de versão da extensão do Adobe Target v2

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 19 de maio de 2021

### Extensão 0.14.1 do Adobe Target v2

- Corrigir regressão introduzida com a versão v0.14, em que a ação Carregar Target disparava chamadas de mbox globais

## 14 de maio de 2021

### Extensão 0.14 do Adobe Target v2

- Adição de uma nova ação Carregar o Target com a [Decisão no dispositivo](./overview.md#load-target-with-on-device-decisioning), que carrega a at.js 2.5 com recursos da Decisão no dispositivo.
- Atualização do at.js para 2.5


## 25 de março de 2021

### Extensão 0.13.7 do Adobe Target v2

- Correção de um problema em que `targetPageParams` era incluído nas solicitações da mBox. `targetPageParams` deve ser incluído somente em solicitações `pageLoad`.
- Correção de um problema com objetos globais document e window na extensão de tag ao substituir dependências de objetos globais por referências diretas a eles.
- Atualização do at.js para 2.4.1.

## 25 de janeiro de 2021

### Extensão 0.13.6 do Adobe Target v2

- Adiciona suporte à ID unificada de perfil/plataforma ao customerIds da API de entrega
- Corrige a injeção de tag de estilo inválida
- Atualização do at.s para 2.4.0.
- Solução de um problema em que parâmetros indefinidos podem resultar em solicitações de entrega incorretas

## 25 de novembro de 2020

### Extensão 0.13.4 do Adobe Target v2

- Correção de um erro em que os parâmetros da mBox não eram exibidos na interface
- Atualizações de marca
- Atualização da versão do at.js para 2.3.3

## 24 de julho de 2020

### Extensão 0.13.3 do Adobe Target v2

- Correção de um erro que fazia com que os links do modo de QA não funcionassem para atividades inativas
- Correção de um erro quando a extensão falhava se um script ou código adicionasse uma propriedade `default` ao `window` ou `document`

## 15 de junho de 2020

### Extensão 0.13.2 do Adobe Target v2

- Correção de um problema ao usar a substituição de CNAME e borda, em que o at.js 1.x poderia criar incorretamente o domínio do servidor, resultando na falha da solicitação do Target.
- Correção de um problema em que, ao usar a extensão de tag v2 para a extensão de tag do Target e do Adobe Analytics, o Target atrasava a chamada do sendBeacon do Analytics.
- Aprimoramento da configuração `deviceIdLifetime` ao torná-la substituível via `targetGlobalSettings`.

## 25 de março de 2020

### Extensão 0.13.0 do Adobe Target v2

- Atualização do at.js para v2.3.
- Adição de suporte à Mbox global do Target na API adobe.target.getOffer.
- Correção de um problema em que os parâmetros e os parâmetros de carregamento de página não eram processados corretamente.

## 10 de outubro de 2019

### Extensão 0.12.0 do Adobe Target v2

- Atualização do at.js para v2.2.
- Desempenho aprimorado para integrações entre a biblioteca da Experience Cloud ID (ECID) v4.4 e o at.js 2.2.
- Anteriormente, a biblioteca ECID fez duas chamadas de bloqueio antes que o at.js pudesse buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.

>[!NOTE]
>Atualize sua extensão de tag da ECID para v4.4.1 para aproveitar esse aprimoramento de desempenho.

## 31 de julho de 2019

### Extensão 0.11.1 do Adobe Target v2

- Versão de extensão atualizada para usar at.js 2.1.1.
- Adição de uma correção para manipulação de parâmetros.

## 3 de junho de 2019

### Extensão 0.11.0 do Adobe Target v2

- Nova extensão de tag para oferecer suporte ao at.js 2.1
