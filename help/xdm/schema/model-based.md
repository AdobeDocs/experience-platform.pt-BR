---
keywords: Experience Platform;página inicial;tópicos populares;esquema baseado em modelo;esquema relacional;esquemas relacionais;esquema;Esquema;xdm;modelo de dados de experiência;
solution: Experience Platform
title: Esquemas baseados em modelo
description: Saiba mais sobre esquemas baseados em modelo (também chamados de esquemas relacionais) no Adobe Experience Platform, incluindo recursos, campos obrigatórios, relações e limitações.
badge: Disponibilidade limitada
source-git-commit: 192e97c97ffcb2d695bcfa6269cc6920f5440832
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Esquemas baseados em modelo

>[!AVAILABILITY]
>
>O Data Mirror e os esquemas baseados em modelo estão disponíveis para os **titulares de licença de campanhas orquestradas** da Adobe Journey Optimizer. Eles também estão disponíveis como uma **versão limitada** para usuários do Customer Journey Analytics, dependendo da sua licença e da ativação de recursos. Entre em contato com o representante da Adobe para obter acesso.

Os esquemas baseados em modelo fornecem um padrão de modelagem flexível e controlado para representar dados estruturados no data lake da Adobe Experience Platform. Eles oferecem suporte a chaves primárias impostas, relacionamentos em nível de esquema e controle refinado sobre registros, tudo sem depender de esquemas de união ou sistemas de banco de dados relacional completo.

