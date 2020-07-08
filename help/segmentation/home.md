---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Serviço de segmentação de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---


# Visão geral do Serviço de segmentação

O Serviço de segmentação de Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir dos dados do Perfil do cliente em tempo real. Esses segmentos são configurados e mantidos centralmente no Platform e são prontamente acessíveis por qualquer solução da Adobe.

Este documento fornece uma visão geral do Serviço de segmentação e o papel que ele desempenha no Adobe Experience Platform.

## Introdução ao serviço de segmentação

É importante entender os seguintes termos principais usados em todo o documento:

- **Segmentação**: Dividindo um grande grupo de indivíduos (como clientes, prospectos, usuários ou organizações) em grupos menores que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.
- **Definição** do segmento: O conjunto de regras usado para descrever as principais características ou comportamento de uma audiência de público alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros da audiência qualificados para um segmento.
- **Audiência**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Como a segmentação funciona

A segmentação é o processo de definição de atributos ou comportamentos específicos compartilhados por um subconjunto de perfis da sua loja de perfis para diferenciar um grupo comercializável de pessoas da sua base de clientes. Por exemplo, em uma campanha de email chamada &quot;Você esqueceu de comprar seus tênis?&quot;, você pode querer uma audiência de todos os usuários que procuraram tênis de corrida nos últimos 30 dias, mas que não concluíram uma compra.

Uma vez que um segmento tenha sido definido conceitualmente, ele é construído em Experience Platform. Normalmente, os segmentos são criados pelo profissional de marketing ou pelo especialista em audiências, embora algumas organizações prefiram que sejam criados pelo departamento de marketing, em colaboração com seus analistas de dados. Ao revisar os dados enviados à Platform, o analista de dados compõe a definição do segmento selecionando quais campos e valores serão usados para criar as regras ou condições do segmento. Isso é feito usando a interface do usuário ou a API.

## Criar segmentos

Independentemente de serem criados usando a API ou o Construtor de segmentos, os segmentos são definidos por meio da Linguagem de Query do Perfil (PQL). É aqui que a definição do segmento conceitual é descrita na linguagem criada para recuperar perfis que atendem aos critérios. Para obter mais informações, consulte a visão geral [do](./pql/overview.md)PQL.

Para saber como criar e usar segmentos no Construtor de segmentos (a implementação da interface do serviço de segmentação), consulte o guia [do Construtor de](./ui/overview.md)segmentos.

