---
title: Permissões de usuário para tags
description: Saiba mais sobre os diferentes tipos de permissões disponíveis para tags e algumas estratégias básicas de implementação para diferentes casos de uso comercial.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: 88593d921d6ad97fc4dfb059f0272817caee06c7
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 23%

---

# Permissões do usuário para tags

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Permissões de usuário para tags no Adobe Experience Platform são atribuídas aos usuários por meio do Adobe Admin Console. Em vez de ser atribuído a usuários individuais, conjuntos diferentes de permissões são configurados separadamente como perfis de produtos. Os usuários são atribuídos a esses perfis de produto para receber as permissões para as quais foram configurados.

Este guia fornece uma visão geral dos diferentes tipos de permissões disponíveis para tags, as funcionalidades às quais concedem acesso e algumas estratégias básicas de implementação para diferentes casos de uso comercial.

>[!NOTE]
>
>Para obter etapas sobre como configurar permissões para usuários que usam o Admin Console, consulte o tutorial em [gerenciar permissões para tags](./manage-permissions.md).

## Tipos de permissão

Em um perfil de produto, as permissões para tags são divididas em quatro categorias:

1. Plataformas
1. Propriedades
1. Direitos de propriedade
1. Direitos da empresa

### Plataformas

Cada propriedade de tag tem uma plataforma. Atualmente, existem duas plataformas que podem ser usadas para tags: Web e Móvel. Você pode usar esse tipo de permissão para restringir ou conceder acesso a um tipo específico de propriedade. Isso pode ser útil quando a equipe que gerencia seus aplicativos móveis for diferente da que gerencia seus sites.

### Propriedades

Por padrão, os perfis de produtos concedem acesso a todas as propriedades que existem na empresa, no momento e no futuro. Usando esse tipo de permissão, você pode restringir ou conceder acesso a propriedades existentes específicas por nome.

### Direitos de propriedade {#property-rights}

Qualquer propriedade criada na interface do usuário da coleta de dados fica disponível no Admin Console, permitindo agrupar a propriedade com direitos de propriedade específicos no mesmo perfil de produto.

Por exemplo, se um determinado perfil de produto não tiver acesso à Propriedade A1, os usuários que pertencem a esse perfil não poderão ver nem modificar nenhuma configuração na Propriedade A1.

Se um usuário pertencer a um perfil que tenha acesso à Propriedade A1, as ações que ele pode executar na Propriedade A1 serão determinadas pelos direitos que foram concedidos a partir desse perfil. Se um usuário tiver permissões para a Propriedade A1, mas não tiver direitos atribuídos, ele terá acesso somente leitura para essa propriedade.

A tabela a seguir descreve os direitos de propriedade disponíveis e as funcionalidades às quais eles concedem acesso:

| Direito de propriedade | Descrição |
| --- | --- |
| **Desenvolver** | Isso permite executar as seguintes ações:<ul><li>Criar regras e elementos de dados</li><li>Crie bibliotecas e as crie em ambientes de desenvolvimento existentes</li><li>Enviar uma biblioteca para aprovação</li></ul>A maioria das tarefas diárias na interface da coleção de dados exige esse direito. |
| **Aprovar** | Isso permite pegar uma biblioteca enviada e criar no ambiente de preparo. Você também pode aprovar uma biblioteca para publicação depois que o teste for concluído. |
| **Publicar** | Isso permite publicar bibliotecas aprovadas no ambiente de produção. |
| **Gerenciar extensões** | Isso permite executar as seguintes ações: <ul><li>Instalar novas extensões em uma propriedade</li><li>Modificar a configuração de uma extensão já instalada</li><li>Excluir uma extensão</li></ul>Consulte a documentação de visão geral das extensões para obter [mais informações sobre extensões](../managing-resources/extensions/overview.md). Normalmente, essa função pertence aos setores de TI ou de Marketing, dependendo de como funciona a sua organização. |
| **Gerenciar ambientes** | Isso permite criar e modificar ambientes. Consulte a [documentação de ambientes](../publishing/environments.md) para obter mais informações. Normalmente, essa função pertence ao grupo de TI. |

{style=&quot;table-layout:auto&quot;}

### Direitos da empresa

Os direitos da empresa se aplicam às permissões que abrangem várias propriedades. Elas estão descritas na tabela abaixo:

| Direito da empresa | Descrição |
| --- | --- |
| **Gerenciar propriedades** | Isso permite executar as seguintes ações:<ul><li>Criar novas propriedades</li><li>Modificar metadados e configurações no nível da propriedade</li><li>Excluir propriedades</li></ul>São administradores que normalmente executam essa função. Consulte a [documentação de propriedades](companies-and-properties.md) para obter mais informações. |
| **Desenvolver extensões** | Concede a capacidade de criar e modificar pacotes de extensão da empresa, incluindo versões privadas e solicitações de lançamento de versão pública. |
| **Gerenciar configurações do aplicativo** | Isso só estará disponível se você tiver uma licença do Adobe Journey Optimizer ou outra solução que conceda acesso a mensagens por push e no aplicativo móvel.  Permite gerenciar os aplicativos que a Experience Cloud conhece, juntamente com as credenciais de push necessárias para se comunicar com o serviço Firebase Cloud Messaging e o Apple Push Notification Service. |

