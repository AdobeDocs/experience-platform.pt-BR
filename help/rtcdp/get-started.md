---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Introdução ao Real-Time Customer Data Platform
description: Use esse modelo de cenário como exemplo ao configurar sua implementação da Adobe Real-Time Customer Data Platform.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 1%

---

# Introdução ao Real-Time Customer Data Platform

Este guia de introdução orienta você em uma amostra de implementação do Real-Time Customer Data Platform (Real-Time CDP). Você pode usá-lo como exemplo ao configurar sua própria implementação do. Embora este guia mostre exemplos específicos, ele vincula às informações adicionais que você pode usar ao criar sua configuração do.

Este exemplo mostra o poder do Real-Time Customer Data Platform, viabilizado pelo Adobe Experience Platform, em:

* Assimilar dados de várias fontes
* Mesclar em um único [!DNL real-time customer profile]
* Ofereça uma experiência consistente, relevante e personalizada em todos os dispositivos.

## Caso de uso

A Luma, uma empresa de vestuário esportivo, está sempre tentando melhorar a experiência do cliente. Eles têm uma nova iniciativa para aumentar as vendas relacionadas a presentes. Eles também querem reduzir a superexposição, como anúncios irritantes que acompanham os clientes.

Atualmente, eles estão gastando muito em mídia que redireciona contra itens que o visitante não vai comprar a partir de agora. Por exemplo, a Luma não quer redirecionar alguém com um item que foi projetado como uma compra única para outra pessoa.

Neste momento, os dados do Luma estão dispersos em várias fontes. Como resultado, enfrentam desafios significativos:

* A organização de marketing deve trabalhar com várias equipes que possuem uma fonte de dados, incluindo um site, aplicativo móvel, sistemas de fidelidade, CRM e assim por diante.
* Quando a equipe de marketing obtém acesso aos dados, eles geralmente ficam obsoletos e não são mais relevantes para sua campanha sensível ao tempo.
* Eles precisam unificar os dados para que direcionem uma pessoa, não canais.

Como resultado, a Luma tem os seguintes objetivos de negócios:

* Crie uma visualização única em tempo real de seus consumidores a partir de suas diferentes fontes de dados.
* Personalize campanhas de marketing com mensagens relevantes em diferentes canais e dispositivos.

Para atingir essas metas, a equipe de marketing precisa ser capaz de gerenciar os dados do cliente em escala.

Com o Real-Time CDP, viabilizado pela Adobe Experience Platform, a organização de marketing da Luma pode:

1. Colete dados de plataformas diferentes e verifique se estão disponíveis para downstream para outras atividades de marketing.
1. Crie uma visualização única e em tempo real dos consumidores, independentemente da origem dos dados.
1. Promover uma experiência consistente, relevante e personalizada em todos os pontos de contato.

## Etapas

Este tutorial inclui as seguintes etapas:

