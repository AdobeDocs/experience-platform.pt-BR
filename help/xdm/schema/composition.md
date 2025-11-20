---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;enum;mixin;Grupo de campos;Grupos de campos;mixins;tipo de dados;tipos de dados;Tipos de dados;Identidade primária;identidade primária;perfil individual XDM;campos XDM;tipo de dados enum;Evento de experiência;Evento de experiência XDM;Evento de experiência XDM;evento de experiência;evento de experiência;evento de experiência XDM;design de esquema;classe;Classe;classes;classes;tipo de dados;tipo de dados;tipo de dados;Esquemas;Mapa de identidade;mapa de identidade;Mapa de identidade;Esquema design;mapa;mapa;esquema de união;união;design;map;Map;union schema;union
solution: Experience Platform
title: Noções básicas da composição do esquema
description: Saiba mais sobre esquemas do Experience Data Model (XDM) e os componentes, princípios e práticas recomendadas para a composição de esquemas no Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: dcb6770d739d0da5cfa339584a769f5311a8c7e1
workflow-type: tm+mt
source-wordcount: '4308'
ht-degree: 8%

---

# Noções básicas da composição do esquema

Saiba mais sobre esquemas do Experience Data Model (XDM) e os componentes, princípios e práticas recomendadas para a composição de esquemas no Adobe Experience Platform. Para obter informações gerais sobre o XDM e como ele é usado no [!DNL Experience Platform], consulte a [visão geral do Sistema XDM](../home.md).

## Noções básicas sobre esquemas {#understanding-schemas}

Um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Em um alto nível, os esquemas fornecem uma definição abstrata de um objeto do mundo real (como uma pessoa) e destacam quais dados devem ser incluídos em cada instância desse objeto (como nome, sobrenome, aniversário e assim por diante).

Além de descrever a estrutura dos dados, os esquemas aplicam restrições e expectativas aos dados para que eles possam ser validados à medida que se movem entre sistemas. Essas definições padrão permitem que os dados sejam interpretados de forma consistente, independentemente da origem, e eliminam a necessidade de tradução entre aplicativos.

O Experience Platform mantém essa normalização semântica usando esquemas. Os Esquemas são a maneira padrão de descrever dados na Experience Platform, permitindo que todos os dados que estão em conformidade com os esquemas sejam reutilizados em uma organização sem conflitos ou até compartilhados entre várias organizações.

