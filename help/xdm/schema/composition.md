---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;tipo de dados;tipos de dados;Tipo de dados;identidade primária;identidade primária;perfil individual XDM;tipo de dados enum;evento de experiência;Evento de experiência XDM;Experience Experience Experience ExperienceEvent;experienceEvent;XDM Experienceevenetet;schema design de ;classe;classes;Classes;datatype;tipo de dados;tipo de dados;Tipo de dados;schemas;Schema;identidadeMap;identidade map;Schema design;mapa;mapa;união schema de dados;união
solution: Experience Platform
tiTle: Basics of Schema Composition
topic: overview
description: Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '3161'
ht-degree: 0%

---


# Noções básicas da composição do schema

Este documento fornece uma introdução aos schemas [!DNL Experience Data Model] (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados no Adobe Experience Platform. Para obter informações gerais sobre o XDM e como ele é usado em [!DNL Platform], consulte [Visão geral do Sistema XDM](../home.md).

## Como entender schemas

Um schema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Em um nível alto, os schemas fornecem uma definição abstrata de um objeto real (como uma pessoa) e descrevem quais dados devem ser incluídos em cada instância desse objeto (como nome, sobrenome, aniversário etc).

Além de descrever a estrutura dos dados, os schemas aplicam restrições e expectativas aos dados para que eles possam ser validados conforme se movem entre os sistemas. Essas definições padrão permitem que os dados sejam interpretados de forma consistente, independentemente da origem, e removem a necessidade de tradução entre aplicativos.

[!DNL Experience Platform] mantém essa normalização semântica com o uso de schemas. Os schemas são a maneira padrão de descrever dados em [!DNL Experience Platform], permitindo que todos os dados que estão em conformidade com schemas sejam reutilizáveis sem conflitos em uma organização e até mesmo compartilháveis entre várias organizações.

### Tabelas relacionais versus objetos incorporados

Ao trabalhar com bancos de dados relacionais, as práticas recomendadas envolvem a normalização de dados, ou a tomada de uma entidade e a divisão em partes discretas que são então exibidas em várias tabelas. Para ler os dados como um todo ou atualizar a entidade, as operações de leitura e gravação devem ser feitas em várias tabelas individuais usando JOIN.

Por meio do uso de objetos incorporados, os schemas XDM podem representar diretamente dados complexos e armazená-los em documentos independentes com uma estrutura hierárquica. Um dos principais benefícios dessa estrutura é que ela permite que você query os dados sem precisar reconstruir a entidade por meio de junções caras a várias tabelas desnormalizadas. Não há restrições rígidas para quantos níveis sua hierarquia de schemas pode ter.

### Schemas e grandes dados

Os sistemas digitais modernos geram grandes quantidades de sinais comportamentais (dados de transação, registros web, internet de coisas, exibição e assim por diante). Esses grandes dados ofertas oportunidades extraordinárias para otimizar experiências, mas são desafiadores para usar devido à escala e variedade dos dados. A fim de obter valor dos dados, a sua estrutura, formato e definições devem ser padronizados de modo a que possam ser processados de forma consistente e eficiente.

Os schemas resolvem esse problema permitindo a integração de dados de várias fontes, padronização por meio de estruturas e definições comuns e compartilhamento entre soluções. Isso permite que processos e serviços subsequentes respondam a qualquer tipo de pergunta que esteja sendo feita sobre os dados, afastando-se da abordagem tradicional à modelagem de dados, onde todas as perguntas que serão feitas sobre os dados são conhecidas antecipadamente e os dados são modelados para atender a essas expectativas.

### Workflows baseados em schemas em [!DNL Experience Platform]

A normalização é um conceito fundamental por trás de [!DNL Experience Platform]. O XDM, impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas padrão para o gerenciamento da experiência do cliente.

A infraestrutura na qual [!DNL Experience Platform] é construído, conhecida como [!DNL XDM System], facilita workflows baseados em schemas e inclui os [!DNL Schema Registry], [!DNL Schema Editor], metadados de schema e padrões de consumo de serviço. Consulte [Visão geral do sistema XDM](../home.md) para obter mais informações.

Há vários benefícios chave para criar e utilizar schemas em [!DNL Experience Platform]. Primeiro, os schemas permitem um melhor controle de dados e minimização de dados, o que é especialmente importante com as regulamentações de privacidade. Segundo, a criação de schemas com componentes padrão do Adobe permite insights prontos e o uso de serviços AI/ML com personalizações mínimas. Por último, os schemas fornecem infraestrutura para informações sobre compartilhamento de dados e orquestração eficiente.

## Planejamento do schema

O primeiro passo para construir um schema é determinar o conceito, ou objeto real, que você está tentando capturar dentro do schema. Depois de identificar o conceito que você está tentando descrever, você pode começar a planejar seu schema pensando sobre coisas como o tipo de dados, campos de identidade potenciais e como o schema pode evoluir no futuro.

### Comportamentos de dados em [!DNL Experience Platform]

Os dados destinados ao uso em [!DNL Experience Platform] são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

Todos os schemas XDM descrevem dados que podem ser classificados como registros ou séries de tempo. O comportamento de dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM são descritas com mais detalhes posteriormente neste documento.

Os schemas de registro e de série de tempo contêm um mapa de identidades (`xdm:identityMap`). Este campo contém a representação de identidade de um assunto, extraída de campos marcados como &quot;Identidade&quot;, conforme descrito na próxima seção.

### [!UICONTROL Identidade] {#identity}

Schemas são usados para assimilar dados em [!DNL Experience Platform]. Esses dados podem ser usados em vários serviços para criar uma visualização única e unificada de uma entidade individual. Portanto, é importante que, ao pensar nos schemas, se pense nas identidades dos clientes e nos campos que podem ser usados para identificar um assunto, independentemente de onde os dados venham.

Para ajudar nesse processo, os campos principais dentro dos schemas podem ser marcados como identidades. Após a ingestão de dados, os dados nesses campos são inseridos no &quot;[!UICONTROL Gráfico de identidade]&quot; desse indivíduo. Os dados do gráfico podem ser acessados por [[!DNL Real-time Customer Profile]](../../profile/home.md) e outros [!DNL Experience Platform] serviços para fornecer uma visualização agrupada de cada cliente individual.

Os campos comumente marcados como &quot;[!UICONTROL Identity]&quot; incluem: endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID CRM ou outros campos de ID exclusivos. Você também deve considerar todos os identificadores exclusivos específicos de sua organização, pois eles também podem ser bons campos &quot;[!UICONTROL Identity]&quot;.

É importante pensar nas identidades dos clientes durante a fase de planejamento do schema, a fim de ajudar a garantir que os dados estejam sendo reunidos para construir o perfil mais robusto possível. Consulte a visão geral do [Adobe Experience Platform Identity Service](../../identity-service/home.md) para saber mais sobre como as informações de identidade podem ajudá-lo a fornecer experiências digitais aos seus clientes.

#### xdm:identityMap {#identityMap}

`xdm:identityMap` é um campo tipo mapa que descreve os vários valores de identidade para um indivíduo, juntamente com suas namespaces associadas. Esse campo pode ser usado para fornecer informações de identidade para seus schemas, em vez de definir valores de identidade dentro da estrutura do próprio schema.

Um exemplo de um mapa de identidade simples seria semelhante ao seguinte:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Como mostra o exemplo acima, cada chave no objeto `identityMap` representa uma namespace de identidade. O valor de cada chave é uma matriz de objetos, representando os valores de identidade (`id`) para a respectiva namespace. Consulte a documentação [!DNL Identity Service] para obter uma [lista de namespaces de identidade padrão](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconhecida pelos aplicativos Adobe.

>[!NOTE]
>
>Um valor booliano para determinar se o valor é uma identidade primária (`primary`) também pode ser fornecido para cada valor de identidade. Só é necessário definir identidades primárias para schemas destinados a serem usados em [!DNL Real-time Customer Profile]. Consulte a seção sobre [schemas de união](#union) para obter mais informações.

### Princípios de evolução do schema {#evolution}

À medida que a natureza das experiências digitais continua a evoluir, também os schemas devem ser utilizados para as representar. Um schema bem projetado pode, portanto, se adaptar e evoluir conforme necessário, sem causar alterações destrutivas em versões anteriores do schema.

Como a manutenção da compatibilidade com versões anteriores é crucial para a evolução do schema, [!DNL Experience Platform] aplica um princípio de controle de versão meramente aditivo para garantir que qualquer revisão do schema resulte apenas em atualizações e alterações não destrutivas. Em outras palavras, **alterações de quebra não são suportadas.**

| Alterações suportadas | Alteração de quebra (não suportado) |
|------------------------------------|---------------------------------|
| <ul><li>Adicionar novos campos a um schema existente</li><li>Como tornar um campo obrigatório opcional</li></ul> | <ul><li>Remoção de campos definidos anteriormente</li><li>Introdução de novos campos obrigatórios</li><li>Renomear ou redefinir campos existentes</li><li>Remoção ou restrição de valores de campo suportados anteriormente</li><li>Mover atributos para um local diferente na árvore</li></ul> |

>[!NOTE]
>
>Se um schema ainda não tiver sido usado para assimilar dados em [!DNL Experience Platform], você pode introduzir uma alteração de quebra nesse schema. No entanto, depois que o schema for usado em [!DNL Platform], ele deverá aderir à política de controle de versão aditiva.

### Schemas e ingestão de dados

Para ingerir dados em [!DNL Experience Platform], um conjunto de dados deve ser criado primeiro. Os conjuntos de dados são os elementos básicos para a transformação e o rastreamento de dados para [[!DNL Catalog Service]](../../catalog/home.md) e geralmente representam tabelas ou arquivos que contêm dados assimilados. Todos os conjuntos de dados são baseados em schemas XDM existentes, que fornecem restrições para o que os dados ingeridos devem conter e como devem ser estruturados. Consulte a visão geral em [Ingestão de dados da Adobe Experience Platform](../../ingestion/home.md) para obter mais informações.

## Elementos básicos de um schema

[!DNL Experience Platform] usa uma abordagem de composição na qual os blocos componentes padrão são combinados para criar schemas. Essa abordagem promove a reutilização dos componentes existentes e orienta a padronização no setor para suportar os schemas e componentes do fornecedor em [!DNL Platform].

Os schemas são compostos usando a seguinte fórmula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Um schema é composto por uma classe e zero ou mais combinações. Isso significa que você pode compor um schema de conjunto de dados sem usar misturas.

### Classe {#class}

A composição de um schema começa com a atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o schema conterá (registro ou série cronológica). Além disso, as classes descrevem o menor número de propriedades comuns que todos os schemas baseados nessa classe precisariam incluir e fornecer uma maneira de vários conjuntos de dados compatíveis serem mesclados.

Uma classe de schemas determina quais combinações serão elegíveis para uso nesse schema. Isso é discutido com mais detalhes na próxima seção [próxima](#mixin).

O Adobe fornece duas classes XDM padrão (&quot;core&quot;): [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização. As classes personalizadas são definidas por uma organização quando não há classes principais definidas por Adobe disponíveis para descrever um caso de uso exclusivo.

### Mistura {#mixin}

Um mixin é um componente reutilizável que define um ou mais campos que implementam certas funções, como detalhes pessoais, preferências de hotel ou endereço. As misturas devem ser incluídas como parte de um schema que implementa uma classe compatível.

As misturas definem a(s) classe(s) com que são compatíveis com base no comportamento dos dados que representam (séries de registros ou de horas). Isso significa que nem todas as combinações estão disponíveis para uso com todas as classes.

[!DNL Experience Platform] inclui muitas combinações de Adobe padrão, além de permitir que os fornecedores definam combinações para seus usuários, e que usuários individuais definam combinações para seus próprios conceitos específicos.

Por exemplo, para capturar detalhes como &quot;[!UICONTROL Nome]&quot; e &quot;[!UICONTROL Endereço Residencial]&quot; para seu schema &quot;[!UICONTROL Membros de Fidelidade]&quot;, você poderá usar combinações padrão que definem esses conceitos comuns. No entanto, conceitos específicos de casos de uso menos comuns (como &quot;[!UICONTROL Nível de Programa de fidelidade]&quot;) geralmente não têm uma combinação predefinida. Nesse caso, você deve definir sua própria combinação para capturar essas informações.

Lembre-se de que os schemas são compostos de combinações &quot;zero ou mais&quot;, o que significa que você pode compor um schema válido sem usar nenhuma mistura.

Para obter uma lista de todas as misturas padrão atuais, consulte o repositório XDM [oficial](https://github.com/adobe/xdm/tree/master/components/mixins).

### Tipo de dados {#data-type}

Os tipos de dados são usados como tipos de campos de referência em classes ou schemas da mesma forma que os campos literais básicos. A principal diferença é que os tipos de dados podem definir vários subcampos. Semelhante a uma combinação, um tipo de dados permite o uso consistente de uma estrutura de vários campos, mas tem mais flexibilidade do que uma combinação, pois um tipo de dados pode ser incluído em qualquer lugar de um schema adicionando-o como o &quot;tipo de dados&quot; de um campo.

>[!NOTE]
>
>Consulte o [apêndice](#mixins-v-datatypes) para obter mais informações sobre as diferenças entre misturas e tipos de dados, e os prós e contras de usar um sobre o outro para casos de uso semelhantes.

[!DNL Experience Platform] fornece vários tipos de dados comuns como parte do  [!DNL Schema Registry] para suportar a utilização de padrões padrão para descrever estruturas de dados comuns. Isso é explicado com mais detalhes nos tutoriais [!DNL Schema Registry], onde ficará mais claro à medida que você percorre as etapas para definir tipos de dados.

### Campo

Um campo é o elemento mais básico de um schema. Os campos fornecem restrições relacionadas ao tipo de dados que podem conter ao definir um tipo de dados específico. Esses tipos básicos de dados definem um único campo, enquanto os [tipos de dados](#data-type) mencionados anteriormente permitem que você defina vários subcampos e reutilize a mesma estrutura de vários campos em vários schemas. Assim, além de definir um &quot;tipo de dados&quot; do campo como um dos tipos de dados definidos no registro, [!DNL Experience Platform] oferece suporte a tipos escalares básicos, como:

* String
* Número inteiro
* Duplo
* Booleano
* Matriz
* Objeto

>[!TIP]
>
>Consulte o [apêndice](#objects-v-freeform) para obter informações sobre os prós e contras do uso de campos de forma livre em campos de tipo de objeto.

Os intervalos válidos desses tipos escalares podem ser restringidos ainda mais a determinados padrões, formatos, mínimos/máximos ou valores predefinidos. Usando essas restrições, uma grande variedade de tipos de campos mais específicos pode ser representada, incluindo:

* Enum
* Longo
* Curto
* Byte
* Data
* Data e hora
* Mapa

>[!NOTE]
>
>O tipo de campo &quot;mapa&quot; permite dados de pares de valores chave, incluindo vários valores para uma única chave. Os mapas só podem ser definidos no nível do sistema, o que significa que você pode encontrar um mapa em um schema definido pelo setor ou pelo fornecedor, mas ele não está disponível para uso nos campos definidos. O [Guia do desenvolvedor da API do Registro do Schema](../api/getting-started.md) contém mais informações sobre a definição de tipos de campos.

Algumas operações de dados usadas por serviços e aplicativos de downstream impõem restrições em tipos de campo específicos. Os serviços afetados incluem, entre outros:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Antes de criar um schema para uso em serviços downstream, reveja a documentação apropriada para esses serviços, a fim de entender melhor os requisitos de campo e as restrições para as operações de dados para as quais o schema se destina.

### Campos XDM

Além dos campos básicos e da capacidade de definir seus próprios tipos de dados, o XDM fornece um conjunto padrão de campos e tipos de dados que são implicitamente compreendidos pelos serviços [!DNL Experience Platform] e proporcionam maior consistência quando usados em [!DNL Platform] componentes.

Esses campos, como &quot;Nome&quot; e &quot;Endereço de email&quot;, contêm conotações adicionadas além dos tipos básicos de campos escalares, informando [!DNL Platform] que quaisquer campos que compartilham o mesmo tipo de dados XDM se comportarão da mesma maneira. Esse comportamento pode ser confiável para ser consistente, independentemente de onde os dados vêm ou em que [!DNL Platform] serviço os dados estão sendo usados.

Consulte o [dicionário de campos XDM](field-dictionary.md) para obter uma lista completa dos campos XDM disponíveis. É recomendável usar campos e tipos de dados XDM sempre que possível para suportar consistência e padronização em [!DNL Experience Platform].

## Exemplo de composição

Os schemas representam o formato e a estrutura dos dados que serão assimilados em [!DNL Platform] e são criados usando um modelo de composição. Como mencionado anteriormente, esses schemas são compostos de uma classe e zero ou mais combinações compatíveis com essa classe.

Por exemplo, um schema que descreve compras feitas em uma loja de varejo pode ser chamado de &quot;[!UICONTROL Transações de loja]&quot;. O schema implementa a classe [!DNL XDM ExperienceEvent] combinada com a combinação padrão [!UICONTROL Commerce] e uma combinação [!UICONTROL Informações do produto] definida pelo usuário.

Outro schema que acompanha o tráfego do site pode ser chamado de &quot;[!UICONTROL Visitas da Web]&quot;. Ela também implementa a classe [!DNL XDM ExperienceEvent], mas dessa vez combina a combinação padrão [!UICONTROL Web].

O diagrama abaixo mostra esses schemas e os campos contribuídos por cada combinação. Ele também contém dois schemas baseados na classe [!DNL XDM Individual Profile], incluindo o schema &quot;[!UICONTROL Membros de Fidelidade]&quot; mencionado anteriormente neste guia.

![](../images/schema-composition/composition.png)

### União {#union}

Embora [!DNL Experience Platform] permita que você componha schemas para casos de uso específicos, também permite que você veja uma &quot;união&quot; de schemas para um tipo de classe específico. O diagrama anterior mostra dois schemas com base na classe XDM ExperienceEvent e dois schemas com base na classe [!DNL XDM Individual Profile]. A união, mostrada abaixo, agregação os campos de todos os schemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], respectivamente).

![](../images/schema-composition/union.png)

Ao ativar um schema para uso com [!DNL Real-time Customer Profile], ele será incluído na união para esse tipo de classe. [!DNL Profile] oferece perfis robustos e centralizados de atributos do cliente, bem como uma conta com carimbos de data e hora de cada evento que o cliente teve em qualquer sistema integrado com  [!DNL Platform]. [!DNL Profile] usa a visualização de união para representar esses dados e fornecer uma visualização holística de cada cliente individual.

Para obter mais informações sobre como trabalhar com [!DNL Profile], consulte [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Mapeamento de arquivos de dados para schemas XDM

Todos os arquivos de dados que são ingeridos em [!DNL Experience Platform] devem estar em conformidade com a estrutura de um schema XDM. Para obter mais informações sobre como formatar arquivos de dados de acordo com hierarquias XDM (incluindo arquivos de amostra), consulte o documento em [amostras de transformações ETL](../../etl/transformations.md). Para obter informações gerais sobre como assimilar arquivos de dados em [!DNL Experience Platform], consulte [visão geral da ingestão em lote](../../ingestion/batch-ingestion/overview.md).

## Próximas etapas

Agora que você entende as noções básicas da composição do schema, está pronto para começar a explorar e criar schemas usando o [!DNL Schema Registry].

Para revisar a estrutura das duas classes XDM principais e suas misturas compatíveis comumente usadas, consulte a seguinte documentação de referência:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

O [!DNL Schema Registry] é usado para acessar o [!DNL Schema Library] no Adobe Experience Platform e fornece uma interface de usuário e uma RESTful API a partir da qual todos os recursos de biblioteca disponíveis estão acessíveis. O [!DNL Schema Library] contém recursos do setor definidos pelo Adobe, recursos do fornecedor definidos pelos parceiros [!DNL Experience Platform] e classes, mixins, tipos de dados e schemas que foram compostos por membros da sua organização.

Para começar a compor o schema usando a interface do usuário, siga o [tutorial do Editor de Schemas](../tutorials/create-schema-ui.md) para criar o schema &quot;Membros de Fidelidade&quot; mencionado neste documento.

Para começar a usar a API [!DNL Schema Registry], leia o [Guia do desenvolvedor da API de Registro de Schemas](../api/getting-started.md). Depois de ler o guia do desenvolvedor, siga as etapas descritas no tutorial em [criar um schema usando a API do Registro do Schema](../tutorials/create-schema-api.md).

## Apêndice

A seção seguinte contém informações adicionais relativas aos princípios da composição do schema.

### Objetos versus campos de forma livre {#objects-v-freeform}

Há alguns fatores chave a serem considerados ao escolher objetos em vez de campos de forma livre ao projetar seus schemas:

| Objetos | Campos de forma livre |
| --- | --- |
| Aumenta o aninhamento | Menos ou sem aninhamento |
| Cria agrupamentos de campos lógicos | Os campos são colocados em locais ad-hoc |

#### Objetos

Os prós e contras do uso de objetos em campos de forma livre estão listados abaixo.

**Vantagens**:

* Os objetos são melhor usados quando você deseja criar um agrupamento lógico de determinados campos.
* Os objetos organizam o schema de forma mais estruturada.
* Os objetos ajudam indiretamente na criação de uma boa estrutura de menu na interface do usuário do Construtor de segmentos. Os campos agrupados dentro do schema são refletidos diretamente na estrutura de pastas fornecida na interface do usuário do Construtor de segmentos.

**Cons**:

* Os campos ficam mais aninhados.
* Ao usar [Adobe Experience Platform Query Service](../../query-service/home.md), strings de referência mais longas devem ser fornecidas para campos de query aninhados em objetos.

#### Campos de forma livre

Os prós e contras do uso de campos de forma livre sobre objetos estão listados abaixo.

**Vantagens**:

* Campos de forma livre são criados diretamente sob o objeto raiz do schema (`_tenantId`), aumentando a visibilidade.
* As strings de referência para campos de forma livre tendem a ser mais curtas ao usar o Serviço de Query.

**Cons**:

* O local dos campos de forma livre no schema é ad-hoc, o que significa que eles aparecem em ordem alfabética no Editor de Schemas. Isso pode tornar os schemas menos estruturados, e campos de forma livre semelhantes podem acabar muito separados dependendo de seus nomes.