---
title: Redirecionamento externo de visitantes não autenticados
description: Saiba como redirecionar usuários não autenticados usando IDs de prospecto para criar um atributo computado que pode ser usado para criar um público-alvo de usuários não autenticados.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 1%

---

# Redirecionamento externo de visitantes não autenticados

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que licenciaram o Real-Time CDP (Serviço de aplicativo), Adobe Experience Platform Ativation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Leia mais sobre esses pacotes nas [descrições do produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) e entre em contato com a pessoa representante da Adobe para obter mais informações.

Saiba como criar um público-alvo de visitantes não autenticados e redirecioná-los usando IDs duráveis fornecidas pelo parceiro.

![Um infográfico que mostra o fluxo de dados do parceiro da assimilação na Adobe Experience Platform para saída via públicos-alvo para um destino downstream.](../assets/offsite-retargeting/header.png)

## Por que considerar este caso de uso {#why-use-case}

Com a eliminação gradual de cookies de terceiros, os profissionais de marketing digital devem reimaginar suas estratégias para se reengajarem com visitantes anônimos. As marcas que escolherem se integrar aos fornecedores de identidade para o reconhecimento de visitantes em tempo real também podem aproveitar os identificadores duráveis fornecidos pelos parceiros para o redirecionamento de mídia paga fora do site.

Apesar do alto volume de tráfego, muitas marcas observam uma queda significativa na fase de conversão. Os visitantes se envolvem com demonstrações de conteúdo e produto, mas saem sem se inscrever ou fazer uma compra.

Você não só pode criar públicos-alvo com base no engajamento no site para personalizar mensagens de marketing, como também pode usar o suporte ao Adobe para IDs de parceiros para reengajar com visitantes em destinos de mídia paga.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao planejar o redirecionamento de visitantes não autenticados, considere os seguintes pré-requisitos durante o processo de planejamento:

- Eu configurei as IDs de parceiro com os namespaces de identidade adequados?

Além disso, para implementar o caso de uso, você usará a seguinte funcionalidade do Real-Time CDP e elementos da interface do usuário. Certifique-se de que você tenha as permissões de controle de acesso com base em atributos necessárias para todas essas áreas ou peça ao administrador do sistema para conceder as permissões necessárias.

- [Públicos-alvo](../../segmentation/home.md)
- [Atributos computados](../../profile/computed-attributes/overview.md)
- [Destinos](../../destinations/home.md)
- [Web SDK](../../web-sdk/home.md)

## Obter dados de parceiros na Real-Time CDP {#get-data-in}

Para criar um público-alvo de visitantes não autenticados, primeiro será necessário obter os dados do parceiro no Real-Time CDP.