Os esquemas XDM são ideais para armazenar grandes quantidades de dados complexos em um formato independente. Consulte as seções em [objetos inseridos](#embedded) e [big data](#big-data) no apêndice deste documento para obter mais informações sobre como o XDM faz isso.

### Fluxos de trabalho baseados em esquema no Experience Platform {#schema-based-workflows}

A padronização é um conceito essencial por trás do Experience Platform. O XDM, orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas padrão para o gerenciamento da experiência do cliente.

A infraestrutura na qual o Experience Platform é criado, conhecida como [!DNL XDM System], facilita fluxos de trabalho baseados em esquema e inclui o [!DNL Schema Registry], [!DNL Schema Editor], metadados de esquema e padrões de consumo de serviço. Consulte a [Visão geral do sistema XDM](../home.md) para obter mais informações.

Há vários benefícios principais em usar esquemas na Experience Platform. Primeiro, os esquemas permitem uma melhor governança de dados e minimização de dados, o que é especialmente importante com as regulamentações de privacidade. Em segundo lugar, a criação de esquemas com componentes padrão da Adobe permite insights prontos para uso e o uso de serviços de IA/ML com personalizações mínimas. Por último, os esquemas fornecem infraestrutura para compartilhamento de dados, insights e orquestração eficiente.

## Planejamento do esquema {#planning}

A primeira etapa na criação de um esquema é determinar o conceito, ou objeto real, que você está tentando capturar no esquema. Depois de identificar o conceito que está tentando descrever, comece a planejar seu esquema pensando em coisas como o tipo de dados, possíveis campos de identidade e como o esquema pode evoluir no futuro.

### Comportamentos de dados no Experience Platform {#data-behaviors}

Os dados destinados ao uso no Experience Platform são agrupados em dois tipos de comportamento:

* **Dados de registro**: fornece informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo.
* **Dados de série temporal**: Fornece um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro.

Todos os esquemas XDM descrevem dados que podem ser categorizados como registro ou série de tempo. O comportamento dos dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM são descritas com mais detalhes posteriormente neste documento.

Os esquemas de registro e série temporal contêm um mapa de identidades (`xdm:identityMap`). Este campo contém a representação de identidade de uma pessoa, desenhada a partir de campos marcados como &quot;Identidade&quot;, conforme descrito na próxima seção.

### [!UICONTROL Identity] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identidades em esquemas"
>abstract="Identidades são campos principais em um esquema que podem ser usados para identificar um assunto, como um endereço de email ou uma ID de marketing. Esses campos são usados para criar o gráfico de identidade de cada pessoa e criar perfis de cliente. Consulte a documentação para obter mais informações sobre identidades em esquemas."

Os esquemas definem a estrutura dos dados assimilados na Experience Platform. Esses dados potencializam vários serviços na plataforma e ajudam a criar uma visualização única e unificada de cada indivíduo. Portanto, ao criar esquemas, pense com cuidado sobre quais campos marcar como identidades — esses controlam como os perfis são compilados entre conjuntos de dados.

Para ajudar nesse processo, os campos principais em seus esquemas podem ser marcados como identidades. Após a assimilação de dados, os dados nesses campos são inseridos em &quot;[!UICONTROL Identity Graph]&quot; para esse indivíduo. Os dados do gráfico podem ser acessados por [[!DNL Real-Time Customer Profile]](../../profile/home.md) e outros serviços da Experience Platform para fornecer uma visualização unificada de cada cliente individual.

Os campos comumente marcados como &quot;[!UICONTROL Identity]&quot; incluem: endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR), ID de CRM ou outros campos de ID exclusivos. Considere quaisquer identificadores exclusivos específicos da sua organização, pois eles também podem ser bons campos &quot;[!UICONTROL Identity]&quot;.

