---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;enum;identidade primária;identidade primária;perfil individual XDM;evento de experiência;Evento de experiência XDM;ExperienceEvent XDM;experienceEvent;experienceevent;XDM Experienceevent;design de esquema;práticas recomendadas
solution: Experience Platform
title: Práticas Recomendadas Para Modelagem De Dados
description: Este documento fornece uma introdução aos esquemas do Experience Data Model (XDM) e aos componentes, princípios e práticas recomendadas para a composição de esquemas a serem usados no Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7a763a978443c0a074e6368448320056759f72bb
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 1%

---

# Práticas recomendadas de modelagem de dados

O [!DNL Experience Data Model] (XDM) é a estrutura principal que padroniza os dados de experiência do cliente fornecendo estruturas e definições comuns para uso nos serviços downstream do Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum e usados para obter insights valiosos das ações do cliente, definir públicos-alvo do cliente e expressar atributos do cliente para fins de personalização.

Como o XDM é extremamente versátil e personalizável por design, é importante seguir as práticas recomendadas para a modelagem de dados ao projetar seus esquemas. Este documento aborda as principais decisões e considerações que você deve tomar ao mapear os dados de experiência do cliente para o XDM.

## Introdução

Antes de ler este guia, revise a [Visão geral do sistema XDM](../home.md) para obter uma introdução geral ao XDM e sua função no Experience Platform.

Como este guia se concentra exclusivamente nas principais considerações relacionadas ao design do esquema, é altamente recomendável ler as [noções básicas da composição do esquema](./composition.md) para obter explicações detalhadas dos elementos do esquema individuais mencionados neste guia.

## Resumo de práticas recomendadas {#summary}

A abordagem recomendada para projetar seu modelo de dados para uso no Experience Platform pode ser resumida da seguinte maneira:

1. Entenda os casos de uso de negócios para seus dados.
1. Identifique as principais fontes de dados que devem ser trazidas para o Experience Platform para lidar com esses casos de uso.
1. Identifique quaisquer fontes de dados secundárias que também possam ser de interesse. Por exemplo, se atualmente apenas uma unidade de negócios em sua organização estiver interessada em portar seus dados para o Experience Platform, uma unidade de negócios semelhante também poderá estar interessada em portar dados semelhantes no futuro. Considerar essas fontes secundárias ajuda a padronizar o modelo de dados em toda a organização.
1. Crie um diagrama de relacionamento de entidade de alto nível (ERD) para as fontes de dados que foram identificadas.
1. Converta o ERD de alto nível em um ERD centrado na Experience Platform (incluindo perfis, eventos de experiência e entidades de pesquisa).

As etapas relacionadas à identificação das fontes de dados aplicáveis necessárias para realizar os casos de uso de negócios variam de uma organização para outra. Embora o restante das seções neste documento se concentre nas últimas etapas de organização e construção de um ERD após a identificação das fontes de dados, as explicações dos vários componentes do diagrama podem informar suas decisões sobre qual das suas fontes de dados deve ser migrada para o Experience Platform.

## Criar um ERD de alto nível {#create-an-erd}

Depois de determinar as fontes de dados que deseja trazer para o Experience Platform, crie um ERD de alto nível para ajudar a orientar o processo de mapeamento de seus dados para esquemas XDM.

O exemplo abaixo representa um ERD simplificado para uma empresa que deseja trazer dados para o Experience Platform. O diagrama destaca as entidades essenciais que devem ser classificadas em classes XDM, incluindo contas de clientes, hotéis e vários eventos comuns de comércio eletrônico.

![Um diagrama relacional de entidade que destaca as entidades essenciais que devem ser classificadas em classes XDM para assimilação de dados.](../images/best-practices/erd.png)

## Classificar entidades em categorias de perfil, pesquisa e evento {#sort-entities}

Depois de criar um ERD para identificar as entidades essenciais que você gostaria de trazer para o Experience Platform, essas entidades devem ser classificadas em categorias de perfil, pesquisa e evento:

