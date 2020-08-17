---
keywords: RTCDP;rtcdp
title: Introdução à Plataforma de dados do cliente em tempo real Adobe
seo-title: Introdução à Plataforma de dados do cliente em tempo real Adobe
description: Exemplo de cenário para a Plataforma de dados do cliente em tempo real do Adobe
seo-description: Exemplo de cenário para a Plataforma de dados do cliente em tempo real do Adobe
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 0%

---


# Introdução à Plataforma de dados do cliente em tempo real Adobe

Este guia de introdução o orienta por uma implementação de amostra da Plataforma de dados do cliente em tempo real (CDP em tempo real) do Adobe. Você pode usá-la como exemplo ao configurar sua própria implementação. Embora este guia mostre exemplos específicos, ele vincula a informações adicionais que podem ser usadas ao criar sua configuração.

Este exemplo mostra o poder do Adobe Real-time Customer Data Platform, capacitado pela Adobe Experience Platform, de:

* Obter dados de várias fontes
* Mesclar em um único [!DNL real-time customer profile]
* Ofereça uma experiência consistente, relevante e personalizada em todos os dispositivos.

## Caso de uso

Luma, uma empresa de vestuário atlético, está sempre tentando melhorar a experiência do cliente. Eles têm uma nova iniciativa para aumentar as vendas relacionadas a ofertas. Eles também querem reduzir a exposição excessiva, como anúncios irritantes que acompanham os clientes.

Atualmente, eles estão gastando muito em mídia que redireciona itens que o visitante não vai comprar para frente. Por exemplo, a Luma não deseja redirecionar alguém com um item que foi planejado como uma compra única para outra pessoa.

Atualmente, os dados do Luma são dispersos por várias fontes. Como resultado, enfrentam desafios significativos:

* A organização de marketing deve trabalhar com várias equipes proprietárias de uma fonte de dados, incluindo um site, aplicativo móvel, sistemas de fidelidade, CRM e assim por diante.
* Quando a equipe de marketing recebe acesso aos dados, eles geralmente são obsoletos e não são mais relevantes para sua campanha que leva em consideração o tempo.
* Eles precisam unificar os dados para que eles públicos alvos uma pessoa, não canais.

Como resultado, a Luma tem os seguintes objetivos de negócios:

* Crie uma visualização única em tempo real de seus consumidores a partir de suas diferentes fontes de dados.
* Personalize campanhas de marketing com mensagens relevantes em diferentes canais e dispositivos.

Para atingir essas metas, a equipe de marketing precisa ser capaz de gerenciar os dados do cliente em escala.

Com a CDP em tempo real, capacitada pela Adobe Experience Platform, a organização de marketing da Luma pode:

1. Colete dados de plataformas diferentes e certifique-se de que estejam disponíveis no downstream para outras atividades de marketing.
1. Crie uma única visualização em tempo real dos seus consumidores, independentemente de onde os dados se originam.
1. Conduza uma experiência consistente, relevante e personalizada em todos os pontos de contato.

## Etapas

Este tutorial inclui as seguintes etapas:

