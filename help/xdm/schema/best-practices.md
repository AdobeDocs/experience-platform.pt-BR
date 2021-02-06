---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;identidade primária;identidade primária;perfil individual XDM;evento de experiência;Evento de experiência XDM;schema de experiência XDM;ExperienceEvent;experience;event;XDM Experience ExperienceEvent;design;best practices
solution: Experience Platform
title: Práticas Recomendadas Para A Modelagem De Dados
topic: overview
description: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '2507'
ht-degree: 1%

---


# Práticas recomendadas para modelagem de dados

[!DNL Experience Data Model] (XDM) é a estrutura principal que padroniza os dados da experiência do cliente ao fornecer estruturas e definições comuns para uso nos serviços Adobe Experience Platform a jusante. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum que permite obter informações valiosas das ações do cliente, definir audiências do cliente por meio de segmentos e expressar atributos do cliente para fins de personalização.

Como o XDM é extremamente versátil e personalizável por design, é importante seguir as práticas recomendadas para modelagem de dados ao projetar seus schemas. Este documento aborda as principais decisões e considerações que você deve tomar ao mapear os dados de experiência do cliente para o XDM.

## Introdução

Antes de ler este guia, reveja a [visão geral do sistema XDM](../home.md) para obter uma introdução de alto nível ao XDM e sua função no Experience Platform.

Além disso, este guia se concentra exclusivamente nas principais considerações relacionadas ao design do schema. Portanto, é altamente recomendável que você se refira às [noções básicas de composição do schema](./composition.md) para obter explicações detalhadas dos elementos de schema individuais mencionados neste guia.

## Resumo das práticas recomendadas

A abordagem recomendada para o design do modelo de dados para uso no Experience Platform pode ser resumida da seguinte maneira:

1. Entenda os casos de uso comercial para seus dados.
1. Identifique as fontes de dados principais que devem ser colocadas em [!DNL Platform] para tratar desses casos de uso.
1. Identifique quaisquer fontes de dados secundárias que também possam ter interesse. Por exemplo, se atualmente apenas uma unidade de negócios em sua organização estiver interessada em portar seus dados para [!DNL Platform], uma unidade de negócios semelhante também pode estar interessada em portar dados similares no futuro. Considerando essas fontes secundárias ajuda a padronizar o modelo de dados em toda a organização.
1. Crie um diagrama de relacionamento de entidade de alto nível (ERD) para as fontes de dados que foram identificadas.
1. Converta o ERD de alto nível em um ERD [!DNL Platform] centralizado (incluindo perfis, Eventos de experiência e entidades de pesquisa).

As etapas relacionadas à identificação das fontes de dados aplicáveis necessárias para executar seus casos de uso comercial variam de organização para organização. Embora o restante das seções ao longo deste documento se concentre nas últimas etapas de organização e construção de um ERD após a identificação das fontes de dados, as explicações dos vários componentes do diagrama podem informar suas decisões sobre quais de suas fontes de dados devem ser migradas para [!DNL Platform].

## Criar um ERD de alto nível

Depois de determinar as fontes de dados que deseja trazer para [!DNL Platform], crie um ERD de alto nível para ajudar a orientar o processo de mapeamento de seus dados para schemas XDM.

O exemplo abaixo representa um ERD simplificado para uma empresa que deseja trazer os dados para [!DNL Platform]. O diagrama destaca as entidades essenciais que devem ser classificadas em classes XDM, incluindo contas de clientes, hotéis, endereços e vários eventos comuns de comércio eletrônico.

![](../images/best-practices/erd.png)

## Classificar entidades em categorias de perfis, pesquisas e eventos

Depois de criar um ERD para identificar as entidades essenciais que você gostaria de trazer para [!DNL Platform], essas entidades devem ser classificadas em categorias de perfil, pesquisa e evento:

| Categoria | Descrição |
| --- | --- |
| entidades perfis | As entidades do perfil representam atributos relacionados a uma pessoa individual, normalmente um cliente. As entidades incluídas nesta categoria devem ser representadas por schemas baseados na classe **[!DNL XDM Individual Profile]**. |
| Entidades de pesquisa | As entidades de pesquisa representam conceitos que podem se relacionar a uma pessoa individual, mas não podem ser usadas diretamente para identificar o indivíduo. As entidades incluídas nesta categoria devem ser representadas por schemas baseados em **classes personalizadas**. |
| entidades eventos | As entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, eventos do sistema ou qualquer outro conceito em que você pode desejar rastrear as alterações ao longo do tempo. As entidades incluídas nesta categoria devem ser representadas por schemas baseados na classe **[!DNL XDM ExperienceEvent]**. |

