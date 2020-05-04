---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Noções básicas da composição do schema
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Noções básicas da composição do schema

Este documento fornece uma introdução aos schemas do Experience Data Model (XDM) e aos blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados na Adobe Experience Platform. Para obter informações gerais sobre o XDM e como ele é usado na Plataforma, consulte a visão geral [do Sistema](../home.md)XDM.

## Como entender schemas

Um schema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Em um nível alto, os schemas fornecem uma definição abstrata de um objeto real (como uma pessoa) e descrevem quais dados devem ser incluídos em cada instância desse objeto (como nome, sobrenome, aniversário etc).

Além de descrever a estrutura dos dados, os schemas aplicam restrições e expectativas aos dados para que eles possam ser validados conforme se movem entre os sistemas. Essas definições padrão permitem que os dados sejam interpretados de forma consistente, independentemente da origem, e removem a necessidade de tradução entre aplicativos.

A plataforma de experiência mantém essa normalização semântica com o uso de schemas. Os Schemas são a forma padrão de descrever dados na plataforma da experiência, permitindo que todos os dados que estão em conformidade com os schemas sejam reutilizáveis sem conflitos em uma organização e até mesmo compartilháveis entre várias organizações.

### Tabelas relacionais versus objetos incorporados

Ao trabalhar com bancos de dados relacionais, as práticas recomendadas envolvem a normalização de dados, ou a tomada de uma entidade e a divisão em partes discretas que são então exibidas em várias tabelas. Para ler os dados como um todo ou atualizar a entidade, as operações de leitura e gravação devem ser feitas em várias tabelas individuais usando JOIN.

Por meio do uso de objetos incorporados, os schemas XDM podem representar diretamente dados complexos e armazená-los em documentos independentes com estrutura hierárquica. Um dos principais benefícios dessa estrutura é que ela permite que você query os dados sem precisar reconstruir a entidade por meio de junções caras a várias tabelas desnormalizadas.

### Schemas e grandes dados

Os sistemas digitais modernos geram grandes quantidades de sinais comportamentais (dados de transação, registros web, internet de coisas, exibição e assim por diante). Esses grandes dados ofertas oportunidades extraordinárias para otimizar experiências, mas são desafiadores para usar devido à escala e variedade dos dados. A fim de obter valor dos dados, a sua estrutura, formato e definições devem ser padronizados de modo a que possam ser processados de forma consistente e eficiente.

Os Schemas resolvem esse problema permitindo a integração de dados de várias fontes, padronização por meio de estruturas e definições comuns e compartilhamento entre soluções. Isso permite que processos e serviços subsequentes respondam a qualquer tipo de pergunta que esteja sendo feita sobre os dados, afastando-se da abordagem tradicional à modelagem de dados, onde todas as perguntas que serão feitas sobre os dados são conhecidas antecipadamente e os dados são modelados para atender a essas expectativas.

### workflows baseados em Schemas na plataforma Experience

A normalização é um conceito fundamental por trás da plataforma da experiência. O XDM, impulsionado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas padrão para o gerenciamento da experiência do cliente.

A infraestrutura na qual a Experience Platform é construída, conhecida como Sistema XDM, facilita workflows baseados em schemas e inclui o Registro do Schema, o Editor de Schemas, os metadados do schema e os padrões de consumo de serviço. See the [XDM System overview](../home.md) for more information.

## Planejamento do schema

O primeiro passo para construir um schema é determinar o conceito, ou objeto real, que você está tentando capturar dentro do schema. Depois de identificar o conceito que você está tentando descrever, você pode começar a planejar seu schema pensando sobre coisas como o tipo de dados, campos de identidade potenciais e como o schema pode evoluir no futuro.

### Comportamentos de dados na plataforma Experience

Os dados destinados ao uso na plataforma Experience são agrupados em dois tipos de comportamento:

* **Registrar dados**: Fornece informações sobre os atributos de um assunto. Um sujeito pode ser uma organização ou um indivíduo.
* **Dados** das séries cronológicas: Fornece um instantâneo do sistema no momento em que uma ação foi tomada, direta ou indiretamente, por um participante do registro.

Todos os schemas XDM descrevem dados que podem ser classificados como registros ou séries de tempo. O comportamento de dados de um schema é definido pela **classe** schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM são descritas com mais detalhes posteriormente neste documento.

Os schemas de registro e de série de tempo contêm um mapa de identidades (`xdm:identityMap`). Este campo contém a representação de identidade de um assunto, extraída de campos marcados como &quot;Identidade&quot;, conforme descrito na próxima seção.

### Identidade

Os Schemas são usados para assimilar dados na Experience Platform. Esses dados podem ser usados em vários serviços para criar uma visualização única e unificada de uma entidade individual. Portanto, é importante que, ao pensar nos schemas, se pense em &quot;Identidade&quot; e em quais campos podem ser usados para identificar um indivíduo, independentemente de onde os dados venham.