| Categoria | Descrição |
| --- | --- |
| Entidades de perfil | As entidades de perfil representam atributos relacionados a uma pessoa individual, normalmente um cliente. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados na classe **[!DNL XDM Individual Profile]**. |
| Pesquisar entidades | As entidades de pesquisa representam conceitos que podem estar relacionados a uma pessoa individual, mas não podem ser usados diretamente para identificá-la. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados em **classes personalizadas**, e estão vinculadas a perfis e eventos por meio de [relações de esquema](../tutorials/relationship-ui.md). |
| Entidades de evento | As entidades de evento representam conceitos relacionados às ações que um cliente pode realizar, eventos do sistema ou quaisquer outros conceitos nos quais você possa querer rastrear as alterações ao longo do tempo. As entidades que se enquadram nesta categoria devem ser representadas por esquemas baseados na classe **[!DNL XDM ExperienceEvent]**. |

{style="table-layout:auto"}

### Considerações para classificação de entidade {#considerations}

As seções abaixo fornecem mais orientação sobre como classificar as entidades nas categorias acima.

#### Dados mutáveis e imutáveis {#mutable-and-immutable-data}

Uma maneira primária de classificar entre categorias de entidade é se os dados capturados são mutáveis ou não.

Os atributos pertencentes a perfis ou entidades de pesquisa normalmente são mutáveis. Por exemplo, as preferências de um cliente podem mudar com o tempo e os parâmetros de um plano de assinatura podem ser atualizados, dependendo das tendências do mercado.

Por outro lado, os dados do evento normalmente são imutáveis. Como os eventos são anexados a um carimbo de data e hora específico, o &quot;instantâneo do sistema&quot; fornecido por um evento não é alterado. Por exemplo, um evento pode capturar as preferências de um cliente ao finalizar a compra de um carrinho e não é alterado mesmo que as preferências do cliente acabem sendo alteradas posteriormente. Os dados do evento não podem ser alterados após serem registrados.

Em resumo, perfis e entidades de pesquisa contêm atributos mutáveis e representam as informações mais atuais sobre os assuntos capturados, enquanto eventos são registros imutáveis do sistema em um momento específico.

#### Atributos do cliente {#customer-attributes}

Se uma entidade contiver atributos relacionados a um cliente individual, ela provavelmente será uma entidade de perfil. Exemplos de atributos do cliente incluem:

* Detalhes pessoais, como nome, data de nascimento, sexo e ID(s) da conta.
* Informações de localização, como endereços e informações de GPS.
* Informações de contato, como números de telefone e endereços de email.

#### Rastreamento de dados ao longo do tempo {#track-data}

Se você quiser analisar como determinados atributos em uma entidade mudam ao longo do tempo, ela provavelmente será uma entidade de evento. Por exemplo, a adição de itens de produto a um carrinho pode ser rastreada como eventos de adição ao carrinho no Experience Platform:

| ID do cliente | Tipo | Identificação do produto | Quantidade | Carimbo de data e hora |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1º de outubro, 10h:32 |
| 1234567 | Remover | 275098 | 1 | 1º de outubro, 10h:33 |
| 1234567 | Add | 486502 | 1 | 1º de outubro, 10h:41 |
| 1234567 | Add | 910482 | 5 | 3 de outubro, 2:15 PM |

{style="table-layout:auto"}

#### Casos de uso de segmentação {#segmentation-use-cases}

Ao categorizar suas entidades, é importante pensar nos públicos que você pode querer criar para atender aos casos de uso específicos da empresa.

Por exemplo, uma empresa quer conhecer todos os membros &quot;Ouro&quot; ou &quot;Platina&quot; de seu programa de fidelidade que fizeram mais de cinco compras no ano passado. Com base nesta lógica de segmentação, podem ser tiradas as seguintes conclusões sobre a forma como as entidades relevantes devem ser representadas:

* &quot;Ouro&quot; e &quot;Platina&quot; representam status de fidelidade aplicáveis a um cliente individual. Como a lógica de segmentação só se preocupa com o status de fidelidade atual dos clientes, esses dados podem ser modelados como parte de um esquema de perfil. Se você quiser rastrear as alterações no status de fidelidade ao longo do tempo, também poderá criar um esquema de evento adicional para as alterações no status de fidelidade.
* Compras são eventos que ocorrem em um momento específico e a lógica de segmentação se refere a eventos de compra em uma janela de tempo especificada. Portanto, esses dados devem ser modelados como um schema de evento.

#### Casos de uso de ativação {#activation-use-cases}

Além das considerações relacionadas aos casos de uso de segmentação, você também deve revisar os casos de uso de ativação para esses públicos-alvo para identificar atributos relevantes adicionais.

