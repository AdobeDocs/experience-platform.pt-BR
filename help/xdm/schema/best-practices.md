---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, enum, identidade primária, identidade primária, perfil individual XDM, evento de experiência, Evento de experiência XDM, ExperienceEvent XDM, evento de experiência, evento de experiência, evento de experiência XDM, design de esquema, práticas recomendadas
solution: Experience Platform
title: Práticas Recomendadas Para A Modelagem De Dados
topic-legacy: overview
description: Este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 1%

---

# Práticas recomendadas para modelagem de dados

[!DNL Experience Data Model] (XDM) é a estrutura principal que padroniza os dados da experiência do cliente fornecendo estruturas e definições comuns para uso nos serviços downstream da Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que permite obter informações valiosas das ações do cliente, definir públicos do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

Como o XDM é extremamente versátil e personalizável por design, é importante seguir as práticas recomendadas para modelagem de dados ao projetar seus esquemas. Este documento aborda as principais decisões e considerações que você deve tomar ao mapear os dados de experiência do cliente para o XDM.

## Introdução

Antes de ler este guia, revise a [Visão geral do sistema XDM](../home.md) para obter uma introdução de alto nível ao XDM e sua função no Experience Platform.

Além disso, este guia se concentra exclusivamente em considerações-chave relacionadas ao design do schema. Portanto, é altamente recomendável consultar as [noções básicas da composição do schema](./composition.md) para obter explicações detalhadas dos elementos de schema individuais mencionados neste guia.

## Resumo das práticas recomendadas

A abordagem recomendada para projetar seu modelo de dados para uso no Experience Platform pode ser resumida da seguinte maneira:

1. Entenda os casos de uso comercial de seus dados.
1. Identifique as fontes de dados primárias que devem ser trazidas para [!DNL Platform] para tratar desses casos de uso.
1. Identifique quaisquer fontes de dados secundárias que também possam ser de interesse. Por exemplo, se atualmente apenas uma unidade de negócios em sua organização estiver interessada em portar seus dados para [!DNL Platform], uma unidade de negócios semelhante também pode estar interessada em portar dados semelhantes no futuro. Considerando essas fontes secundárias ajuda a padronizar o modelo de dados em toda a organização.
1. Crie um diagrama de relacionamento de entidade de alto nível (ERD) para as fontes de dados que foram identificadas.
1. Converta o ERD de alto nível em um ERD centrado em [!DNL Platform] (incluindo perfis, Eventos de experiência e entidades de pesquisa).

As etapas relacionadas à identificação das fontes de dados aplicáveis necessárias para realizar seus casos de uso de negócios variam de organização para organização. Embora o restante das seções deste documento se concentre nas últimas etapas da organização e construção de um ERD após as fontes de dados terem sido identificadas, as explicações dos vários componentes do diagrama podem informar suas decisões sobre quais de suas fontes de dados devem ser migradas para [!DNL Platform].

## Criar um ERD de alto nível

Depois de determinar as fontes de dados que deseja trazer para [!DNL Platform], crie um ERD de alto nível para ajudar a orientar o processo de mapeamento de seus dados para esquemas XDM.

O exemplo abaixo representa um ERD simplificado para uma empresa que deseja trazer dados para [!DNL Platform]. O diagrama destaca as entidades essenciais que devem ser classificadas em classes XDM, incluindo contas de clientes, hotéis, endereços e vários eventos de comércio eletrônico comuns.

![](../images/best-practices/erd.png)

## Classificar entidades em perfil, pesquisa e categorias de evento

Depois de criar um ERD para identificar as entidades essenciais que deseja trazer para [!DNL Platform], essas entidades devem ser classificadas em perfil, pesquisa e categorias de evento:

| Categoria | Descrição |
| --- | --- |
| Entidades de perfil | As entidades de perfil representam atributos relacionados a uma pessoa individual, normalmente um cliente. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados na **[!DNL XDM Individual Profile]classe**. |
| Entidades de pesquisa | As entidades de pesquisa representam conceitos que podem estar relacionados a uma pessoa, mas não podem ser usados diretamente para identificar o indivíduo. As entidades que se encaixam nesta categoria devem ser representadas por esquemas baseados em **classes personalizadas**. |
| Entidades de evento | As entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, aos eventos do sistema ou a qualquer outro conceito, onde você pode querer rastrear as alterações ao longo do tempo. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados na **[!DNL XDM ExperienceEvent]classe**. |

