---
title: Referência de construção de regra de política de consentimento
description: Saiba como usar tipos de dados XDM, operadores compatíveis e lógica avançada para criar regras de política de consentimento granulares na interface do usuário do Adobe Experience Platform.
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Referência de construção de regra de política de consentimento

Use essa referência na lógica de regra avançada para definir regras precisas e legalmente válidas na cláusula **[!UICONTROL Then]** do Construtor de políticas de consentimento no Adobe Experience Platform.

![A interface do construtor de políticas de consentimento destacando a seção de cláusula [!UICONTROL Then], onde os usuários definem as condições da regra.](../images/policies/multiple-rules.png)

Saiba como as regras de política se aplicam à estrutura e aos tipos dos dados de consentimento para aplicar com precisão as preferências de consentimento do cliente.

Leia este documento para saber como filtrar perfis com base em consentimento navegando até campos de container no esquema XDM e selecionando um campo primitivo. Em seguida, use o operador apropriado para definir o valor exato que um perfil deve corresponder.

## Pré-requisitos

Antes de usar essa referência, verifique se a configuração da sua política de consentimento está completa e se você compreende os conceitos fundamentais da arquitetura de dados e da estrutura de governança da Adobe Experience Platform.

Certifique-se de atender aos seguintes pré-requisitos:

* **Configuração de Política Concluída**: você criou ou começou a criar uma política de consentimento na interface do usuário do Adobe Experience Platform. Para obter etapas detalhadas, consulte o [guia do usuário de políticas de uso de dados](user-guide.md#consent-policy).

* **Familiaridade com Estruturas de Dados**: esta referência requer conhecimento prático dos seguintes conceitos principais:
   * **XDM e esquema de união**: entenda como as estruturas do Experience Data Model definem relações de dados e como o esquema de união representa perfis unificados de clientes. Consulte a [Visão geral do sistema XDM](../../xdm/home.md) para saber mais.
   * **Estrutura de governança de dados**: saiba como o Adobe Experience Platform aplica políticas de uso de dados e regras de governança. Consulte a [visão geral da Governança de dados](../home.md) para obter detalhes.
   * **Processamento de consentimento do cliente**: entenda como os dados de consentimento são coletados, armazenados e aplicados nos fluxos de trabalho da experiência do cliente. Consulte a [visão geral do processamento de consentimento](../../landing/governance-privacy-security/consent/adobe/overview.md).

## Conceitos principais: campos primitivos e de contêiner

Leia esta seção para saber como as regras de política de consentimento usam diferentes tipos de campo em esquemas XDM. Entender a distinção entre contêiner e campos primitivos ajuda a selecionar o campo e o operador corretos ao definir as condições da política.

### Tipos de campo e lógica de regra compatíveis

As políticas de consentimento aceitam vários tipos de campo, cada um com operadores específicos para a criação de condições de regra. Os tipos de campo são agrupados em duas categorias: **tipos de contêiner** e **tipos primitivos**.

### Tipos de contêiner (navegação por esquema)

Os tipos de contêiner organizam os dados de consentimento, mas não podem ser usados diretamente nas condições da política. Eles servem como caminhos de navegação para alcançar os campos primitivos que contêm valores reais.

| Tipo de contêiner | Descrição |
|----------------|-------------|
| **Objeto** | Um container com um esquema fixo que armazena vários campos de tipos diferentes. |
| Matriz **1}** | Um contêiner que armazena vários valores do mesmo tipo. |
| **Mapa** | Um contêiner com chaves dinâmicas que pode conter objetos ou outros tipos de campo. |

>[!IMPORTANT]
>
>Campos de container não podem ser selecionados diretamente nas condições da política de consentimento. Você deve navegar nos contêineres para selecionar **campos primitivos** (como sequência, número ou booleano) para a criação de regras. Os operadores de contêiner são usados somente para navegação de esquema, não para definir condições de política.

### Tipos primitivos (condições da regra)

Os campos primitivos contêm os valores de dados de consentimento reais (por exemplo, `true` ou `"weekly"`) e são os únicos tipos de campo que podem ser usados para definir condições de política.

A tabela abaixo descreve cada tipo primitivo suportado e os operadores disponíveis.

