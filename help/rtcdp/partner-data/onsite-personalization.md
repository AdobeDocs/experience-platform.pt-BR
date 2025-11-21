---
title: Personalizar experiências no site para visitantes desconhecidos usando o reconhecimento de visitantes auxiliados por parceiros
description: Saiba como usar o reconhecimento de visitante com auxílio de parceiros para fornecer experiências de site personalizadas para visitantes.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 72%

---

# Personalizar experiências no site para visitantes desconhecidos usando o reconhecimento de visitantes auxiliados por parceiros

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que licenciaram o Real-Time CDP (Serviço de aplicativo), Adobe Experience Platform Ativation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Leia mais sobre esses pacotes nas [descrições do produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) e entre em contato com a pessoa representante da Adobe para obter mais informações.

Saiba como usar o reconhecimento com auxílio de parceiros para fornecer experiências personalizadas a visitantes de sua propriedade na Web. Use este tutorial para entender o processo de implementação de vários elementos na Experience Platform e outras soluções da Experience Cloud, a fim de criar uma experiência personalizada para visitantes autenticados e não autenticados.

![Um infográfico que descreve como usar atributos fornecidos pelo parceiro para oferecer experiências personalizadas a visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## Por que considerar este caso de uso {#why-this-use-case}

A fragmentação das experiências digitais à medida que os consumidores interagem com as marcas de inúmeras maneiras é muito real e está se tornando cada vez mais difícil de resolver. As melhores estratégias de engajamento do cliente para experiências coesas, recomendações direcionadas e interações personalizadas são todas restritas pelo reconhecimento do usuário.

É aqui que o reconhecimento em tempo real auxiliado por parceiros pode fazer uma diferença significativa. O Adobe permite que os parceiros de identidade se conectem às nossas sofisticadas ofertas de coleta de dados no lado do cliente e otimização de experiência líder de mercado, para elevar efetivamente o padrão na entrega de experiência a partir da primeira visita, sem histórico ou autenticação anteriores.

Isso é especialmente valioso para mercados verticais que têm baixas taxas de autenticação, como Mercadorias embaladas do consumidor, varejo on-line e muito mais.

## Exemplo do setor {#industry-example}

Como exemplo, considere uma marca de materiais de construção com baixas taxas de autenticação. Essa marca gostaria de fornecer experiências personalizadas para visitantes novos, sem histórico ou autenticação anteriores e sem a dependência de cookies de terceiros.

Essa marca aproveita a tecnologia de reconhecimento de parceiros para reconhecer probabilisticamente o visitante e oferecer uma experiência mais personalizada. Isso ajuda a promover a consideração à medida que o(a) visitante se move para baixo no funil de marketing. Por exemplo, a marca pode usar sinais demográficos fornecidos pelo parceiro para conteúdos do site destinados a pessoas que se mudaram recentemente e oferecer um desconto em produtos populares do tipo “faça você mesmo”.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao planejar usar atributos fornecidos pelo parceiro para oferecer experiências personalizadas a visitantes autenticados e não autenticados, considere os seguintes pré-requisitos no processo de planejamento:

* Quais entradas são esperadas pela tecnologia de reconhecimento do seu parceiro para criar camadas de atributos adicionais?
* Até que ponto você se sente confortável em fornecer personalização em diferentes canais e para casos de uso diferentes com base em conjuntos de dados derivados probabilisticamente, em comparação com atributos confirmados deterministicamente?
* Como a experiência de visitantes pré-autenticados, mas reconhecidos, deve ser alterada durante a autenticação?

### Funcionalidade da interface do usuário, componentes do Experience Platform e produtos da Experience Cloud que você usará {#ui-functionality-and-elements}

Para implementar com sucesso esse caso de uso, você deve usar várias áreas da Real-time Customer Data Platform e outras soluções da Experience Cloud. Verifique se tem as [permissões de controle de acesso baseado em atributo](/help/access-control/abac/overview.md) necessárias para todas essas áreas, ou solicite ao(à) administrador(a) que as conceda a você.

* Coleção de dados
   * [SDK da Web da Adobe Experience Platform](/help/web-sdk/home.md)
   * [Tags](/help/tags/home.md)
   * [Sequências de dados](/help/datastreams/overview.md)
* Gerenciamento de dados na Real-Time CDP
   * [Identidades](/help/identity-service/features/namespaces.md)
   * [Esquemas](/help/xdm/home.md)
   * [Rótulos de uso de dados](/help/data-governance/labels/overview.md)
   * [Conjuntos de dados](/help/catalog/datasets/overview.md)
* Personalização de propriedade da Web
   * [Segmentação de borda](/help/segmentation/methods/edge-segmentation.md)
   * [Destinos de personalização de borda](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (ou uma plataforma de personalização de sua escolha. Este tutorial de caso de uso destaca o Adobe Target como mecanismo de personalização)

## Apresentação em vídeo {#video-walkthrough}

Assista ao tutorial em vídeo abaixo para obter uma apresentação de como personalizar experiências no site para visitantes desconhecidos:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

![Um infográfico que descreve como usar atributos fornecidos pelo parceiro para oferecer experiências personalizadas a visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Como **cliente**, você licencia do **parceiro de dados** a capacidade de obter insights em tempo real de visitantes anônimos do site.
2. Como **cliente**, você implanta bibliotecas do lado do cliente em suas propriedades para chamar APIs do **parceiro** e configura o SDK da Web ou o SDK móvel para enviar sinais fornecidos pelo parceiro para a Real-Time CDP.
3. Ao navegar no site ou aplicativo, o(a) **visitante** é probabilisticamente reconhecido(a) pelo **parceiro**, que retorna atributos juntamente com uma ID.
4. A Real-Time CDP executa a segmentação de borda para avaliar ocorrências de evento recebidas e mantém os resultados em relação ao [identificador ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).
5. O Adobe Target usa a saída da segmentação de borda para renderizar novamente a experiência para o(a) **visitante**, oferecendo uma personalização da sessão.
6. O evento é mantido em sua totalidade para fluxos de trabalho downstream, como análise e redirecionamento.

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Gerenciamento de dados: crie um namespace de identidade, esquema e conjunto de dados para gerenciar os atributos de dados {#data-management}

Como preparo para atingir o caso de uso de personalização da experiência de visitantes não autenticados, primeiro você deve configurar a estrutura de gerenciamento de dados na Real-Time CDP para receber os dados de entrada do evento em tempo real e da qualificação do público-alvo.

#### Criar namespace de identidade de ID de parceiro

Primeiro, é necessário criar um namespace de identidade de ID de parceiro. Navegue até **[!UICONTROL Customer]** > **[!UICONTROL Identities]** no painel esquerdo e selecione **[!UICONTROL Create identity namespace]** no canto superior direito da tela.

![A caixa de diálogo Criar namespace de identidade com a ID de parceiro realçada.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Leia mais sobre como [criar um namespace de identidade de ID de parceiro](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Criar um esquema

Em seguida, crie um esquema [!UICONTROL Experience Event] para manter os dados de série temporal que você coletará posteriormente de suas propriedades da Web e certifique-se de usar [!UICONTROL XDM ExperienceEvent] como classe base para o esquema. Leia sobre como [criar um esquema usando a interface da Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![O espaço de trabalho Esquemas com a opção Criar esquema e o evento de experiência do XDM destacados.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

À medida que você cria seu esquema e [adiciona grupos de campos ao esquema](/help/xdm/ui/resources/schemas.md#add-field-groups), considere adicionar os grupos de campos [Visitar página da Web](/help/xdm/field-groups/event/web-details.md) e [Mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Eles são um acréscimo a outros grupos de campos que se aplicam à sua propriedade digital e práticas de coleção de dados.

Além disso, você pode criar ou reutilizar um grupo de campos existente e adicioná-lo ao esquema para capturar insights fornecidos pelo parceiro sobre o(a) visitante. Leia como [criar um grupo de campos](/help/xdm/ui/resources/field-groups.md) e [adicionar campos](/help/xdm/ui/resources/field-groups.md) ao grupo de campos. Por exemplo, se você planeja utilizar insights fornecidos pelo parceiro na sua personalização, como faixa etária, situação profissional, poder aquisitivo mensal ou comportamentos de compra, certifique-se de que o grupo de campos inclua os campos apropriados.

Supondo que o parceiro de dados forneça um identificador estável para o(a) visitante e que você queira utilizar isso na Real-Time CDP, certifique-se de ter um campo nomeado adequadamente para o identificador em seu grupo de campos personalizados. Você também deve marcar o campo como uma identidade no namespace de identidade criado anteriormente. Lembre-se também de [habilitar a inclusão do esquema no perfil](/help/xdm/ui/resources/schemas.md#profile).

#### Criar um conjunto de dados

Em seguida, você deve criar um conjunto de dados para manter os dados de série temporal coletados dos visitantes da propriedade web e que serão usados para personalização no site.

Leia o tutorial sobre [como criar um conjunto de dados](/help/catalog/datasets/user-guide.md#create) e lembre-se de selecionar a opção de criá-lo a partir de um esquema. Crie o conjunto de dados com base no esquema criado na etapa anterior.

Semelhante à etapa ao criar um esquema, é necessário habilitar o conjunto de dados para ser incluído no [!UICONTROL Real-Time Customer Profile]. Para obter mais informações sobre como habilitar o conjunto de dados para uso no [!UICONTROL Real-Time Customer Profile], leia o [tutorial sobre criação de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementar a coleta de dados do evento na propriedade web {#implement-data-collection}

Depois de definir a configuração de gerenciamento de dados, é necessário implementar a [coleta de dados](/help/collection/home.md) de evento em tempo real na propriedade web. Você precisa instrumentar sua propriedade com a biblioteca de coleta de dados da Adobe - [!UICONTROL Web SDK] - para coletar chamadas de evento em tempo real e enviá-las de volta para a Real-Time CDP. Este item consiste em algumas tarefas separadas em alguns componentes de coleção de dados.

>[!IMPORTANT]
>
>Para recuperar atributos fornecidos pelo parceiro, você também deve *integrar sua propriedade web com APIs de parceiros ou outros métodos para chamar e recuperar atributos de parceiros de dados em tempo real*. Discuta esse aspecto com o parceiro escolhido, pois esse não é o foco deste tutorial.

Primeiro, use o alternador de aplicativos no canto superior direito da tela para navegar até a seção **[!UICONTROL Data Collection]**.

>[!TIP]
>
>Contate o administrador do sistema para solicitar acesso se não conseguir ver [!UICONTROL Data Collection] no alternador de aplicativos.

![Alternador de aplicativos para acessar a seção Coleção de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

A seção **[!UICONTROL Data Collection]** da interface do usuário é semelhante à imagem abaixo.

![Seção de coleta de dados da interface do Experience Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Criar sequência de dados

Como a primeira etapa da seção de coleção de dados, [crie uma nova sequência de dados](/help/datastreams/configure.md). A sequência de dados é a base de como os dados são coletados e roteados corretamente para o aplicativo da Adobe, neste caso, a Experience Platform.

À medida que você cria a sequência de dados, no campo **[!UICONTROL Event schema]**, selecione o esquema criado anteriormente.

![Seletor de esquema de evento realçado ao configurar uma nova sequência de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Selecione o conjunto de dados de evento](/help/datastreams/configure.md#aep) criado anteriormente na lista suspensa, marque as caixas ao lado de **[!UICONTROL Edge Segmentation]** e **[!UICONTROL Personalization Destinations]** e selecione **[!UICONTROL Save]**.

Observe que não é necessário selecionar um conjunto de dados de perfil nesse cenário, pois você está trazendo dados de série temporal com base em eventos.

#### Criar propriedade de tag

Uma propriedade é um container que você preenche com extensões, regras, elementos de dados e bibliotecas ao implantar tags no site.

Navegue até **[!UICONTROL Tags]** e selecione **[!UICONTROL New property]**.

![Crie uma nova propriedade de tag.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Preencha os campos obrigatórios e selecione **[!UICONTROL Save]**.

![Preencha os campos obrigatórios da nova propriedade.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Obtenha informações completas sobre como [criar uma propriedade de tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=pt-BR).

Em seguida, você deve instalar várias extensões na propriedade. Selecione a propriedade da tag e navegue até a seção [!UICONTROL Extensions].

![Selecione sua nova propriedade de tag.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observe que a extensão [!UICONTROL Core] já está instalada. Você deve instalar mais duas extensões, conforme detalhado nas próximas seções.

![Exibir extensões instaladas.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Instalação da extensão do SDK da Web

Observe que este tutorial orienta você a instrumentar o site com o SDK da Web. Também é possível usar o [SDK móvel](https://developer.adobe.com/client-sdks/documentation/) no aplicativo para personalizar a experiência de visitantes.

![Exibição da extensão do SDK da Web no catálogo de extensões.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Na tela para configurar o Web SDK, navegue até a seção **[!UICONTROL Datastreams]** e forneça informações sobre a sandbox da Experience Platform que você está usando. Selecione a sandbox apropriada e a sequência de dados criada em etapas anteriores na próxima lista suspensa. Você pode escolher a mesma sandbox e sequência de dados para todos os outros ambientes. Deixe as outras configurações inalteradas e selecione **[!UICONTROL Save]**.

Obtenha informações completas sobre [como instalar o SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=pt-BR).

#### Instalar extensão do serviço de ID

Use a [extensão do serviço de ID da Experience Cloud](/help/tags/extensions/client/id-service/overview.md) para criar uma identidade própria exclusiva baseada em dispositivos para visitantes em todas as soluções da Experience Cloud. Procure por **[!UICONTROL ID Service]** no catálogo de extensões e instale-o. Mantenha todas as configurações padrão ao instalar a extensão.

![Exibição da extensão do serviço de ID no catálogo de extensões.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configuração de ambientes

Em seguida, passe para a seção **[!UICONTROL Environments]** a partir da navegação à esquerda. Nesta etapa, você deve conectar seu site à rede de borda da Adobe para recuperar e fornecer informações de visitantes em tempo real.

Selecione o ícone de caixa à direita para o ambiente de desenvolvimento e copie a versão padrão do trecho de código JavaScript que aparece em uma janela modal.

![Seleção do ícone de caixa realçada na seção Ambientes da interface da coleção de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Você deve adicionar esse trecho de código na parte superior do site. Como resultado, seu site fará uma chamada para a rede de borda da Adobe para recuperar a lógica do JavaScript que será carregado e executado na página. Isso permite o funcionamento de recursos como a geração de IDs de visitante, coleta de dados e personalização de experiência em tempo real.

#### Configurar elementos de dados

Os elementos de dados são os aspectos fundamentais do seu dicionário de dados (ou mapa de dados). Um único elemento de dados é uma variável cujo valor pode ser mapeado para consultar strings, URLs, valores de cookie, variáveis JavaScript e assim por diante. Leia mais sobre [elementos de dados](/help/tags/ui/managing-resources/data-elements.md).

Para o propósito deste caso de uso, você deve configurar dois elementos de dados.

Primeiro, configure um elemento `partnerData`. Navegue até a seção **[!UICONTROL Data Elements]** e selecione **[!UICONTROL Create New Data Element]**.

![Crie um novo elemento de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Nomeie o elemento de dados `partnerData`, deixe o valor [!UICONTROL extension] como [!UICONTROL Core] e defina **[!UICONTROL Data Element Type]** como **[!UICONTROL JavaScript Variable]**. Digite `partnerData` no campo intitulado **[!UICONTROL JavaScript variable name]** e selecione **[!UICONTROL Save]**.

![Realce das opções para configurar corretamente o elemento de dados partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Para configurar o segundo elemento de dados, nomeie a nova variável `pageVisit`, defina o **[!UICONTROL Extension]** como **[!UICONTROL Adobe Experience Platform]** e escolha **[!UICONTROL XDM Object]** como o tipo de dados.

![Seleções realçadas para configurar corretamente o elemento de dados pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

No esquema, selecione os atributos de terceiros que correspondem aos valores que você espera do parceiro de dados. Em seguida, selecione o botão de opção intitulado **[!UICONTROL Provide entire object]**. Selecione o ícone semelhante a um banco de dados e escolha o elemento de dados `partnerData` criado anteriormente.

#### Configuração de regras

Na seção **[!UICONTROL Rules]**, você pode configurar o site para enviar uma solicitação de personalização ao Adobe com os atributos carregados nos elementos de dados que você acabou de criar. Leia mais sobre a [criação de regras](/help/tags/ui/managing-resources/rules.md).

Selecione **[!UICONTROL Create new Rule]**. Nomeie esta regra **[!UICONTROL Personalize]** e selecione o sinal + ao lado de **[!UICONTROL Events]**. Selecione **[!UICONTROL Page Bottom]** como evento e salve.

![Seleções para o tipo de evento de uma regra.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Selecione o sinal + ao lado de **[!UICONTROL Actions]**. Atualize a extensão para **[!UICONTROL Adobe Experience Platform Web SDK]** e defina **[!UICONTROL Action Type]** como **[!UICONTROL Send event]**.

![Seleções para o tipo de ação de uma regra.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

No seletor suspenso **[!UICONTROL Type]** à direita, selecione `web.webpagedetails.pageViews` como o tipo de evento.

![Selecione o tipo de evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Clique no ícone de banco de dados ao lado dos dados do XDM e selecione o elemento de dados `pageVisit`.

Role para baixo na lista de configurações de Ação e certifique-se de marcar a caixa denominada **[!UICONTROL Render visual personalization decisions]**. Isso é importante para permitir que as experiências entregues por meio do Adobe Target ou outros produtos semelhantes sejam renderizadas visualmente na página web. Selecione **[!UICONTROL Keep Changes]** e **[!UICONTROL Save]** a regra.

![Marque a caixa de seleção Renderizar decisões de personalização visual.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configuração do fluxo de trabalho de publicação

Para implantar essa configuração na página web, a próxima etapa é criar uma biblioteca que inclua os recursos recém-criados. Leia mais sobre [configuração de um fluxo de publicação](/help/tags/ui/publishing/publishing-flow.md).

Selecione **[!UICONTROL Publishing Flow]** e depois **[!UICONTROL Add Library]**.

Selecione **[!UICONTROL Add all Changed Resources]**, dê um nome à biblioteca, defina o ambiente como **[!UICONTROL Development]** e selecione **[!UICONTROL Save & Build to Development]**.

![Criar biblioteca e implantar no ambiente de desenvolvimento](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Teste seu site

Neste ponto, o site deve ser totalmente instrumentado com o SDK da Web. Para testar se a coleção de dados está funcionando como esperado, você pode navegar até o site e usar as ferramentas de desenvolvedor do navegador para inspecionar o tráfego da rede.

Insira `interact` na caixa de pesquisa, atualize a página e você deverá ver chamadas de rede do seu site para a rede de borda da Adobe.

![Exibição dos eventos de rede preenchidos nas ferramentas do desenvolvedor.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalização {#personalization}

Agora você está pronto para criar e ativar públicos-alvo para personalização.

#### Criar público-alvo e configurar a segmentação de borda

Na interface do usuário do Experience Platform, navegue até **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** e crie um público-alvo para capturar os visitantes do site.

![Exibir como navegar até públicos-alvo.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

Você deve configurar seu público-alvo com [segmentação de borda](/help/segmentation/methods/edge-segmentation.md) para que a associação de público-alvo de seus visitantes seja avaliada em tempo real à medida que eles visitam sua propriedade da Web.

Configure também uma [política de mesclagem ativa na borda](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) para os públicos-alvo de borda.

#### Integrar ao Adobe Target ou outro destino de personalização individual

Agora está tudo pronto para a integração com um mecanismo de personalização para exibir conteúdo personalizado a visitantes do seu site ou aplicativo. A Adobe recomenda utilizar o [destino do Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) para essa finalidade.

>[!IMPORTANT]
>
>Leia o tutorial sobre [ativação de públicos-alvo para destinos de personalização de borda](/help/destinations/ui/activate-edge-personalization-destinations.md) para obter uma visão completa das etapas necessárias para ativar seus públicos-alvo.

## Limitações e solução de problemas {#limitations-and-troubleshooting}

Observe as seguintes limitações ao explorar o caso de uso descrito nesta página:

* Se optar por usar IDs de parceiro, saiba que essas IDs não são usadas ao criar o [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md).

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Use o suporte a dados de terceiros da Real-Time CDP para [expandir sua base de perfis com perfis de clientes potenciais de parceiros de dados e interaja com eles para adquirir ou alcançar novos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Ativação ampliada de perfis de prospecto e públicos-alvo de prospecto](/help/destinations/ui/activate-prospect-audiences.md) para selecionar destinos.