### Considerações para classificação de entidade

As seções abaixo fornecem mais orientações sobre como classificar suas entidades nas categorias acima.

#### Atributos do cliente

Se uma entidade contiver atributos relacionados a um cliente individual, é provável que ela seja uma entidade do perfil. Exemplos de atributos do cliente incluem:

* Detalhes pessoais, como nome, data de nascimento, gênero e ID(s) da conta.
* Informações de localização, como endereços e informações de GPS.
* Informações de contato, como números de telefone e endereços de email.

#### Rastreamento de dados ao longo do tempo

Se você quiser analisar como certos atributos em uma entidade são alterados ao longo do tempo, é provável que seja uma entidade de evento. Por exemplo, adicionar itens de produto a um carrinho pode ser rastreado como eventos de adição ao carrinho em [!DNL Platform]:

| Customer ID | Tipo | Identificação do produto | Quantidade | Carimbo de data e hora |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1 de out de 10:32 |
| 1234567 | Remover | 275098 | 1 | 1 de out de 10:33 |
| 1234567 | Adicionar | 486502 | 3 | 1 de out de 10:41 |
| 1234567 | Adicionar | 910482 | 5 | 3 de out, 14:15 |

#### Casos de uso de segmentação

Ao categorizar suas entidades, é importante pensar nos segmentos de audiência que você pode querer criar para lidar com seus casos específicos de uso comercial.

Por exemplo, uma empresa quer conhecer todos os membros &quot;Ouro&quot; ou &quot;Platinum&quot; de seu programa de fidelidade que fizeram mais de cinco compras no último ano. Com base nesta lógica de segmento, podem ser tiradas as seguintes conclusões sobre a forma como as entidades relevantes devem ser representadas:

* &quot;Ouro&quot; e &quot;Platina&quot; representam status de fidelidade aplicáveis a um cliente individual. Como a lógica do segmento está relacionada somente ao status atual de fidelidade dos clientes, esses dados podem ser modelados como parte de um schema de perfil. Se você deseja rastrear as alterações no status de fidelidade ao longo do tempo, também é possível criar um schema de evento adicional para alterações no status de fidelidade.
* Compras são eventos que ocorrem em um determinado momento, e a lógica do segmento se preocupa com eventos de compra dentro de um intervalo de tempo especificado. Estes dados devem, por conseguinte, ser modelizados como um schema evento.

#### Casos de uso de ativação

Além das considerações sobre casos de uso de segmentação, você também deve revisar os casos de uso de ativação para esses segmentos para identificar atributos relevantes adicionais.

Por exemplo, uma empresa criou um segmento de audiência com base na regra `country = US`. Em seguida, ao ativar esse segmento para determinados públicos alvos downstream, a empresa deseja filtrar todos os perfis exportados com base no estado inicial. Portanto, um atributo `state` também deve ser capturado na entidade do perfil aplicável.

#### Valores agregados

Com base no caso de uso e na granularidade dos dados, você deve decidir se determinados valores precisam ser pré-agregados antes de serem incluídos em uma entidade de perfil ou evento.

Por exemplo, uma empresa deseja criar um segmento com base no número de compras do carrinho. Você pode optar por incorporar esses dados na granularidade mais baixa incluindo cada evento de compra com carimbos de data e hora como sua própria entidade. No entanto, isso pode às vezes aumentar exponencialmente o número de eventos registrados. Para reduzir o número de eventos ingeridos, você pode optar por criar um valor de agregação `numberOfPurchases` em um período de uma semana ou de um mês. Outras funções de agregação, como MIN e MAX, também podem se aplicar a essas situações.

>[!CAUTION]
>
>No momento, o Experience Platform não executa a agregação automática de valor, embora isso esteja planejado para versões futuras. Se você optar por usar valores agregados, deverá executar os cálculos externamente antes de enviar os dados para [!DNL Platform].

#### Cardinalidade

As cardinalidades estabelecidas em seu ERD também podem fornecer algumas pistas sobre como classificar suas entidades. Se houver uma relação um para muitos entre duas entidades, a entidade que representa o &quot;muitos&quot; provavelmente será uma entidade evento. No entanto, também há casos em que &quot;muitos&quot; é um conjunto de entidades de pesquisa que são fornecidas como um storage dentro de uma entidade de perfil.