1. Crie o perfil [do](#customer-profile)cliente.
1. [Personalize](#personalizing-the-user-experience) a experiência do usuário.
1. Use [várias fontes](#using-multiple-data-sources)de dados.
1. [Configure uma fonte](#configuring-a-data-source)de dados.
1. [Colete os dados](#bringing-the-data-together-for-a-specific-customer) para um cliente específico.
1. Configurar [segmentos](#segments).
1. Configurar [destinos](#destinations).
1. [Encaixe o perfil nos dispositivos](#cross-device-identity-stitching).
1. [Analise o perfil](#analyzing-the-profile).

## Perfil do cliente

Quando os clientes visitam site pela primeira vez, você não sabe nada sobre eles.

![imagem](assets/luma-site.png)

À medida que navegam, os dados são capturados em tempo real e enviados não apenas para um conjunto de relatórios no Adobe Analytics, mas também diretamente para a Adobe Experience Platform. À medida que os dados são coletados, você começa a formar uma única visualização do consumidor, com base nos dados comportamentais em [!DNL Experience Platform's real-time customer profile].

Muitos visitantes ao website são provavelmente clientes recorrentes que já compraram anteriormente da Luma.  É importante que o Luma personalize as mensagens e ofertas para tratar de visitantes novos e repetidos, bem como clientes conhecidos.

### Primeira visita do novo cliente

Por exemplo, um visitante não identificado navega até a seção Men’s (Masculino) no site Luma, e visualização alguns camisas de camisa correndo.

![imagem](assets/luma-sweatshirts.png)

À medida que o cliente clica para saber mais sobre esses produtos, essas visualizações de produtos são coletadas na Adobe Analytics e enviadas para [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma pode mapear o comportamento do visitante para um perfil do usuário no Adobe Experience Platform e começar a montar uma visualização mais rica do comportamento do consumidor.

### Obter uma visualização mais detalhada do cliente

À medida que o cliente continua a interagir com o site, uma imagem mais clara surge. Por exemplo, suponha que o visitante adicione um produto ao carrinho de compras e faça logon.

Quando o cliente entra, ela se identifica como Sarah Rose.

![imagem](assets/luma-login.png)

Duas identidades são unidas:

* Os dados de navegação anônimos
* Os dados existentes associados à conta de Sarah Rose

Ambas as identidades são combinadas em um único perfil em [!DNL Experience Platform]. Luma agora tem uma visualização unificada desse consumidor.

Com base no comportamento de navegação do visitante anônimo na seção Men&#39;s do site, pode ter sido considerado que o cliente era um homem. Agora que ela está conectada, Luma reconhece Sarah Rose. Luma usa o poder do [!DNL Real-time Customer Profile] para refinar as mensagens enviadas a ela através dos canais.

## Personalização da experiência do usuário

Sarah é recebida com uma mensagem de lealdade e agradecida por ser uma membro do Bronze com mais informações sobre benefícios e como aumentar seu status e pontos.

Ela clica no home page para procurar mais um pouco.

![imagem](assets/luma-personal.png)

Sarah recebe uma experiência personalizada de home page que é dinamicamente entregue, com base nela [!DNL Real-time Customer Profile] no Adobe Experience Platform.

Ela vê conteúdo relevante, graças à personalização da Adobe Sensei na Adobe Target, que leva em conta suas compras passadas e afinidade para roupas e equipamentos. Luma também adapta o conteúdo do catálogo masculino em direção ao equipamento de corrida para homens, com base em sua navegação mais recente.

Mais adiante, Sarah é mostrada como produtos em destaque, bem como uma nova bandeja de recomendações com base em seus itens visualizados mais recentemente.

Este conteúdo personalizado ajuda a Sarah a encontrar rapidamente itens relevantes. Isso aumenta as conversões e proporciona uma experiência mais agradável ao cliente.

### Devolvendo o cliente

Sarah se distrai e deixa o site, terminando sua sessão. Luma pode usar seus dados no Adobe Experience Platform para ajudar a trazê-la de volta ao site.

A Plataforma de dados do cliente em tempo real Adobe, capacitada pela Adobe Experience Platform, foi criada para o gerenciamento da experiência do cliente. Ela permite que as organizações:

* Simplificar a integração e a ativação de dados
* Governar o uso de dados conhecidos e desconhecidos
* Acelere os casos de uso de marketing em escala

## Uso de várias fontes de dados

A equipe da Luma tem todos os dados comportamentais e do cliente em um único lugar.

![imagem](assets/luma-dash.png)

Eles podem assimilar dados de todas as seguintes fontes:

* Dados de soluções Adobe Experience Cloud existentes
* Fontes não-Adobe, como o programa de fidelidade da Luma, a central de atendimento e os dados do sistema de ponto de venda
* Dados de streaming em tempo real de fontes de dados Luma
* Dados em tempo real das soluções de Adobe (nenhuma nova tag necessária)

Todos esses dados de fontes diferentes são mesclados em um único perfil unificado do cliente.

## Configurar uma fonte de dados

Use [!DNL Real-time Customer Data Platform] para trazer novas fontes de dados para a plataforma. A CDP em tempo real inclui um catálogo de fontes de dados que podem ser adicionadas ao perfil em apenas alguns cliques.

![imagem](assets/luma-source-cat.png)

Por exemplo, para assimilar os dados do CRM da Luma, filtre o catálogo por *CRM* e todos os conectores prontos contendo *CRM* serão listados. Para adicionar [!DNL Microsoft Dynamics CRM] dados:

1. Autorize a conexão.

   ![imagem](assets/luma-source-auth.png)

1. Escolha o que deseja importar de uma lista recomendada de tabelas pré-mapeadas XDM.

   <!--    ![image](assets/luma-source-import.png) -->

   Por exemplo, selecione **[!UICONTROL Contatos]**. Uma pré-visualização dos dados de contatos é carregada automaticamente para que você possa garantir que tudo tenha a aparência esperada.

   A plataforma Adobe Experience retira muito do trabalho manual desse processo mapeando automaticamente os campos padrão para o schema do perfil [!DNL Experience Data Model] (XDM).

1. Revise os mapeamentos de campo.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Por exemplo, o duplo verifica se o campo de email para contatos está mapeado corretamente.\
   Você tem a opção de pré-visualização os dados e executar o mapeamento avançado.

1. Defina um agendamento.

   ![imagem](assets/luma-source-sched.png)

Está feito. Você acabou de adicionar [!DNL Microsoft CRM] como uma fonte de dados no [!DNL Experience Platform].

### Rotular dados ingeridos para políticas de uso

O Luma tem muitas políticas internas que restringem o uso de certos tipos de informações coletadas e também devem estar em conformidade com as preocupações legais e de privacidade relacionadas ao uso de dados. Usando o Adobe Experience Platform [!DNL Data Governance], rótulos de uso de dados predefinidos podem ser aplicados a conjuntos de dados (e campos específicos nesses conjuntos de dados), permitindo que o Luma categorize seus dados de acordo com restrições específicas de uso.

![](assets/governance-labels.png)

Depois que os rótulos de uso de dados forem aplicados, o Luma poderá então usar [!DNL Data Governance] para criar políticas de uso de dados. As políticas de uso de dados são regras que descrevem os tipos de ações que você pode executar em dados que contêm determinados rótulos. Ao tentar executar uma ação em CDP em tempo real que constitui uma violação de política, a ação é impedida e um alerta é fornecido para mostrar qual política foi violada e por que.

## Reunindo os dados para um cliente específico

Neste cenário, procure perfis para Sarah Rose. Sua perfil aparece, com o e-mail que ela costumava acessar.

<!-- ![image](assets/luma-find-profile.png) -->

Todas as informações do perfil que Luma tem sobre a Sarah. Isso inclui suas informações pessoais, como endereço e número de telefone, preferências de comunicação e os segmentos para os quais ela se qualifica.

| Categoria | Descrição |
|---|---|
| Identidades | Mostra as identidades que foram unidas nas interações [!DNL Platform] de Sarah com Luma através de canais e dispositivos. Seu ECID do site é exibido. Sua identidade também inclui a ECID de seu aplicativo móvel, sua ID de email, uma ID CRM do conjunto de dados recém-adicionado e uma ID de fidelidade passada para a Adobe Experience Platform pelo sistema de fidelidade Luma. [!DNL Microsoft Dynamics] |
| Eventos | Mostra todos os dados de interação da Sarah com a marca Luma. Isto inclui o item que ela acabou de ver, qualquer coisa que ela tenha visto no passado, os emails que ela recebeu, suas interações com a central de atendimento, e o canal e o dispositivo em que cada uma dessas interações aconteceram. |

O perfil CDP em tempo real reduz o fluxo de trabalho da equipe de marketing da Luma de semanas para minutos e desbloqueia possibilidades de personalização com base nessa visualização de 360 graus do cliente. A perfil combina os dados comportamentais de quando ela navegou no site antes de entrar, com seu perfil de cliente existente, criando uma visualização abrangente da Sarah.

A equipe de marketing pode usar isso aprimorado, [!DNL Real-time Customer Profile] para personalizar melhor a experiência de Sarah e aumentar a fidelidade de sua marca com a Luma.

## Segmentos

Os poderosos recursos de segmentação do Adobe Experience Platform permitem que os profissionais de marketing combinem atributos, eventos e segmentos existentes, com base nos dados capturados no [!DNL Real-time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

Neste cenário, as recentes interações de Sarah no site exibem um comportamento diferente de suas ações passadas. Ela geralmente compra roupas femininas. No entanto, o item no carrinho dela é uma camisola grande para homens.

A equipe da Luma de Ciência dos Dados criou modelos em torno da propensão a comprar. Um modelo identifica uma alteração súbita na categoria de vestuário (como homens/mulheres) ou na dimensão do consumidor existente. A mudança de comportamento de compra de Sarah sugere que ela não está fazendo compras para si mesma.

<!-- ![image](assets/luma-gift.png) -->

### Definição de um segmento

Modifique ou crie um segmento que represente os abandonadores de carrinho que parecem estar no processo de comprar um presente:

```
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

Como Sarah adicionou um aparente item de presente no carrinho e o abandonou, Luma pode público alvo-la com uma oferta grátis.

## Destinos

Quando você adiciona o segmento &quot;Presente Doando Abandonadores de Carrinho&quot;, você pode ver aproximadamente quantas pessoas fazem parte desse segmento. É possível executar ações e disponibilizá-las para personalização em todos os canais.

Clique em **[!UICONTROL Enviar para destinos]**.

Na CDP em tempo real do Adobe, a Luma pode agir perfeitamente em seus segmentos de audiência para personalização.\
Aqui vemos todos os destinos disponíveis para o Luma para enviar este destino, tanto soluções Adobe quanto não-Adobe:

![imagem](assets/luma-dest.png)

### Seleção de destinos

Nesse cenário, a Luma deseja redirecionar essa audiência com personalização nesses destinos:

* Google, para exibição

   <!--* Facebook -->
* Adobe Campaign, para email

<!-- ![image](assets/luma-sched-dest.png) -->

### Programação de destinos

Você também pode programar o segmento para start ou término em um horário específico. O segmento será publicado e atualizado automaticamente nas plataformas configuradas nas datas programadas.

>[!NOTE]
>Como opção, se você clicar no campo de data, ele automaticamente será programado por 90 dias.

Clique em **[!UICONTROL Salvar]** para ir para a próxima página.

Quando um cliente nesta audiência efetua uma compra, sua associação a essa audiência é suprimida em tempo real. Eles não se qualificam mais porque seu status mudou.

Isso economiza centenas de milhares de dólares para o diretor da equipe de mídia Luma, não usando o inventário para uma audiência que não é qualificada.

### Impondo políticas de uso de dados para destinos

A Adobe Experience Platform inclui controles de privacidade e segurança para determinar se um segmento está disponível para ser ativado para um destino específico. A ativação é ativada ou restrita com base na(s) finalidade(ões) de marketing atribuída(s) ao destino quando foi criada, bem como nas políticas de uso de dados definidas pela organização.

Se sua atividade violar a política, um aviso será exibido. Este aviso contém informações de linhagem de dados que podem ajudá-lo a identificar por que a política foi violada e o que você pode fazer para resolver a violação.

Com esses controles, [!DNL Experience Platform] ajuda o Luma a cumprir regulamentos e comercializar de forma responsável. Esses controles são flexíveis e podem ser modificados para atender aos requisitos das equipes Luma de segurança e controle, permitindo que elas atendam com confiança aos requisitos regionais e organizacionais para gerenciar dados conhecidos e desconhecidos do cliente.

### Tela de fluxo de dados

Quando você salva, uma tela de fluxo de dados visual mostra o segmento mapeado do perfil unificado para os três destinos selecionados.

![imagem](assets/luma-flow.png)

## Correção de identidade entre dispositivos

Sarah navega em um site de mídia social em seu dispositivo móvel, e ela vê um anúncio Luma. Ela lembra o item que ela deixou no carrinho.

Mais tarde, ela abre seu e-mail e vê os e-mails redirecionados. Ela clica em um link para a Luma por e-mail.

O link leva Sarah à página inicial do Luma móvel, onde ela vê uma experiência altamente personalizada da Adobe Target.

* Ela é bem-vinda como membro do Bronze.
* Ela vê a mensagem do &quot;Presente&quot;.
* Ela também vê a mensagem &quot;Free Gift Wrap&quot;, que faz parte dos benefícios da associação ao Bronze.
* Ela ainda é alvo da imagem do herói com base na sua afinidade de correr.

Ela compra o suéter, adiciona papel de presente e escreve uma nota de presente. Ela também tem a opção de se lembrar desse evento e receber um lembrete no próximo ano para ganhar um presente neste momento. Ela diz que sim, e está agendada para uma campanha de email no ano seguinte para lembrá-la de comprar outro presente.

Graças às capacidades de supressão de audiências, Sarah não será alvejada com o suéter daquele homem avançando.

## Analisando o perfil

Os profissionais de marketing luma usam a Adobe Experience Platform para observar o segmento de fornecedores de presentes no Painel CDP em tempo real. Eles visualizações os resultados dessa iniciativa ao longo do tempo e veem que ela está crescendo. Os clientes estão respondendo às ofertas e gastando mais dinheiro.

Esses insights permitem que os profissionais de marketing ajam nesse sinal, que foi alimentado por ter esses dados disponíveis no CDP e ter clientes como Sarah conectados ao segmento.

A Luma usa esses dados de CDP para estimular maior fidelidade e satisfação do cliente.
