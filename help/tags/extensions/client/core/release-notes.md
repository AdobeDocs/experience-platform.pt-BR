---
title: Notas de versão da extensão principal
description: As notas de versão mais recentes da extensão principal no Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 1dab2b2778844ac08c1fbc013405dc81fa7dc0b5
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 58%

---

# Notas de versão da extensão principal

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 25 de setembro de 2025

v3.4.4

* Adicione o campo `releaseNotesUrl` ao extension.json com esta página como o valor.
* Dependências de auditoria.
* Remova o Yarn e alinhe o processo de criação com nossos outros repositórios de código aberto.


## 8 de maio de 2025

v3.4.3

* Corrige um problema em que **Elementos de Dados** > **Ferramentas de Javascript** > **Substituição Simples** mostra uma caixa de seleção para **Substituir Tudo**, mas causa um erro ao tentar salvar a Regra com a caixa de seleção ativada.
* Atualiza @adobe/react-spectrum para v3.41.0.
* Atualiza @adobe/reator-sandbox para v13.2.1.

## 23 de outubro de 2024

v3.4.2

* Corrigir erro de validação de esquema para o evento Formulário -> Alterar quando &quot;e tendo determinados valores de propriedade...&quot; estiver ativo.

## 29 de março de 2023

v3.4.1

* Adiciona novos eventos delegados nativos da Web:
   * Pressionar tecla
   * KeyUp
* Adiciona a capacidade de testar em relação a muitos valores (opções &quot;Adicionar outro&quot;) em relação aos seguintes delegados:
   * Eventos
      * Alterar
   * Condições
      * Cookie
      * Página de destino
      * Query String Parameter
      * Traffic Source
      * Variable
* Altera o representante events/EntersViewport para usar a [API de Observador de Interseção](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) em vez da detecção manual de elementos que entram no visor.
* Remove o código que estava migrando cookies do DTM para o LocalStorage.
* Registra um aviso no console quando as APIs LocalStorage e SessionStorage não estão disponíveis.

## 4 de janeiro de 2022

v3.3.0

