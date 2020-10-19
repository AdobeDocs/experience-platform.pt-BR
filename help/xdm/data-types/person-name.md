---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do nome da pessoa
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do Nome da Pessoa.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# [!UICONTROL Tipo de dados do nome] da pessoa

[!UICONTROL O nome] da pessoa é um tipo de dados XDM padrão que descreve o nome completo de uma pessoa. Como as convenções para as estruturas de nomes diferem muito entre as línguas e as culturas, os nomes devem ser sempre modelados com base neste tipo de dados.

Além disso, o tipo de dados fornece várias propriedades opcionais que podem ser usadas em situações que exigem o uso de apenas um fragmento do nome completo, como a criação de uma saudação formal ou informal.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propriedade | Descrição |
| --- | --- |
| `courtesyTitle` | Abreviação do título, da honra ou da saudação de uma pessoa (como `Mr.`, `Miss.`ou `Dr.`). |
| `firstName` | O primeiro segmento do nome na ordem de gravação mais comumente aceito no idioma do nome. |
| `fullName` | O nome completo da pessoa, na ordem escrita mais comumente aceite na língua do nome. |
| `lastName` | O último segmento do nome na ordem de gravação mais comumente aceito no idioma do nome. |
| `middleName` | Nomes médios, alternativos ou adicionais fornecidos entre o nome e o sobrenome. |
| `suffix` | Um grupo de letras fornecido após o nome de uma pessoa para fornecer informações adicionais (como `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`etc.). |

Para obter mais detalhes sobre o tipo de dados do nome da pessoa, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)