Para obter informações sobre como criar definições de segmentos usando a API, consulte o tutorial sobre como [criar segmentos de audiência usando a API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>No evento em que um schema é estendido, todos os uploads futuros devem atualizar os campos recém-adicionados de acordo. Para obter mais informações sobre como personalizar o Modelo de dados de experiência (XDM), visite o tutorial [do Editor de](../xdm/tutorials/create-schema-ui.md)Schemas.

## Avaliar segmentos

### Segmentação em streaming

A segmentação de transmissão é um processo contínuo de seleção de dados que atualiza seus segmentos em resposta à atividade do usuário. Depois que um segmento é criado e salvo, a definição do segmento é aplicada em relação aos dados recebidos no Perfil do cliente em tempo real. Adições e remoções do segmento são processadas regularmente, garantindo que sua audiência do público alvo permaneça relevante.

Para saber mais sobre a segmentação de streaming, leia a documentação [de segmentação de](./api/streaming-segmentation.md)streaming.

### Segmentação em lote

Como alternativa a um processo de seleção de dados em andamento, a segmentação em lote move todos os dados do perfil de uma só vez pelas definições de segmento para produzir audiências correspondentes. Depois de criado, esse segmento é salvo e armazenado para que você possa exportá-lo para uso.

Para saber como avaliar segmentos, consulte o tutorial [de avaliação de](./tutorials/evaluate-a-segment.md)segmentos.

## Acessar resultados da segmentação

Para saber como acessar um segmento exportado, consulte o tutorial [de avaliação de](./tutorials/evaluate-a-segment.md)segmento.

## Metadados do segmento

Os metadados do segmento facilitam a indexação no evento para que qualquer um de seus segmentos seja reutilizado e/ou combinado.

A composição de seus segmentos (por meio da API ou do Construtor de segmentos) exige que você defina um nome de segmento e uma política de mesclagem.

### Nomes de segmentos

Ao criar um novo segmento, é necessário fornecer um nome de segmento. O nome do segmento é usado para identificar um segmento específico entre a coleção criada pelo Serviço de segmentação. Os nomes de segmentos devem, portanto, ser descritivos, concisos e exclusivos.

>[!NOTE]
>
>Ao planejar um segmento, lembre-se de que os segmentos podem ser referenciados e combinados a qualquer outro segmento. Ao selecionar um nome, considere a possibilidade de seu segmento conter partes reutilizáveis.

### Mesclar políticas

As políticas de mesclagem são regras usadas pelo Perfil para determinar como os dados serão priorizados e combinados em uma visualização unificada em determinadas condições.
Se uma política de mesclagem não estiver definida, a política de mesclagem padrão do Platform será usada. Se você preferir usar uma política de mesclagem específica para a sua organização, poderá criar sua própria política e marcá-la como padrão da sua organização.

>[!NOTE]
>
>A estimativa de tamanhos de audiência é baseada na política padrão de mesclagem de perfis da organização.

### Outros metadados de segmento

Além do nome do segmento e da política de mesclagem, o Construtor de segmentos oferta um campo de metadados adicional de &quot;descrição do segmento&quot; no qual você pode resumir a finalidade da definição do segmento.

## Recursos avançados de segmentação

Os segmentos podem ser configurados para gerar uma audiência continuamente, combinando a assimilação [de dados de](../ingestion/streaming-ingestion/overview.md) fluxo contínuo com qualquer um dos seguintes recursos de segmentação avançada:
- [Segmentação sequencial](#sequential)
- [Segmentação dinâmica](#dynamic)
- [Segmentação de várias entidades](#multi-entity)

Esses recursos avançados são discutidos com mais detalhes nas seções a seguir.

## Segmentação sequencial {#sequential}

Uma jornada padrão do usuário é sequencial por natureza.  O Adobe Experience Platform permite que você defina uma série ordenada de segmentos para refletir essa jornada, capturando assim sequências de eventos à medida que ocorrem. Você pode organizar os eventos na ordem desejada usando a linha do tempo do evento visual no Construtor de segmentos.

Um exemplo de uma jornada do cliente que exigiria segmentação sequencial seria visualização do produto > adição do produto > finalização > Nenhuma compra.

## Segmentação dinâmica {#dynamic}

A segmentação dinâmica resolve os problemas de escalabilidade que os comerciantes enfrentam tradicionalmente ao criar segmentos para campanhas de marketing.

Diferentemente da segmentação estática que exige que você capture explícita e repetidamente todos os casos de uso possíveis, a segmentação dinâmica usa variáveis para criar a lógica da regra e as relações dinamicamente expressas.

### Caso de uso: Procurando clientes que fazem compras fora do seu país

Para ilustrar o valor desse recurso de segmentação avançada, considere a colaboração de um arquiteto de dados com um profissional de marketing para identificar os clientes que fizeram compras fora do estado de origem.

**O problema**

A segmentação estática exige que você defina segmentos individuais com um atributo de estado inicial exclusivo, antes de filtrar eventos de compra que não sejam iguais ao estado inicial. Um segmento explícito desse tipo diria &quot;Estou procurando pessoas de Utah onde o estado de sua compra não é Utah&quot;. A criação de uma audiência usando esse método exige a definição de um segmento para cada estado dos EUA, para um total de 50 segmentos.

Como resultado das diferentes combinações de segmentos que inevitavelmente surgem à medida que você dimensiona, o processo manual necessário para a segmentação estática se torna mais demorado, reduzindo a eficiência geral.

**A solução**

Ao atribuir uma variável ao atributo de estado da compra, seu segmento dinâmico simplifica para &quot;localizar uma compra em que o estado dessa compra não seja igual ao estado inicial do cliente&quot;. Isso permite consolidar 50 segmentos estáticos em um único segmento dinâmico.

## Segmentação de várias entidades {#multi-entity}

Com o recurso avançado de segmentação de várias entidades, é possível criar segmentos usando várias classes XDM, adicionando extensões aos schemas pessoais. Como resultado, o Serviço de segmentação pode acessar campos adicionais durante a definição do segmento como se eles fossem nativos no armazenamento de dados do perfil.

A segmentação de várias entidades proporciona a flexibilidade necessária para identificar audiências com base em dados relevantes às suas necessidades comerciais. Esse processo pode ser feito de forma rápida e fácil, sem precisar de especialização em consultas a bancos de dados. Isso permite que você adicione dados principais aos seus segmentos sem precisar fazer alterações dispendiosas nos fluxos de dados ou aguardar uma união de dados back-end.

### Caso de uso: Promoção orientada por preços

Para ilustrar o valor desse recurso de segmentação avançada, considere um arquiteto de dados colaborando com um comerciante.

Neste exemplo, o arquiteto de dados está unindo dados para um indivíduo (composto de schemas com Perfil XDM Individual e ExperienceEvent XDM como suas classes base) para outra classe usando uma chave. Depois de associados, o arquiteto de dados ou o comerciante pode usar esses novos campos durante a definição do segmento como se fossem nativos para o schema da classe base.

**O problema**

O arquiteto de dados e o comerciante trabalham para o mesmo varejista de roupas. O varejista tem mais de mil lojas em toda a América do Norte e diminui periodicamente os preços dos produtos ao longo de seu ciclo de vida. Como resultado, o comerciante quer executar uma campanha especial para dar aos compradores que compraram esses itens a chance de comprá-los a preços atualizados.

Os recursos do arquiteto de dados incluem acesso a dados da Web da navegação do cliente, bem como dados de adição do carrinho que contêm identificadores SKU de produto. Eles também têm acesso a uma classe separada de &quot;produtos&quot;, onde são armazenadas informações adicionais sobre o produto (incluindo o preço do produto). A orientação deles é focar nos clientes que adicionaram um produto ao carrinho nos últimos 14 dias, mas não compraram o item, cujo preço já caiu.

**A solução**

>[!NOTE]
>
>Neste exemplo, presumiremos que o arquiteto de dados já estabeleceu uma Namespace de ID.

Usando a API, o arquiteto de dados relaciona a chave do schema ExperienceEvent com a classe &quot;products&quot;. Isso permite que o arquiteto de dados utilize os campos adicionais da classe &quot;products&quot; como se fossem nativos do schema ExperienceEvent. Como etapa final do trabalho de configuração, o arquiteto de dados precisa trazer os dados apropriados para o Perfil do cliente em tempo real. Isso é feito habilitando o conjunto de dados &quot;produtos&quot; para uso com o Perfil. Com o trabalho de configuração concluído, o arquiteto de dados ou o comerciante pode criar o segmento de público alvo no Construtor de segmentos.

Consulte a visão geral [da composição do](../xdm/schema/composition.md#union) schema para saber como definir relações entre as classes XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Casos de uso

Para ilustrar o valor desse recurso de segmentação avançada, considere três casos de uso padrão que ilustram os desafios presentes nos aplicativos de marketing antes do aprimoramento da Carga do segmento:
- Personalização de email
- Redirecionamento de email
- Redefinição de metas de anúncios

**Personalização de email**

Um profissional de marketing que está criando uma campanha de email pode ter tentado criar um segmento para uma audiência de público alvo usando compras recentes de lojas de clientes nos últimos três meses. Idealmente, esse segmento exigiria o nome do item e o nome da loja onde a compra foi realizada. Antes da melhoria, o desafio era capturar o identificador da loja do evento de compra e atribuí-lo ao perfil do cliente.

**Redirecionamento de email**

Geralmente, é complexo criar e qualificar segmentos para campanhas de e-mail direcionadas ao &quot;abandono do carrinho&quot;. Antes da melhoria, saber quais produtos incluir em uma mensagem personalizada era difícil devido à disponibilidade dos dados necessários. Os dados para os quais os produtos foram abandonados estão vinculados a eventos que antes desafiavam o monitoramento e a extração de dados.

**Redefinição de metas de anúncios**

Outro desafio tradicional para os comerciantes tem sido criar anúncios para redirecionar os clientes com itens abandonados do carrinho de compras. Embora as definições de segmento tenham abordado esse desafio, antes do aprimoramento, não havia um método formal de diferenciação entre produtos comprados e produtos abandonados. Agora você pode público alvo conjuntos de dados específicos durante a definição do segmento.

## Tipos de dados do Serviço de segmentação

Todos os tipos de dados XDM são suportados no Serviço de segmentação. As regras que constituem uma definição de segmento são contextualizadas pelos seguintes tipos de dados.

### Dados da string

As definições de segmento usam dados de string para definir restrições não numéricas para audiências de segmento, como &quot;nome do país&quot; ou &quot;nível de programa de fidelidade&quot;.

Os dados de sequência de caracteres são incluídos nas definições de segmento usando declarações lógicas, inclusivas/exclusivas e comparativas. Depois que um atributo de string é adicionado à definição do segmento, você pode usar declarações relevantes de string para avaliá-lo em relação a outros campos de string.

| Tipo de declaração | Exemplos |
| -------------- | -------- |
| Lógica | e, ou não |
| Inclusivo/exclusivo | incluir, deve existir, excluir, não deve existir |
| Comparação | igual, não é igual, contém, start com |


### Dados de data

Os dados de data permitem que você atribua contexto baseado em tempo às definições de segmento, usando datas de start/término específicas ou usando declarações relevantes de data, conforme mostrado na tabela abaixo. Uma implementação pode estar criando uma audiência de clientes que interagiram com a sua marca a qualquer momento *neste ano* e também tem estado ativo *nos últimos* dias.

| Exemplo de campo | Declarações relevantes à data | Linha do tempo |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | hoje, ontem, este mês, este ano | Relevante para o dia em que o segmento foi construído. |
| person.lastPurchase | por último, durante, antes, depois, dentro | Relevante dentro de uma determinada semana/mês. |

### Eventos de experiência

Como um schema Adobe Experience Platform, o XDM ExperienceEvents registra interações explícitas e implícitas entre os clientes e os aplicativos integrados da Platform, incluindo um instantâneo do sistema no momento em que a interação ocorreu. ExperienceEvents são registros de fatos. Dessa forma, eles são uma fonte de dados disponível para você durante a definição do segmento.

Conforme visto na tabela abaixo, os dados do evento são renderizados usando palavras-chave que ajudam a refinar o comportamento do evento e a especificar atributos do evento.

| Palavra-chave | Use |
| ------- | --- |
| Incluir/excluir | Descreve o comportamento do evento através da inclusão ou omissão de dados. |
| Qualquer/todos | Ajuda a determinar o número de segmentos qualificados. |
| Botão de alternância &quot;Aplicar regra de tempo&quot; | Incorpora dados de data. |
| É igual, não é igual, start com, não start, termina com, não termina com, contém, não contém, existe, não existe | Incorpora dados de string. |

### Segmentos

As definições de segmentos existentes também podem ser usadas como componentes de uma nova definição de segmento, adicionando seus atributos e regras baseadas em eventos ao novo segmento.

### Audiences

audiências externas também podem ser usadas como componentes de uma nova definição de segmento, adicionando suas regras de atributo ao novo segmento.

Atualmente, somente Adobe Audience Manager é suportado como uma audiência. Fontes adicionais serão ativadas no futuro.

### Outros tipos de dados

Além dos mencionados acima, a lista de tipos de dados suportados também inclui:
- String
- Identificador de recurso uniforme
- Enum
- Número
- Longo
- Número inteiro
- Curto
- Byte
- Booleano
- Data
- Data e hora
- Matriz
- Objeto
- Mapa
- Eventos

## Próximas etapas

O Serviço de segmentação fornece um fluxo de trabalho consolidado para construir segmentos a partir dos dados de Perfil do cliente em tempo real. Em resumo:

- A segmentação é o processo de definição de um subconjunto de perfis da sua loja de perfis, que permite caracterizar o comportamento ou os atributos de um grupo comercializável desejado. O Serviço de segmentação torna esse processo possível.
- Ao planejar um segmento, lembre-se de que um segmento pode ser referenciado e combinado a qualquer outro segmento.
- Um segmento pode ser criado a partir de regras baseadas em dados de perfil, dados de séries de tempo relacionados ou ambos.
- Os segmentos podem ser avaliados sob demanda ou continuamente. Quando avaliados sob demanda, todos os dados do perfil são passados pelas definições do segmento de uma só vez. Quando avaliados continuamente, os dados são transmitidos pelas definições de segmento à medida que entram no Platform.

Para saber como definir segmentos na interface do usuário, consulte o guia [Construtor de](./ui/overview.md)segmentos. Para obter informações sobre como criar definições de segmentos usando a API, consulte o tutorial sobre como [criar segmentos usando a API](./tutorials/create-a-segment.md).