>[!NOTE]
>
>Como não há uma abordagem universal para atender a todos os casos de uso, é importante considerar os prós e contras de cada situação ao classificar as entidades com base na cardinalidade. Consulte [próxima seção](#pros-and-cons) para obter mais informações.

A tabela a seguir descreve alguns relacionamentos de entidade comuns e as categorias que podem ser derivadas deles:

| Relação | Cardinalidade | Categorias de entidade |
| --- | --- | --- |
| Clientes e Check-outs do carrinho | Um para muitos | Um único cliente pode ter muitos check-outs de carrinho, que são eventos que podem ser rastreados ao longo do tempo. Os clientes seriam, portanto, uma entidade perfil, enquanto os Check-outs do carrinho seriam uma entidade do evento. |
| Clientes e Contas de Fidelidade | Um para um | Um único cliente só pode ter uma conta de fidelidade, e vice-versa. Como o relacionamento é um para um, tanto Clientes quanto Contas de Fidelidade representam entidades de perfil. |
| Clientes e Subscrições | Um para muitos | Um único cliente pode ter muitas subscrições. Como a empresa só está preocupada com as subscrições atuais de um cliente, os Clientes são uma entidade do perfil, enquanto o Subscrição é uma entidade de pesquisa. |

### Prós e contras de diferentes classes de entidade {#pros-and-cons}

Embora a seção anterior tenha fornecido algumas orientações gerais para decidir como categorizar suas entidades, é importante entender que geralmente pode haver prós e contras para escolher uma categoria de entidade em vez de outra. O estudo de caso a seguir destina-se a ilustrar como você pode considerar suas opções nessas situações.

Uma empresa rastreia subscrições ativas para seus clientes, onde um cliente pode ter muitas subscrições. A empresa também deseja incluir subscrições para casos de uso de segmentação, como localizar todos os usuários com subscrições ativas.

Nesse cenário, a empresa tem duas opções possíveis para representar as subscrições de um cliente em seu modelo de dados:

1. [Usar atributos de perfil](#profile-approach)
1. [Usar entidades do evento](#event-approach)

#### Abordagem 1: Usar atributos de perfil {#profile-approach}

A primeira abordagem seria incluir uma matriz de subscrições como atributos na entidade perfil para clientes. Os objetos nesta matriz conteriam campos para `category`, `status`, `planName`, `startDate` e `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Prós**

* A segmentação é viável para o caso de uso pretendido.
* O schema só preservará os registros de subscrição mais recentes de um cliente.

**Cons**

* Toda a matriz deve ser reiniciada sempre que houver alterações em qualquer campo da matriz.
* Se fontes de dados ou unidades de negócios diferentes estiverem alimentando dados no storage, será difícil manter o storage atualizado mais recente sincronizado em todos os canais.

#### Abordagem 2: Usar entidades de evento {#event-approach}

A segunda abordagem seria usar schemas eventos para representar subscrições. Isso implica assimilar os mesmos campos de subscrição da primeira abordagem, com a adição de uma ID de subscrição, uma ID do cliente e um carimbo de data e hora de quando o evento de subscrição ocorreu.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Prós**

* As regras de segmentação podem ser mais flexíveis (como localizar todos os clientes que alteraram suas subscrições nos últimos 30 dias).
* Quando o status da subscrição de um cliente muda, não é mais necessário atualizar uma matriz longa e potencialmente complexa dentro dos atributos do perfil do cliente. Isso é especialmente útil se alterações simultâneas na lista de subscrição do cliente ocorrerem a partir de várias fontes.

**Cons**

* A segmentação torna-se mais complexa para o caso de uso pretendido original (identificando o status das subscrições mais recentes dos clientes). O segmento agora precisa de lógica adicional para sinalizar a última evento de subscrição de um cliente para verificar seu status.

## Criar schemas com base em suas entidades categorizadas

Depois de classificar suas entidades em categorias de perfil, pesquisa e evento, você pode start a conversão do modelo de dados em schemas XDM. Para fins de demonstração, o modelo de dados de exemplo mostrado anteriormente foi classificado como categorias apropriadas no diagrama a seguir:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

A categoria na qual uma entidade foi classificada deve determinar a classe XDM na qual você baseia seu schema. Para reiterar:

* As entidades do perfil devem usar a classe [!DNL XDM Individual Profile].
* As entidades do evento devem usar a classe [!DNL XDM ExperienceEvent].
* As entidades de pesquisa devem usar classes XDM personalizadas definidas pela sua organização.

>[!NOTE]
>
>Embora as entidades eventos quase sempre sejam representadas por schemas separados, as entidades no perfil ou nas categorias de pesquisa podem ser combinadas em um único schema XDM, dependendo de sua cardinalidade.
>
>Por exemplo, como a entidade Clientes tem um relacionamento um para um com a entidade LoyaltyAccounts, o schema da entidade Clientes também pode incluir um objeto `LoyaltyAccount` para conter os campos de fidelidade apropriados para cada cliente. No entanto, se o relacionamento for um para muitos, a entidade que representa o &quot;muitos&quot; poderá ser representada por um schema separado ou por uma matriz de atributos do perfil, dependendo de sua complexidade.

As seções abaixo fornecem orientações gerais sobre a construção de schemas com base em seu ERD.

### Adotar uma abordagem de modelagem iterativa

As [regras de evolução do schema](./composition.md#evolution) ditam que só podem ser feitas alterações não destrutivas nos schemas depois de implementadas. Em outras palavras, depois que um campo é adicionado a um schema e os dados são assimilados nesse campo, o campo não pode mais ser removido. É, portanto, essencial adotar uma abordagem de modelagem iterativa quando você cria seus schemas pela primeira vez, começando com uma implementação simplificada que ganha complexidade progressivamente com o tempo.

Se você não tiver certeza se um campo específico é necessário para incluir em um schema, a prática recomendada é deixá-lo de fora. Se for determinado posteriormente que o campo é necessário, ele sempre poderá ser adicionado na próxima iteração do schema.

### Campos de identidade

No Experience Platform, os campos XDM marcados como identidades são usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Embora um schema possa ter vários campos marcados como identidades, uma única identidade primária deve ser definida para que o schema seja habilitado para uso em [!DNL Real-time Customer Profile]. Consulte a seção sobre [campos de identidade](./composition.md#identity) nas noções básicas da composição do schema para obter informações mais detalhadas sobre o caso de uso desses campos.

Ao projetar seus schemas, qualquer chave primária nas tabelas de banco de dados relacional provavelmente será candidata para identidades primárias. Outros exemplos de campos de identidade aplicáveis são endereços de email do cliente, números de telefone, IDs de conta e [ECID](../../identity-service/ecid.md).

### Misturas de aplicativos Adobe

O Experience Platform fornece várias mixins XDM predefinidos para capturar dados relacionados aos seguintes aplicativos de Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Por exemplo, a [[!UICONTROL Mistura de modelos do Adobe Analytics ExperienceEvent]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) permite mapear campos específicos de [!DNL Analytics] para seus schemas XDM. Dependendo dos aplicativos de Adobe com os quais você está trabalhando, você deve estar usando essas misturas fornecidas pelo Adobe em seus schemas.

<img src="../images/best-practices/analytics-mixin.png" width="700"><br>

As combinações de aplicativo Adobe atribuem automaticamente uma identidade primária padrão por meio do uso do campo `identityMap`, que é um objeto somente leitura gerado pelo sistema que mapeia valores de identidade padrão para um cliente individual.

Para Adobe Analytics, ECID é a identidade primária padrão. Se um valor ECID não for fornecido por um cliente, a identidade primária assumirá como padrão AAID.

>[!IMPORTANT]
>
>Ao usar combinações de aplicativo Adobe, nenhum outro campo deve ser marcado como a identidade primária. Se houver propriedades adicionais que precisam ser marcadas como identidades, esses campos precisam ser atribuídos como identidades secundárias.

## Próximas etapas

Este documento aborda as diretrizes gerais e as práticas recomendadas para o design do modelo de dados para o Experience Platform. Para resumir:

* Use uma abordagem de cima para baixo classificando suas tabelas de dados em categorias de perfil, pesquisa e evento antes de construir seus schemas.
* Muitas vezes, há várias abordagens e opções quando se trata de projetar schemas para diferentes fins.
* Seu modelo de dados deve suportar casos de uso de sua empresa, como segmentação ou análise de jornada do cliente.
* Torne seus schemas o mais simples possível e adicione apenas novos campos quando absolutamente necessário.

Quando estiver pronto, consulte o tutorial em [criar um schema na interface do usuário](../tutorials/create-schema-ui.md) para obter instruções passo a passo sobre como criar um schema, atribuir a classe apropriada para a entidade e adicionar campos para mapear seus dados.