| Tipo primitivo | Operadores compatíveis | Descrição |
|----------------|---------------------|-------------|
| **String** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Atributos de consentimento baseados em texto. |
| **Número** | `is equal to`, `is not equal to`, `is greater than`, `is less than`, `exists`, `does not exist` | Atributos numéricos de consentimento. |
| **Booleano** | `is equal to`, `is not equal to` | Valores de consentimento verdadeiros ou falsos. |
| **Data** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Atributos de consentimento baseados em data. |


## Trabalho com estruturas de dados complexas

Leia esta seção para saber como navegar em containers aninhados no esquema de consentimento para alcançar campos primitivos. Ele apresenta padrões de esquema comuns e explica como estruturas mais profundas permitem uma lógica de consentimento mais granular.

### Manuseio de estruturas de esquema aninhadas e complexas

Esquemas de consentimento complexos geralmente incluem estruturas de contêiner aninhadas que oferecem suporte a gerenciamento de dados flexível e escalável. Como as regras de política só podem fazer referência a campos primitivos, você deve navegar pelas hierarquias de container para chegar aos campos que podem ser usados nas condições de política de consentimento. O aninhamento mais profundo permite o direcionamento de regras mais granulares e específicas.

Padrões comuns de contêiner aninhado incluem:

* **Mapa de mapa** - Chaves dinâmicas que contêm outros mapas.
* **Mapa de objeto** - Chaves dinâmicas que contêm objetos com esquemas fixos.
* **Matriz de mapa** - Matrizes que contêm mapas com chaves dinâmicas.
* **Matriz de objeto** - Matrizes que contêm objetos com esquemas fixos.
* **Objeto com propriedades de mapa ou matriz** - Objetos que incluem campos de mapa ou matriz.

### Exemplo de estrutura de campo

A estrutura a seguir serve como referência visual para exemplos de regras neste guia.

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## Criação de regra avançada por tipo de campo

Leia esta seção para obter uma orientação detalhada sobre como criar regras de política de consentimento com base no tipo de campo. Você aprenderá a configurar a lógica de regras para boolianos, mapas, objetos e arrays para capturar condições de consentimento precisas.

### Componentes e etapas de criação de regras

A criação de regras eficazes de política de consentimento requer a compreensão de como navegar na estrutura do esquema e aplicar os operadores corretos para cada tipo de campo. Cada regra segue a mesma abordagem básica: navegue até um campo primitivo, selecione o operador apropriado e defina a condição que deve ser atendida.

Siga estas etapas para criar uma regra:

1. **Selecione um campo** - Navegue pelos campos de contêiner para obter um campo primitivo.
2. **Escolher um operador** - Selecione o operador aceito pelo tipo de campo.
   ![O painel de navegação do esquema hierárquico, mostrando um usuário expandindo um contêiner para atingir um campo primitivo.](../images/policies/consent-policy-map-field.png)
3. **Definir um valor** - Defina o valor ou a condição a ser correspondida.
4. **Corresponder chaves de mapa** - Escolha se deseja direcionar uma chave específica ou corresponder em todas as chaves de um mapa.
5. **Adicionar condições** - Combine várias regras usando a lógica AND ou OR, conforme necessário.

### Trabalhar com campos booleanos (lógica de consentimento implícito)

Os campos booleanos armazenam valores de consentimento verdadeiros ou falsos e representam os atributos de consentimento mais comuns. O operador `is not equal to` permite que você inclua perfis que não tenham sido explicitamente excluídos, oferecendo suporte a cenários de consentimento implícito.

**Operadores e resultados booleanos**

| Operador | Valor | Resultado |
|----------|-------|--------|
| `is equal to` | `true` | Inclui perfis com consentimento explícito (`true`). |
| `is equal to` | `false` | Inclui perfis com recusa explícita (`false`). |
| `is not equal to` | `true` | Inclui perfis sem consentimento explícito (`false` ou ausente). |
| `is not equal to` | `false` | Inclui perfis que não recusaram explicitamente (`true` ou estão ausentes). |

**Exemplo: Consentimento de email implícito**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### Trabalho com campos de mapa (preferências dinâmicas)

Os campos de mapa armazenam pares de valores-chave com chaves dinâmicas, ao contrário de objetos que têm esquemas fixos. Os mapas são usados com frequência em centros de preferências, onde novas categorias podem ser adicionadas sem atualizações de esquema. Você pode direcionar chaves específicas ou usar a correspondência curinga em todas as chaves.

**Correspondência de chave específica**

Use essa abordagem para direcionar uma categoria de preferência específica.

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**Qualquer correspondência de chave**

