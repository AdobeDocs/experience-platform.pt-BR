---
keywords: Experience Platform;página inicial;tópicos populares;tags unificadas;tags;
title: Visão geral das tags unificadas (beta)
description: Este documento fornece informações sobre tags unificadas na Adobe Experience Platform
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---

# Visão geral das tags unificadas (beta)

>[!IMPORTANT]
>
>As tags unificadas estão na versão beta. Se quiser deixar um feedback, selecione o botão na parte superior da página de administração de tags.

As tags são um recurso da Adobe Experience Platform que permitem gerenciar taxonomias de metadados para classificar objetos de negócios e facilitar sua descoberta e categorização. As tags são metadados que podem ser considerados como palavras-chave que podem ser anexadas a um segmento, conjunto de dados, jornada ou outros objetos para permitir que as pesquisas localizem esse objeto e objetos relacionados. As tags são classificadas em dois tipos: categorizadas e não categorizadas.

Para fornecer mais contexto e definir a finalidade de uma tag, as categorias organizam as tags em conjuntos úteis. Um administrador define quais tags categorizadas estão disponíveis para os usuários adicionarem aos objetos. Novas tags que não contêm categorias também podem ser criadas em linha em fluxos de trabalho nos quais tags são aplicadas. Essas tags serão exibidas na seção sem categoria do inventário de tags. As tags podem ser aplicadas por administradores e usuários, independentemente de quem as criou. Todos os tipos de tags estão disponíveis para seleção ao atribuí-las a um objeto, pesquisá-las ou filtrá-las.

## Terminologia de tags

As tags possuem os seguintes componentes:

| Terminologia | Definição |
| --- | --- |
| Arquivado | O estado de uma tag que mantém suas associações atuais com os objetos, mas que a impede de ser aplicada a outros.  As tags arquivadas não aparecem no seletor de tags. |
| Objeto | Um item da Experience Cloud que pode ter uma tag aplicada.  Exemplos: segmento, jornada, conjunto de dados. |
| Tag | Tags são metadados e podem ser consideradas como palavras-chave que podem ser anexadas a um segmento, conjunto de dados, jornada ou outros objetos para permitir que as pesquisas localizem esse objeto e objetos relacionados. |
| Categoria de tag | As categorias de tags agrupam as tags em conjuntos significativos para fornecer maior contexto ou descrever a finalidade da tag.  Os administradores gerenciam as categorias de tags e as tags dentro delas. |
| Tag não categorizada | Uma nova tag criada em linha, onde tags são aplicadas. Essas tags podem ser criadas e aplicadas por qualquer usuário, mas não estão vinculadas a uma categoria.  Os administradores podem mover essas tags para uma categoria para alinhá-las a outras tags semelhantes. |

## Inventário de tags

As categorias e o gerenciamento de tags usando o inventário de tags estão disponíveis no painel de navegação da Experience Platform e do Journey Optimizer. As alterações nas tags no inventário são refletidas em todos os objetos compatíveis com tags. Todos os usuários podem acessar e navegar pelo inventário de tags, mas o gerenciamento de tags está restrito apenas aos administradores do sistema e do produto.

O inventário de tags tem três níveis de hierarquia, permitindo que os usuários gerenciem as categorias de tags, tags em uma categoria e tags individuais. Ao gerenciar uma tag individual, os usuários podem visualizar e navegar para qualquer objeto ao qual essa tag está atualmente aplicada.

### Categorias de tags

As categorias agrupam as tags em conjuntos significativos para fornecer maior contexto ou descrever a finalidade da tag. Em qualquer tag do com uma categoria, o nome da categoria seguido de dois pontos precede o nome da tag.

As seguintes ações são possíveis ao usar categorias de tag:

* [Criar categoria de tag](./ui/tags-categories.md#create-tag-category)
* [Editar categoria de tag](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Excluir categoria de tag](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gerenciar tags em uma categoria

>[!NOTE]
>
>Para gerenciar as tags da Experience Cloud, é necessário ser um administrador de sistema ou de produto da Adobe Experience Platform da sua organização que tem uma assinatura da Experience Cloud.

Em uma categoria (ou no grupo padrão “Sem categoria”), é possível criar e gerenciar tags. As seguintes ações são possíveis ao gerenciar tags:

* [Criação de uma tag](./ui/managing-tags.md#create-a-tag-create-tag)
* [Edição de uma tag](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Deslocamento de uma tag entre categorias](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Arquivamento de uma tag](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restauração de uma tag arquivada](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Exclusão de uma tag](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Exibir objetos com tags](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
