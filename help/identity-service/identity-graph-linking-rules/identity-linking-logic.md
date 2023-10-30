---
title: Lógica de vinculação do serviço de identidade
description: Saiba mais sobre como o Serviço de identidade vincula identidades diferentes para criar uma visualização abrangente de um cliente.
hide: true
hidefromtoc: true
badge: Alfa
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 4%

---

# Lógica de vinculação do Serviço de identidade

>[!IMPORTANT]
>
>As regras de vinculação do gráfico de identidade estão atualmente em Alpha. O recurso e a documentação estão sujeitos a alterações.

Um link entre duas identidades é estabelecido quando o namespace de identidade e os valores de identidade são correspondentes.

Há dois tipos de identidades que são vinculadas:

* **Registros de perfil**: essas identidades geralmente vêm de sistemas CRM.
* **Eventos de experiência**: essas identidades geralmente vêm da implementação do SDK da Web ou da fonte do Adobe Analytics.

## Compreender a lógica de vinculação do Serviço de identidade

Uma identidade consiste em um namespace de identidade e um valor de identidade.

* Um namespace de identidade é o contexto de um determinado valor de identidade para. Exemplos comuns de namespaces de identidade incluem CRM ID, Email e Telefone.
* Um valor de identidade é a string que representa uma entidade real. Por exemplo: &quot;julien<span>@acme.com&quot; pode ser um valor de identidade para um namespace de email e 555-555-1234 pode ser um valor de identidade correspondente para um namespace de telefone.

>[!TIP]
>
>O namespace de identidade é importante porque, sem ele, o valor de identidade perde seu contexto e não terá informações suficientes para corresponder com êxito às identidades.

Consulte os diagramas a seguir para obter uma representação visual de como funciona a lógica de vinculação do Serviço de identidade:

>[!BEGINTABS]

>[!TAB Gráfico existente]

Suponha que você tenha um gráfico de identidade existente com três identidades vinculadas:

* TELEFONE:(555)-555-1234
* EMAIL:julien<span>@acme.com
* ID DO CRM: 60013ABC

![gráfico existente](../images/identity-settings/existing-graph.png)

>[!TAB Dados de entrada]

Um par de identidades é assimilado em seu gráfico e esse par contém:

* ID DO CRM: 60013ABC
* ECID:100066526

![dados de entrada](../images/identity-settings/incoming-data.png)

>[!TAB Gráfico atualizado]

O Serviço de identidade reconhece que a ID do CRM:60013ABC já existe no gráfico e, portanto, vincula apenas a nova ECID

![gráfico atualizado](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Cenário do cliente

Você é um engenheiro de dados e assimila o seguinte conjunto de dados do CRM (registro de Perfil) no Experience Platform.

| ID do CRM** | Telefone* | Email* | Nome | Sobrenome |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Indica o campo marcado como identidade principal.
>* `*` - Indica o campo marcado como identidade secundária.
>
>O serviço de identidade não faz distinção entre a identidade primária e secundária. Desde que um campo esteja marcado como uma identidade, ele será assimilado no Serviço de identidade.

Você também implementou o SDK da Web e assimilou um conjunto de dados do SDK da Web (Evento de experiência) com as seguintes tabelas de dados:

| Carimbo de data e hora | Identidades no evento* | Evento |
| --- | --- | --- |
| `t=1` | ECID:38652 | Visualizar página inicial |
| `t=2` | ECID:38652, CRM ID:31260XYZ | Procurar sapatos |
| `t=3` | ECID:44675 | Visualizar página inicial |
| `t=4` | ECID:44675, ID DO CRM: 31260XYZ | Exibir histórico de compras |

>[!NOTE]
>
>* `*` - Denota um campo marcado como identidade, com a ECID marcada como primária.
>* Por padrão, o identificador de pessoa (nesse caso, a ID de CRM) é designado como a identidade principal. Se o identificador de pessoa não existir, o identificador de cookie (nesse caso, a ECID) se tornará a identidade principal.

Neste exemplo:

* `t=1`, usou um computador desktop (ECID:38652) e para exibir a navegação da página inicial de forma anônima.
* `t=2`, usou o mesmo computador desktop, fez logon (ID do CRM:31260XYZ) e procurou sapatos.
   * Depois que um usuário é conectado, o evento envia a ECID e a ID do CRM para o Serviço de identidade.
* `t=3`, usou um laptop (ECID:44675) e navegou anonimamente.
* `t=4`, usou o mesmo notebook, fez logon (ID de CRM: 31260XYZ) e visualizou o histórico de compras.


>[!BEGINTABS]

>[!TAB timestamp=0]

Em `timestamp=0`, você tem dois gráficos de identidade para dois clientes diferentes. Ambos são representados por três identidades vinculadas.

| | ID do CRM | Email | Telefone |
| --- | --- | --- | --- |
| Cliente um | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Cliente dois | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

Em `timestamp=1`, um cliente usa um laptop para visitar seu site de comércio eletrônico, visualizar sua página inicial e navegar anonimamente. Esse evento de navegação anônimo é identificado como ECID:38652. Como o Serviço de identidade armazena apenas eventos com pelo menos duas identidades, essas informações não são armazenadas.

![timestamp-um](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

Em `timestamp=2`, um cliente usa o mesmo laptop para visitar o site de comércio eletrônico. Eles fazem logon com sua combinação de nome de usuário e senha e procuram sapatos. O serviço de identidade identifica a conta do cliente quando ele faz logon, pois ela corresponde à ID do CRM: 31260XYZ. Além disso, o Serviço de identidade relaciona ECID:38562 à CRM ID:31260XYZ, pois ambos usam o mesmo navegador no mesmo dispositivo.

![carimbo de data e hora-dois](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

Em `timestamp=3` um cliente usa um tablet para visitar seu site de comércio eletrônico e navegar anonimamente. Esse evento de navegação anônimo é identificado como ECID:44675. Como o Serviço de identidade armazena apenas eventos com pelo menos duas identidades, essas informações não são armazenadas.

![timestamp-três](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

Em `timestamp=4`, um cliente usa o mesmo tablet, faz logon em sua conta (ID do CRM:31260XYZ) e visualiza o histórico de compras. Esse evento vincula sua ID de CRM:31260XYZ ao identificador de cookie atribuído à atividade de navegação anônima, ECID:44675, e vincula ECID:44675 ao gráfico de identidade do cliente dois.

![timestamp-quatro](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Visão geral das regras de vinculação do gráfico de identidade](./overview.md)
* [Exemplos de cenários para configurar regras de vinculação de gráficos de identidade](./example-scenarios.md)
* [Serviço de identidade e perfil do cliente em tempo real](identity-and-profile.md)
