---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; fullName; xdm:fullName; nome da pessoa; nome; nome; tipo de dados; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados do nome da pessoa
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do Nome da pessoa.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# [!UICONTROL Tipo ] de dados de nome da pessoa

[!UICONTROL O ] nome da pessoa é um tipo de dados XDM padrão que descreve o nome completo de uma pessoa. Como as convenções para as estruturas de nomes diferem muito entre as línguas e as culturas, os nomes devem ser sempre modelados utilizando este tipo de dados.

Além disso, o tipo de dados fornece várias propriedades opcionais que podem ser usadas em situações que exigem o uso de apenas um fragmento do nome completo, como a criação de uma saudação formal ou informal.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propriedade | Descrição |
| --- | --- |
| `courtesyTitle` | Uma abreviação do título, honraria ou saudação de uma pessoa (como `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | O primeiro segmento do nome na ordem de escrita mais comumente aceito no idioma do nome. |
| `fullName` | Nome completo da pessoa, por ordem escrita mais comumente aceite na língua do nome. |
| `lastName` | O último segmento do nome na ordem de escrita mais comumente aceito no idioma do nome. |
| `middleName` | Nomes do meio, alternativos ou adicionais fornecidos entre o nome e sobrenome. |
| `suffix` | Um grupo de cartas fornecido após o nome de uma pessoa para fornecer informações adicionais (como `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III` e assim por diante). |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados do nome da pessoa, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