Por exemplo, uma empresa criou um público-alvo com base na regra que `country = US`. Em seguida, ao ativar esse público-alvo para determinados destinos downstream, a empresa deseja filtrar todos os perfis exportados com base no estado inicial. Portanto, um atributo `state` também deve ser capturado na entidade de perfil aplicável.

#### Valores agregados {#aggregated-values}

Com base no caso de uso e na granularidade dos dados, você deve decidir se determinados valores precisam ser pré-agregados antes de serem incluídos em um perfil ou entidade de evento.

Por exemplo, uma empresa deseja criar um público-alvo com base no número de compras de carrinho. Você pode optar por incorporar esses dados na menor granularidade ao incluir cada evento de compra com carimbo de data e hora como sua própria entidade. No entanto, às vezes isso pode aumentar o número de eventos registrados exponencialmente. Para reduzir o número de eventos assimilados, você pode optar por criar um valor agregado `numberOfPurchases` durante uma semana ou um mês. Outras funções agregadas, como MIN e MAX, também podem ser aplicadas a essas situações.

>[!CAUTION]
>
>No momento, o Experience Platform não executa a agregação automática de valores, embora isso esteja planejado para versões futuras. Se você optar por usar valores agregados, deverá realizar os cálculos externamente antes de enviar os dados para o Experience Platform.

#### Cardinalidade {#cardinality}

As cardinalidades estabelecidas no seu ERD também podem fornecer algumas pistas sobre como categorizar suas entidades. Se houver uma relação um para muitos entre duas entidades, a entidade que representa o &quot;muitos&quot; provavelmente será uma entidade de evento. No entanto, também há casos em que &quot;muitos&quot; é um conjunto de entidades de pesquisa que são fornecidas como uma matriz em uma entidade de perfil.

