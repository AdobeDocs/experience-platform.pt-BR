---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Modelo de domínio de decisão de experiência
topic: overview
description: Nesta seção, os componentes do Serviço de tomada de decisão são explicados e as formas como esses componentes interagem são detalhados. Os conceitos e seus relacionamentos formam o *Domínio* do problema de decisão. Esses componentes fundamentais são acionados independentemente de como você usa o Serviço de tomada de decisão].
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---


# Modelo de domínio de experiência [!DNL Decisioning]

Nesta seção, os componentes de [!DNL Decisioning Service] são explicados e a forma como esses componentes interagem são detalhados. Os conceitos e suas relações formam o *Domínio* do problema de decisão. Esses componentes fundamentais entram em cena independentemente de como você usa [!DNL Decisioning Service].

## Opções de decisão

Uma opção *de* decisão de experiência é uma experiência potencial que pode ser apresentada a um cliente específico. Uma opção também é referida como uma escolha ou alternativa. Ao decidir a próxima melhor opção para um cliente, [!DNL Decisioning Service] considera as opções ***d<sub>1</sub>*** para ***<sub>dN</sub>*** entre um conjunto finito de opções **`D`**.

As decisões são tomadas identificando a melhor opção entre um conjunto de opções disponíveis. Uma abordagem é eliminar sucessivamente as opções *de* decisão ***<sub>di</sub>*** do conjunto ***D*** até que apenas uma seja deixada e, em seguida, escolher um &quot;vencedor&quot; aleatoriamente do conjunto restante. Outra forma de tomada de decisão consiste em classificar as restantes opções (elegíveis) de acordo com os resultados esperados.

### Conjunto finito de opções de decisão

No domínio Decisão de experiência, as opções a partir das quais uma ou mais opções são selecionadas existem a priori e a computação de uma decisão não cria novas opções dinamicamente. Dizemos que o domínio das opções é finito no momento em que as decisões são tomadas. Isso pode parecer uma limitação, mas um conjunto finito de opções dá origem à possibilidade de usar algoritmos de aprendizado de máquina e técnicas similares para decidir qual das opções é &quot;a melhor&quot;. Muitos algoritmos de aprendizado não seriam capazes de produzir a melhor opção entre um conjunto de alternativas infinitas que não podem ser comparadas entre si e para as quais não existem dados de amostra.

## Resultados da decisão

É importante diferenciar entre os resultados da decisão `d` e os resultados `o`, ou seja, os resultados pretendidos que foram estipulados pela decisão. Uma decisão muitas vezes não pode produzir um resultado diretamente. A decisão é apenas selecionar (ou propor) a opção com o melhor resultado esperado. Entre proposições e resultados, muitos eventos e interações ocorrem, muitas vezes atrasados em dias ou semanas. Em termos mais formais, o resultado é uma função da decisão `o = f(d)`.

Para encontrar a decisão ideal, cada resultado recebe um valor ***de*** utilitário `U(o) = U(f(d))`.
Para o caso de uso da Decisão de Oferta, essa função calcularia o custo para atender à oferta e o valor ganho pela empresa quando a oferta é aceita pelo cliente. O resultado seria usado para encontrar a decisão ideal (oferta) maximizando o valor do utilitário em todas as opções (oferta).

De um modo geral, não é possível prever com segurança qual será o resultado de uma determinada decisão e, por conseguinte, é necessária uma abordagem probabilística. O valor ***do*** utilitário `U(o)` se torna o valor do utilitário ***esperado de uma opção de decisão*** `EU(d)`

## Propostas de decisão

Uma proposta de *decisão* é uma seleção da opção de decisão que foi tomada em resposta a um pedido de decisão real. Tal como acima referido, os resultados de uma decisão podem ocorrer muito mais tarde e os resultados podem também não ser alcançados numa só etapa. Por conseguinte, é importante acompanhar as propostas através de vários eventos *de* experiência, para que possam ser atribuídas de volta às opções de decisão. Este ciclo de feedback é usado para melhorar a precisão da previsão para `EU(d)`.

Uma proposta é persistente como uma entidade e, portanto, tem um identificador. A entidade mantém referências às opções selecionadas e pode registrar dados de contexto que foram usados para tomar a decisão. Ter um identificador também permite que outras entidades o referenciem. Uma dessas entidades é o evento *de* decisões. O carimbo de data e hora é válido, indicando quando foi tomada a sua decisão (proposta). Um evento de decisão é uma ocorrência registrada da ação de execução da decisão. Outros eventos que fazem referência à entidade da proposta são eventos de experiência. Todo evento de experiência pode ser estendido para fazer referência a uma proposta de decisão. A interpretação de tal procedimento é a de que o evento de experiências pode ser total ou parcialmente atribuído à proposta da decisão.

## Estratégia de decisão - Algoritmo

