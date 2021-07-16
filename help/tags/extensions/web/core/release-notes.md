---
title: Notas de versão da extensão principal
description: As notas de versão mais recentes da extensão principal no Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 90%

---

# Notas de versão da extensão principal

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 20 de maio de 2021

v2.0.7

* Corrige um problema em que as interações do mouse em Entradas de texto não funcionavam mais corretamente.
* Substitui o uso das condições do Navegador e do Sistema operacional.

## 4 de maio de 2021

v2.0.6

* Pequena atualização para corrigir ícones que ficam distorcidos quando o tamanho da tela muda.

## 11 de março de 2021

v2.0.5

* Atualização do código na avaliação de tempo de execução para eventos e ações que têm uma opção de atraso, que agora aceitam valores de elementos de dados adicionados na versão v2.0.4, para forçar sequências de caracteres corretamente a números.

## 9 de março de 2021

v2.0.4

* Adição de Suporte ao elemento de dados para vários campos - O suporte ao elemento de dados foi adicionado aos seguintes eventos: &quot;Tempo na página&quot;, &quot;Insere Viewport&quot;, &quot;Passe o mouse&quot; e &quot;Tempo de mídia reproduzido&quot;. Além das seguintes condições: &quot;Tempo no site&quot; e &quot;Comparação de valores&quot;
* Adiciona suporte para comportamento padrão para ctrl/cmd + clique e clique do meio do mouse ao usar o atraso de link
* **Atraso de link marcado no evento de clique como &quot;não é mais compatível&quot;.** - mais informações podem ser encontradas no  [Data Collection ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) Blogfor Adobe Experience Platform

## 6 de janeiro de 2021

v1.9.0

