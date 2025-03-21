---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;fullName;xdm:fullName;nome da pessoa;nome;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Nome da Pessoa
description: Saiba mais sobre o tipo de dados XDM do Nome da pessoa.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Nome da pessoa]

[!UICONTROL Nome da pessoa] é um tipo de dados XDM padrão que descreve o nome completo de uma pessoa. Como as convenções para estruturas de nome diferem amplamente entre idiomas e culturas, os nomes devem sempre ser modelados usando esse tipo de dados.

Além disso, o tipo de dados fornece várias propriedades opcionais que podem ser usadas em situações que exigem o uso de apenas um fragmento do nome completo, como a criação de uma saudação formal ou informal.

![](../images/data-types/person-name.png){width=500}

| Propriedade | Descrição |
| --- | --- |
| `courtesyTitle` | Uma abreviação do título, honorífico ou saudação de uma pessoa (como `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | O primeiro segmento do nome na ordem de escrita aceito com mais frequência no idioma do nome. |
| `fullName` | O nome completo da pessoa, na ordem de escrita aceita com mais frequência no idioma do nome. |
| `lastName` | O último segmento do nome na ordem de escrita aceito com mais frequência no idioma do nome. |
| `middleName` | Nomes do meio, alternativos ou adicionais fornecidos entre o nome e o sobrenome. |
| `suffix` | Um grupo de letras fornecido após o nome de uma pessoa para fornecer informações adicionais (como `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III` e assim por diante). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados do nome da pessoa, consulte o Repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