* Altera a [ação de Acionar Chamada Direta](./overview.md#direct-call-action) para que você possa fornecer informações de evento personalizadas para enviar a regras de chamada direta.

## 8 de outubro de 2021

v3.2.2

* Corrija o esquema JSON do elemento de dados de valor condicional para todos os operadores disponíveis.
* Corrigir https://github.com/adobe/reactor-extension-core/issues/64.

## 23 de setembro de 2021

v3.2.1

* Correção de um erro em que a inicialização da exibição do elemento de dados do valor condicional não funcionava corretamente quando os valores do campo eram 0.

## 23 de setembro de 2021

v3.2.0

As seguintes alterações foram introduzidas no elemento de dados Valor condicional:

* Adicione uma caixa de seleção para os valores condicional e de fallback que permita ao usuário escolher se deseja que indefinido seja o valor retornado.
* Os valores numéricos são expostos como números no objeto de configurações.
* O valor condicional não é mais necessário para que possa se comportar da mesma maneira que o valor de fallback.

## 17 de setembro de 2021

v3.1.1

* Correção de um erro JS que impedia que a exibição de condição do intervalo de datas fosse carregada.

## 16 de setembro de 2021

v3.1.0

Novos elementos de dados foram adicionados:

* Objeto mesclado - Selecione vários elementos de dados que fornecerão um objeto. Esses objetos serão profundamente (recursivamente) mesclados para produzir um novo objeto.
* Valor condicional - Retorna um dos dois valores (conditionalValue ou fallbackValue) com base no resultado da comparação.
* Ambiente de tempo de execução - Retorna uma das seguintes variáveis de ambiente do Launch: estágio do ambiente, data de criação da biblioteca, nome da propriedade, ID da propriedade, nome da regra, ID da regra, tipo de evento, carga de detalhes do evento, identificador de chamada direta.
* Ferramentas do JavaScript - Wrapper para operações comuns do JavaScript: manipulação básica de string (replace, substring, regex match, first e last index, split, slice), operações básicas de array (slice, join, pop, shift) e operações universais básicas (slice, length).
* Atributos do dispositivo - Retorna atributos do dispositivo como tamanho da janela ou tamanho da tela.

## 11 de agosto de 2021

v3.0.0

* PDCL-6153: adiciona suporte para obter de forma confiável o URL totalmente qualificado para ações de código personalizado em cache.

A v3.0.0 da Extensão principal é combinada com alterações no [v27.2.0 do tempo de execução da Web do Turbine](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), que permite que os usuários carreguem sua biblioteca entre muitas regiões de hospedagem gerenciadas pela Adobe se a empresa do usuário oferecer suporte à CDN Premium.

Essa atualização é opcional e compatível com versões anteriores para usuários sem a CDN Premium e obrigatória para clientes que têm a CDN Premium ativada em suas empresas.

## 20 de maio de 2021

v2.0.7

* Corrige um problema em que as interações do mouse em Entradas de texto não funcionavam mais corretamente.
* Substitui o uso das condições do Navegador e do Sistema operacional.

## 4 de maio de 2021

v2.0.6

* Pequena atualização para corrigir ícones que ficam distorcidos quando o tamanho da tela muda.

## 11 de março de 2021

v2.0.5

* Atualização do código na avaliação de tempo de execução para eventos e ações que têm uma opção de atraso, que agora aceitam valores de elementos de dados adicionados na versão v2.0.4, para forçar strings corretamente a números.

## 9 de março de 2021

v2.0.4

* Adição de Suporte ao elemento de dados para vários campos - O suporte ao elemento de dados foi adicionado aos seguintes eventos: &quot;Tempo na página&quot;, &quot;Insere Viewport&quot;, &quot;Passe o mouse&quot; e &quot;Tempo de mídia reproduzido&quot;. Além das seguintes condições: &quot;Tempo no site&quot; e &quot;Comparação de valores&quot;
* Adiciona suporte para comportamento padrão para ctrl/cmd + clique e clique do meio do mouse ao usar o atraso de link
* **Atraso de link marcado no evento de clique como &quot;não é mais suportado&quot;.** — mais informações podem ser encontradas no [Blog de coleção de dados](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) da Adobe Experience Platform

## 6 de janeiro de 2021

v1.9.0

* **Nova Ação &quot;Acionar Chamada Direta&quot;** - A extensão Principal agora inclui um novo tipo de ação chamado `Trigger Direct Call`.  Isso pode ser usado quando você deseja acionar uma regra de chamada direta por meio de uma ação de uma regra diferente. Ela é mapeada diretamente para o método `_satellite.track()`. Muito obrigado a Jan Exner por esta contribuição.

## 8 de dezembro de 2020

v1.8.4

* Correção de um erro em que um usuário não conseguia limpar ou não definir o nonce CSP.

## 28 de julho de 2020

v1.8.3

* Correção de um erro em que o nonce do CSP era lido somente uma vez na inicialização da extensão em vez de ser reproduzido durante a invocação da ação de código personalizado.

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

* **Acesso à `event` Variável dentro do elemento de dados Custom Code** - agora você pode fazer referência ao evento a partir de um elemento de dados de código personalizado quando executado no contexto de uma regra. O objeto conterá informações úteis sobre o evento que acionou a regra. Muito obrigado a Stewart Schilling pela sua contribuição.

## 7 de outubro de 2019

v1.6.2

* **Novo tipo de elemento de dados &quot;constante&quot;** - A extensão principal agora inclui um novo elemento de dados chamado `Constant`.  Isso pode ser usado quando você precisa armazenar um valor constante que será referenciado em várias condições, ações ou códigos personalizados. Muito obrigado a Jan Exner por esta contribuição.

## 11 de setembro de 2019

v1.6.1

* **Suporte para CSP Nonce** - a extensão principal agora tem um parâmetro de configuração opcional. Você pode adicionar um elemento de dados que faça referência a um nonce. Se configurado, todos os scripts incorporados adicionados pela tag à página usarão o nonce que você configurou. Essa alteração aceita o uso de uma Política de segurança de conteúdo com um nonce para que os scripts de tag ainda possam ser carregados em um ambiente CSP. Você pode ler mais sobre como usar marcas com um CSP [aqui](../../../ui/client-side/content-security-policy.md).

## 18 de junho de 2019

v1.5.0

* **Registro de chamada direta** - O registro do Navegador para regras de chamada direta agora fornecerá detalhes adicionais quando for passado.

## 8 de maio de 2019

v1.4.3

* **Campos de entrada** - Os campos de entrada agora são muito maiores!
* **Evento personalizado** - O tipo de evento personalizado agora pode ser usado com eventos despachados fora da janela.
* **Correção de erros** - Corrigido um erro no qual a condição de comparação de valores não possuía um valor 0.
* **Correção de erros** - O campo exchange\_url foi atualizado para que você possa ver a listagem da extensão principal no Adobe Exchange.

## 8 de janeiro de 2019

v1.4.2

* **Evento Enters Viewport** - Anteriormente, o evento Enters Viewport só era acionado uma vez por página. Esse comportamento pode ser configurado para ser acionado sempre que o elemento entrar no viewport.
* **Custom Event** - Os eventos personalizados agora podem conter dados contextuais que podem ser usados dentro de condições e ações.
* **Evento Click** - Ao definir um atraso de link no evento Click, essa função agora faz corretamente o registro para descendentes da âncora e não apenas na âncora propriamente dita.

## 8 de novembro de 2018

* **Opção Persisti Cohort** - A opção para persistir uma cohort foi adicionada à condição de amostragem. Essa opção tem o efeito de manter um usuário dentro ou fora da coorte de amostra nas sessões. Por exemplo, se a caixa de seleção &quot;persist cohort&quot; estiver marcada e a condição retornar &quot;true&quot; na primeira vez em que for executada para um determinado visitante, ela retornará &quot;true&quot; em todas as execuções subsequentes da condição para o mesmo visitante. Da mesma forma, se a caixa de seleção &quot;persist cohort&quot; estiver marcada e a condição retornar &quot;false&quot; na primeira vez em que for executada para um determinado visitante, ela retornará &quot;false&quot; em todas as execuções subsequentes da condição para o mesmo visitante.
* **Correção de erros** — foi corrigido um problema em que uma regra que usava um evento Page Bottom e uma ação de código personalizado em uma página em que tags estavam sendo carregadas sincronicamente, mas estavam incorretamente instaladas (sem chamada para `_satellite.pageBottom()`) limpava o conteúdo do site.
* **Correção de erros** - Corrigido um problema em que a opção Enters Viewport não funcionava se a biblioteca de marcas fosse carregada de forma assíncrona e terminasse de ser carregada após o evento DOMContentLoaded do navegador ser disparado.

## 24 de maio de 2018

* **Recurso** - Adicionada uma condição Value Comparison, essa comparação compara dois valores usando qualquer um dos vários operadores disponíveis. Isso substitui a funcionalidade de várias condições mais antigas que eram muito específicas.
* **Recurso** - Adição de uma condição Frequência máx.; essa condição permite especificar o número de vezes que a condição deve retornar “true” dentro de um período ou ocorrência de evento. Exemplos: 5 vezes por dia, 2 vezes por visita.

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
