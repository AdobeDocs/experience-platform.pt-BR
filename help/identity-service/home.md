---
keywords: Experience Platform;página inicial;tópicos populares;identidade;Identidade;gráficos XDM;serviço de identidade;serviço de identidade
solution: Experience Platform
title: Visão geral do serviço de identidade
description: O Serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo as identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: f791940300036159ceaad11ff725eecfaa8332f4
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 2%

---

# Serviço de identidade da Adobe Experience Platform

Para fornecer experiências digitais relevantes, você precisa de uma representação abrangente e precisa das entidades do mundo real que compõem sua base de clientes.

Atualmente, organizações e empresas enfrentam um grande volume de conjuntos de dados diferentes: seus clientes individuais são representados por uma variedade de identificadores diferentes. Seu cliente pode estar vinculado a diferentes navegadores da Web (Safari, Google Chrome), dispositivos de hardware (telefones, notebooks) e outros identificadores de pessoa (CRMIDs, contas de email). Isso cria uma visualização desarticulada do cliente.

Você pode resolver esses desafios com o Adobe Experience Platform Identity Service e seus recursos para:

* Gere um **gráfico de identidade** que vincula identidades diferentes, fornecendo uma representação visual de como um cliente interage com sua marca em diferentes canais.
* Crie um gráfico para o Perfil do cliente em tempo real, que é usado para criar uma visualização abrangente do cliente ao mesclar atributos e comportamentos.
* Execute a validação e a depuração usando as várias ferramentas.

Este documento fornece uma visão geral do Serviço de identidade e como você pode usar suas funcionalidades no contexto do Experience Platform.

## Terminologia {#terminology}

Antes de mergulhar nos detalhes do Serviço de identidade, leia a tabela a seguir para obter um resumo dos termos principais:

| Termo | Definição |
| --- | --- |
| Identidade | Uma identidade são dados exclusivos de uma entidade. Normalmente, esse é um objeto do mundo real, como uma pessoa individual, um dispositivo de hardware ou um navegador da Web (representado por um cookie). Uma identidade totalmente qualificada consiste em dois elementos: um **namespace de identidade** e um **valor de identidade**. |
| Namespace de identidade | Um namespace de identidade é o contexto de uma determinada identidade. Por exemplo, um namespace de `Email` pode corresponder ao valor de identidade: **julien<span>@acme.com**. Da mesma forma, um namespace de `Phone` pode corresponder ao valor de identidade: `555-555-1234`. Para obter mais informações, leia a [visão geral do namespace de identidade](./features/namespaces.md). |
| Valor de identidade | Um valor de identidade é uma string que representa uma entidade do mundo real e é categorizada no Serviço de identidade por meio de um namespace. Por exemplo, o valor de identidade (cadeia de caracteres) **julien<span>@acme.com** pode ser categorizado como um namespace `Email`. |
| Tipo de identidade | Um tipo de identidade é um componente de um namespace de identidade. O tipo de identidade designa se os dados de identidade estão ou não vinculados em um gráfico de identidade. |
| Link | Um link ou um vínculo é um método para estabelecer que duas identidades diferentes representam a mesma entidade. Por exemplo, um link entre &quot;`Email` = julien<span>@acme.com&quot; e &quot;`Phone` = 555-555-1234&quot; significa que ambas as identidades representam a mesma entidade. Isso sugere que o cliente que interagiu com sua marca usando o endereço de email julien<span>@acme.com e o número de telefone 555-555-1234 é o mesmo. |
| Serviço de identidade | O Serviço de identidade é um serviço na Experience Platform que vincula (ou desvincula) identidades para manter gráficos de identidade. |
| Gráfico de identidade | O gráfico de identidade é uma coleção de identidades que representam um único cliente. Para obter mais informações, leia o manual sobre [usando o visualizador de gráficos de identidade](./features/identity-graph-viewer.md). |
| Perfil do cliente em tempo real | O Perfil do cliente em tempo real é um serviço na Adobe Experience Platform que: <ul><li>Mescla fragmentos de perfis para criar um perfil, com base em um gráfico de identidade.</li><li>Segmenta perfis para que eles possam ser enviados ao destino para ativações.</li></ul> |
| Perfil | Um perfil é uma representação de um sujeito, uma organização ou um indivíduo. Um perfil é composto de quatro elementos: <ul><li>Atributos: os atributos fornecem informações como nome, idade ou gênero.</li><li>Comportamento: os comportamentos fornecem informações sobre as atividades de um determinado perfil. Por exemplo, um comportamento de perfil pode informar se um determinado perfil estava &quot;procurando sandálias&quot; ou &quot;comprando camisetas&quot;.</li><li>Identidades: para um perfil mesclado, isso fornece informações de todas as identidades associadas à pessoa. As identidades podem ser classificadas em três categorias: Pessoa (CRMID, email, telefone), dispositivo (IDFA, GAID) e cookie (ECID, AAID).</li><li>Associações de público-alvo: os grupos aos quais o perfil pertence (usuários fiéis, usuários que vivem na Califórnia etc.)</li></ul> |

