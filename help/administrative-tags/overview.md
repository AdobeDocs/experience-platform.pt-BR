---
keywords: Experience Platform;página inicial;tópicos populares;tags administrativas;tags;
title: Visão geral das tags administrativas
description: Este documento fornece informações sobre tags administrativas no Adobe Experience Platform
source-git-commit: f184e94350a79936cbbd9072791650af99fa945f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# Visão geral das tags

As tags são um recurso da Adobe Experience Platform que permite aos administradores gerenciar taxonomias de metadados para classificar objetos de negócios para facilitar a descoberta e a categorização. Tags são metadados que podem ser considerados palavras-chave que podem ser anexadas a um segmento, conjunto de dados, jornada ou outros objetos para permitir que as pesquisas localizem esse objeto e objetos relacionados. As tags são classificadas em dois tipos: categorizadas e não categorizadas.

Para fornecer mais contexto e definir a finalidade de uma tag, as categorias organizam tags em conjuntos úteis. Um administrador define quais tags categorizadas estão disponíveis para os usuários adicionarem aos objetos. Novas tags que não contêm categorias também podem ser criadas em linha em workflows nos quais as tags são aplicadas. Essas tags serão exibidas na seção sem categoria do inventário de tags. As tags podem ser aplicadas por administradores e usuários, independentemente de quem as criou. Todos os tipos de tags estão disponíveis para seleção ao atribuir a um objeto, pesquisar ou filtrar.

## Terminologia de tags

A marcação envolve os seguintes componentes:

| Terminologia | Definição |
| --- | --- |
| Arquivado | Um estado para uma tag que mantém associações atuais com objetos, mas restringe a tag de ser aplicada a outros objetos.  Tags arquivadas são ocultas do seletor de tags. |
| Objeto | Um item Experience Cloud que pode ter uma tag aplicada.  Exemplos: Segmento, Jornada, Conjunto de dados. |
| Tag | Tags são metadados e podem ser consideradas palavras-chave que podem ser anexadas a um segmento, conjunto de dados, jornada ou outros objetos para permitir que as pesquisas localizem esse objeto e objetos relacionados. |
| Categoria da tag | As Categorias de tags agrupam as tags em conjuntos significativos para fornecer maior contexto ou descrever a finalidade da tag.  Os administradores gerenciam categorias de tags e tags em categorias. |
| Tag sem categoria | Uma nova tag criada em linha, onde as tags são aplicadas. Essas tags podem ser criadas e aplicadas por qualquer usuário, mas não estão vinculadas a uma categoria.  Os administradores podem mover essas tags para uma categoria para alinhá-las a outras tags semelhantes. |

## Estoque de etiquetas

A categoria e o gerenciamento de tags usando o inventário de tags estão disponíveis na navegação por Experience Platform e Journey Optimizer. As alterações nas etiquetas no inventário são refletidas em todos os objetos que suportam etiquetas. Todos os usuários podem acessar e navegar pelo inventário de tags, mas o gerenciamento de tags está limitado aos administradores do sistema e do produto.

O inventário de tags tem três níveis de hierarquia, permitindo que os usuários gerenciem categorias de tags, tags em uma categoria e tags individuais. Ao gerenciar uma tag individual, os usuários podem visualizar e navegar para qualquer objeto no qual essa tag é aplicada no momento.

### Categorias de tags

As categorias agrupam tags em conjuntos significativos para fornecer maior contexto ou descrever a finalidade da tag. Em qualquer tag do com uma categoria, o nome da categoria seguido de dois pontos precede o nome da tag.

As seguintes ações são possíveis ao usar categorias de tag:

* [Criar categoria de tag](./ui/tags-categories.md#create-tag-category)
* [Editar categoria de tag](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Excluir categoria de tag](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gerenciamento de tags em uma categoria

>[!NOTE]
>
>Para gerenciar tags para o Experience Cloud, você deve ser um administrador de sistema ou um administrador de produto do Adobe Experience Platform para sua organização, que tem uma assinatura do Experience Cloud.

Em uma categoria (ou no grupo &quot;Não categorizado&quot; padrão), é possível criar e gerenciar tags. As seguintes ações são possíveis ao gerenciar tags:

* [Criar uma tag](./ui/managing-tags.md#create-a-tag-create-tag)
* [Editar uma tag](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Mover uma tag entre categorias](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Arquivar uma tag](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restaurar uma tag arquivada](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Excluir uma tag](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Exibir objetos marcados](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