### Considerações para classificação de entidade

As seções abaixo fornecem mais orientações sobre como classificar suas entidades nas categorias acima.

#### Atributos do cliente

Se uma entidade contiver quaisquer atributos relacionados a um cliente individual, provavelmente será uma entidade de perfil. Exemplos de atributos do cliente incluem:

* Detalhes pessoais, como nome, data de nascimento, gênero e ID(s) da conta.
* Informações de localização, como endereços e informações de GPS.
* Informações de contato, como números de telefone e endereços de email.

#### Rastreamento de dados ao longo do tempo

Se quiser analisar como determinados atributos em uma entidade são alterados ao longo do tempo, é provável que seja uma entidade de evento. Por exemplo, a adição de itens de produto ao carrinho pode ser rastreada como eventos de adição ao carrinho em [!DNL Platform]:

| Customer ID | Tipo | Identificação do produto | Quantidade | Carimbo de data e hora |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1 de outubro, 10:32 |
| 1234567 | Remover | 275098 | 1 | 1 de outubro, 10:33 |
| 1234567 | Adicionar | 486502 | 1 | 1 de outubro, 10:41 |
| 1234567 | Adicionar | 910482 | 5 | 3 de outubro de 2015 |

#### Casos de uso de segmentação

Ao categorizar suas entidades, é importante pensar nos segmentos de público-alvo que você pode criar para lidar com casos de uso comerciais específicos.

Por exemplo, uma empresa quer conhecer todos os membros &quot;Ouro&quot; ou &quot;Platinum&quot; de seu programa de fidelidade que fizeram mais de cinco compras no ano passado. Com base nesta lógica de segmento, podem ser tiradas as seguintes conclusões sobre como as entidades relevantes devem ser representadas:

* &quot;Gold&quot; e &quot;Platinum&quot; representam os status de fidelidade aplicáveis a um cliente individual. Como a lógica do segmento se preocupa apenas com o status de fidelidade atual dos clientes, esses dados podem ser modelados como parte de um esquema de perfil. Se você quiser rastrear alterações no status da fidelidade ao longo do tempo, também poderá criar um schema de evento adicional para alterações no status da fidelidade.
* Compras são eventos que ocorrem em um determinado momento e a lógica do segmento se preocupa com eventos de compra em um período especificado. Esses dados devem, portanto, ser modelados como um schema de eventos.

#### Casos de uso de ativação

Além das considerações relacionadas aos casos de uso de segmentação, você também deve rever os casos de uso de ativação desses segmentos para identificar outros atributos relevantes.

Por exemplo, uma empresa criou um segmento de público-alvo com base na regra que `country = US`. Em seguida, ao ativar esse segmento para determinados destinos downstream, a empresa deseja filtrar todos os perfis exportados com base no estado inicial. Portanto, um atributo `state` também deve ser capturado na entidade de perfil aplicável.

#### Valores agregados

Com base no caso de uso e na granularidade dos dados, você deve decidir se determinados valores precisam ser pré-agregados antes de serem incluídos em um perfil ou entidade de evento.

Por exemplo, uma empresa deseja criar um segmento com base na quantidade de compras de carrinho. É possível optar por incorporar esses dados na granularidade mais baixa, incluindo cada evento de compra com carimbo de data e hora como sua própria entidade. No entanto, isso pode às vezes aumentar o número de eventos registrados exponencialmente. Para reduzir o número de eventos assimilados, você pode optar por criar um valor agregado `numberOfPurchases` em um período de duração de semana ou de mês. Outras funções agregadas, como MIN e MAX, também podem se aplicar a essas situações.

>[!CAUTION]
>
>No momento, o Experience Platform não executa a agregação automática de valor, embora isso esteja planejado para versões futuras. Se você optar por usar valores agregados, deverá executar os cálculos externamente antes de enviar os dados para [!DNL Platform].

#### Cardinalidade

As cardinalidades estabelecidas em seu ERD também podem fornecer algumas pistas sobre como categorizar suas entidades. Se houver uma relação um para muitos entre duas entidades, a entidade que representa &quot;muitos&quot; provavelmente será uma entidade de evento. No entanto, também há casos em que &quot;muitos&quot; é um conjunto de entidades de pesquisa que são fornecidas como uma matriz dentro de uma entidade de perfil.

