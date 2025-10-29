---
title: Criptografar valores
description: Saiba como criptografar valores confidenciais ao usar a API do Reactor.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# Criptografar valores

Ao serem usadas tags na Adobe Experience Platform, alguns fluxos de trabalho exigem o fornecimento de valores confidenciais (por exemplo, o fornecimento de uma chave privada ao enviar bibliotecas a ambientes por meio de hosts). A natureza confidencial dessas credenciais exige
transferência e armazenamento seguros.

Este documento descreve como criptografar valores confidenciais usando a [criptografia GnuPG](https://www.gnupg.org/gph/en/manual/x110.html) (também conhecida como GPG) para que somente o sistema de tags possa lê-los.

## Obter a chave GPG pública e a soma de verificação

Depois de [baixar](https://gnupg.org/download/) e instalar a versão mais recente do GPG, você deve obter a chave GPG pública para o ambiente de produção das tags:

* [Chave GPG](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Soma de verificação](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importe a chave para seu chaveiro

Depois de salvar a chave em seu computador, o próximo passo é adicioná-la a seu chaveiro GPG.

**Sintaxe**

```shell
gpg --import {KEY_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{KEY_NAME}` | O nome do arquivo de chave pública. |

{style="table-layout:auto"}

**Exemplo**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Criptografar valores

Depois de adicionar a chave ao chaveiro, você pode começar a criptografar valores usando o sinalizador `--encrypt`. O script a seguir demonstra como esse comando funciona:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Esse comando pode ser detalhado da seguinte maneira:

* A entrada é fornecida para o comando `gpg`.
* `--armor` cria saída blindada ASCII em vez de binária. Isso simplifica a transferência do valor por meio do JSON.
* `--encrypt` instrui o GPG para criptografar os dados.
* `-r` define o destinatário dos dados. Somente o destinatário (o detentor da chave privada que corresponde à chave pública) pode descriptografar os dados. Para encontrar o nome do destinatário da chave desejada, examine a saída de `gpg --list-keys`.

O comando acima usa a chave pública de `Tags Data Encryption <launch@adobe.com>` para criptografar o valor, `Example value`, no formato ASCII blindado.

A saída do comando seria semelhante ao seguinte:

```shell
|-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
|-----END PGP MESSAGE-----
```

Essa saída só pode ser descriptografada por sistemas que tenham a chave privada que
corresponde à chave pública `Tags Data Encryption <launch@adobe.com>`.

Essa saída é o valor que deve ser fornecido ao serem enviados dados à API do Reactor. O sistema armazena essa saída criptografada e a descriptografa temporariamente, conforme a necessidade. Por exemplo, o sistema descriptografa as credenciais do host por tempo suficiente para iniciar uma conexão com o servidor e remove imediatamente todos os rastreamentos do valor descriptografado.

>[!NOTE]
>
>O formato do valor blindado e criptografado é importante. Certifique-se de que os retornos de linha tenham um escape adequado no valor fornecido na solicitação.