1. Crie o [perfil de cliente](#customer-profile).
1. [Personalize](#personalizing-the-user-experience) a experiência do usuário.
1. Use [várias fontes de dados](#using-multiple-data-sources).
1. [Configurar uma fonte de dados](#configuring-a-data-source).
1. [Colete os dados](#bringing-the-data-together-for-a-specific-customer) de um cliente específico.
1. Configurar [públicos-alvo](#audiences).
1. Configurar [destinos](#destinations).
1. [Compilar o perfil entre os dispositivos](#cross-device-identity-stitching).
1. [Analisar o perfil](#analyzing-the-profile).

## Perfil do cliente

Quando os clientes visitam seu site pela primeira vez, você não sabe nada sobre eles.

![imagem](assets/luma-site.png)

À medida que navegam, os dados são capturados em tempo real e enviados não apenas para um conjunto de relatórios no Adobe Analytics, mas também diretamente para o Adobe Experience Platform. Conforme os dados são coletados, você começa a formar uma única visualização do consumidor, com base nos dados comportamentais em [!DNL Experience Platform's real-time customer profile].

Muitos visitantes do site provavelmente são clientes recorrentes que compraram anteriormente da Luma.  É importante para a Luma personalizar mensagens e ofertas para direcionar visitantes novos e repetidos, bem como clientes conhecidos.

### Primeira visita de um novo cliente

Por exemplo, um visitante não identificado navega até a seção Masculino no site Luma e visualiza um casal que usa moletons.

![imagem](assets/luma-sweatshirts.png)

À medida que o cliente navega para saber mais sobre esses produtos, essas exibições de produtos são coletadas no Adobe Analytics e enviadas para [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

O Luma pode mapear o comportamento do visitante para um perfil de usuário no Adobe Experience Platform e começar a reunir uma visualização mais avançada do comportamento desse consumidor.

### Obter uma visão mais detalhada do cliente

À medida que o cliente continua a interagir com o site, surge uma imagem mais clara. Por exemplo, suponha que o visitante adicione um produto ao carrinho de compras e faça logon.

Quando o cliente faz logon, ela se identifica como Sarah Rose.

![imagem](assets/luma-login.png)

Duas identidades são mescladas:

* Os dados de navegação anônimos
* Os dados existentes associados com a conta de Sarah Rose

Ambas as identidades estão combinadas em um único perfil em [!DNL Experience Platform]. A Luma agora tem uma visão unificada desse consumidor.

Com base no comportamento de navegação do visitante anônimo na seção masculina do site, pode ter sido presumido que o cliente era um homem. Agora que ela está logada, Luma reconhece Sarah Rose. Luma usa o poder da [!DNL Real-Time Customer Profile] para refinar as mensagens entregues a ela entre canais.

## Personalização da experiência do usuário

Sarah é recebida com uma mensagem de fidelidade e agradecida por ser uma integrante do Bronze com mais informações sobre os benefícios e como aumentar seu status e pontos.

Ela navega até a página inicial para navegar mais um pouco.

![imagem](assets/luma-personal.png)

Sarah recebe uma experiência personalizada de página inicial que é entregue dinamicamente, com base em sua [!DNL Real-Time Customer Profile] no Adobe Experience Platform.

Ela vê conteúdo relevante, graças à personalização baseada no Adobe Sensei no Adobe Target, que leva em conta suas compras anteriores e afinidade com a execução de roupas e equipamentos. Luma também adapta o conteúdo do catálogo masculino em direção a equipamentos de corrida para homens com base em seu navegador mais recente.

Mais abaixo na página, Sarah é mostrada em produtos em destaque, bem como uma nova bandeja de recomendações com base em seus itens visualizados mais recentemente.

Esse conteúdo personalizado ajuda Sarah a encontrar itens relevantes rapidamente. Isso aumenta as conversões e fornece uma experiência do cliente mais agradável.

### Retornando o cliente

Sarah se distrai e deixa o local, encerrando sua sessão. Luma pode usar seus dados no Adobe Experience Platform para ajudá-la a voltar ao site.

O Real-Time Customer Data Platform, desenvolvido pela Adobe Experience Platform, foi desenvolvido para o gerenciamento da experiência do cliente. Ele permite que as organizações:

* Simplificar a integração e a ativação de dados
* Controlar o uso de dados conhecidos e desconhecidos
* Acelere os casos de uso de marketing em escala

## Uso de múltiplas fontes de dados

A equipe da Luma tem todos os seus dados comportamentais e de clientes em um único local.

![imagem](assets/luma-dash.png)

Eles podem assimilar dados de todas as seguintes fontes:

* Dados existentes das soluções da Adobe Experience Cloud
* Fontes que não são da Adobe, como o programa de fidelidade da Luma, a central de atendimento e os dados do sistema de ponto de venda
* Dados de transmissão em tempo real de fontes de dados da Luma
* Dados em tempo real das soluções da Adobe (não são necessárias novas tags)

Todos esses dados de fontes diferentes são mesclados em um único perfil de cliente unificado.

## Configurar uma fonte de dados

Use o [!DNL Real-Time Customer Data Platform] para trazer novas fontes de dados para a Experience Platform. O Real-Time CDP inclui um catálogo de fontes de dados que podem ser adicionadas ao perfil de maneira rápida e fácil.

![imagem](assets/luma-source-cat.png)

Por exemplo, para assimilar os dados do CRM da Luma, filtre o catálogo pelo *CRM* e todos os conectores prontos para uso que contêm *CRM* serão listados. Para adicionar dados do [!DNL Microsoft Dynamics CRM]:

1. Autorizar a conexão.

   ![imagem](assets/luma-source-auth.png)

1. Escolha o que deseja importar de uma lista recomendada de tabelas pré-mapeadas XDM.

   <!--    ![image](assets/luma-source-import.png) -->

   Por exemplo, selecione **[!UICONTROL Contacts]**. Uma visualização dos dados de contatos é carregada automaticamente para que você possa verificar se tudo está conforme esperado.

   A Real-Time CDP tira muito do trabalho manual desse processo, mapeando automaticamente campos padrão para o esquema de perfil [!DNL Experience Data Model] (XDM).

1. Revise os mapeamentos de campo.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Por exemplo, verifique se o campo de email dos contatos está mapeado corretamente.\
   Você tem a opção de pré-visualizar os dados e executar o mapeamento avançado.

1. Defina uma programação.

   ![imagem](assets/luma-source-sched.png)

Está feito. Você acabou de adicionar [!DNL Microsoft CRM] como fonte de dados em [!DNL Experience Platform].

### Rotular dados assimilados para políticas de uso

A Luma tem muitas políticas internas que restringem o uso de determinados tipos de informações coletadas e também deve estar em conformidade com as preocupações legais e de privacidade relacionadas ao uso de dados. Usando a Governança de dados da Adobe Experience Platform, os rótulos de uso de dados predefinidos podem ser aplicados a conjuntos de dados (e campos específicos dentro desses conjuntos de dados), permitindo que a Luma categorize seus dados de acordo com restrições de uso específicas.

![](assets/governance-labels.png)

Depois que os rótulos de uso de dados forem aplicados, a Luma poderá usar a Governança de dados para criar políticas de uso de dados. As políticas de uso de dados são regras que descrevem os tipos de ações que você tem permissão para executar em dados que contêm determinados rótulos. Ao tentar executar uma ação no Real-Time CDP que constitui uma violação de política, a ação é impedida e um alerta é fornecido para mostrar qual política foi violada e por quê.

Além disso, a Real-Time CDP

## Reunindo os dados para um cliente específico

Neste cenário, procure perfis para Sarah Rose. O perfil dela aparece, com o email que ela usou para fazer logon.

<!-- ![image](assets/luma-find-profile.png) -->

Todas as informações de perfil que a Luma tem sobre as exibições de Sarah. Isso inclui suas informações pessoais, como endereço e número de telefone, preferências de comunicação e os públicos para os quais ela se qualifica.

| Categoria | Descrição |
|---|---|
| Identidades | Mostra as identidades que foram vinculadas em [!DNL Experience Platform] a partir das interações de Sarah com a Luma em canais e dispositivos. Sua ECID do site é exibida. Sua identidade também inclui a ECID de seu aplicativo móvel, sua ID de email, uma ID de CRM do conjunto de dados [!DNL Microsoft Dynamics] adicionado recentemente e uma ID de fidelidade passada para o Adobe Experience Platform pelo sistema de fidelidade Luma. |
| Eventos | Mostra todos os dados de interação de Sarah com a marca Luma. Isso inclui o item que ela acabou de ver, qualquer coisa que ela viu no passado, os emails que recebeu, suas interações com a central de atendimento e em que canal e dispositivo cada uma dessas interações aconteceu. |

O perfil do Real-Time CDP reduz o fluxo de trabalho da equipe de marketing da Luma de semanas para minutos e desbloqueia possibilidades de personalização com base nessa visualização de 360 graus do cliente. O perfil mescla os dados comportamentais de quando ela navegou no site antes de entrar, com seu perfil de cliente existente, criando uma visualização abrangente de Sarah.

A equipe de marketing pode usar este [!DNL Real-Time Customer Profile] aprimorado para personalizar melhor a experiência de Sarah e aumentar sua fidelidade à marca com a Luma.

## Públicos-alvo

Os poderosos recursos de segmentação do Adobe Experience Platform permitem que os profissionais de marketing combinem atributos, eventos e públicos existentes, com base nos dados capturados no [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

Neste cenário, as interações recentes de Sarah no site exibem um comportamento diferente de suas ações anteriores. Ela geralmente compra roupas femininas. No entanto, o item em seu carrinho é uma camiseta grande masculina.

A equipe de ciência de dados da Luma criou modelos em torno da propensão para comprar. Um modelo identifica uma mudança repentina na categoria do vestuário (como homens/mulheres) ou no tamanho para o consumidor existente. A mudança no comportamento de compra de Sarah sugere que ela não está fazendo compras para si mesma.

<!-- ![image](assets/luma-gift.png) -->

### Definir um público

Use as várias opções de composição visual ou editor de expressão baseado em código no espaço de trabalho de públicos-alvo para modificar ou criar um público-alvo que represente os abandonadores de carrinho que parecem estar no processo de compra de um presente:

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Como Sarah adicionou um item de presente aparente no carrinho e o abandonou, Luma pode direcioná-la com uma oferta de wrap de presente gratuito.

## Destinos

Ao adicionar o público-alvo &quot;Abandonadores do carrinho de presente&quot;, você pode ver aproximadamente quantas pessoas fazem parte desse público-alvo. É possível executar ações nele e disponibilizá-lo para personalização em canais.

Selecione **[!UICONTROL Send to destinations]**.

No Real-Time CDP, o Luma pode atuar de forma contínua em seus públicos para personalização.\
Aqui vemos todos os destinos disponíveis para a Luma enviar esse destino para o, soluções da Adobe e não-Adobe:

![imagem](assets/luma-dest.png)

### Seleção de destinos

Neste cenário, a Luma deseja redirecionar esse público-alvo com personalização nesses destinos:

* Google, para exibição
  <!--* Facebook -->
* Adobe Campaign, para email

<!-- ![image](assets/luma-sched-dest.png) -->

### Destinos de agendamento

Você também pode agendar a exportação de público-alvo para iniciar ou encerrar em um momento específico. O público será publicado e atualizado automaticamente nas plataformas configuradas nas datas programadas.

>[!NOTE]
>
>Opcionalmente, se você selecionar o campo de data, ele agendará automaticamente 90 dias para sair.

Selecione **[!UICONTROL Save]** para ir para a próxima página.

Quando um cliente neste público-alvo faz uma compra, sua associação a este público-alvo é suprimida em tempo real. Eles não se qualificam mais porque seu status mudou.

Isso economiza centenas de milhares de dólares para o diretor da equipe de mídia da Luma ao não usar o inventário para um público que não é qualificado.

### Aplicação de políticas de uso de dados para destinos

O Adobe Experience Platform inclui controles de privacidade e segurança para determinar se um público-alvo está disponível para ser ativado para um destino específico. A ativação é ativada ou restrita com base nas finalidades de marketing atribuídas ao destino quando foi criada, bem como nas políticas de uso de dados definidas pela organização.

Se a atividade violar a política, um aviso será exibido. Este aviso contém informações de linhagem de dados que podem ajudar a identificar por que a política foi violada e o que você pode fazer para resolver a violação.

Com esses controles, o [!DNL Experience Platform] ajuda a Luma a cumprir as regulamentações e a comercializar de forma responsável. Esses controles são flexíveis e podem ser modificados para atender aos requisitos das equipes de segurança e governança da Luma, permitindo que atendam com confiança aos requisitos regionais e organizacionais para gerenciar dados conhecidos e desconhecidos do cliente.

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## Compilação de identidade entre dispositivos

Sarah navega em um site de mídia social em seu dispositivo móvel e vê um anúncio da Luma. Isso a lembra do item que ela deixou no carrinho.

Mais tarde, ela abre seu email e vê os emails redirecionados. Ela seleciona um link para a Luma a partir de um email.

O link leva Sarah para a página inicial do Luma para dispositivos móveis, onde ela vê uma experiência altamente personalizada disponibilizada pelo Adobe Target.

* Ela é bem-vinda como um membro do Bronze.
* Ela vê a mensagem do &quot;presente&quot;.
* Ela também vê a mensagem &quot;Free Gift Wrap&quot;, que faz parte de seus benefícios de adesão ao Bronze.
* Ela ainda é visada na imagem de heroína baseada em sua afinidade por correr.

Ela compra o suéter, adiciona embrulho para presente e escreve um brinde. Ela também tem a opção de lembrar-se deste evento e receber um lembrete no próximo ano para ficar em presente neste momento. Ela diz que sim e está programada para entrar em uma campanha por email no ano seguinte para lembrá-la de comprar outro presente.

Graças às capacidades de supressão de público, Sarah não será alvo com o suéter daquele homem daqui para frente.

## Análise do perfil

Os profissionais de marketing da Luma usam o Adobe Experience Platform para observar o público-alvo dos brindes no painel do Real-Time CDP. Eles veem os resultados dessa iniciativa ao longo do tempo e veem que ela está crescendo. Os clientes estão respondendo às ofertas e gastando mais dinheiro.

Esses insights permitem que os profissionais de marketing ajam nesse sinal, que foi alimentado pela disponibilização desses dados no CDP e pela anexação de clientes como Sarah ao público-alvo.

A Luma usa esses dados da CDP para impulsionar maior fidelidade e satisfação do cliente.
