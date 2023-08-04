---
title: Use o reconhecimento de visitantes auxiliados pelo parceiro para personalizar experiências no local
description: Saiba como usar o reconhecimento de visitantes auxiliado por parceiros para fornecer experiências personalizadas no local para seus visitantes.
hide: true
hidefromtoc: true
source-git-commit: f63cddc1158e739ce26e0ce1d3d54b491bd80c06
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 7%

---

# Use o reconhecimento de visitantes auxiliados por parceiros para personalizar experiências no local

Saiba como usar o reconhecimento auxiliado pelo parceiro para fornecer experiências personalizadas aos visitantes de propriedades da Web. Use este tutorial para entender a sequência de implementação de vários elementos no Experience Platform e outras soluções da Experience Cloud para exibir uma experiência personalizada para visitantes autenticados e não autenticados.

![Um infográfico que descreve como usar atributos fornecidos pelo parceiro para fornecer experiências personalizadas aos visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Exemplo do setor {#industry-example}

Como exemplo, considere uma marca de aprimoramento residencial com baixas taxas de autenticação. Essa marca gostaria de fornecer experiências personalizadas para visitantes novos, sem histórico ou autenticação anteriores e sem a dependência cada vez maior de cookies de terceiros.

Essa marca escolhe aproveitar a tecnologia de reconhecimento de parceiros para reconhecer probabiliticamente o visitante e oferecer uma experiência mais personalizada. Isso ajuda a promover a consideração, à medida que o visitante move para baixo o funil de marketing. Por exemplo, a marca pode usar sinais demográficos fornecidos pelo parceiro para conteúdo no site que atrai pessoas que se mudaram recentemente e oferecem um desconto em produtos populares que fazem você mesmo.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao planejar usar atributos fornecidos pelo parceiro para fornecer experiências personalizadas aos visitantes autenticados e não autenticados, considere os seguintes pré-requisitos no processo de planejamento:

* Quais entradas são esperadas pela tecnologia de reconhecimento do seu parceiro para que ele possa criar camadas de atributos adicionais?
* Até que ponto você se sente confortável em fornecer personalização em diferentes canais e para casos de uso diferentes com base em atributos derivados probabilísticos, em comparação a atributos confirmados deterministicamente?
* Como a experiência de um visitante pré-autenticado, mas reconhecido, deve ser alterada durante a autenticação?

### Funcionalidade da interface do usuário, componentes da plataforma e produtos de Experience Cloud que você usará {#ui-functionality-and-elements}

Para implementar com êxito esse caso de uso, você deve usar várias áreas da Real-time Customer Data Platform e outras soluções de Experience Cloud. Certifique-se de ter as [permissões de controle de acesso baseado em atributo](/help/access-control/abac/overview.md) para todas essas áreas, ou peça ao administrador do sistema para conceder as permissões necessárias.

* Coleção de dados
   * [SDK da Web da Adobe Experience Platform](/help/edge/home.md)
   * [Tags](/help/tags/home.md)
   * [Datastreams](/help/datastreams/overview.md)
* Gerenciamento de dados no Real-Time CDP
   * [Identidades](/help/identity-service/namespaces.md)
   * [Esquemas](/help/xdm/home.md)
   * [Rótulos de uso de dados](/help/data-governance/labels/overview.md)
   * [Conjuntos de dados](/help/catalog/datasets/overview.md)
* Personalização de propriedade da Web
   * [Segmentação de borda](/help/segmentation/ui/edge-segmentation.md)
   * [Destinos de personalização de borda](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (ou uma plataforma de personalização de sua escolha. Este tutorial de caso de uso destaca o Adobe Target como mecanismo de personalização)

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

![Um infográfico que descreve como usar atributos fornecidos pelo parceiro para fornecer experiências personalizadas aos visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Como um **cliente**, sua licença do **parceiro de dados** a capacidade de buscar insights em tempo real em visitantes anônimos de sites.
2. Como um **cliente**, você implanta bibliotecas do lado do cliente em suas propriedades para chamar **parceiro** e você configura o SDK da Web ou o SDK móvel para enviar sinais fornecidos pelo parceiro para a Real-Time CDP.
3. Ao navegar em seu site ou aplicativo, a variável **visitante** é probabilisticamente reconhecido pela **parceiro**, que retorna atributos juntamente com uma ID.
4. O Real-Time CDP executa a segmentação de borda para avaliar ocorrências de evento recebidas e resultados persistentes em relação à [Identificador ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).
5. O Adobe Target usa a saída da segmentação de borda para renderizar a experiência de volta para o **visitante** para personalização na sessão.
6. O evento é persistente em sua totalidade para workflows downstream como análise e redirecionamento.

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Gerenciamento de dados - crie um namespace de identidade, esquema e conjunto de dados para gerenciar os atributos de dados {#data-management}

Como preparo para atingir o caso de uso para personalizar a experiência de visitantes não autenticados, primeiro você deve configurar a estrutura de gerenciamento de dados no Real-Time CDP para receber os dados recebidos do evento em tempo real e da qualificação do público-alvo.

#### Criar namespace de identidade da ID de parceiro

Primeiro, é necessário criar um namespace de identidade da ID de parceiro. Navegue até **[!UICONTROL Cliente]** > **[!UICONTROL Identidades]** no painel à esquerda e selecione **[!UICONTROL Criar namespace de identidade]** no canto superior direito da tela.

![A caixa de diálogo Criar namespace de identidade com ID de parceiro está realçada.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Leia mais sobre como [criar um namespace de identidade de ID de parceiro](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Criar um esquema

Em seguida, crie um [!UICONTROL Evento de experiência] esquema para armazenar os dados de série temporal que você coletará posteriormente de suas propriedades da web e certifique-se de usar [!UICONTROL XDM ExperienceEvent] como a classe base do esquema. Leia sobre como [criar um esquema usando a interface do Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![A área de trabalho Esquemas com Criar esquema e o evento Experiência XDM destacados.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

À medida que você cria seu esquema e [adicionar grupos de campos a seu esquema](/help/xdm/ui/resources/schemas.md#add-field-groups), considere adicionar o [Visitar página da Web](/help/xdm/field-groups/event/web-details.md) e [Mapa de identidade](/help/xdm/field-groups/profile/identitymap.md) grupos de campos. Além de outros grupos de campo aplicáveis à propriedade digital e às práticas de coleta de dados.

Além disso, você pode criar ou reutilizar um grupo de campos existente e adicioná-lo ao esquema para capturar insights fornecidos pelo parceiro sobre o visitante. Ler como [criar um grupo de campos](/help/xdm/ui/resources/field-groups.md) e como [adicionar campos](/help/xdm/ui/resources/field-groups.md) ao grupo de campos. Por exemplo, se você espera personalizar em relação a insights fornecidos pelo parceiro, como faixa etária, status de emprego, poder de gastos mensais ou comportamentos de compra, solicite que o grupo de campos inclua campos apropriados.

Supondo que o parceiro de dados forneça um identificador estável para o visitante e que você gostaria de trazê-lo para o Real-Time CDP, certifique-se de ter um campo nomeado adequadamente para o identificador em seu grupo de campos personalizados. Você também deve marcar o campo como uma identidade no namespace de identidade criado anteriormente. Lembre-se também de [ativar o esquema para ser incluído no Perfil](/help/xdm/ui/resources/schemas.md#profile).

#### Criar um conjunto de dados

Em seguida, você deve criar um conjunto de dados para manter os dados de série temporal coletados dos visitantes da propriedade da Web e que serão usados para personalização no site.

Leia o tutorial sobre [como criar um conjunto de dados](/help/catalog/datasets/user-guide.md#create) e lembre-se de selecionar a opção para criar o conjunto de dados a partir de um esquema. Crie o conjunto de dados com base no esquema criado na etapa anterior.

Semelhante à etapa ao criar um esquema, é necessário ativar o conjunto de dados para ser incluído na [!UICONTROL Perfil do cliente em tempo real]. Para obter mais informações sobre como ativar o conjunto de dados para uso no [!UICONTROL Perfil do cliente em tempo real], leia o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementar a coleta de dados do evento na propriedade da Web {#implement-data-collection}

Depois de definir a configuração de gestão de dados, é necessário implementar o evento em tempo real [coleção de dados](/help/collection/home.md) na propriedade da web. É necessário instrumentar sua propriedade com a biblioteca de coleção de dados do Adobe - [!UICONTROL SDK da Web] - para coletar chamadas de evento em tempo real e enviá-las de volta para a Real-Time CDP. Este item consiste em algumas tarefas separadas em alguns componentes de coleção de dados.

>[!IMPORTANT]
>
>Para recuperar atributos fornecidos pelo parceiro, você também deve *integre sua propriedade da web com APIs de parceiros ou outros métodos para chamar e recuperar atributos de parceiros de dados em tempo real*. Discuta esse aspecto com seu parceiro de escolha, pois ele não é assunto deste tutorial.

Primeiro, use o alternador de aplicativos no canto superior direito da tela para navegar até o **[!UICONTROL Coleta de dados]** seção.

>[!TIP]
>
>Entre em contato com o administrador do sistema para solicitar acesso se não conseguir visualizar [!UICONTROL Coleta de dados] no alternador de aplicativos.

![Seletor de aplicativos para acessar a seção Coleção de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

A variável **[!UICONTROL Coleta de dados]** A seção da interface do usuário do é semelhante à imagem abaixo.

![Seção de coleção de dados da interface do usuário da Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Criar sequência de dados

Como primeira etapa na seção de coleção de dados, [criar um novo fluxo de dados](/help/datastreams/configure.md). A sequência de dados é a base de como os dados são coletados e roteados corretamente para o aplicativo Adobe correto, neste caso, Experience Platform.

À medida que você cria o fluxo de dados, no **[!UICONTROL Esquema de evento]** selecione o schema criado anteriormente.

![Seletor de esquema de evento realçado ao configurar um novo fluxo de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Selecionar o conjunto de dados do evento](/help/datastreams/configure.md#aep) que você criou anteriormente a partir da lista suspensa, marque as caixas ao lado de **[!UICONTROL Segmentação de borda]** e **[!UICONTROL Destinos de personalização]** e selecione **[!UICONTROL Salvar]**.

Observe que não é necessário selecionar um conjunto de dados de perfil nesse cenário, pois você está trazendo dados de série temporal com base em eventos.

#### Criar propriedade de tag

Pense em uma propriedade como um contêiner que você preenche com extensões, regras, elementos de dados e bibliotecas enquanto implanta tags no site.

Navegue até **[!UICONTROL Tags]** e selecione **[!UICONTROL Nova propriedade]**.

![Crie uma nova propriedade de tag.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Preencha os campos obrigatórios e selecione **[!UICONTROL Salvar]**.

![Preencha os campos obrigatórios da nova propriedade.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Obter informações completas sobre como [criar uma propriedade de tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Em seguida, você deve instalar várias extensões na propriedade. Selecione a propriedade da tag e navegue até a [!UICONTROL Extensões] seção.

![Selecione sua nova propriedade de tag.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observe que [!UICONTROL Núcleo] extensão já está instalada. Você deve instalar mais duas extensões, conforme detalhado nas próximas seções.

![Exibir extensões instaladas.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Instalar extensão SDK da Web

Observe que este tutorial indica como você pode instrumentar seu site com o SDK da Web. Também é possível usar [SDK móvel](https://developer.adobe.com/client-sdks/documentation/) no aplicativo para personalizar a experiência para os visitantes do aplicativo.

![Exibição da extensão SDK da Web no catálogo de extensões.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Na tela para configurar o SDK da Web, navegue até o **[!UICONTROL Datastreams]** e forneça informações sobre a sandbox Experience Platform que você está usando. Na próxima lista suspensa, selecione a sandbox apropriada e o fluxo de dados criado nas etapas anteriores. Você pode escolher os mesmos valores de sandbox e sequência de dados para todos os outros ambientes. Deixe as outras configurações inalteradas e selecione **[!UICONTROL Salvar]**.

Obter informações completas sobre [como instalar o SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Instalar extensão do serviço de ID

Use o [Extensão do Experience Cloud ID Service](/help/tags/extensions/client/id-service/overview.md) para criar uma identidade própria exclusiva baseada em dispositivos para visitantes em todas as soluções Experience Cloud. Pesquisar por **[!UICONTROL Serviço de ID]** no catálogo de extensões e instale-o. Mantenha todas as configurações padrão ao instalar a extensão.

![Exibição da extensão do serviço de ID no catálogo de extensões.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configurar ambientes

Em seguida, siga para o **[!UICONTROL Ambientes]** da navegação à esquerda. Nesta etapa, você deve conectar seu site à Rede Adobe Edge para recuperar e fornecer informações do visitante em tempo real.

Selecione o ícone de caixa à direita para o ambiente de desenvolvimento e copie a versão padrão do trecho de código JavaScript que aparece em uma janela modal.

![Selecione o ícone de caixa destacado na seção Ambientes da interface da Coleção de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Você deve adicionar esse trecho de código à parte superior do site. Como resultado, seu site fará uma chamada para a Rede Adobe Edge para recuperar a lógica do JavaScript que será carregada e executada na página. Isso permite que funcionalidades como geração de ID de visitante, coleção de dados e personalização de experiência em tempo real funcionem.

#### Configurar elementos de dados

Os elementos de dados são os blocos fundamentais do seu dicionário de dados (ou mapa de dados). Um único elemento de dados é uma variável cujo valor pode ser mapeado para consultar strings, URLs, valores de cookie, variáveis JavaScript e assim por diante. Leia mais sobre [elementos de dados](/help/tags/ui/managing-resources/data-elements.md).

Para o propósito deste caso de uso, você deve configurar dois elementos de dados.

Primeiro, configure um `partnerData` elemento. Navegue até a **[!UICONTROL Elementos de dados]** e selecione **[!UICONTROL Criar novo elemento de dados]**.

![Crie um novo elemento de dados.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Nomeie o elemento de dados `partnerData`, deixe o [!UICONTROL extensão] value as [!UICONTROL Núcleo]e defina **[!UICONTROL Tipo de elemento de dados]** as **[!UICONTROL Variável JavaScript]**. Enter `partnerData` no campo intitulado **[!UICONTROL Nome da variável JavaScript]** e selecione **[!UICONTROL Salvar]**.

![Seleções realçadas para configurar corretamente o elemento de dados partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Para configurar o segundo elemento de dados, nomeie a nova variável `pageVisit`, defina o **[!UICONTROL Extensão]** para **[!UICONTROL Adobe Experience Platform]** e escolha **[!UICONTROL Objeto XDM]** como o tipo de dados.

![Seleções destacadas para configurar corretamente o elemento de dados pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

No esquema, selecione os atributos de terceiros que correspondem aos valores que você está esperando do parceiro de dados. Em seguida, selecione o botão de opção intitulado **[!UICONTROL Fornecer o objeto inteiro]**. Selecione o ícone que se parece com um banco de dados e escolha o `partnerData` elemento de dados criado anteriormente.

#### Configurar regras

No **[!UICONTROL Regras]** você pode configurar seu site para enviar uma solicitação de personalização ao Adobe com os atributos carregados nos elementos de dados que você acabou de criar. Leia mais sobre [criação de regras](/help/tags/ui/managing-resources/rules.md).

Selecionar **[!UICONTROL Criar nova regra]**. Nomear esta regra **[!UICONTROL Personalizar]** e selecione o sinal + ao lado de **[!UICONTROL Eventos]**. Selecionar **[!UICONTROL Page Bottom]** como o evento e salve.

![Seleções para a parte do tipo de evento de uma regra.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Selecione o sinal + ao lado de **[!UICONTROL Ações]**. Atualizar a extensão para **[!UICONTROL Adobe Experience Platform Web SDK]** e defina **[!UICONTROL Tipo de ação]** para **[!UICONTROL Enviar evento]**.

![Seleções para a parte do tipo de ação de uma regra.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

No **[!UICONTROL Tipo]** seletor suspenso à direita, selecione `web.webpagedetails.pageViews` como o tipo de evento.

![Selecione o tipo de evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Selecione o ícone de banco de dados ao lado de dados XDM e selecione o `pageVisit` elemento de dados.

Role para baixo na lista de configurações de Ação e marque a caixa intitulada **[!UICONTROL Renderizar decisões de personalização visual]**. Isso é importante para permitir que as experiências entregues por meio do Adobe Target ou outros produtos semelhantes sejam renderizadas visualmente na página da Web. Selecionar **[!UICONTROL Manter alterações]** e depois **[!UICONTROL Salvar]** a regra.

![Marque a caixa de seleção Renderizar decisões de personalização visual.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configurar fluxo de trabalho de publicação

Para implantar essa configuração na página da Web, a próxima etapa é criar uma biblioteca que inclua os recursos que você acabou de criar. Leia mais sobre [configurar um fluxo de publicação](/help/tags/ui/publishing/publishing-flow.md).

Selecionar **[!UICONTROL Fluxo de publicação]** e depois **[!UICONTROL Adicionar biblioteca]**.

Selecionar **[!UICONTROL Adicionar todos os recursos alterados]**, nomeie a biblioteca, defina o ambiente como **[!UICONTROL Desenvolvimento]** e selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

![Criar biblioteca e implantar no ambiente de desenvolvimento](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Testar seu site

Neste ponto, o site deve ser totalmente instrumentado com o SDK da Web. Para testar se a coleção de dados está funcionando como esperado, você pode navegar até o site e usar as ferramentas de desenvolvedor do navegador para inspecionar o tráfego da rede.

Entrada `interact` na caixa de pesquisa, atualize a página e você deverá ver chamadas de rede do seu site para a rede Adobe Edge preenchendo.

![Exibição dos eventos de rede preenchidos nas ferramentas do desenvolvedor.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalização {#personalization}

Agora você está pronto para criar e ativar públicos para personalização.

#### Configurar segmentação de borda

Configurar [segmentação de borda](/help/segmentation/ui/edge-segmentation.md) portanto, a associação de público-alvo de seus visitantes é avaliada em tempo real, à medida que eles visitam sua propriedade da web.

Certifique-se também de configurar um [política de mesclagem ativa na borda](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) para os públicos-alvo de borda.

#### Integrar ao Adobe Target ou outro destino de personalização personalizado

Agora você está pronto para se integrar a um mecanismo de personalização para exibir conteúdo personalizado para os visitantes do seu site ou aplicativo. O Adobe recomenda o uso de [Destino do Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) para este efeito.

>[!IMPORTANT]
>
>Leia o tutorial sobre [ativação de públicos-alvo para destinos de personalização de borda](/help/destinations/ui/activate-edge-personalization-destinations.md) para obter uma visão completa das etapas necessárias para ativar seus públicos-alvo.

## Limitações e solução de problemas {#limitations-and-troubleshooting}

Observe as seguintes limitações ao explorar o caso de uso descrito nesta página:

* Se você usa IDs de parceiro, esteja ciente de que essas IDs não são usadas ao criar sua [gráfico de identidade](/help/identity-service/ui/identity-graph-viewer.md).

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Use o suporte a dados de terceiros no Real-Time CDP para [expanda sua base de perfis com perfis de clientes potenciais de parceiros de dados e envolva-se com eles para adquirir ou alcançar novos clientes](/help/rtcdp/partner-data/prospecting.md).
* (**Em breve**) [!BADGE Beta]{type=Informative}**Ativação expandida** usando IDs de parceiros para ecossistemas de publicação que não aceitam PII ou PII com hash.