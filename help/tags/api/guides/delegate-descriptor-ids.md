---
title: Delegar IDs do descritor
description: Saiba mais sobre as IDs do descritor delegado na API do Reactor e como elas vinculam recursos às extensões.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 100%

---

# Delegar IDs do descritor

Quando você usa tags na Adobe Experience Platform, todas as funcionalidades que pode implantar no site são fornecidas por extensões. Os recursos fornecidos por cada extensão são definidos pelo desenvolvedor da extensão. Quando uma extensão é implantada, ela é fornecida com seus vários recursos na forma de um [pacote de extensão](../endpoints/extension-packages.md). As funcionalidades que os desenvolvedores adicionam a um pacote de extensão são consideradas &quot;delegados&quot; desse pacote.

Cada delegado em um pacote de extensão recebe uma ID exclusiva de descritor delegado. A ID do descritor delegado de um recurso específico informa ao sistema o tipo de recurso e o pacote de extensão ao qual ele pertence.

## Sintaxe

Uma ID de descritor delegado consiste em três strings unidas por caracteres de dois-pontos (`::`), representando o nome do pacote de extensão, o tipo delegado e o nome delegado, respectivamente. Essas strings são compostas para serem legíveis por humanos e são geradas e atribuídas automaticamente pelo sistema quando um pacote de extensão é assimilado.

Por exemplo, se um pacote de extensão chamado `example-package`tiver uma ação chamada`custom-code`, essa ação terá a seguinte ID de descritor delegado: `example-package::actions::custom-code`.

## Utilização de IDs de descritor delegado em recursos aplicáveis

Delegar IDs de descritor é importante para entender quando se trata de definir componentes de regra (eventos, condições e ações) e elementos de dados na API. As seções abaixo descrevem como essas IDs são exibidas para cada recurso.

### Componentes da regra

Um [componente de regra](../endpoints/rule-components.md) deve ser associado a um evento, uma condição ou uma ação que pertença a um pacote de extensão. Representa o &quot;tipo&quot; do componente de regra, pois pertence à lógica da regra geral (um evento, uma condição ou uma ação). Portanto, ao criar um componente de regra, uma ID de descritor delegado deve ser fornecida para indicar a qual evento, condição ou ação o componente de regra deve ser associado.

Por exemplo, para criar um componente de regra de evento baseado em um `click` evento em um pacote de extensão `example-package`, o componente de regra usaria o seguinte valor: `delegate_descriptor_id`: `example-package::events::click`.

Consulte a seção sobre [criação de um componente de regra](../endpoints/rule-components.md#create) para obter mais informações.

### Elementos de dados

Um [elemento de dados](../endpoints/data-elements.md) deve ser associado a um pacote de extensão ao ser criado pela primeira vez, pois cada pacote de extensão define os tipos compatíveis para seus elementos de dados delegados, bem como o comportamento pretendido.

Por exemplo, para criar um elemento de dados que use o `cookie` tipo conforme definido por um pacote de extensão `example-package`, o elemento de dados usaria o seguinte valor `delegate_descriptor_id`: `example-package::dataElements::cookie`.

Consulte a seção sobre [criação de um elemento de dados](../endpoints/data-elements.md#create) para obter mais informações.

### Extensões

Uma [extensão](../endpoints/extensions.md) é automaticamente associada a um pacote de extensão quando ele é criado pela primeira vez e é representada no objeto `relationships` da extensão. Se sua extensão exigir configurações personalizadas, ela também exigirá uma ID de descritor delegado.

>[!NOTE]
>
>As extensões que não exigem configurações personalizadas não precisam de uma ID de descritor delegado.

Por exemplo, para adicionar uma ID de descritor delegado a uma extensão que pertence ao pacote de extensão `example-package`, a extensão usaria o seguinte valor `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Consulte o manual sobre [criação de uma extensão](../endpoints/extensions.md#create) para obter mais informações.