>[!NOTE]
>
>Como não há uma abordagem universal para todos os casos de uso, é importante considerar os prós e os contras de cada situação ao categorizar entidades com base na cardinalidade. Consulte a [próxima seção](#pros-and-cons) para obter mais informações.

A tabela a seguir descreve alguns relacionamentos de entidade comuns e as categorias que podem ser derivadas deles:

| Relação | Cardinalidade | Categorias de entidade |
| --- | --- | --- |
| Cliente e finalização do carrinho | De um para muitos | Um único cliente pode ter muitos check-outs do carrinho, que são eventos que podem ser rastreados ao longo do tempo. O cliente seria, portanto, uma entidade de perfil, enquanto o Check-out do carrinho seria uma entidade de evento. |
| Conta de Cliente e Fidelidade | Um para um | Um único cliente pode ter apenas uma conta de fidelidade, e uma conta de fidelidade só pode pertencer a um cliente. Como o relacionamento é individualizado, o Cliente e a Conta de fidelidade representam entidades de perfil. |
| Cliente e Assinatura | De um para muitos | Um único cliente pode ter muitas assinaturas. Como a empresa se preocupa somente com as assinaturas atuais de um cliente, o Cliente é uma entidade de perfil, enquanto a Assinatura é uma entidade de pesquisa. |

{style="table-layout:auto"}

### Vantagens e desvantagens de diferentes classes de entidade {#pros-and-cons}

Embora a seção anterior tenha fornecido algumas diretrizes gerais para decidir como categorizar suas entidades, é importante entender que geralmente pode haver vantagens e desvantagens em escolher uma categoria de entidade em vez de outra. O estudo de caso a seguir ilustra como você pode considerar suas opções nessas situações.

Uma empresa rastreia assinaturas ativas para seus clientes, onde um cliente pode ter muitas assinaturas. A empresa também deseja incluir assinaturas para casos de uso de segmentação, como encontrar todos os usuários com assinaturas ativas.

Nesse cenário, a empresa tem duas opções possíveis para representar as assinaturas de um cliente em seu modelo de dados:

1. [Usar atributos de perfil](#profile-approach)
1. [Usar entidades de evento](#event-approach)

#### Abordagem 1: usar atributos de perfil {#profile-approach}

A primeira abordagem seria incluir uma matriz de `subscriptionID` na entidade de perfil do Cliente.

![O esquema do Cliente no Editor de Esquemas com a classe e a estrutura realçadas](../images/best-practices/profile-schema.png)

**Vantagens**

* A segmentação é viável para o caso de uso pretendido.
* O esquema preserva apenas os registros de assinatura mais recentes de um cliente.

**Contras**

* A matriz inteira deve ser reiterada sempre que ocorrerem alterações em qualquer campo na matriz.
* Se diferentes fontes de dados ou unidades de negócios estiverem alimentando dados no array, torna-se desafiador manter o array atualizado mais recente sincronizado em todos os canais.

#### Abordagem 2: usar entidades de evento {#event-approach}

A segunda abordagem seria usar schemas de evento para representar um evento de subscrição. Isso incluiria a ID de assinatura junto com uma ID do cliente e um carimbo de data e hora de quando o evento de assinatura ocorreu.

![Um diagrama do esquema de Evento de Inscrição com a classe de Evento de Experiência XDM e a estrutura de inscrições realçadas.](../images/best-practices/event-schema.png)

**Vantagens**

* As regras de segmentação podem ser mais flexíveis (como encontrar todos os clientes que alteraram suas assinaturas nos últimos 30 dias).
* Quando o status da assinatura de um cliente muda, você não precisa mais atualizar um array longo e potencialmente complexo nos atributos do perfil do cliente. Isso é especialmente útil se ocorrerem alterações simultâneas na lista de assinaturas do cliente a partir de várias fontes.

**Contras**

* A segmentação se torna mais complexa para o caso de uso pretendido original (identificando o status das assinaturas mais recentes dos clientes). O público-alvo agora precisa de lógica adicional para sinalizar o último evento de assinatura para que um cliente verifique seu status.
* Os eventos têm um risco maior de expiração automática e de serem removidos da loja de perfis. Consulte o manual sobre [Expirações do evento de experiência](../../profile/event-expirations.md) para obter mais informações.

## Criar esquemas com base nas entidades categorizadas {#schemas-for-categorized-entities}

Depois de classificar as entidades em perfis, pesquisas e categorias de eventos, você pode começar a converter o modelo de dados em esquemas XDM. Para fins de demonstração, o modelo de dados de exemplo mostrado anteriormente foi classificado em categorias apropriadas no diagrama a seguir:

![Um diagrama dos esquemas contidos nas entidades de perfil, pesquisa e evento](../images/best-practices/erd-sorted.png)

A categoria em que uma entidade foi classificada deve determinar a classe XDM na qual você baseia seu esquema. Para reiterar:

* As entidades de perfil devem usar a classe [!DNL XDM Individual Profile].
* As entidades de evento devem usar a classe [!DNL XDM ExperienceEvent].
* As entidades de pesquisa devem usar classes XDM personalizadas definidas por sua organização. As entidades de perfil e evento podem fazer referência a essas entidades de pesquisa por meio de relacionamentos de esquema.

>[!NOTE]
>
>Embora as entidades do evento sejam quase sempre representadas por esquemas separados, as entidades no perfil ou nas categorias de pesquisa podem ser combinadas em um único esquema XDM, dependendo de sua cardinalidade.
>
>Por exemplo, como a entidade Cliente tem um relacionamento um para um com a entidade LoyaltyAccount, o esquema para a entidade Cliente também pode incluir um objeto `LoyaltyAccount` para conter os campos de fidelidade apropriados para cada cliente. Se a relação for um para muitos, no entanto, a entidade que representa o &quot;muitos&quot; pode ser representada por um schema separado ou uma matriz de atributos de perfil, dependendo de sua complexidade.

As seções abaixo fornecem orientações gerais sobre a construção de esquemas com base no seu ERD.

### Adotar uma abordagem de modelagem iterativa {#iterative-modeling}

As [regras de evolução do esquema](./composition.md#evolution) determinam que somente alterações não destrutivas poderão ser feitas nos esquemas depois de implementadas. Em outras palavras, depois que você adiciona um campo a um esquema e os dados são assimilados nesse campo, o campo não pode mais ser removido. Portanto, é essencial adotar uma abordagem de modelagem iterativa ao criar seus esquemas pela primeira vez, começando com uma implementação simplificada que ganha progressivamente complexidade ao longo do tempo.

Se você não tiver certeza se um campo específico é necessário incluir em um esquema, a prática recomendada é deixá-lo de fora. Se posteriormente for determinado que o campo é necessário, ele sempre poderá ser adicionado na próxima iteração do schema.

### Campos de identidade {#identity-fields}

No Experience Platform, os campos XDM marcados como identidades são usados para unir informações sobre clientes individuais provenientes de várias fontes de dados. Embora um esquema possa ter vários campos marcados como identidades, uma única identidade primária deve ser definida para que o esquema seja habilitado para uso em [!DNL Real-Time Customer Profile]. Consulte a seção sobre [campos de identidade](./composition.md#identity) nas noções básicas da composição de esquema para obter informações mais detalhadas sobre o caso de uso desses campos.

Ao criar seus esquemas, todas as chaves primárias nas tabelas do banco de dados relacional provavelmente são candidatas a identidades primárias. Outros exemplos de campos de identidade aplicáveis são endereços de email de clientes, números de telefone, IDs de conta e [ECID](../../identity-service/features/ecid.md).

### Grupos de campos de esquema do aplicativo Adobe {#adobe-application-schema-field-groups}

O Experience Platform fornece vários grupos de campos de esquema XDM prontos para uso para capturar dados relacionados aos seguintes aplicativos da Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Por exemplo, você pode usar o [[!UICONTROL Adobe Analytics ExperienceEvent Template] grupo de campos](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) para mapear campos específicos do [!DNL Analytics] para seus esquemas XDM. Dependendo dos aplicativos do Adobe com os quais você está trabalhando, você deve usar esses grupos de campos fornecidos pela Adobe em seus esquemas.

![Um diagrama de esquema do [!UICONTROL Adobe Analytics ExperienceEvent Template].](../images/best-practices/analytics-field-group.png)

Os grupos de campos de aplicativos do Adobe atribuem automaticamente uma identidade primária padrão por meio do uso do campo `identityMap`, que é um objeto somente leitura gerado pelo sistema que mapeia valores de identidade padrão para um cliente individual.

Para o Adobe Analytics, a ECID é a identidade principal padrão. Se um valor de ECID não for fornecido por um cliente, a identidade principal assumirá AAID como padrão.

>[!IMPORTANT]
>
>Ao usar grupos de campos de aplicativo do Adobe, nenhum outro campo deve ser marcado como a identidade principal. Se houver propriedades adicionais que precisam ser marcadas como identidades, esses campos deverão ser atribuídos como identidades secundárias.

## Campos de validação de dados {#data-validation-fields}

Ao assimilar dados no data lake, a validação de dados é imposta apenas para campos restritos. Para validar um campo específico durante a assimilação em lote, você deve marcar o campo como restrito no esquema XDM. Para evitar que dados inválidos entrem no Experience Platform, defina seus requisitos de validação ao criar seus esquemas.

>[!IMPORTANT]
>
>A validação não se aplica a colunas aninhadas. Se o formato do campo estiver localizado em uma coluna de matriz, os dados não serão validados.

Para definir restrições em um campo, selecione o campo no Editor de Esquemas para abrir a barra lateral **[!UICONTROL Field properties]**. Consulte a documentação em [propriedades de campo específicas do tipo](../ui/fields/overview.md#type-specific-properties) para obter descrições exatas dos campos disponíveis.

![O Editor de Esquemas com os campos de restrição realçados na barra lateral [!UICONTROL Field properties].](../images/best-practices/data-validation-fields.png)

### Dicas para manter a integridade dos dados {#data-integrity-tips}

As sugestões a seguir ajudam a manter a integridade dos dados ao criar um esquema.

* **Considerar identidades primárias**: para produtos da Adobe como Web SDK, Mobile SDK, Adobe Analytics e Adobe Journey Optimizer, o campo `identityMap` geralmente serve como a identidade primária. Evite designar campos adicionais como identidades primárias para esse esquema.
* **Verifique se `_id` não está sendo usado como uma identidade**: o campo `_id` nos esquemas de Evento de Experiência não pode ser usado como uma identidade porque se destina à exclusividade do registro.
* **Definir restrições de comprimento**: é prática recomendada definir comprimentos mínimos e máximos em campos marcados como identidades. Um aviso será acionado se você tentar atribuir um namespace personalizado a um campo de identidade sem atender às restrições de comprimento mínimo e máximo. Essas limitações ajudam a manter a consistência e a qualidade dos dados.
* **Aplicar padrões para valores consistentes**: se os valores de identidade seguirem um padrão específico, use a configuração **[!UICONTROL Pattern]** para impor restrições. Essa configuração pode incluir regras como somente dígitos, maiúsculas ou minúsculas ou combinações de caracteres específicas. Use expressões regulares para corresponder padrões em suas cadeias de caracteres.
* **Limitar eVars em esquemas do Analytics**: normalmente, um esquema do Analytics deve ter apenas uma eVar designada como uma identidade. Se você pretende usar mais de uma eVar como identidade, verifique se a estrutura de dados pode ser otimizada.
* **Garantir a exclusividade de um campo selecionado**: o campo escolhido deve ser exclusivo em comparação à identidade primária no esquema. Se não estiver, não marque-a como uma identidade. Por exemplo, se vários clientes puderem fornecer o mesmo endereço de email, esse namespace não será uma identidade adequada. Esse princípio também se aplica a outros namespaces de identidade, como números de telefone. Marcar um campo não exclusivo como uma identidade pode causar o recolhimento indesejado do perfil.
* **Verificar comprimento mínimo da cadeia de caracteres**: todos os campos da cadeia de caracteres devem ter pelo menos um caractere, pois os valores da cadeia de caracteres nunca devem estar vazios. Valores nulos para campos não obrigatórios, no entanto, são aceitáveis. Por padrão, os novos campos de sequência recebem um comprimento mínimo de um.

## Gerenciamento de esquemas habilitados para perfil {#managing-profile-enabled-schemas}

Esta seção explica como gerenciar esquemas que já estão ativados para o Perfil de cliente em tempo real. Depois que um esquema é ativado, não é possível desativá-lo ou excluí-lo. Você deve determinar como evitar mais uso e como gerenciar conjuntos de dados que não podem ser excluídos.

Depois que um esquema é ativado para o Perfil, a configuração não pode ser revertida. Se um schema não deve mais ser usado, renomeie-o para esclarecer seu status e criar um schema de substituição com a estrutura e a configuração de identidade corretas. Isso ajuda a impedir a reutilização acidental do esquema obsoleto quando os usuários criam novos conjuntos de dados ou configuram fluxos de trabalho de assimilação.

Os conjuntos de dados do sistema às vezes aparecem junto com esquemas habilitados para o Perfil do cliente em tempo real. Não é possível excluir conjuntos de dados do sistema, mesmo quando o esquema associado está obsoleto. Para evitar o uso não intencional, renomeie o esquema descontinuado habilitado para perfis e confirme se nenhum fluxo de trabalho de assimilação aponta para o conjunto de dados do sistema que permanece em vigor.

Use as práticas recomendadas a seguir para evitar a reutilização acidental de esquemas descontinuados habilitados para perfis:

* Use uma convenção de nomenclatura clara ao descontinuar um esquema. Inclua rótulos como &quot;Obsoleto&quot;, &quot;Não usar&quot; ou uma tag de versão.
* Pare de assimilar dados em qualquer conjunto de dados com base no esquema que deseja desativar.
* Crie um novo esquema com a estrutura correta, a configuração de identidade e o padrão de nomenclatura.
* Revise os conjuntos de dados do sistema que não podem ser excluídos e verifique se nenhum fluxo de trabalho de assimilação faz referência a eles.
* Documente a alteração internamente para que outros usuários entendam por que o esquema está obsoleto.

>[!TIP]
>
>Consulte o [guia de solução de problemas do XDM](../troubleshooting-guide.md#delete-profile-enabled) para obter orientação adicional sobre esquemas habilitados para perfil e limitações relacionadas.

## Próximas etapas

Este documento aborda as diretrizes gerais e as práticas recomendadas para projetar seu modelo de dados para o Experience Platform. Para resumir:

* Classifique as tabelas de dados em categorias de perfil, pesquisa e evento antes de construir seus esquemas.
* Avalie várias abordagens ao criar esquemas para casos de uso diferentes.
* Certifique-se de que seu modelo de dados seja compatível com suas metas de segmentação ou jornada de clientes.
* Mantenha os esquemas o mais simples possível. Adicione novos campos somente quando necessário.

Quando estiver pronto, consulte o tutorial sobre [criação de um esquema na interface](../tutorials/create-schema-ui.md) para obter instruções passo a passo sobre criação de esquema, atribuição de classe e mapeamento de campo.
