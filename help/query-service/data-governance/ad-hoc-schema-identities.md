---
title: Definir identidades principais em um conjunto de dados ad hoc
description: O Adobe Experience Platform Query Service permite definir uma identidade ou uma identidade primária para campos de conjunto de dados de esquema ad hoc diretamente por meio do comando SQL ALTER TABLE. O documento explica como usar o comando ALTER TABLE para definir uma identidade primária ou secundária.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Definir identidades primárias em um conjunto de dados ad hoc

O Adobe Experience Platform Query Service permite marcar colunas de conjunto de dados como identidades primárias ou secundárias usando restrições para o comando SQL `ALTER TABLE`. Você pode usar esse recurso para garantir que os campos sinalizados sejam consistentes com os requisitos de privacidade de dados. Esse comando permite adicionar ou excluir restrições para colunas de tabela de identidade primária e secundária diretamente por meio do SQL.

## Introdução

Rotular as colunas do conjunto de dados como identidade primária ou secundária requer uma compreensão do comando SQL `ALTER TABLE` e uma boa compreensão dos requisitos de privacidade de dados. Antes de continuar com este documento, reveja a seguinte documentação:

* [O guia de sintaxe SQL para o comando `ALTER TABLE`](../sql/syntax.md).
* [A visão geral de Governança de Dados](../../data-governance/home.md) para obter mais informações.

## Adicionar restrições {#add-constraints}

O comando `ALTER TABLE` permite rotular uma coluna de conjunto de dados como a identidade de uma pessoa e, em seguida, usar esse rótulo como a identidade primária, atualizando os metadados associados usando SQL. Isso é especialmente útil quando conjuntos de dados são criados por SQL, em vez de diretamente de um esquema por meio da interface do usuário do Experience Platform. O comando pode ser usado para garantir que suas operações de dados no Experience Platform estejam em conformidade com as políticas de uso de dados.

**Exemplos**

O exemplo a seguir adiciona uma restrição à tabela `t1` existente. Os valores da coluna `id` agora são marcados como identidades primárias no namespace `IDFA`. Um namespace de identidade é uma palavra-chave que declara o tipo de dados de identidade que o campo representa.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

O segundo exemplo garante que a coluna `id` seja marcada como uma identidade secundária.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Descartar restrições {#drop-constraints}

Restrições também podem ser removidas das colunas da tabela usando o comando `ALTER TABLE`.

**Exemplos**

O exemplo a seguir remove o requisito de que a coluna `c1` seja rotulada como identidade primária na tabela `t1` existente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Como visto abaixo, a mesma sintaxe é usada para ao remover uma restrição de identidade.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostrar identidades

Use o comando de metadados `show identities` da interface de linha de comando para exibir uma tabela com todos os atributos atribuídos como uma identidade.

```shell
> show identities;
```

Um exemplo de uma tabela retornada é exibido abaixo.

```console
 tableName | columnName | datatype | namespace | ifPrimary
|-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitações do XDM {#limitations}

A lista a seguir explica considerações importantes para atualizar identidades em conjuntos de dados existentes ao usar o XDM.

* Para especificar uma coluna como identidade, você **deve** também definir o namespace a ser preservado como metadados para a coluna.
* O XDM não oferece suporte à especificação de um nome de coluna no atributo de namespace.
* Se o esquema usar o campo XDM `identityMap`, o objeto `identityMap` de nível superior ou raiz **deverá** ser rotulado como uma identidade ou identidade primária.