>[!NOTE]
>
>Como não há uma abordagem universal para se adequar a todos os casos de uso, é importante considerar os prós e contras de cada situação ao categorizar entidades com base na cardinalidade. Consulte a [próxima seção](#pros-and-cons) para obter mais informações.

A tabela a seguir descreve alguns relacionamentos de entidade comuns e as categorias que podem ser derivadas deles:

| Relação | Cardinalidade | Categorias de entidades |
| --- | --- | --- |
| Clientes e check-outs do carrinho | Um para muitos | Um único cliente pode ter muitos check-outs de carrinho, que são eventos que podem ser rastreados ao longo do tempo. Portanto, os clientes seriam uma entidade de perfil, enquanto os Check-outs do carrinho seriam uma entidade de evento. |
| Clientes e contas de fidelidade | Um para um | Um único cliente pode ter apenas uma conta de fidelidade, e vice-versa. Como o relacionamento é um para um, tanto Clientes quanto Contas de fidelidade representam entidades de perfil. |
| Clientes e assinaturas | Um para muitos | Um único cliente pode ter muitas subscrições. Como a empresa só está preocupada com as assinaturas atuais de um cliente, os Clientes são uma entidade de perfil, enquanto as Assinaturas são uma entidade de pesquisa. |

### Prós e contras de diferentes classes de entidade {#pros-and-cons}

Embora a seção anterior tenha fornecido algumas diretrizes gerais para decidir como categorizar suas entidades, é importante compreender que geralmente pode haver vantagens e desvantagens na escolha de uma categoria de entidade em vez de outra. O estudo de caso a seguir serve para ilustrar como você pode considerar suas opções nessas situações.

Uma empresa rastreia assinaturas ativas de seus clientes, onde um cliente pode ter muitas assinaturas. A empresa também deseja incluir assinaturas para casos de uso de segmentação, como encontrar todos os usuários com assinaturas ativas.

Nesse cenário, a empresa tem duas opções possíveis para representar as assinaturas de um cliente em seu modelo de dados:

1. [Usar atributos de perfil](#profile-approach)
1. [Usar entidades de evento](#event-approach)

#### Abordagem 1: Usar atributos de perfil {#profile-approach}

A primeira abordagem seria incluir uma matriz de subscrições como atributos na entidade de perfil para clientes. Os objetos nesta matriz conteriam campos para `category`, `status`, `planName`, `startDate` e `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Prós**

* A segmentação é viável para o caso de uso pretendido.
* O schema preservará apenas os registros de subscrição mais recentes de um cliente.

**Desvantagens**

* Toda a matriz deve ser reiniciada sempre que ocorrerem alterações em qualquer campo da matriz.
* Se diferentes fontes de dados ou unidades de negócios estiverem alimentando dados no array, será desafiador manter o storage atualizado mais recente sincronizado em todos os canais.

#### Abordagem 2: Usar entidades de evento {#event-approach}

A segunda abordagem seria usar esquemas de eventos para representar assinaturas. Isso implica assimilar os mesmos campos de assinatura da primeira abordagem, com adição de uma ID de assinatura, uma ID do cliente e um carimbo de data e hora de quando o evento de assinatura ocorreu.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Prós**

* As regras de segmentação podem ser mais flexíveis (como encontrar todos os clientes que alteraram suas subscrições nos últimos 30 dias).
* Quando o status de assinatura de um cliente é alterado, não é mais necessário atualizar uma matriz longa e potencialmente complexa dentro dos atributos do perfil do cliente. Isso é especialmente útil se alterações simultâneas na lista de assinaturas do cliente estiverem ocorrendo de várias fontes.

**Desvantagens**

* A segmentação se torna mais complexa para o caso de uso pretendido original (identificando o status das assinaturas mais recentes dos clientes). O segmento agora precisa de lógica adicional para sinalizar o último evento de assinatura para um cliente para verificar seu status.

## Criar esquemas com base em suas entidades categorizadas

Depois de classificar suas entidades em categorias de perfil, pesquisa e evento, você pode começar a converter seu modelo de dados em esquemas XDM. Para fins de demonstração, o modelo de dados de exemplo mostrado anteriormente foi classificado em categorias apropriadas no diagrama a seguir:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

A categoria na qual uma entidade foi classificada deve determinar a classe XDM na qual você baseia seu esquema. Para reiterar:

* As entidades de perfil devem usar a classe [!DNL XDM Individual Profile] .
* As entidades de evento devem usar a classe [!DNL XDM ExperienceEvent] .
* As entidades de pesquisa devem usar classes XDM personalizadas definidas pela sua organização.

>[!NOTE]
>
>Embora as entidades de evento quase sempre sejam representadas por esquemas separados, as entidades nas categorias de perfil ou pesquisa podem ser combinadas em um único esquema XDM, dependendo de sua cardinalidade.
>
>Por exemplo, como a entidade Customers tem uma relação um para um com a entidade LoyaltyAccounts, o esquema da entidade Customers também pode incluir um objeto `LoyaltyAccount` para conter os campos de fidelidade apropriados para cada cliente. No entanto, se a relação for uma para muitos, a entidade que representa o &quot;muitos&quot; poderá ser representada por um schema separado ou por uma matriz de atributos de perfil, dependendo de sua complexidade.

As seções abaixo fornecem orientação geral sobre a construção de schemas com base em seu ERD.

### Adotar uma abordagem de modelagem iterativa

As [regras de evolução do schema](./composition.md#evolution) ditam que somente alterações não destrutivas podem ser feitas em esquemas depois de terem sido implementadas. Em outras palavras, depois de adicionar um campo a um esquema e os dados tiverem sido assimilados em relação a esse campo, o campo não poderá mais ser removido. Portanto, é essencial adotar uma abordagem de modelagem iterativa ao criar seus esquemas pela primeira vez, começando com uma implementação simplificada que aumenta progressivamente a complexidade ao longo do tempo.

Se você não tiver certeza se um campo específico é necessário para incluir em um schema, a prática recomendada é deixá-lo de fora. Se for posteriormente determinado que o campo é necessário, ele sempre poderá ser adicionado na próxima iteração do schema.

### Campos de identidade

No Experience Platform, os campos XDM marcados como identidades são usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Embora um schema possa ter vários campos marcados como identidades, uma única identidade primária deve ser definida para que o schema seja ativado para uso em [!DNL Real-time Customer Profile]. Consulte a seção [identity fields](./composition.md#identity) nas noções básicas da composição do schema para obter informações mais detalhadas sobre o caso de uso desses campos.

Ao projetar seus esquemas, qualquer chave primária nas tabelas do banco de dados relacional provavelmente será candidata para identidades primárias. Outros exemplos de campos de identidade aplicáveis são endereços de email do cliente, números de telefone, IDs de conta e [ECID](../../identity-service/ecid.md).

### Misturas de aplicações Adobe

O Experience Platform fornece várias mixins XDM prontos para uso para capturar dados relacionados aos seguintes aplicativos do Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Por exemplo, o [[!UICONTROL Adobe Analytics ExperienceEvent Template Mixin]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) permite mapear campos específicos do [!DNL Analytics] para seus esquemas XDM. Dependendo dos aplicativos do Adobe com os quais você está trabalhando, você deve usar essas mixins fornecidas por Adobe nos seus esquemas.

<img src="../images/best-practices/analytics-mixin.png" width="700"><br>

Os mixins de aplicativos Adobe atribuem automaticamente uma identidade primária padrão por meio do uso do campo `identityMap` , que é um objeto somente leitura gerado pelo sistema que mapeia valores de identidade padrão para um cliente individual.

Para Adobe Analytics, ECID é a identidade primária padrão. Se um valor de ECID não for fornecido por um cliente, a identidade primária assumirá AAID como padrão.

>[!IMPORTANT]
>
>Ao usar mixins de aplicativo Adobe, nenhum outro campo deve ser marcado como a identidade primária. Se houver propriedades adicionais que precisam ser marcadas como identidades, esses campos precisam ser atribuídos como identidades secundárias.

## Próximas etapas

Este documento cobriu as diretrizes gerais e as práticas recomendadas para projetar seu modelo de dados para o Experience Platform. Para resumir:

* Use uma abordagem de cima para baixo, classificando as tabelas de dados em categorias de perfil, pesquisa e evento antes de criar seus esquemas.
* Geralmente, há várias abordagens e opções quando se trata de projetar schemas para diferentes finalidades.
* Seu modelo de dados deve ser compatível com casos de uso de negócios, como segmentação ou análise de jornada do cliente.
* Torne seus esquemas o mais simples possível e adicione novos campos somente quando absolutamente necessário.

Quando estiver pronto, consulte o tutorial em [criar um esquema na interface do usuário](../tutorials/create-schema-ui.md) para obter instruções passo a passo sobre como criar um esquema, atribuir a classe apropriada para a entidade e adicionar campos para mapear seus dados.