{style="table-layout:auto"}

## O que é o Serviço de identidade?

![Identificação de identidade no Experience Platform](./images/identity-service-stitching.png)

Em um contexto B2C (Business-To-Customer, empresa para cliente), os clientes interagem com sua empresa e estabelecem uma relação com sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas na infraestrutura de dados de sua organização. Qualquer cliente pode estar ativo em seus sistemas de comércio eletrônico, fidelidade e help desk. Esse mesmo cliente também pode se envolver anonimamente ou por meios autenticados em qualquer número de dispositivos diferentes.

Considere a seguinte jornada do cliente:

* Julien criou uma conta no seu site de comércio eletrônico e encomendou alguns itens no passado. Julien geralmente usa seu notebook pessoal para comprar e fazer logon em sua conta a cada momento de uso.
* No entanto, durante uma de suas visitas ao seu site, ela usa um tablet para procurar sandálias. Durante essa sessão, como ela usou um dispositivo diferente, ela não faz logon nem faz um pedido.
* Nesse ponto, as atividades de Julien estão representadas em dois perfis separados:
   * Seu primeiro perfil é sua ID de logon de comércio eletrônico. Esse perfil é usado quando ela usa uma combinação de nome de usuário e senha para autenticar sua sessão no site de comércio eletrônico. Esse perfil é identificado por um identificador entre dispositivos.
   * Seu segundo perfil é o tablet dela. Esse perfil foi criado depois que ela navega em seu site de comércio eletrônico de forma anônima usando um tablet sem fazer logon em sua conta. Este perfil é identificado por um identificador de cookie.
* Mais tarde, Julien retoma sua sessão de tablet. No entanto, dessa vez, ela faz logon em sua conta. Como resultado, o Serviço de identidade agora relaciona a atividade do dispositivo tablet de Julien com sua ID de logon de comércio eletrônico.
* A partir de agora, seu conteúdo direcionado poderá refletir o perfil completo, o histórico de compras e a atividade de navegação anônima da Julien.

>[!IMPORTANT]
>
>Você pode usar o Serviço de identidade para vincular identidades e reunir uma imagem completa do cliente que, de outra forma, poderia estar espalhada por diferentes sistemas.

## O que o Serviço de identidade faz?

O Serviço de identidade fornece as seguintes operações para atingir sua missão:

* Crie namespaces personalizados para atender às necessidades da sua organização.
* Criar, atualizar e exibir gráficos de identidade.
* Excluir identidades com base em conjuntos de dados.
* Exclua identidades para garantir a conformidade regulamentar.

## Como o Serviço de identidade vincula identidades

>[!IMPORTANT]
>
>O Serviço de identidade diferencia maiúsculas e minúsculas. Por exemplo, **abc<span>@gmail.com** e **ABC<span>@GMAIL.COM** seriam tratados como duas identidades de email separadas.

Um link entre duas identidades é estabelecido quando o namespace de identidade e os valores de identidade são correspondentes.

Um evento de logon típico **envia duas identidades** para o Experience Platform:

* O identificador de pessoa (como uma CRMID) que representa um usuário autenticado.
* O identificador do navegador (como uma ECID) que representa o navegador da Web.