Use a opção de caixa de seleção &quot;**[!UICONTROL find any matching item]**&quot; para corresponder todas as chaves dinâmicas em um mapa.

![Construtor de regras de política mostrando a caixa de seleção &quot;Localizar qualquer item correspondente&quot; para campos de Mapa, usados para corresponder valores em todas as chaves dinâmicas.](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### Trabalhar com campos de objeto (navegação fixa)

Os campos de objeto atuam como contêineres com esquemas fixos. Eles são usados apenas para navegação e não podem ser referenciados diretamente em condições de política.

**Exemplo de navegação**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**Exemplo de caso de uso:**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### Trabalhar com campos de matriz (vários valores)

Os campos de matriz contêm vários valores do mesmo tipo e requerem manipulação diferente dependendo se eles armazenam primitivos ou objetos. As opções de navegação e operador variam de acordo com o tipo de matriz.

**Matriz de exemplos primitivos**

Use o operador `contains` para identificar perfis com base em valores específicos em uma matriz.

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**Exemplo de matriz de objetos**

Navegue até a matriz para acessar campos primitivos dentro de objetos aninhados.

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## Combinação de regras com lógica complexa

Esta seção explica como combinar várias condições de regra usando a lógica AND ou OR. Você aprenderá como os operadores lógicos trabalham juntos para definir políticas avançadas de consentimento de várias condições.

### Combinação de várias condições (lógica AND ou OR)

É possível combinar várias condições de regra usando a lógica AND ou OR para criar políticas de consentimento mais sofisticadas que segmentem segmentos de perfil específicos.\
A lógica **AND** exige que todas as condições sejam verdadeiras, produzindo correspondências de público-alvo mais estreitas.\
A lógica **OR** permite que qualquer condição seja verdadeira, expandindo o alcance do público-alvo.

Na interface da política de consentimento, use o seletor de lógica que aparece entre as condições da regra para alternar entre a lógica E e OU.

### Exemplo de regra complexa geral

O exemplo a seguir combina o status de consentimento básico com a frequência de preferência para criar um segmento direcionado.

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### Lógica avançada para arrays de objetos

Ao combinar condições em matrizes de objetos, o comportamento depende do uso da lógica AND ou OR entre as condições.

**Exemplo: Matriz de objetos com condições AND**

Use a lógica AND quando todas as condições forem aplicáveis ao elemento de matriz *same*.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**Práticas recomendadas para a lógica AND**
>
>Lembre-se desses comportamentos principais ao criar condições de array baseadas em AND:
>
>* Use a lógica AND quando todas as condições forem aplicáveis ao **mesmo elemento de matriz**.
>* Lembre-se de que AND cria direcionamento restritivo (menos perfis corresponderão).
>* Não espere que a lógica AND corresponda a várias entradas de matriz; ela se aplica a cada entrada.
>* Evite usar a lógica AND quando precisar de correspondência flexível entre entradas.

>[!IMPORTANT]
>
>Com a lógica AND, cada entrada de matriz deve atender a todas as condições especificadas de uma só vez. Esse comportamento é ideal quando você precisa corresponder a atributos combinados, como categorias que são habilitadas e promocionais.

>[!NOTE]
>
>A lógica AND se aplica à mesma entrada de matriz **somente para matrizes de objetos.**\
>Para matrizes de primitivos, a lógica AND é avaliada no nível do campo em toda a matriz.

**Exemplo: Matriz de objetos com condições OR**

Use a lógica OU para criar correspondências de público-alvo inclusivas, permitindo que qualquer condição seja verdadeira nas entradas da matriz.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### Próximas etapas

Depois de criar e refinar suas regras de política de consentimento, use os seguintes recursos para finalizar a configuração, validar a aplicação de política e revisar os modelos de dados subjacentes.

* **Fluxo de Trabalho de Criação de Política**: implemente as regras definidas na interface do usuário do construtor de políticas com o [Guia de Interface de Política de Consentimento](user-guide.md#consent-policy.md)
* **Avaliação e Imposição de Política de Consentimento**: verifique como a política habilitada afeta a ativação de público-alvo e o uso de dados de perfil. Consulte o [Guia de aplicação automática de política](../enforcement/auto-enforcement.md) para obter detalhes
* **Tipos de dados de consentimento XDM**: faça referência às estruturas de esquema específicas e definições de campo para atributos de consentimento usados em suas regras de política. Consulte o guia do [tipo de dados Consentimentos e Preferências XDM](../../xdm/data-types/consents.md).
