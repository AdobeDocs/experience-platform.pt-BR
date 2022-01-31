---
title: Notas de versão da extensão do Adobe Target v2
description: As mais recentes notas de versão de extensão de tag do Adobe Target v2 na Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 824fea41bc7e7082814648efd58184f5208e5e6f
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 70%

---

# Notas de versão da extensão do Adobe Target v2

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 28 de janeiro de 2022

### Extensão 0.17.1 do Adobe Target v2

- Atualizado para suporte `at.js` v2.8.1
- Fixo `pageLoad` não está sendo mapeado para `target-global-mbox` no modo de execução híbrida ODD
- Correção de um problema com detalhes de análises para `mbox` solicitação
- Dependências de desenvolvimento atualizadas para corrigir vulnerabilidades de segurança

## 7 de janeiro de 2022

### Extensão 0.17.0 do Adobe Target v2

- Atualizado para suporte `at.js` v2.8.0, que agora está coletando dados de uso de recursos e telemetria de desempenho.  Os dados pessoais não são coletados. Para recusar esse recurso, defina `telemetryEnabled` para `false` em `targetGlobalSettings`.

## 28 de outubro de 2021

### Extensão 0.16.0 do Adobe Target v2

- Atualizado para suporte `at.js` v2.7.0, agora disponível para download no Adobe Target.

## 20 de julho de 2021

### Extensão 0.15.1 do Adobe Target v2

- Correção de um problema com um conflito de nome de função `stringify`, que resultava na geração de valores UUID incorretos para `sessionId`, `requestId` e assim por diante.

## 16 de julho de 2021

### Extensão 0.15.0 do Adobe Target v2

- Adicionar atributo seguro aos cookies sempre que `at.js` settings secureOnly está definido como true
- Os tokens de resposta agora estão disponíveis ao usar o `triggerView()`
- Correção de um erro relacionado ao evento `CONTENT_RENDERING_NO_OFFERS`. Agora é acionado corretamente sempre que não há conteúdo retornado do Target
- Os detalhes das métricas de clique do A4T são retornados corretamente ao serem usadas solicitações de pré-busca
- A geração UUID não usa mais `Math.random()`, mas depende de `window.crypto`
- A expiração do cookie `sessionId` é estendida corretamente em cada chamada de rede
- A inicialização do cache de visualização de SPA agora é realizada corretamente e atende às configurações `viewsEnable`

## 2 de junho de 2021

### Extensão 0.14.2 do Adobe Target v2

- Correção de um erro em que o pacote final contém dois `at.js` , uma com o On-Device Decisioning e outra sem.

## 19 de maio de 2021

### Extensão 0.14.1 do Adobe Target v2

- Corrigir regressão introduzida com a versão v0.14, em que a ação Carregar Target disparava chamadas de mbox globais

## 14 de maio de 2021

### Extensão 0.14 do Adobe Target v2

- Adição de uma nova ação Carregar o Target com a [Decisão no dispositivo](./overview.md#load-target-with-on-device-decisioning), que carrega a 2.5 com recursos da Decisão no dispositivo.`at.js`
- Atualizado `at.js` a 2.5


## 25 de março de 2021

### Extensão 0.13.7 do Adobe Target v2

- Correção de um problema em que `targetPageParams` era incluído nas solicitações da mBox. `targetPageParams` deve ser incluído somente em solicitações `pageLoad`.
- Correção de um problema em documentos e objetos globais de janela na extensão de tag substituindo as dependências de objetos globais por referências diretas a eles.
- Atualizado `at.js` a 2.4.1.

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
- Atualização do `at.js` versão para 2.3.3

## 24 de julho de 2020

### Extensão 0.13.3 do Adobe Target v2

- Correção de um erro que fazia com que os links do modo de QA não funcionassem para atividades inativas
- Correção de um erro quando a extensão falhava se um script ou código adicionasse uma propriedade `default` ao `window` ou `document`

## 15 de junho de 2020

### Extensão 0.13.2 do Adobe Target v2

- Correção de um problema ao usar a substituição de CNAME e borda, em que `at.js` A 1.x pode criar o domínio do servidor incorretamente, resultando na falha da solicitação do Target
- Correção de um problema em que, ao ser usada a extensão de tag v2 para a extensão de tag do Target e do Adobe Analytics, o Target atrasava a chamada de sendBeacon do Analytics.
- Aprimoramento da configuração `deviceIdLifetime` ao torná-la substituível via `targetGlobalSettings`.

## 25 de março de 2020

### Extensão 0.13.0 do Adobe Target v2

- Atualizado `at.js` para v2.3.
- Adição de suporte à Mbox global do Target na API adobe.target.getOffer.
- Correção de um problema em que os parâmetros e os parâmetros de carregamento de página não eram processados corretamente.

## 10 de outubro de 2019

### Extensão 0.12.0 do Adobe Target v2

- Atualizado `at.js` para v2.2.
- Desempenho aprimorado para integrações entre a biblioteca de Experience Cloud ID (ECID) v4.4 e `at.js` 2.2.
- Anteriormente, a biblioteca ECID fazia duas chamadas de bloqueio antes `at.js` O pode buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.

>[!NOTE]
>Atualize sua extensão de tag do ECID para v4.4.1 para aproveitar esse aprimoramento de desempenho.

## 31 de julho de 2019

### Extensão 0.11.1 do Adobe Target v2

- Versão de extensão atualizada para usar `at.js` 2.1.1.
- Adição de uma correção para manipulação de parâmetros.

## 3 de junho de 2019

### Extensão 0.11.0 do Adobe Target v2

- Nova extensão de tag para oferecer suporte a `at.js` 2.1.