Considere o exemplo a seguir:

* Você faz logon com sua combinação de nome de usuário e senha em um site de comércio eletrônico usando seu laptop. Esse evento qualifica você como um usuário autenticado, portanto, o Serviço de identidade reconhece seu CRMID.
* O uso de um navegador para acessar o site de comércio eletrônico também é reconhecido pelo Serviço de identidade como um evento. Esse evento é representado no Serviço de identidade por meio de uma ECID.
* Em segundo plano, o Serviço de Identidade processa os dois eventos como: `CRM_ID:ABC, ECID:123`.
   * CRMID: ABC é o namespace e o valor que representam você, como um usuário autenticado.
   * ECID: 123 é o namespace e o valor que representam o uso do navegador da Web em seu laptop.
* Em seguida, se você fizer logon com as mesmas credenciais no mesmo site de comércio eletrônico, mas usar o navegador da Web no telefone em vez do navegador da Web no laptop, uma nova ECID será registrada no Serviço de identidade.
* Em segundo plano, o Serviço de Identidade processa esse novo evento como `{CRM_ID:ABC, ECID:456}`, em que CRM_ID: ABC representa sua ID de cliente autenticada e ECID:456 representa o navegador da Web em seu dispositivo móvel.

Considerando os cenários acima, o Serviço de Identidade estabelece um vínculo entre `{CRM_ID:ABC, ECID:123}` e `{CRM_ID:ABC, ECID:456}`. Isso resulta em um gráfico de identidade em que você &quot;é proprietário&quot; de três identidades: uma para identificador de pessoa (CRMID) e duas para identificadores de cookie (ECIDs).

Para obter mais informações, leia o manual no [como o Serviço de Identidade vincula as identidades](./features/identity-linking-logic.md).

## Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, que permite visualizar e entender melhor quais identidades de clientes são unidas e como. Leia o tutorial sobre [usando o visualizador de gráficos de identidade](./features/identity-graph-viewer.md) para obter mais informações.

O vídeo a seguir tem como objetivo fornecer suporte à sua compreensão de identidades e gráficos de identidade.

>[!VIDEO](https://video.tv.adobe.com/v/3422776?quality=12&learn=on&captions=por_br)

## Noções básicas sobre a função do serviço de identidade na infraestrutura da Experience Platform

O Serviço de identidade desempenha um papel vital na Experience Platform. Algumas dessas integrações principais incluem o seguinte:

* [Esquemas](../xdm/home.md): em um determinado esquema, os campos de esquema marcados como identidade permitem a criação de gráficos de identidade.
* [Conjuntos de dados](../catalog/datasets/overview.md): quando um conjunto de dados é habilitado para assimilação no Perfil do cliente em tempo real, os gráficos de identidade são gerados a partir do conjunto de dados, visto que o conjunto de dados tem pelo menos dois campos marcados como identidade.
* [Web SDK](../web-sdk/home.md): o Web SDK envia eventos de experiência para o Adobe Experience Platform e o Serviço de Identidade gera um gráfico quando existem duas ou mais identidades no evento.
* [Perfil de cliente em tempo real](../profile/home.md): antes que os atributos e eventos de um determinado perfil sejam mesclados, o Perfil de cliente em tempo real pode fazer referência ao gráfico de identidade. Para obter mais informações, leia o manual sobre [noções básicas sobre a relação entre o Serviço de Identidade e o Perfil de Cliente em Tempo Real](./identity-and-profile.md).
* [Destinos](../destinations/home.md): os destinos podem enviar informações de perfil para outros sistemas com base em um namespace de identidade, como email com hash.
* [Correspondência de segmentos](../segmentation/ui/segment-match/overview.md): a Correspondência de segmentos corresponde a dois perfis em duas sandboxes diferentes que têm o mesmo namespace de identidade e valor de identidade.
* [Privacy Service](../privacy-service/home.md): se a solicitação de exclusão incluir `identity`, a combinação de namespace e valor de identidade especificada poderá ser excluída do Serviço de Identidade usando o recurso de processamento de solicitação de privacidade no Privacy Service.