Para ajudar nesse processo, os campos principais podem ser marcados como &quot;Identidade&quot;. Após a ingestão dos dados, os dados nesses campos serão inseridos no &quot;Gráfico de identidade&quot; desse indivíduo. Os dados do gráfico podem ser acessados pelo Perfil [do cliente em tempo](../../profile/home.md) real e por outros serviços da plataforma de experiência para fornecer uma visualização agrupada de cada cliente individual.

Os campos comumente marcados como &quot;Identidade&quot; incluem: endereço de email, número de telefone, [Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/pt-BR/id-service/using/home.html), CRM ID ou outros campos de ID exclusivos. Você também deve considerar todos os identificadores exclusivos específicos de sua organização, pois eles também podem ser bons campos de &quot;Identidade&quot;.

É importante pensar nas identidades dos clientes durante a fase de planejamento do schema, a fim de ajudar a garantir que os dados estejam sendo reunidos para construir o perfil mais robusto possível. Consulte a visão geral [do Serviço de](../../identity-service/home.md) identidade para saber mais sobre como as informações de identidade podem ajudá-lo a fornecer experiências digitais aos seus clientes.

### Princípios de evolução do Schema {#evolution}

À medida que a natureza das experiências digitais continua a evoluir, também os schemas devem ser utilizados para as representar. Um schema bem projetado pode, portanto, se adaptar e evoluir conforme necessário, sem causar alterações destrutivas em versões anteriores do schema.

Como a manutenção da compatibilidade com versões anteriores é crucial para a evolução do schema, a plataforma Experience aplica um princípio de controle de versão meramente aditivo para garantir que qualquer revisão do schema resulte apenas em atualizações e alterações não destrutivas. Em outras palavras, não há suporte para alterações **de quebra.**

| Alterações suportadas | Alteração de quebra (não suportado) |
|------------------------------------|---------------------------------|
| <ul><li>Adicionar novos campos a um schema existente</li><li>Como tornar um campo obrigatório opcional</li></ul> | <ul><li>Remoção de campos definidos anteriormente</li><li>Introdução de novos campos obrigatórios</li><li>Renomear ou redefinir campos existentes</li><li>Remoção ou restrição de valores de campo suportados anteriormente</li><li>Mover atributos para um local diferente na árvore</li></ul> |

>[!NOTE] Se um schema ainda não tiver sido usado para assimilar dados na Experience Platform, você pode introduzir uma alteração radical nesse schema. No entanto, uma vez utilizado na Plataforma, o schema deve aderir à política de controle de versão adicional.

### Schemas e ingestão de dados

Para ingerir dados na Experience Platform, um conjunto de dados deve ser criado primeiro. Os conjuntos de dados são os elementos básicos para a transformação e o rastreamento de dados para o Serviço [de](../../catalog/home.md)catálogo e geralmente representam tabelas ou arquivos que contêm dados assimilados. Todos os conjuntos de dados são baseados em schemas XDM existentes, que fornecem restrições para o que os dados ingeridos devem conter e como devem ser estruturados. Consulte a visão geral sobre a assimilação [de dados da plataforma](../../ingestion/home.md) Adobe Experience para obter mais informações.

## Elementos básicos de um schema

A plataforma Experience usa uma abordagem de composição na qual os blocos componentes padrão são combinados para criar schemas. Essa abordagem promove a reutilização dos componentes existentes e orienta a padronização em todo o setor para suportar os schemas e componentes do fornecedor na Plataforma.

Os Schemas são compostos usando a seguinte fórmula:

**Classe + Mixin&amp;ast; = Schema XDM**

&amp;ast;Um schema é composto por uma classe e _zero ou mais_ combinações. Isso significa que você pode compor um schema de conjunto de dados sem usar misturas.

### Classe

A composição de um schema começa com a atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o schema conterá (registro ou série cronológica). Além disso, as classes descrevem o menor número de propriedades comuns que todos os schemas baseados nessa classe precisariam incluir e fornecer uma maneira de vários conjuntos de dados compatíveis serem mesclados.