Para saber mais sobre como as informações de identidade podem ajudar você a fornecer experiências digitais aos seus clientes, consulte a [visão geral do Serviço de identidade](../../identity-service/home.md). Consulte o documento de práticas recomendadas de modelagem de dados para [dicas sobre o uso de identidades ao criar um esquema](./best-practices.md#data-validation-fields).

Há duas maneiras de enviar dados de identidade para o Experience Platform:

1. Adicionando descritores de identidade a campos individuais, por meio da [Interface do Editor de Esquemas](../ui/fields/identity.md) ou usando a [API do Registro de Esquemas](../api/descriptors.md#create)
2. Usando um campo [`identityMap`](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` é um campo do tipo mapa que descreve os vários valores de identidade para um indivíduo, juntamente com seus namespaces associados. Este campo pode ser usado para fornecer informações de identidade para seus esquemas, em vez de definir valores de identidade na estrutura do próprio esquema.

A principal desvantagem de usar o `identityMap` é que os valores de identidade estão aninhados e pode ser mais difícil de utilizar em ferramentas que esperam campos de identidade de nível superior, como o Construtor de segmentos ou algumas integrações de terceiros.

>[!NOTE]
>
>Um esquema que usa `identityMap` pode ser usado como um esquema de origem em uma relação, mas não pode ser usado como um esquema de referência. Isso ocorre porque todos os esquemas de referência devem ter uma identidade visível que possa ser mapeada em um campo de referência no esquema de origem. Consulte o guia de interface do usuário em [relações](../tutorials/relationship-ui.md) para obter mais informações sobre os requisitos de esquemas de origem e referência.

No entanto, os mapas de identidade podem ser úteis se houver um número variável de identidades para um esquema ou se você estiver trazendo dados de fontes que armazenam identidades juntas (como [!DNL Airship] ou Adobe Audience Manager). Além disso, os mapas de identidade serão necessários se você estiver usando a [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/).

Um exemplo de um mapa de identidade simples seria semelhante ao seguinte:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Como mostra o exemplo acima, cada chave no objeto `identityMap` representa um namespace de identidade. O valor de cada chave é uma matriz de objetos, representando os valores de identidade (`id`) do respectivo namespace. Consulte a documentação [!DNL Identity Service] para obter uma [lista de namespaces de identidade padrão](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconhecidos pelos aplicativos da Adobe.

>[!NOTE]
>
>Um valor booleano para determinar se o valor é uma identidade primária (`primary`) também pode ser fornecido para cada valor de identidade. Você só precisa definir identidades primárias para esquemas destinados a serem usados em [!DNL Real-Time Customer Profile]. Consulte a seção sobre [esquemas de união](#union) para obter mais informações.

### Princípios de evolução do esquema {#evolution}

À medida que a natureza das experiências digitais continua a evoluir, o mesmo deve acontecer com os esquemas utilizados para representá-las. Um esquema bem projetado é, portanto, capaz de se adaptar e evoluir conforme necessário, sem causar alterações destrutivas nas versões anteriores do esquema.

Como manter a compatibilidade com versões anteriores é crucial para a evolução do esquema, o Experience Platform impõe um princípio de controle de versão puramente aditivo. Esse princípio garante que qualquer revisão do esquema resulte apenas em atualizações e alterações não destrutivas. Em outras palavras, não há suporte para **alterações de quebra.**

>[!NOTE]
>
>Você só poderá introduzir uma mudança radical em um esquema se ele ainda não tiver sido usado para assimilar dados na Experience Platform e não tiver sido habilitado para uso no Perfil do cliente em tempo real. No entanto, uma vez que o esquema tenha sido usado em [!DNL Experience Platform], ele deve aderir à política de controle de versão aditivo.

A tabela a seguir detalha quais alterações são suportadas ao editar esquemas, grupos de campos e tipos de dados:

| Alterações suportadas | Quebra de alterações (não suportado) |
| --- | --- |
| <ul><li>Adicionar novos campos ao recurso</li><li>Tornar um campo obrigatório opcional</li><li>Introdução de novos campos obrigatórios*</li><li>Alteração do nome de exibição e da descrição do recurso</li><li>Ativação do esquema para participar do perfil</li></ul> | <ul><li>Remoção de campos definidos anteriormente</li><li>Renomear ou redefinir campos existentes</li><li>Remoção ou restrição de valores de campo compatíveis anteriormente</li><li>Mover campos existentes para um local diferente na árvore</li><li>Exclusão do esquema</li><li>Desativar a participação do esquema no perfil</li><li>Alteração do campo de identidade principal em um esquema habilitado para Perfil e que tenha dados assimilados</li></ul> |

\**Consulte a seção abaixo para considerações importantes sobre a [configuração de novos campos obrigatórios](#post-ingestion-required-fields).*

### Campos obrigatórios

Campos de esquema individuais podem ser [marcados como obrigatórios](../ui/fields/required.md), o que significa que quaisquer registros assimilados devem conter dados nesses campos para passar na validação. Por exemplo, definir o campo de identidade principal de um esquema conforme necessário pode ajudar a garantir que todos os registros assimilados participem do Perfil do cliente em tempo real. Da mesma forma, definir um campo de carimbo de data e hora conforme necessário garante que todos os eventos de série temporal sejam preservados cronologicamente.

>[!IMPORTANT]
>
>Independentemente de um campo de esquema ser obrigatório ou não, a Experience Platform não aceita `null` ou valores vazios para qualquer campo assimilado. Se não houver valor para um campo específico em um registro ou evento, a chave desse campo deverá ser excluída da carga de assimilação.

#### Definindo campos conforme necessário após a assimilação {#post-ingestion-required-fields}

Se um campo tiver sido usado para assimilar dados e não tiver sido originalmente definido como obrigatório, esse campo poderá ter um valor nulo para alguns registros. Se você definir esse campo como pós-assimilação obrigatória, todos os registros futuros deverão conter um valor para esse campo, mesmo que os registros históricos possam ser nulos.

Ao definir um campo opcional anteriormente como obrigatório, lembre-se do seguinte:

1. Se você consultar dados históricos e gravar os resultados em um novo conjunto de dados, haverá falha em algumas linhas porque elas contêm valores nulos para o campo obrigatório.
1. Se o campo participar do [Perfil de cliente em tempo real](../../profile/home.md) e você exportar dados antes de configurá-los como necessário, ele poderá ser nulo para alguns perfis.
1. Você pode usar a API do registro de esquema para exibir um registro de alterações com carimbo de data e hora para todos os recursos XDM na Experience Platform, incluindo novos campos obrigatórios. Consulte o manual no [ponto de extremidade do log de auditoria](../api/audit-log.md) para obter mais informações.

### Esquemas e assimilação de dados

Para assimilar dados na Experience Platform, um conjunto de dados deve ser criado primeiro. Os conjuntos de dados são os blocos de construção para transformação e rastreamento de dados para [[!DNL Catalog Service]](../../catalog/home.md) e geralmente representam tabelas ou arquivos que contêm dados assimilados. Todos os conjuntos de dados se baseiam em esquemas XDM existentes, que fornecem restrições sobre o que os dados assimilados devem conter e como devem ser estruturados. Consulte a visão geral em [Assimilação de dados Adobe Experience Platform](../../ingestion/home.md) para obter mais informações.

## Blocos de construção de um esquema {#schema-building-blocks}

O Experience Platform usa uma abordagem de composição na qual os blocos de construção padrão são combinados para criar esquemas. Essa abordagem promove a reutilização dos componentes existentes e promove a padronização em todo o setor para dar suporte a esquemas e componentes de fornecedores no [!DNL Experience Platform].

Os esquemas são compostos usando a seguinte fórmula:

**Classe + Grupo de Campos de Esquema&ast; = Esquema XDM**

&ast;Um esquema é composto por uma classe e zero ou mais grupos de campos de esquema. Isso significa que você pode compor um esquema de conjunto de dados sem usar grupos de campos.

### Classe {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Classe"
>abstract="Cada esquema se baseia em uma única classe. A classe define o comportamento do esquema e as propriedades comuns que todos os esquemas baseados nessa classe devem conter. Consulte a documentação para saber mais sobre como as classes estão envolvidas na composição do esquema."

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="Tipo de setor"
>abstract="Ao selecionar um setor relevante para o seu negócio, o modelo de aprendizado de máquina poderá fornecer uma melhor organização de dados, mapeando com mais precisão os campos de origem com grupos de campos padrão alinhados aos padrões do setor. Isso garante que a integração de dados seja personalizada para as necessidades específicas do setor e resulta em insights de dados mais precisos e relevantes."

A composição de um esquema começa com a atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o esquema conterá (registro ou série temporal). Além disso, as classes descrevem o menor número de propriedades comuns que todos os esquemas baseados nessa classe precisariam incluir e fornecem uma maneira de vários conjuntos de dados compatíveis serem mesclados.

A classe de um esquema determina quais grupos de campos estão qualificados para uso nesse esquema. Isso é discutido com mais detalhes na [próxima seção](#field-group).

O Adobe fornece várias classes XDM padrão (&quot;núcleo&quot;). Duas dessas classes, [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent], são necessárias para quase todos os processos downstream do Experience Platform. Além dessas classes principais, você também pode criar suas próprias classes personalizadas para descrever casos de uso mais específicos para sua organização. As classes personalizadas são definidas por uma organização quando não há classes principais definidas pela Adobe disponíveis para descrever um caso de uso exclusivo.

A captura de tela a seguir demonstra como as classes são representadas na interface do usuário do Experience Platform. Como o esquema de exemplo mostrado não contém nenhum grupo de campos, todos os campos exibidos são fornecidos pela classe do esquema ([!UICONTROL XDM Individual Profile]).

![O [!UICONTROL XDM Individual Profile] no Editor de Esquemas.](../images/schema-composition/class.png)

Para obter a lista mais atualizada de classes XDM padrão disponíveis, consulte o [repositório XDM oficial](https://github.com/adobe/xdm/tree/master/components/classes). Como alternativa, consulte o guia em [explorando componentes XDM](../ui/explore.md) se preferir exibir recursos na interface.

### Grupo de campos {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Grupo de campos"
>abstract="Os grupos de campos são componentes reutilizáveis que permitem estender esquemas com atributos adicionais. A maioria dos grupos de campos é compatível somente com determinadas classes. Você pode usar grupos de campos padrão definidos pela Adobe ou pode definir manualmente seus próprios grupos de campos personalizados. Consulte a documentação para saber mais sobre como os grupos de campos estão envolvidos na composição do esquema."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Grupo de campos obrigatório"
>abstract="Esse grupo de campos é exigido pela origem usada. Por esse motivo, não é possível excluí-lo do esquema."

Um grupo de campos é um componente reutilizável que define um ou mais campos que implementam determinadas funções, como detalhes pessoais, preferências de hotel ou endereço. Os grupos de campos devem ser incluídos como parte de um esquema que implementa uma classe compatível.

Os grupos de campos definem a(s) classe(s) com a(s) qual(is) eles são compatíveis, com base no comportamento dos dados que representam (registro ou série temporal). Isso significa que nem todos os grupos de campos estão disponíveis para uso com todas as classes.

O Experience Platform inclui muitos grupos de campos padrão do Adobe, além de permitir que os fornecedores definam grupos de campos para seus usuários e que os usuários individuais definam grupos de campos para seus próprios conceitos específicos.

Por exemplo, para capturar detalhes como &quot;[!UICONTROL First Name]&quot; e &quot;[!UICONTROL Home Address]&quot; para o esquema &quot;[!UICONTROL Loyalty Members]&quot;, você poderia usar grupos de campos padrão que definem esses conceitos comuns. No entanto, os conceitos mais específicos da sua organização (como detalhes do programa de fidelidade personalizado ou atributos do produto) que podem não ser cobertos por grupos de campos padrão. Nesse caso, você deve definir seu próprio grupo de campos para capturar essas informações.

>[!NOTE]
>
>É altamente recomendável usar grupos de campos padrão sempre que possível em seus esquemas, pois esses campos são implicitamente compreendidos pelos serviços da Experience Platform e fornecem maior consistência quando usados em [!DNL Experience Platform] componentes.
>
>Os campos fornecidos pelos componentes padrão (como &quot;Nome&quot; e &quot;Endereço de email&quot;) contêm conotações adicionadas além dos tipos de campos escalares básicos. Eles informam a [!DNL Experience Platform] que todos os campos que compartilham o mesmo tipo de dados se comportarão da mesma maneira. Pode-se confiar que esse comportamento é consistente independentemente de onde os dados vêm ou em qual serviço do [!DNL Experience Platform] os dados estão sendo usados.

Lembre-se de que os esquemas são compostos de &quot;zero ou mais&quot; grupos de campos, portanto, isso significa que você pode compor um esquema válido sem usar nenhum grupo de campos.

A captura de tela a seguir demonstra como os grupos de campos são representados na interface do usuário do Experience Platform. Um único grupo de campos ([!UICONTROL Demographic Details]) é adicionado a um esquema neste exemplo, que fornece um agrupamento de campos para a estrutura do esquema.

![O Editor de Esquemas com o grupo de campos [!UICONTROL Demographic Details] realçado em um esquema de exemplo.](../images/schema-composition/field-group.png)

Para obter a lista mais atualizada de grupos de campos XDM padrão disponíveis, consulte o [repositório XDM oficial](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Como alternativa, consulte o guia em [explorando componentes XDM](../ui/explore.md) se preferir exibir recursos na interface.

>[!NOTE]
>
> Os grupos de campos XDM padrão estão sempre evoluindo e alguns grupos de campos foram descontinuados. Para obter a lista mais atualizada de grupos de campos obsoletos, consulte a [seção de grupos de campos obsoletos](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) no repositório XDM oficial.

### Tipo de dados {#data-type}

Os tipos de dados são usados como tipos de campo de referência em classes ou esquemas da mesma forma que os campos literais básicos. A principal diferença é que os tipos de dados podem definir vários subcampos da mesma forma que os grupos de campos. A principal diferença entre eles é que os tipos de dados podem ser incluídos em qualquer lugar de um esquema adicionando-o como o &quot;tipo de dados&quot; de um campo. Embora os grupos de campos sejam compatíveis apenas com determinadas classes, os tipos de dados podem ser incluídos em qualquer classe principal ou grupo de campos.

>[!NOTE]
>
>Se um campo for definido como um tipo de dados específico, você não poderá criar o mesmo campo com um tipo de dados diferente em outro esquema. Essa restrição se aplica ao locatário da organização.

O Experience Platform fornece vários tipos de dados comuns como parte do [!DNL Schema Registry] para dar suporte ao uso de padrões padrão para descrever estruturas de dados comuns. Isso é explicado com mais detalhes nos [tutoriais do Registro de esquemas](../tutorials/create-schema-api.md) e ficará mais claro à medida que você percorrer as etapas para definir os tipos de dados.

A captura de tela a seguir demonstra como os tipos de dados são representados na interface do usuário do Experience Platform. Um dos campos fornecidos pelo grupo de campos [!UICONTROL Demographic Details] usa o tipo de dados &quot;[!UICONTROL Object]&quot;, conforme indicado pelo texto após o caractere de barra vertical (`|`) ao lado do nome do campo. Esse tipo de dados específico fornece vários subcampos relacionados ao nome de uma pessoa individual, uma construção que pode ser reutilizada para outros campos em que o nome de uma pessoa precisa ser capturado.

![Um diagrama no Editor de Esquemas para uma pessoa individual com o objeto Nome completo e os atributos realçados.](../images/schema-composition/data-type.png)

Para obter a lista mais atualizada dos tipos de dados XDM padrão disponíveis, consulte o [repositório XDM oficial](https://github.com/adobe/xdm/tree/master/components/datatypes). Como alternativa, consulte o guia em [explorando componentes XDM](../ui/explore.md) se preferir exibir recursos na interface.

>[!NOTE]
>
> Os tipos de dados XDM padrão estão sempre evoluindo e alguns tipos de dados foram descontinuados. Para obter a lista mais atualizada dos tipos de dados obsoletos, consulte a [seção de tipos de dados obsoletos](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) no repositório oficial do XDM.

### Campo {#field}

Um campo é o bloco de construção mais básico de um esquema. Os campos fornecem restrições relacionadas ao tipo de dados que eles podem conter ao definir um tipo de dados específico. Esses tipos de dados básicos definem um único campo, enquanto os [tipos de dados](#data-type) mencionados anteriormente permitem definir vários subcampos e reutilizar a mesma estrutura de vários campos em vários esquemas. Portanto, além de definir o &quot;tipo de dados&quot; de um campo como um dos tipos de dados definidos no registro, o Experience Platform é compatível com tipos escalares básicos, como:

* String
* Número inteiro
* Duplo
* Booleano
* Matriz
* Objeto

>[!TIP]
>
>Consulte o [apêndice](#objects-v-freeform) para obter informações sobre os prós e contras do uso de campos de forma livre em campos de tipo de objeto.

Os intervalos válidos desses tipos escalares podem ser ainda mais restritos a determinados padrões, formatos, mínimos/máximos ou valores predefinidos. Usando essas restrições, uma grande variedade de tipos de campos mais específicos pode ser representada, incluindo:

* Lista Discriminada
* Longo
* Curto
* Byte
* Data
* Data e hora
* Mapa

>[!NOTE]
>
>O tipo de campo &quot;map&quot; permite dados de par de valores chave, incluindo vários valores para uma única chave. Os mapas podem ser encontrados em classes XDM padrão e grupos de campos, mas você também pode definir mapas personalizados. Consulte o tutorial da API em [definindo campos de mapa personalizados](../tutorials/custom-fields-api.md#custom-maps) ou o guia em [definindo campos de mapa na interface](../ui/fields/map.md) para obter mais informações.

## Exemplo de composição {#composition-example}

Os esquemas são criados usando um modelo de composição e representam o formato e a estrutura dos dados a serem assimilados em [!DNL Experience Platform]. Como mencionado anteriormente, esses esquemas são compostos de uma classe e zero ou mais grupos de campos compatíveis com essa classe.

Por exemplo, um esquema que descreve compras feitas em uma loja de varejo pode ser chamado de &quot;[!UICONTROL Store Transactions]&quot;. O esquema implementa a classe [!DNL XDM ExperienceEvent] combinada com o grupo de campos [!UICONTROL Commerce] padrão e um grupo de campos [!UICONTROL Product Info] definido pelo usuário.

Outro esquema que rastreia o tráfego do site pode ser chamado de &quot;[!UICONTROL Web Visits]&quot;. Ele também implementa a classe [!DNL XDM ExperienceEvent], mas desta vez combina o grupo de campos [!UICONTROL Web] padrão.

O diagrama abaixo mostra esses esquemas e os campos contribuídos por cada grupo de campos. Ela também contém dois esquemas baseados na classe [!DNL XDM Individual Profile], incluindo o esquema &quot;[!UICONTROL Loyalty Members]&quot; mencionado anteriormente neste guia.

![Um diagrama de fluxo de quatro esquemas e dos grupos de campos que contribuem com eles.](../images/schema-composition/composition.png)

### União {#union}

Embora o Experience Platform permita compor esquemas para casos de uso específicos, ele também permite ver uma &quot;união&quot; de esquemas para um tipo de classe específico. O diagrama anterior mostra dois esquemas baseados na classe XDM ExperienceEvent e dois esquemas baseados na classe [!DNL XDM Individual Profile]. A união, mostrada abaixo, agrega os campos de todos os esquemas que compartilham a mesma classe ([!DNL XDM ExperienceEvent] e [!DNL XDM Individual Profile], respectivamente).

![Um diagrama de fluxo de esquema de união que retrata os campos que os compõem.](../images/schema-composition/union.png)

Ao habilitar um esquema para uso com [!DNL Real-Time Customer Profile], ele é incluído na união para esse tipo de classe. O [!DNL Profile] fornece perfis robustos e centralizados de atributos do cliente e uma conta com carimbo de data e hora de cada evento que o cliente teve em qualquer sistema integrado ao [!DNL Experience Platform]. [!DNL Profile] usa a exibição de união para representar esses dados e fornecer uma exibição holística de cada cliente individual.

Para obter mais informações sobre como trabalhar com [!DNL Profile], consulte a [Visão geral do Perfil do Cliente em Tempo Real](../../profile/home.md).

## Mapeamento de arquivos de dados para esquemas XDM {#mapping-datafiles}

Todos os arquivos de dados assimilados na Experience Platform devem estar em conformidade com a estrutura de um esquema XDM. Para obter mais informações sobre como formatar arquivos de dados para estar em conformidade com hierarquias XDM (incluindo arquivos de exemplo), consulte o documento em [transformações ETL de amostra](../../etl/transformations.md). Para obter informações gerais sobre como assimilar arquivos de dados na Experience Platform, consulte a [visão geral de assimilação em lote](../../ingestion/batch-ingestion/overview.md).

## Esquemas para públicos externos

Se você estiver trazendo públicos-alvo de sistemas externos para a Experience Platform, deverá usar os seguintes componentes para capturá-los em seus esquemas:

* [[!UICONTROL Segment definition] classe](../classes/segment-definition.md): use esta classe padrão para capturar atributos de chave de uma definição de segmento externo.
* [[!UICONTROL Segment Membership Details] grupo de campos](../field-groups/profile/segmentation.md): adicione este grupo de campos ao esquema [!UICONTROL XDM Individual Profile] para associar perfis de clientes a públicos específicos.

## Próximas etapas

Agora que você entende as noções básicas da composição de esquema, está pronto para começar a explorar e criar esquemas usando o [!DNL Schema Registry].

Para revisar a estrutura das duas classes XDM principais e seus grupos de campos compatíveis comumente usados, consulte a seguinte documentação de referência:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

O [!DNL Schema Registry] é usado para acessar o [!DNL Schema Library] no Adobe Experience Platform e fornece uma interface de usuário e uma API RESTful a partir das quais todos os recursos de biblioteca disponíveis podem ser acessados. O [!DNL Schema Library] contém Recursos do setor definidos pela Adobe, Recursos do fornecedor definidos pelos parceiros da Experience Platform e classes, grupos de campos, tipos de dados e esquemas que foram compostos por membros da organização.

Para começar a compor o esquema usando a interface do usuário, siga o [tutorial do Editor de esquemas](../tutorials/create-schema-ui.md) para criar o esquema &quot;Membros de fidelidade&quot; mencionado neste documento.

Para começar a usar a API [!DNL Schema Registry], comece lendo o [guia do desenvolvedor da API do Registro de Esquema](../api/getting-started.md). Depois de ler o guia do desenvolvedor, siga as etapas descritas no tutorial sobre [criação de um esquema usando a API do Registro de Esquema](../tutorials/create-schema-api.md).

## Apêndice

As seções a seguir contêm informações adicionais sobre os princípios da composição do schema.

### Tabelas relacionais versus objetos incorporados {#embedded}

Ao trabalhar com bancos de dados relacionais, as práticas recomendadas envolvem normalizar dados ou pegar uma entidade e dividi-la em partes distintas que são exibidas em várias tabelas. Para ler os dados como um todo ou atualizar a entidade, as operações de leitura e gravação devem ser feitas em muitas tabelas individuais usando JOIN.

Ao usar objetos incorporados, os esquemas XDM podem representar diretamente dados complexos e armazená-los em documentos autocontidos com uma estrutura hierárquica. Um dos principais benefícios dessa estrutura é que ela permite consultar os dados sem precisar reconstruir a entidade por junções caras a várias tabelas desnormalizadas. Não há restrições rígidas quanto à quantidade de níveis que sua hierarquia de esquema pode ter.

### Esquemas e big data {#big-data}

Sistemas digitais modernos geram grandes quantidades de sinais comportamentais (dados de transação, registros da Web, internet das coisas, exibição e assim por diante). Esses big data oferecem oportunidades extraordinárias para otimizar experiências, mas são desafiadores de usar devido à escala e variedade dos dados. Para obter valor dos dados, sua estrutura, formato e definições devem ser padronizados para que possam ser processados de forma consistente e eficiente.

Os esquemas resolvem esse problema permitindo que os dados sejam integrados de várias fontes, padronizados por meio de estruturas e definições comuns e compartilhados entre as soluções. Isso permite que processos e serviços subsequentes respondam a qualquer tipo de pergunta feita sobre os dados. Ela se afasta da abordagem tradicional de modelagem de dados, em que todas as perguntas a serem feitas sobre os dados são conhecidas antecipadamente e os dados são modelados para se adequar a essas expectativas.

### Objetos versus campos de formato livre {#objects-v-freeform}

Há alguns fatores principais a serem considerados ao escolher objetos em vez de campos de formato livre ao projetar seus esquemas:

| Objetos | Campos de forma livre |
| --- | --- |
| Aumenta o aninhamento | Menos ou nenhum aninhamento |
| Cria agrupamentos de campos lógicos | Os campos são colocados em locais ad hoc |

{style="table-layout:auto"}

#### Objetos

Os prós e contras do uso de objetos em campos de formato livre estão listados abaixo.

**Vantagens**:

* Os objetos são usados melhor quando você deseja criar um agrupamento lógico de determinados campos.
* Os objetos organizam o esquema de maneira mais estruturada.
* Os objetos indiretamente ajudam a criar uma boa estrutura de menu na interface do usuário do Construtor de segmentos. Os campos agrupados no esquema são refletidos diretamente na estrutura de pastas fornecida na interface do usuário do Construtor de segmentos.

**Contras**:

* Os campos ficam mais aninhados.
* Ao usar o [Serviço de Consulta do Adobe Experience Platform](../../query-service/home.md), cadeias de caracteres de referência mais longas devem ser fornecidas para campos de consulta aninhados em objetos.

#### Campos de forma livre

Os prós e contras do uso de campos de forma livre sobre objetos estão listados abaixo.

**Vantagens**:

* Os campos de forma livre são criados diretamente no objeto raiz do esquema (`_tenantId`), aumentando a visibilidade.
* As cadeias de caracteres de referência para campos de formato livre tendem a ser mais curtas ao usar o Serviço de consulta.

**Contras**:

* A localização dos campos de forma livre no esquema é ad hoc, o que significa que eles aparecem em ordem alfabética no Editor de esquemas. Isso pode tornar os esquemas menos estruturados e campos de forma livre semelhantes podem acabar sendo muito separados, dependendo de seus nomes.