* **Nova ação &quot;Acionar chamada direta&quot;** - a extensão principal agora inclui um novo tipo de ação chamado `Trigger Direct Call`. Isso pode ser usado quando você deseja acionar uma regra de chamada direta por meio de uma ação de uma regra diferente. Ela é mapeada diretamente para o método `_satellite.track()`. Muito obrigado a [Jan Exner](https://twitter.com/jexner) por esta contribuição.

## 8 de dezembro de 2020

v1.8.4

* Correção de um bug em que um usuário não conseguia limpar ou não definir o nonce CSP.

## 28 de julho de 2020

v1.8.3

* Correção de um bug em que o nonce do CSP era lido somente uma vez na inicialização da extensão em vez de ser reproduzido durante a invocação da ação de código personalizado.

## 13 de julho de 2020

v1.8.2

* Correção de um bug em que a ação de código personalizado gerava um erro para o código HTML que contém tokens sem um nome de tag (por exemplo, comentários).

## 10 de julho de 2020

v1.8.1

* Correção de um erro em que entidades HTML personalizadas dentro de atributos de `script` e tags `style` não eram decodificadas corretamente antes de serem gravadas na página.
* Correção de um erro que ocorria quando uma ação de código personalizado externo não tinha conteúdo. A ação de código personalizado externo é a ação carregada de um arquivo diferente da biblioteca (isso acontece quando o evento que aciona a regra não é libraryLoaded ou pageBottom)

## 6 de julho de 2020

v1.8.0

* **Promessas no Custom Code** - as condições Custom Code e as ações JavaScript que não são executadas no escopo global agora podem retornar Promessas. É possível usá-las para que as condições e ações subsequentes aguardem a conclusão de um processo assíncrono no Custom Code antes de avançar para o próximo item.
* **Retornos de chamada em ações Custom Code HTML** - você pode obter a mesma coisa em ações Custom Code HTML usando os retornos de chamada `onCustomCodeSuccess()` e `onCustomCodeFailure()`.

Consulte a [referência da Extensão principal](./overview.md) em Conditions > Custom Code and Actions > Custom Code para obter informações mais detalhadas.

## 7 de abril de 2020

v1.7.3

* **Aumento do comprimento do campo de texto** - Os campos de entrada de texto foram alterados para um layout flexível, a fim de melhor utilizar a largura da tela do usuário e fornecer mais espaço para sequências de texto mais longas.

## 1 de novembro de 2019

v1.7.0

* **Acesso à `event` Variável dentro do elemento de dados Custom Code** - agora você pode fazer referência ao evento a partir de um elemento de dados de código personalizado quando executado no contexto de uma regra. O objeto conterá informações úteis sobre o evento que acionou a regra. Muito obrigado a [Stewart Schilling](https://twitter.com/sdi_stewart) pela sua contribuição.

## 7 de outubro de 2019

v1.6.2

* **Novo tipo de elemento de dados “constante”** - A extensão principal agora inclui um novo elemento de dados chamado `Constant`. Isso pode ser usado quando você precisa armazenar um valor constante que será referenciado em várias condições, ações ou códigos personalizados. Muito obrigado a [Jan Exner](https://twitter.com/jexner) por esta contribuição.

## 11 de setembro de 2019

v1.6.1

* **Suporte para CSP Nonce** - a extensão principal agora tem um parâmetro de configuração opcional. Você pode adicionar um elemento de dados que faça referência a um nonce. Se configurado, todos os scripts incorporados adicionados por uma tag à página usarão o nonce que você configurou. Essa alteração aceita o uso de uma Política de segurança de conteúdo com um nonce para que os scripts do Platform Launch ainda possam ser carregados em um ambiente CSP. Você pode ler mais sobre como usar o Platform Launch com um CSP [aqui](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/content-security-policy.html).

## 18 de junho de 2019

v1.5.0

* **Registro de chamada direta** - O registro do Navegador para regras de chamada direta agora fornecerá detalhes adicionais quando for passado.

## 8 de maio de 2019

v1.4.3

* **Campos de entrada** - Os campos de entrada agora são muito maiores!
* **Custom Event** - O tipo de evento personalizado agora pode ser usado com eventos despachados fora da janela.
* **Correção de erros** - Corrigido um erro no qual a condição Value Comparison não possuía um valor 0.
* **Correção de erros** - O campo exchange\_url foi atualizado para que você possa ver a listagem da extensão principal no Adobe Exchange.

## 8 de janeiro de 2019

v1.4.2

* **Evento Enters Viewport** - Anteriormente, o evento Enters Viewport só era disparado uma vez por página. Esse comportamento pode ser configurado para ser acionado sempre que o elemento entrar no viewport.
* **Custom Event** - Os eventos personalizados agora podem conter dados contextuais que podem ser usados dentro de condições e ações.
* **Evento Click** - Ao definir um atraso de link no evento Click, essa função agora faz corretamente o registro para descendentes da âncora e não apenas na âncora propriamente dita.

## 8 de novembro de 2018

* **Opção Persisti Cohort** - A opção para persistir uma cohort foi adicionada à condição de amostragem. Essa opção tem o efeito de manter um usuário dentro ou fora da coorte de amostra nas sessões. Por exemplo, se a caixa de seleção “persist cohort” estiver marcada e a condição retornar &quot;true&quot; na primeira vez em que for executada para um determinado visitante, ela retornará &quot;true&quot; em todas as execuções subsequentes da condição para o mesmo visitante. Da mesma forma, se a caixa de seleção “persist cohort” estiver marcada e a condição retornar &quot;false&quot; na primeira vez em que for executada para um determinado visitante, ela retornará &quot;false&quot; em todas as execuções subsequentes da condição para o mesmo visitante.
* **Correção de erros**  - Correção de um problema em que uma regra que utiliza um evento Page Bottom e uma ação Custom Code em uma página em que as tags estavam sendo carregadas de forma síncrona, mas instaladas incorretamente (sem chamada para  `_satellite.pageBottom()`), limpava o conteúdo do site.
* **Correção de erros**  - Corrigido um problema em que a opção Inserir Viewport não funcionava se a biblioteca de tags fosse carregada de forma assíncrona e terminasse de ser carregada após o evento DOMContentLoaded do navegador ser disparado.

## 24 de maio de 2018

* **Recurso** - Adicionada uma condição Value Comparison, essa comparação compara dois valores usando qualquer um dos vários sinais de operação disponíveis. Isso substitui a funcionalidade de várias condições mais antigas que eram muito específicas.
* **Recurso** - Adição de uma condição Max Frequency; essa condição permite especificar o número de vezes que a condição deve retornar “true” dentro de um período ou ocorrência de evento. Exemplos: 5 vezes por dia, 2 vezes por visita.

## 11 de abril de 2018

* **Recurso** - Os elementos de dados agora podem fazer referência a outros elementos de dados.

## 20 de março de 2018

* **Correção de erros** - As janelas Custom Code estavam gerando erros de `document.write` e não executavam em implantações assíncronas
* **Correção de erros** - Os módulos principais não foram incluídos em uma biblioteca
* **Correção de erros** - Problemas com valores mín. e máx. no elemento de dados chamado Número aleatório

## 10 de janeiro de 2018

* **Recurso** - Elemento de dados Número aleatório
* **Recurso** - Elemento de dados Informações da página
* **Recurso** - Condição Date
* **Recurso** - Condição de amostragem