Para saber como importar dados para o Real-Time CDP usando o SDK da Web, leia as [seções de gerenciamento de dados e coleta de dados do evento](./onsite-personalization.md#data-management) do caso de uso de personalização no site.

## Antecipando IDs fornecidas pelo parceiro {#bring-partner-ids-forward}

Depois de importar as IDs fornecidas pelo parceiro para um conjunto de dados de evento, será necessário obter esses dados nos registros de perfil. Você pode fazer isso utilizando atributos computados.

Os atributos computados permitem converter rapidamente os dados comportamentais do perfil em valores agregados no nível do perfil. Como resultado, você pode usar essas expressões, como &quot;total de compras vitalícias&quot; no perfil, permitindo usar facilmente o atributo calculado em seus públicos-alvo. Mais informações sobre atributos computados podem ser encontradas na [visão geral sobre atributos computados](../../profile/computed-attributes/overview.md).

Para acessar atributos computados, selecione **[!UICONTROL Perfis]** seguidos por **[!UICONTROL Atributos computados]** e **[!UICONTROL Criar atributo computado]**.

![O botão [!UICONTROL Criar atributos computados] é realçado além da guia [!UICONTROL Atributos computados] no espaço de trabalho [!UICONTROL Perfis].](../assets/offsite-retargeting/create-ca.png)

A página **[!UICONTROL Criar atributo computado]** é exibida. Nesta página, você pode usar os componentes para criar seu atributo calculado.

![O espaço de trabalho criar atributos computados é exibido.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Para obter informações mais detalhadas sobre como criar atributos computados, leia o [guia da interface do usuário de atributos computados](../../profile/computed-attributes/ui.md).

Para este caso de uso, você pode criar um atributo calculado que, se a ID do parceiro existir, obterá o valor mais recente da ID do parceiro nas últimas 24 horas.

Usando a barra de pesquisa, você pode localizar e adicionar o evento &quot;ID do parceiro&quot; que [você criou durante o caso de uso de personalização no site](#get-data-in) para a tela de atributos computada.

![A guia [!UICONTROL Eventos] e a barra de pesquisa estão realçadas.](../assets/offsite-retargeting/ca-add-partner-id.png)

Depois de adicionar o evento &quot;ID do Parceiro&quot; à definição, defina a condição de filtragem do evento como **[!UICONTROL Existe]**, defina a condição de filtragem do evento como o valor **[!UICONTROL Mais Recente]** da ID do parceiro adicionada e com um período de pesquisa de 24 horas.

![A definição do atributo computado que você deseja criar está realçada.](../assets/offsite-retargeting/ca-add-definition.png)

Dê ao atributo computado um nome apropriado (como &quot;ID de Parceiro&quot;) e uma descrição, em seguida, selecione **[!UICONTROL Publish]** para concluir o processo de criação do atributo computado.

![As informações básicas do atributo computado que você deseja criar estão destacadas.](../assets/offsite-retargeting/ca-publish.png)

## Criar um público-alvo usando o atributo calculado {#create-audience}

Agora que você criou o atributo calculado, pode usar este atributo calculado para criar um público-alvo. Neste exemplo, você criará um público-alvo composto por visitantes que visitaram seu site mais de 5 vezes este mês, mas ainda não se inscreveram.

Para criar um público, selecione **[!UICONTROL Públicos-alvo]**, seguido de **[!UICONTROL Criar público-alvo]**.

![O botão [!UICONTROL Criar público-alvo] está realçado.](../assets/offsite-retargeting/create-audience.png)

Uma caixa de diálogo é exibida, solicitando que você escolha entre [!UICONTROL Compor público-alvo] e [!UICONTROL Criar regra]. Selecione a **[!UICONTROL Regra de compilação]** seguida de **[!UICONTROL Criar]**.

![O botão [!UICONTROL Regra de compilação] está realçado.](../assets/offsite-retargeting/select-build-rule.png)

A página Construtor de segmentos é exibida. Nesta página, você pode usar os componentes para criar seu público-alvo.

![O Construtor de segmentos é exibido.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Para obter informações mais detalhadas sobre como usar o Construtor de segmentos, leia o [Guia da interface do Construtor de segmentos](../../segmentation/ui/segment-builder.md).

Para atingir o objetivo de encontrar esses visitantes, primeiro você precisará adicionar um evento de **[!UICONTROL Exibição de página]** ao seu público-alvo. Selecione a guia **[!UICONTROL Eventos]** em **[!UICONTROL Campos]**, arraste e solte o evento **[!UICONTROL Exibição de página]** e adicione-o à tela da seção de eventos.

![A guia [!UICONTROL Eventos] da seção [!UICONTROL Campos] é realçada ao exibir o evento [!UICONTROL Exibição de Página].](../assets/offsite-retargeting/add-page-view.png)

Selecione o evento **[!UICONTROL Exibição de página]** recém-adicionado. Altere o período de pesquisa de **[!UICONTROL A qualquer momento]** para **[!UICONTROL Este mês]** e altere a regra de evento para incluir **Pelo menos 5**.

![Detalhes do evento [!UICONTROL Exibição de página] adicionado são exibidos.](../assets/offsite-retargeting/edit-event.png)

Depois de adicionar o evento, será necessário adicionar um atributo. Como você está trabalhando com visitantes não autenticados, é possível adicionar o atributo calculado que acabou de criar. Este atributo calculado recém-criado permite vincular IDs de parceiros a um público-alvo.

Para adicionar o atributo calculado, em **[!UICONTROL Atributos]**, selecione **[!UICONTROL Perfil Individual XDM]**, seguido da **[ID de locatário de sua organização](../../xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** e **[!UICONTROL PartnerID]**. Agora, adicione o **[!UICONTROL Valor]** do atributo computado à seção de atributos da tela.

![O caminho da pasta para acessar o atributo computado é exibido.](../assets/offsite-retargeting/access-computed-attribute.png)

Além disso, pesquise por **[!UICONTROL Email Pessoal]** e adicione o atributo **[!UICONTROL Endereço]** abaixo de **[!UICONTROL PartnerID]** à seção de atributos da tela.

![O atributo computado [!UICONTROL PartnerID] e o atributo [!UICONTROL Endereço de Email Pessoal] estão destacados na tela do Construtor de Segmentos.](../assets/offsite-retargeting/added-attributes.png)

Agora que seus atributos foram adicionados, será necessário definir seus critérios de avaliação. Para **[!UICONTROL PartnerID]**, defina o critério como **[!UICONTROL existe]** e, para **[!UICONTROL Address]**, defina o critério como **[!UICONTROL não existe]**.

![Os valores adequados dos atributos são realçados.](../assets/offsite-retargeting/set-attribute-values.png)

Você criou com sucesso um público-alvo que procura visitantes de alta intensidade com uma ID fornecida pelo parceiro, mas que ainda não se inscreveram no site. Nomeie seu público-alvo como &quot;Redirecionando usuários não autenticados&quot; e selecione **[!UICONTROL Salvar]** para concluir a criação do seu público-alvo.

![As propriedades do público-alvo são destacadas.](../assets/offsite-retargeting/save-audience-properties.png)

## Ativar seu público {#activate-audience}

Depois de criar seu público-alvo com êxito, você pode ativá-lo para destinos downstream. Selecione **[!UICONTROL Públicos-alvo]** no painel de navegação esquerdo, procure o público-alvo recém-criado, selecione o ícone de reticências e selecione **[!UICONTROL Ativar para destino]**.

![O botão [!UICONTROL Ativar para destino] está realçado.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Todos os tipos de destino, incluindo destinos baseados em arquivos, oferecem suporte à ativação de público-alvo com IDs de parceiros.
>
>Para obter mais informações sobre como ativar públicos para um destino, leia a [visão geral da ativação](../../destinations/ui/activation-overview.md).

A página **[!UICONTROL Ativar destino]** é exibida. Nesta página, você pode selecionar para qual destino deseja ativar seu destino. Depois de selecionar o destino escolhido, selecione **[!UICONTROL Próximo]**.

![O destino para o qual você deseja ativar o público-alvo está realçado.](../assets/offsite-retargeting/select-destination.png)

A página **[!UICONTROL Agendando]** é exibida. Nesta página, você pode criar um agendamento que determina a frequência com que deseja ativar o público-alvo. Selecione **[!UICONTROL Criar agendamento]** para criar um agendamento para a ativação de público-alvo.

![O botão [!UICONTROL Criar agendamento] está realçado.](../assets/offsite-retargeting/select-create-schedule.png)

O popover [!UICONTROL Agendando] é exibido. Nesta página, você pode criar a programação para a ativação do público-alvo. Depois de configurar o agendamento, selecione **[!UICONTROL Criar]** para continuar.

![O popover de configuração de agendamento é exibido.](../assets/offsite-retargeting/configure-schedule.png)

Depois de confirmar os detalhes do agendamento, selecione **[!UICONTROL Avançar]**.

![Os detalhes do agendamento são exibidos.](../assets/offsite-retargeting/created-schedule.png)

A página **[!UICONTROL Selecionar atributos]** é exibida. Nesta página, você pode selecionar quais atributos deseja exportar junto com o público-alvo ativado. No mínimo, inclua a ID do parceiro, pois isso permitirá identificar os visitantes que você planeja redirecionar. Selecione **[!UICONTROL Adicionar novo mapeamento]** e procure o atributo computado. Depois de adicionar os atributos necessários, selecione **[!UICONTROL Próximo]**.

![O botão [!UICONTROL Adicionar novo mapeamento] e o atributo computado estão realçados.](../assets/offsite-retargeting/add-new-mapping.png)

A página **[!UICONTROL Revisão]** é exibida. Nesta página, você pode revisar os detalhes da ativação do público-alvo. Se você estiver satisfeito com os detalhes fornecidos, selecione **[!UICONTROL Concluir]**.

![A página [!UICONTROL Revisão] é exibida, mostrando detalhes da ativação do público-alvo.](../assets/offsite-retargeting/review-destination-activation.png)

Agora você ativou um público-alvo de usuários não autenticados para um destino downstream para redirecionamento adicional.

## Outros casos de uso {#other-use-cases}

Você pode explorar mais casos de uso ativados por meio do suporte a dados de parceiros no Real-Time CDP:

- [Envolva e adquira novos clientes](./prospecting.md) usando dados de parceiros.
- [Personalize experiências no site](./offsite-retargeting.md) com reconhecimento de visitante auxiliado por parceiro.
- [Complemente perfis próprios](./supplement-first-party-profiles.md) com atributos fornecidos pelo parceiro.
