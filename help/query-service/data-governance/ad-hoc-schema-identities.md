---
title: Definir identidades principais em um conjunto de dados ad hoc
description: O Adobe Experience Platform Query Service permite definir uma identidade ou uma identidade primária para campos de conjunto de dados de esquema ad hoc diretamente por meio do comando SQL ALTER TABLE. O documento explica como usar o comando ALTER TABLE para definir uma identidade primária ou secundária.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Definir identidades primárias em um conjunto de dados ad hoc

O Adobe Experience Platform Query Service permite marcar colunas de conjunto de dados como identidades primárias ou secundárias usando restrições para o SQL `ALTER TABLE` comando. Você pode usar esse recurso para garantir que os campos sinalizados sejam consistentes com os requisitos de privacidade de dados. Esse comando permite adicionar ou excluir restrições para colunas de tabela de identidade primária e secundária diretamente por meio do SQL.

## Introdução

Rotular as colunas do conjunto de dados como identidade primária ou secundária requer uma compreensão das `ALTER TABLE` Comando SQL e uma boa compreensão dos requisitos de privacidade de dados. Antes de continuar com este documento, reveja a seguinte documentação:

* [O guia de sintaxe SQL para o `ALTER TABLE` comando](../sql/syntax.md).
* [A visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

## Adicionar restrições {#add-constraints}

A variável `ALTER TABLE` permite rotular uma coluna de conjunto de dados como a identidade de uma pessoa e, em seguida, usar esse rótulo como a identidade principal, atualizando os metadados associados usando SQL. Isso é especialmente útil quando conjuntos de dados são criados por SQL, em vez de diretamente de um esquema por meio da interface do usuário da plataforma. O comando pode ser usado para garantir que suas operações de dados na Platform estejam em conformidade com as políticas de uso de dados.

**Exemplos**

O exemplo a seguir adiciona uma restrição ao existente `t1` tabela. Os valores de `id` agora são marcadas como identidades primárias na variável `IDFA` namespace. Um namespace de identidade é uma palavra-chave que declara o tipo de dados de identidade que o campo representa.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

O segundo exemplo garante que a variável `id` é marcada como uma identidade secundária.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Descartar restrições {#drop-constraints}

As restrições também podem ser removidas das colunas da tabela usando o `ALTER TABLE` comando.

**Exemplos**

O exemplo a seguir remove o requisito de que a variável `c1` ser rotulada como uma identidade principal na variável existente `t1` tabela.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Como visto abaixo, a mesma sintaxe é usada para ao remover uma restrição de identidade.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostrar identidades

Usar o comando de metadados `show identities` na interface de linha de comando para exibir uma tabela com todos os atributos atribuídos como uma identidade.

```shell
> show identities;
```

Um exemplo de uma tabela retornada é exibido abaixo.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitações do XDM {#limitations}

A lista a seguir explica considerações importantes para atualizar identidades em conjuntos de dados existentes ao usar o XDM.

* Para especificar uma coluna como uma identidade, você **deve** defina também o namespace a ser preservado como metadados para a coluna.
* O XDM não oferece suporte à especificação de um nome de coluna no atributo de namespace.
* Se o esquema usar a variável `identityMap` Campo XDM, a raiz ou o nível superior `identityMap` objeto **deve** ser rotulados como uma identidade ou identidade principal.