>[!IMPORTANT]
>
>As considerações de exclusão de dados se aplicam a todas as implementações de esquema baseadas em modelo. Os aplicativos que usam esses esquemas devem entender como as exclusões afetam os conjuntos de dados relacionados, os requisitos de conformidade e os processos de downstream. Planeje cenários de exclusão e revise as [orientações sobre higiene de dados](../../hygiene/ui/record-delete.md#model-based-record-delete) antes da implementação.

>[!NOTE]
>
>Os aplicativos podem se referir a esquemas baseados em modelo como &quot;esquemas relacionais&quot; ao solicitar a criação de esquema para casos de uso de modelagem de dados relacionais.

Use esquemas baseados em modelo para:

* Garanta a integridade dos dados com chaves primárias de campo único ou compostas.
* Habilite o controle preciso de alterações usando o controle de versão para inserções, atualizações e exclusões.
* Defina relações reutilizáveis no nível do esquema para modelar conexões de entidade reais.
* Evite duplicar estruturas de esquema entre aplicativos ao oferecer suporte a vários modelos de dados.
* Ignore as restrições do esquema de união para simplificar a integração, reduzir o inchaço do esquema e evitar alterações indesejadas no esquema.

## Como os esquemas baseados em modelo diferem dos esquemas XDM padrão

Os esquemas XDM padrão no Experience Platform seguem um dos três comportamentos de dados: Registro, Série temporal ou Ad-hoc. Para obter definições e detalhes, consulte [Comportamentos de dados XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/home#data-behaviors).

No modelo tradicional, os esquemas de registro e série temporal participam de [esquemas de união](../api/unions.md) (consulte também o [guia da interface do usuário do esquema de união](../../profile/ui/union-schema.md)). Esses esquemas evoluem automaticamente à medida que [grupos de campos](./composition.md#field-group) compartilhados são atualizados e os campos personalizados devem ser aninhados em um namespace de locatário. Embora eficiente, esse modelo pode retardar a integração, produzir esquemas muito complexos com campos não utilizados e exigir mapeamento ou transformação de dados adicionais. Esses fatores aumentam a curva de aprendizado e o esforço contínuo de manutenção.

Os esquemas baseados em modelo removem as dependências do esquema de união, que eliminam atualizações automáticas de grupos de campos compartilhados e permitem definições de campo direto sem restrições de namespace de locatário. Você obtém controle explícito sobre chaves primárias, relações e design inicial do esquema, facilitando a modelagem de dados para atender às suas necessidades no momento da criação.

## Recursos de esquemas baseados em modelo

Use os seguintes recursos para modelar dados estruturados no data lake e, ao mesmo tempo, manter a governança, a integridade e a interoperabilidade.

* **Suporte a comportamento de esquema**: configurar com:
   * **Comportamento do registro**: captura o estado atual de uma entidade, como um cliente, conta ou campanha.
   * **Comportamento de série temporal**: captura eventos e o tempo em que ocorrem, úteis para sequências de rastreamento ou alterações ao longo do tempo.
* **Imposição de chave primária**: defina uma chave primária para identificar exclusivamente cada registro e evitar duplicatas durante a assimilação.
* **Controle de versão**: use um **identificador de versão** (um descritor) para garantir que as atualizações sejam aplicadas na ordem correta, mesmo que os registros cheguem fora de sequência.
* **Mapeamento de relação**: crie relações um para um ou muitos para um entre esquemas baseados em modelo ou entre esquemas baseados em modelo e padrão. As definições de relacionamento são armazenadas como descritores para permitir associações eficientes.
* **Evolução simplificada**: os esquemas baseados em modelo não participam das exibições de união e não são atualizados quando os grupos de campos compartilhados são alterados, evitando alterações downstream inesperadas.
* **Definição de campo flexível**: adicione campos diretamente sem namespace de id de locatário. Os esquemas baseados em modelo não são compatíveis com grupos de campos XDM.
* **Nenhuma dependência em esquemas de união**: melhora o desempenho da consulta e reduz a sobrecarga operacional de gerenciar exibições de esquema globais.
* **Ordenação de tempo de evento**: para esquemas de série temporal, use um **identificador de carimbo de data/hora** para ordenar eventos por hora de ocorrência em vez de hora de assimilação.

## Campos obrigatórios

Esquemas baseados em modelo exigem determinados descritores — metadados na definição do esquema que controlam comportamentos e restrições principais. Adicione os descritores a seguir como parte da definição do esquema.

### Descritor de chave primária

Use um descritor de chave primária para garantir que cada registro seja identificável exclusivamente. As configurações compatíveis são:

* **Chave primária de campo único**: use um campo com um valor exclusivo para cada registro.
* **Chave primária composta**: use vários campos para formar um identificador exclusivo. Para esquemas de série temporal, a chave composta deve incluir o campo de carimbo de data e hora identificado pelo descritor do carimbo de data e hora.

>[!NOTE]
>
>No Editor de Esquema de Interface do Usuário, o descritor de versão e os descritores de carimbo de data/hora aparecem como &quot;[ !UICOTRNOL Identificador de versão]&quot; e &quot;[ !UICOTRNOL Identificador de carimbo de data/hora]&quot;, respectivamente.

**Exemplo (campo único):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Exemplo (composto para série temporal)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Descritor de versão (identificador)

Defina um descritor de versão (identificador) para manter o estado de registro correto e garantir que a atualização mais recente seja aplicada. Quando vários registros compartilham a mesma chave primária, o registro com o maior valor de versão é considerado o mais recente.

**Exemplo:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Descritor de carimbo de data e hora (identificador)

Para esquemas de série temporal, defina um descritor de carimbo de data e hora (identificador) para definir a hora do evento para ordenação.

**Exemplo:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Os descritores fazem parte dos metadados de definição do esquema e não são armazenados em linhas de dados.

Para obter instruções sobre como criar descritores no Editor de esquemas, consulte [Criar descritores no Editor de esquemas](../tutorials/relationship-ui.md). Para criação baseada em API, consulte [Criar descritores usando a API](../tutorials/relationship-api.md).

## Suporte a relacionamento {#relationship-support}

A modelagem de dados relacionais é um uso principal de esquemas baseados em modelo. Os casos de uso de aplicativos podem até mesmo se referir a esses esquemas como &quot;esquemas relacionais&quot;. Os descritores de relacionamento ativam essas conexões vinculando conjuntos de dados em esquemas sem incorporar chaves estrangeiras nas linhas de dados. Elas melhoram a integridade referencial, permitem padrões de modelagem reutilizáveis e dão suporte a consultas conectadas entre aplicativos.

Crie descritores de relacionamento no nível do esquema para resolução dinâmica no momento da consulta. Os valores de cardinalidade (1:1, muitos para um) fornecem orientação, mas não impõem restrições durante a assimilação, oferecendo suporte à modelagem de dados flexível em conjuntos de dados conectados.

Antes de adicionar descritores de relacionamento, determine o tipo e o público-alvo apropriados:

* **Um para um** - Cada registro no esquema de origem corresponde a no máximo um registro no esquema de destino.
* **De muitos para um** - Vários registros no esquema de origem podem fazer referência ao mesmo registro no esquema de destino.

>[!NOTE]
>
>Você pode definir relações entre dois esquemas baseados em modelo ou entre um esquema baseado em modelo e um esquema padrão. Não há suporte para relações com esquemas ad-hoc.

<!-- Q) 
Madeline commented: "model-based schema to standard might only be offered for b2b customers; that's how it will be on the UI" - is that still accurate? -->

**Exemplo: relação um para um**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

<!-- Q) 
Should these be `@type: "xdm:descriptorRelationship",` This could be a copy-pasting error? -->

**Exemplo: relação muitos para um**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Para obter uma lista de tipos de descritores de relacionamento e sintaxe, consulte a [referência de API de descritores](../api/descriptors.md). Para saber como aplicar esses conceitos na prática, siga os tutoriais para [definir uma relação na API](../tutorials/relationship-api.md) ou [criar uma relação na interface](../tutorials/relationship-ui.md).

>[!NOTE]
>
>Como as relações são definidas no nível do esquema, certifique-se de unir explicitamente conjuntos de dados relacionados em suas consultas. Use uma ferramenta como o Data Distiller para resolver essas relações durante o tempo de consulta.

>[!IMPORTANT]
>
>A cardinalidade da relação é informativa e não é aplicada durante a assimilação. É aplicado somente ao resolver relações durante query ou análise. Não confie nas configurações de cardinalidade para validar seus dados durante a assimilação. Verifique e limpe seus dados e certifique-se de que as regras de relacionamento definidas correspondem à maneira como você pretende consultar ou analisar os dados.

>[!NOTE]
>
> Os esquemas baseados em modelo podem vincular a esquemas padrão, mas não podem vincular a esquemas ad-hoc.

## Exclusão de dados e considerações de higiene {#data-hygiene-support}

Os esquemas baseados em modelo permitem exclusões precisas no nível do registro, que têm implicações universais para todos os aplicativos e casos de uso. Os descritores de chave primária, versão e carimbo de data e hora fornecem a base para a identificação precisa do registro durante as operações de exclusão.

### Impactos da exclusão universal

Todos os aplicativos que usam esquemas baseados em modelo devem considerar:

* **Integridade referencial**: exclusões podem afetar registros relacionados entre conjuntos de dados conectados
* **Requisitos de conformidade**: alguns setores exigem comportamentos de exclusão e trilhas de auditoria específicos
* **Comportamento do aplicativo**: sistemas downstream podem precisar manipular eventos de exclusão adequadamente
* **Consistência de dados**: conjuntos de dados relacionados devem manter a consistência durante operações de exclusão
* **Planejamento de exclusão**: considere os impactos downstream em todos os conjuntos de dados e aplicativos conectados durante a fase de design

Para obter orientação sobre implementação, consulte [Excluindo registros dos conjuntos de dados baseados em modelo](../../hygiene/ui/record-delete.md#model-based-record-delete).

## Limitações e considerações {#limitations}

Revise as seguintes limitações antes de usar esquemas baseados em modelo:

* Os esquemas baseados em modelo não participam de esquemas de união.
* A evolução do esquema é manual; elas não são atualizadas automaticamente quando os grupos de campos são alterados.

>[!IMPORTANT]
>
>A evolução do esquema fica restrita depois que um conjunto de dados é inicializado usando o esquema. Planeje os nomes e tipos de campo com antecedência, pois após a assimilação dos dados, os campos não poderão ser excluídos ou modificados.

* As relações são limitadas a um e muitos a um.
* A disponibilidade depende da sua licença ou da ativação de recursos.
* As chaves primárias compostas são necessárias para esquemas de série temporal.

