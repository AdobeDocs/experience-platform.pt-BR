---
title: Definir identidades primárias em um conjunto de dados ad hoc
description: O Adobe Experience Platform Query Service permite definir uma identidade ou uma identidade primária para campos de conjunto de dados de esquema ad hoc diretamente através do comando SQL ALTER TABLE. O documento explica como usar o comando ALTER TABLE para definir uma identidade primária ou secundária.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Definir identidades primárias em um conjunto de dados ad hoc

O Adobe Experience Platform Query Service permite marcar colunas do conjunto de dados como identidades primárias ou secundárias usando restrições para o SQL `ALTER TABLE` comando. Você pode usar esse recurso para garantir que os campos sinalizados sejam consistentes com os requisitos de privacidade de dados. Este comando permite adicionar ou excluir restrições para colunas da tabela de identidade primária e secundária diretamente por meio do SQL.

## Introdução

Rotular colunas do conjunto de dados como identidade primária ou secundária requer uma compreensão do `ALTER TABLE` Comando SQL e boa compreensão dos requisitos de privacidade de dados. Antes de continuar com este documento, reveja a seguinte documentação:

* [O guia de sintaxe SQL para o `ALTER TABLE` comando](../sql/syntax.md).
* [A visão geral da Governança de dados](../../data-governance/home.md) para obter mais informações.

## Adicionar restrições {#add-constraints}

O `ALTER TABLE` permite rotular uma coluna de conjunto de dados como identidade de uma pessoa e usar esse rótulo como uma identidade primária atualizando os metadados associados usando SQL. Isso é especialmente útil quando os conjuntos de dados são criados por meio do SQL, em vez de diretamente de um esquema por meio da interface do usuário da plataforma. O comando pode ser usado para garantir que suas operações de dados no Platform sejam compatíveis com as políticas de uso de dados.

**Exemplos**

O exemplo a seguir adiciona uma restrição ao existente `t1` tabela. Os valores da variável `id` agora são marcadas como identidades primárias em `IDFA` namespace. Um namespace de identidade é uma palavra-chave que declara o tipo de dados de identidade que o campo representa.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

O segundo exemplo garante que a variável `id` é marcada como uma identidade secundária.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Restrições de soltar {#drop-constraints}

As restrições também podem ser removidas das colunas da tabela usando o `ALTER TABLE` comando.

**Exemplos**

O exemplo a seguir remove o requisito de que a variável `c1` deve ser rotulada como uma identidade primária no `t1` tabela.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Como visto abaixo, a mesma sintaxe é usada para remover uma restrição de identidade.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostrar identidades

Usar o comando de metadados `show identities` na interface da linha de comando para exibir uma tabela com todos os atributos atribuídos como uma identidade.

```shell
> show identities;
```

Um exemplo de tabela retornada é exibido abaixo.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitações do XDM {#limitations}

A lista a seguir explica considerações importantes para a atualização de identidades em conjuntos de dados existentes ao usar o XDM.

* Para especificar uma coluna como uma identidade, você **must** também defina o namespace a ser preservado como metadados para a coluna.
* O XDM não suporta a especificação de um nome de coluna no atributo de namespace.
* Se o esquema usar a variável `identityMap` Campo XDM, a raiz ou o nível superior `identityMap` objeto **must** Ser rotuladas como uma identidade ou identidade primária.