Com um conjunto finito de alternativas para escolher, cada estratégia *de* decisão é essencialmente um algoritmo - ou uma função - que toma as opções de **`N`** decisão *{d<sub>1</sub>, d<sub>2</sub>, ...<sub>dN</sub>* *<sub></sub><sub></sub><sub></sub>* }como entrada e produz uma lista classificada das opções de decisão... (tdr1,dr2drr, ..... k)Em que a primeira opção de decisão na lista é considerada ótima de acordo com um utilitário esperado, a segunda opção na lista resultante é então considerada a segunda melhor opção e assim por diante. Normalmente, o conjunto terá uma cardinalidade maior que a lista classificada resultante, já que o algoritmo de decisão elimina opções que não são elegíveis e um algoritmo pode ser configurado para retornar somente as **`K`** opções principais, interrompendo depois que encontrar opções suficientes.
O quadro de decisão geral é mostrado no diagrama a seguir.

![Figura 1](./images/decisioning-optimization.png)

## Atividades de decisão

*As atividades* de decisão configuram o algoritmo e os parâmetros de fornecimento para uma estratégia de decisão específica. Os parâmetros de estratégia incluem as restrições aplicadas às opções e à função de classificação. Todas as decisões são tomadas no contexto de uma atividade. [!DNL Decisioning Service] hosts com muitas atividades e atividades podem ser reutilizadas em canais. Em qualquer momento, a melhor opção é avaliada com base no conjunto mais atual de restrições, regras e modelos.

Uma atividade de decisão define a coleta das opções de decisão a serem consideradas. Ele filtros o subconjunto de todas as opções que são de interesse nesta atividade. Isso permite que o usuário gerencie categorias tópicas no catálogo de todas as opções. [!DNL Decisioning service]

Uma atividade de decisão especifica uma opção *de* fallback se as restrições combinadas desqualificarem todas as outras opções. Isso significa que há sempre uma resposta para a questão: Qual é atualmente a opção &quot;melhor&quot;?

As atividades de decisão podem especificar o local em que a experiência é fornecida. Isso reduz ainda mais o número de opções de decisão que podem ser consideradas e é outra restrição imposta pela atividade de decisão. Isso é chamado de restrição *de posicionamento*. Somente as opções que tiverem conteúdo que atendam a essa restrição de posicionamento serão consideradas. Este aspecto é avaliado nas fases iniciais da estratégia de decisão. Quando as definições mudam, as restrições de posicionamento de cada atividade de decisão são reavaliadas e a opção de decisão pode ser tomada ou não ser considerada para uma ou mais atividades de decisão.

## Contexto da decisão

Até o momento, apenas a *lógica* empresarial que afeta a decisão foi descrita. Mas ainda mais impactante para o resultado são os *dados* de entrada da decisão. Esses dados são chamados de contexto *de* decisão e são diferentes para cada usuário e cada vez que uma decisão é tomada - em oposição a restrições, regras e modelos que são os mesmos para diferentes usuários para a mesma atividade. As regras, restrições e modelos também mudam com menos frequência. Para a tomada de decisões em tempo real, o contexto da decisão também terá de ser determinado em tempo real.

Os dados de contexto de decisão podem ser divididos em dados relacionados ao perfil do usuário, dados comerciais e dados coletados internamente.

- *As entidades* do perfil são usadas para representar dados do usuário final, mas nem todas as entidades do perfil representam um indivíduo. Pode ser um lar, um grupo social, ou qualquer outro assunto. Os eventos de experiência são registros de dados da série cronológica ligados a um perfil. Se houver experiência, esses dados serão *sujeitos* a essa experiência.
- Por outro lado, há as entidades *empresariais*. Podem ser considerados como os *objetos* das interações. Essas entidades são frequentemente referenciadas nos eventos de experiência de entidades perfis. Exemplos de entidades de negócios são sites e páginas, lojas, detalhes do produto, conteúdo digital, dados de inventário do produto e assim por diante.
- A última categoria de dados no contexto de decisão são os dados criados durante a operação do [!DNL Decisioning Service]. Cada evento de decisão se encaixa nessa categoria, junto com as respostas dos clientes, os dados da proposta formam um conjunto de dados interno chamado histórico ** proposition-response.

Há três caminhos que os dados podem tomar para se tornarem parte do contexto de decisão. Os dados de registro e de série cronológica podem ser carregados por meio de arquivos de conjunto de dados. Este caminho é principalmente para sincronização em massa com sistemas externos. Os dados dos registros e das séries cronológicas também podem ser transmitidos para [!DNL Platform] onde os dados são indexados e unidos às entidades de formulário. Pelo terceiro caminho, os dados de contexto podem ser passados como parâmetros para a solicitação de decisão. Esta forma de dados tem um caráter efêmero e só é relevante para a decisão solicitada. Não é persistente como uma entidade e não está disponível para outras solicitações.