Uma classe também determina quais combinações serão elegíveis para uso no schema. Esta questão é discutida com mais detalhes na seção [de mistura](#mixin) que se segue.

Há classes padrão fornecidas com cada integração da plataforma de experiência, conhecida como classes &quot;Indústria&quot;. As classes do setor são geralmente aceitas como padrões do setor que se aplicam a um amplo conjunto de casos de uso. Exemplos de classes do setor incluem o Perfil individual XDM e as classes ExperienceEvent XDM fornecidas pela Adobe.

A plataforma de experiência também permite classes de &quot;Fornecedor&quot;, que são classes definidas pelos parceiros da plataforma de experiência e disponibilizadas a todos os clientes que usam esse serviço ou aplicativo do fornecedor dentro da plataforma.

Há também classes usadas para descrever casos de uso mais específicos para organizações individuais dentro da Plataforma, chamadas classes &quot;Cliente&quot;. As classes Customer são definidas por uma organização quando não há classes Industry ou Vendor disponíveis para descrever um caso de uso exclusivo.

Por exemplo, um schema que representa membros de um programa de Fidelidade descreve dados de registro sobre um indivíduo e, portanto, pode ser baseado na classe de Perfil individual XDM, uma classe padrão do Setor definida pela Adobe.

### Mistura {#mixin}

Um mixin é um componente reutilizável que define um ou mais campos que implementam certas funções, como detalhes pessoais, preferências de hotel ou endereço. As misturas devem ser incluídas como parte de um schema que implementa uma classe compatível.

As misturas definem a(s) classe(s) com que são compatíveis com base no comportamento dos dados que representam (séries de registros ou de horas). Isso significa que nem todas as combinações estão disponíveis para uso com todas as classes.

As misturas têm o mesmo escopo e a mesma definição que as classes: há misturas do setor, misturas de fornecedores e misturas de clientes definidas por organizações individuais usando a plataforma. A plataforma de experiência inclui muitas combinações padrão do setor, além de permitir que os fornecedores definam combinações para seus usuários, e que usuários individuais definam combinações para seus próprios conceitos específicos.

Por exemplo, para capturar detalhes como &quot;Nome&quot; e &quot;Endereço residencial&quot; para o schema &quot;Membros de fidelidade&quot;, você poderá usar combinações padrão que definem esses conceitos comuns. No entanto, conceitos específicos de casos de uso menos comuns (como &quot;Nível de Programa de fidelidade&quot;) geralmente não têm uma combinação predefinida. Nesse caso, você deve definir sua própria combinação para capturar essas informações.

Lembre-se de que os schemas são compostos de combinações &quot;zero ou mais&quot;, o que significa que você pode compor um schema válido sem usar nenhuma mistura.

### Tipo de dados {#data-type}

Os tipos de dados são usados como tipos de campos de referência em classes ou schemas da mesma forma que os campos literais básicos. A principal diferença é que os tipos de dados podem definir vários subcampos. Semelhante a uma combinação, um tipo de dados permite o uso consistente de uma estrutura de vários campos, mas tem mais flexibilidade do que uma combinação, pois um tipo de dados pode ser incluído em qualquer lugar de um schema adicionando-o como o &quot;tipo de dados&quot; de um campo.

A plataforma Experience fornece vários tipos de dados comuns como parte do Registro do Schema para suportar o uso de padrões padrão para descrever estruturas de dados comuns. Isso é explicado com mais detalhes nos tutoriais do Registro do Schema, onde ficará mais claro ao percorrer as etapas para definir tipos de dados.

### Campo

Um campo é o elemento mais básico de um schema. Os campos fornecem restrições relacionadas ao tipo de dados que podem conter ao definir um tipo de dados específico. Esses tipos básicos de dados definem um único campo, enquanto os tipos [de](#data-type) dados mencionados anteriormente permitem que você defina vários subcampos e reutilize a mesma estrutura de vários campos em vários schemas. Assim, além de definir um &quot;tipo de dados&quot; de um campo como um dos tipos de dados definidos no registro, a Plataforma de experiência oferece suporte a tipos escalares básicos, como:

* String
* Número inteiro
* Número
* Booleano
* Matriz
* Objeto

Os intervalos válidos desses tipos escalares podem ser restringidos ainda mais a determinados padrões, formatos, mínimos/máximos ou valores predefinidos. Usando essas restrições, uma grande variedade de tipos de campos mais específicos pode ser representada, incluindo:

* Enum
* Longo
* Curto
* Byte
* Data
* Data e hora
* Mapa

>[!NOTE] O tipo de campo &quot;mapa&quot; permite dados de pares de valores chave, incluindo vários valores para uma única chave. Os mapas só podem ser definidos no nível do sistema, o que significa que você pode encontrar um mapa em um schema definido pelo setor ou pelo fornecedor, mas ele não está disponível para uso nos campos definidos. O guia [do desenvolvedor da API de Registro de](../api/getting-started.md) Schemas contém mais informações sobre a definição de tipos de campos.

Algumas operações de dados usadas por serviços e aplicativos de downstream impõem restrições em tipos de campo específicos. Os serviços afetados incluem, entre outros:

* [Perfil do cliente em tempo real](../../profile/home.md)
* [Serviço de identidade](../../identity-service/home.md)
* [Segmentação](../../segmentation/home.md)
* [Serviço de Query](../../query-service/home.md)
* [Área de trabalho da ciência de dados](../../data-science-workspace/home.md)

Antes de criar um schema para uso em serviços downstream, reveja a documentação apropriada para esses serviços, a fim de entender melhor os requisitos de campo e as restrições para as operações de dados para as quais o schema se destina.

### Campos XDM

Além dos campos básicos e da capacidade de definir seus próprios tipos de dados, o XDM fornece um conjunto padrão de campos e tipos de dados que são implicitamente compreendidos pelos serviços da plataforma de experiência e proporcionam maior consistência quando usados em componentes da plataforma.

Esses campos, como &quot;Nome&quot; e &quot;Endereço de email&quot;, contêm conotações adicionadas além dos tipos básicos de campos escalares, informando à Plataforma que quaisquer campos que compartilham o mesmo tipo de dados XDM se comportarão da mesma maneira. Esse comportamento pode ser confiável para ser consistente, independentemente de onde os dados vêm ou em qual serviço da plataforma os dados estão sendo usados.

Consulte o dicionário [de campos](field-dictionary.md) XDM para obter uma lista completa dos campos XDM disponíveis. É recomendável usar campos e tipos de dados XDM sempre que possível para oferecer suporte à consistência e padronização na plataforma da experiência.

## Exemplo de composição

Os Schemas representam o formato e a estrutura dos dados que serão assimilados na Plataforma e são criados usando um modelo de composição. Como mencionado anteriormente, esses schemas são compostos de uma classe e zero ou mais combinações compatíveis com essa classe.

Por exemplo, um schema que descreve compras feitas em uma loja de varejo pode ser chamado de &quot;Transações de loja&quot;. O schema implementa a classe XDM ExperienceEvent combinada com a mixina de Comércio padrão e uma mixina de Informações do produto definida pelo usuário.

Outro schema que acompanha o tráfego do site pode ser chamado de &quot;Visitas à Web&quot;. Ela também implementa a classe XDM ExperienceEvent, mas dessa vez combina a mixagem da Web padrão.

O diagrama abaixo mostra esses schemas e os campos contribuídos por cada combinação. Ele também contém dois schemas baseados na classe Perfil individual XDM, incluindo o schema &quot;Membros da fidelidade&quot; mencionado anteriormente neste guia.

![](../images/schema-composition/composition.png)

### União {#union}

Embora a plataforma Experience permita que você componha schemas para casos de uso específicos, ela também permite que você veja uma &quot;união&quot; de schemas para um tipo de classe específico. O diagrama anterior mostra dois schemas com base na classe XDM ExperienceEvent e dois schemas com base na classe XDM Individual Perfil. A união, mostrada abaixo, agregação os campos de todos os schemas que compartilham a mesma classe (Perfil XDM ExperienceEvent e XDM Individual, respectivamente).

![](../images/schema-composition/union.png)

Ao habilitar um schema para uso com o Perfil de cliente em tempo real, ele será incluído na união para esse tipo de classe. O Perfil oferece perfis robustos e centralizados de atributos do cliente, bem como uma conta com carimbos de data e hora de cada evento que o cliente teve em qualquer sistema integrado à Plataforma. O Perfil usa a visualização da união para representar esses dados e fornecer uma visualização holística de cada cliente individual.

Para obter mais informações sobre como trabalhar com o Perfil, consulte a visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## Mapeamento de arquivos de dados para schemas XDM

Todos os arquivos de dados que são ingeridos na plataforma Experience devem estar em conformidade com a estrutura de um schema XDM. Para obter mais informações sobre como formatar arquivos de dados de acordo com hierarquias XDM (incluindo arquivos de amostra), consulte o documento sobre transformações [ETL de](../../etl/transformations.md)amostra. Para obter informações gerais sobre como assimilar arquivos de dados na Experience Platform, consulte a visão geral [da ingestão em](../../ingestion/batch-ingestion/overview.md)lote.

## Próximas etapas

Agora que você entende as noções básicas da composição do schema, está pronto para começar a criar schemas usando o Registro do Schema.

O Registro de Schemas é usado para acessar a Biblioteca de Schemas na Adobe Experience Platform e fornece uma interface de usuário e uma RESTful API, a partir da qual todos os recursos disponíveis da biblioteca estão acessíveis. A Biblioteca de Schemas contém recursos do setor definidos pela Adobe, recursos do fornecedor definidos pelos parceiros da plataforma de experiência e classes, mixins, tipos de dados e schemas que foram compostos por membros de sua organização.

Para começar a compor o schema usando a interface do usuário, siga o tutorial [do Editor de](../tutorials/create-schema-ui.md) Schemas para criar o schema &quot;Membros da fidelidade&quot; mencionado em todo o documento.

Para começar a usar a API de registro do Schema, leia o guia [do desenvolvedor da API de registro do](../api/getting-started.md)Schema. Após ler o guia do desenvolvedor, siga as etapas descritas no tutorial sobre como [criar um schema usando a API](../tutorials/create-schema-api.md)de registro do Schema.