{style=&quot;table-layout:auto&quot;}

## Total de permissões de usuário

O total de permissões de um usuário individual é determinado pela associação total em diferentes perfis de produto. Se um usuário pertencer a vários perfis de produto, as permissões de cada perfil serão adicionadas juntas, em vez de serem multiplicadas.

Por exemplo, o Perfil de produto A concede a você o direito de desenvolvimento para a Propriedade 1. O Perfil do produto B concede a você o direito de Publicação para a Propriedade 2. Nesse caso, você pode desenvolver na propriedade 1 e publicar na propriedade 2, mas não pode publicar na propriedade 1 ou desenvolver na propriedade 2, pois não recebeu direitos explícitos para isso.

## Cenários de concedimento de direitos

Empresas diferentes têm necessidades diferentes ao criar novos perfis de produto. Essas necessidades variam com base no tamanho da empresa, na estrutura da organização, no número de sites, no número de pessoas envolvidas no gerenciamento de tags e assim por diante.

Abaixo estão alguns cenários comuns e um ponto de partida recomendado conforme você pensa em criar perfis de produtos e adicionar usuários a eles.

### Uma pessoa controla tudo

Se você administrar uma pequena empresa que tenha uma pessoa responsável por tudo, conceda a esse usuário permissões para todas as propriedades e atribua a ele todos os direitos listados acima.

### Separação de tarefas

Considere uma situação em que muitas pessoas em sua organização estão envolvidas na marcação. Você tem um conjunto de pessoas (como um consultor externo) que cria regras e elementos de dados, mas não quer que eles tenham acesso ao ambiente de produção. Nesse caso, você deseja garantir que ninguém implante em produção, exceto a equipe de TI.

Para fazer isso:

1. Crie uma conta para seus consultores e conceda a eles somente o direito de desenvolver.
1. O consultor cria e faz testes dentro dos limites definidos.
1. Se o consultor quiser uma nova extensão ou estiver pronto para entrar em vigor, um representante da sua organização (com os direitos apropriados) executará essas ações.

### Empresarial

Uma empresa com assinatura Empresarial pode ter vários sites divididos geograficamente, com equipes diferentes responsáveis por cada local. Nessas equipes, indivíduos diferentes desenvolvem e publicam.

Isso é semelhante à &quot;Separação de tarefas&quot; mencionada acima, mas é organizado por áreas geográficas. Por exemplo, você pode criar um perfil &quot;Desenvolver&quot; e um perfil &quot;Publicar&quot; para a América do Norte e criar grupos &quot;Desenvolver&quot; e &quot;Publicar&quot; separados para a Europa.

## Exemplo de funções

A tabela a seguir fornece alguns exemplos dos tipos de funções que você pode ter em sua organização e quais permissões você deve atribuir a eles:

| Função | Descrição | Propriedades | Direitos de propriedade | Direitos da empresa |
| --- | --- | --- | --- | --- |
| O gerente | Quer ver o que está acontecendo no sistema, mas não deve poder fazer alterações. | Incluir automaticamente | (None) | (Nenhum) |
| O profissional de marketing | Pode instalar extensões e configurar novas tags para propriedades existentes, mas não pode publicar nos ambientes de preparo ou produção. | Incluir automaticamente | <ul><li>Desenvolver</li><li>Gerenciar extensões</li></ul> | <ul><li>Gerenciar propriedades</li></ul> |
| O desenvolvedor de aplicativos móveis | É responsável pela implementação de soluções Adobe e de terceiros dentro de um aplicativo móvel nativo. | Incluir automaticamente | <ul><li>Desenvolver</li><li>Gerenciar extensões</li></ul> | <li>Gerenciar propriedades</li><li>Gerenciar configurações do aplicativo</li> |
| A equipe de TI | Na verdade, não modifica nenhuma tag, mas elas têm controle total sobre os ambientes de preparação e produção e o que está neles. | Incluir automaticamente | (Nenhum) | <ul><li>Aprovar</li><li>Publicar</li><li>Gerenciar ambientes</li></ul> |
| O desenvolvedor de extensões | Desenvolve extensões e pode enviar para aprovação, mas não pode publicá-las ou adicioná-las às propriedades existentes. | Incluir automaticamente | <ul><li>Desenvolver</li></ul> | <ul><li>Gerenciar propriedades</li><li>Desenvolver extensões</li></ul> |
| O Superusuário | Faz tudo. | Incluir automaticamente | <ul><li>Desenvolver</li><li>Aprovar</li><li>Publicar</li><li>Gerenciar extensões</li><li>Gerenciar ambientes</li></ul> | <ul><li>Gerenciar propriedades</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Este documento forneceu uma visão geral das permissões disponíveis para tags no Experience Platform. Para obter etapas sobre como configurar perfis de produto para tags no Adobe Admin Console, consulte o guia sobre [gerenciamento de permissões de usuário](./manage-permissions.md).
