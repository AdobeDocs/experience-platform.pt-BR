---
keywords: perfil rtcdp;perfis rtcdp;identidade rtcdp;políticas de mesclagem rtcdp;perfil do cliente em tempo real
title: Guia da interface do usuário do perfil da conta
description: Com o uso de perfis de conta, o Adobe Real-time Customer Data Platform B2B Edition permite unificar informações de conta de várias fontes. Este guia fornece detalhes para interagir com perfis de conta na interface do usuário do Adobe Experience Platform.
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 96f29d5c64bb29125d8a63dd3ddb3bdedb5ebd52
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 0%

---

# Guia da interface do perfil da conta

>[!NOTE]
>
>Os perfis de conta só estão disponíveis para clientes do Real-time Customer Data Platform B2B Edition. Para saber mais sobre o Real-Time CDP, incluindo os recursos e a funcionalidade disponíveis para cada tipo de licença, comece lendo a [visão geral do Real-Time CDP](../overview.md).

Os perfis de conta permitem unificar informações de conta de várias fontes. Essa visualização unificada de uma conta reúne dados de vários canais de marketing e os diversos sistemas que sua organização está usando atualmente para armazenar informações de contas de clientes. Este documento fornece um guia para interagir com perfis de conta usando os recursos do Real-Time CDP, B2B Edition disponíveis na interface do usuário (UI) do Adobe Experience Platform.

Para saber mais sobre como os perfis de conta são criados como parte do fluxo de trabalho B2B, consulte o [tutorial completo](../b2b-tutorial.md).

## Visão geral dos perfis de conta {#account-profiles-overview}

Selecione **[!UICONTROL Perfis]** em [!UICONTROL Contas] no menu de navegação esquerdo para exibir a visão geral dos perfis de conta. Na guia [!UICONTROL Visão geral], o painel mostra um gráfico que exibe widgets em um único ponto de entrada.

![A guia Visão Geral de Perfis de Conta com Perfis na navegação à esquerda e Visão Geral realçada.](images/b2b-account-profile-overview.png)

Consulte a documentação no painel [[!UICONTROL Perfis de conta]](../../dashboards/guides/account-profiles.md) para saber mais. Consulte a documentação no [Real-time Customer Data Platform Insights data model B2B Edition](../../dashboards/data-models/cdp-insights-data-model-b2b.md) para obter mais informações sobre como seus modelos de dados de insights podem ser usados para criar gráficos personalizados para seus painéis.

## Configurar lead para correspondência de conta {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Somente administradores de IA B2B podem habilitar, desabilitar e configurar o lead para o serviço de correspondência de contas. Ao desabilitar o serviço, os resultados correspondentes serão excluídos em 24 horas.

Para configurar o cliente potencial para correspondência de contas, selecione **[!UICONTROL Perfis]** em [!UICONTROL Contas] na navegação à esquerda. Na guia **[!UICONTROL Visão geral]**, selecione **[!UICONTROL Configurações]** no canto superior direito.

![A guia Visão Geral de Perfis de Conta com Configuração realçada.](images/b2b-configuring-accounts-profile.png)

A caixa de diálogo **[!UICONTROL Configurações da conta]** é aberta. Aqui, selecione a opção **[!UICONTROL Habilitar correspondência entre lead e conta]** para habilitar o recurso. Use o menu suspenso para selecionar **[!UICONTROL Diariamente]** para a configuração **[!UICONTROL Cadência de correspondência]**. Finalmente, selecione as opções relevantes de **[!UICONTROL Critérios de correspondência]** seguidas por **[!UICONTROL Salvar]** para confirmar suas configurações e retornar à tela **[!UICONTROL Perfis de conta]**.

>[!NOTE]
>
> O Endereço não pode ser usado como o único critério de correspondência. Um ou mais dos outros critérios de correspondência devem ser selecionados.

![Definir configurações da conta](images/b2b-configuring-account-settings.png)

Para saber mais sobre correspondência entre lead e conta, consulte a [Correspondência entre lead e conta na visão geral B2B do Real-Time CDP](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## Procurar perfis de conta {#browse-account-profiles}

Para procurar perfis de conta, comece selecionando **[!UICONTROL Perfis]** em [!UICONTROL Contas] no menu de navegação esquerdo.

Na guia **[!UICONTROL Procurar]**, você pode explorar perfis de conta usando uma ID de conta de uma fonte corporativa conectada ou inserindo os detalhes da fonte diretamente.

![Usar ID da conta para explorar perfis](images/b2b-account-browse-by.png)

### Procurar por [!UICONTROL Fonte corporativa conectada] {#browse-by-connected-enterprise-source}

Para procurar perfis de conta por uma origem corporativa conectada, selecione **[!UICONTROL Origem corporativa conectada]** na lista suspensa **[!UICONTROL Procurar por]** e escolha uma origem conectada usando o botão seletor ao lado do campo **[!UICONTROL Source]**.

![Procurar perfis de conta por fonte corporativa conectada](images/b2b-account-browse.png)

Isso abre a caixa de diálogo **[!UICONTROL Selecionar origem]**, na qual você pode selecionar uma origem com base nas conexões que sua organização estabeleceu.

>[!NOTE]
>
>Sua organização pode ter várias origens configuradas para o mesmo provedor de serviços (por exemplo, Marketo), portanto, é importante revisar o nome da conexão, o sistema de origem e a instância do sistema de origem para garantir que você esteja pesquisando pela instância de origem correta.

Para saber mais sobre como conectar fontes da empresa, consulte a [visão geral das fontes](../sources/sources-overview.md).

Você pode escolher uma origem selecionando o botão de opção ao lado do nome da conexão e, em seguida, usar **[!UICONTROL Selecionar]** para retornar à guia [!UICONTROL Procurar].

![Selecionar fluxo de trabalho de origem](images/b2b-account-select-source.png)

Com uma origem selecionada, agora você deve inserir uma **[!UICONTROL ID da conta]** relacionada à origem. Por exemplo, selecionar uma origem do Salesforce exigiria que você inserisse uma ID de conta na instância do Salesforce para exibir o perfil da conta vinculado a essa ID.

>[!NOTE]
>
>Para IDs de conta da Marketo, há duas tabelas de conta possíveis que podem ser referenciadas. Portanto, você deve usar uma sintaxe específica para garantir que está visualizando a conta correta.
>
>A sintaxe padrão mais comum é a ID de conta do Marketo anexada por `.mkto_org` (por exemplo, `1234567.mkto_org`). Os clientes do Marketo Account-Based Marketing podem ter valores adicionais que podem ser encontrados usando a ID de conta da Marketo anexada por `.mkto_account`. Se não tiver certeza de qual sintaxe usar, consulte o administrador do Marketo.

![Seleção da ID da conta](images/b2b-account-browse-id.png)

### Procurar por [!UICONTROL Outros] {#browse-by-others}

O Real-Time CDP, B2B Edition dá suporte à capacidade de realizar uma pesquisa direta permitindo que você insira um **[!UICONTROL nome do Source]**, **[!UICONTROL instância do Source]** e **[!UICONTROL ID da Conta]** para uma conta que você queira exibir. Ao inserir o nome de origem e a instância diretamente, você fornece o contexto necessário para que o Experience Platform pesquise e exiba os dados corretos do perfil da conta.

A capacidade de executar uma pesquisa direta é útil em circunstâncias em que não é possível fazer uma conexão de origem diretamente com os dados. Por exemplo, se sua organização tiver políticas de governança de dados em vigor que impeçam a conexão direta com um CRM, você poderá exportar esses dados para um sistema de armazenamento na nuvem e assimilá-los no Experience Platform.

Outro exemplo pode ser que você esteja executando uma transformação nos dados entre o momento em que ele sai de um sistema e entra na Platform. Você pode usar a funcionalidade de pesquisa direta para fornecer contexto para os dados (como especificar que são dados do Marketo, apesar de virem de um bucket do Amazon S3, por exemplo) para que o sistema saiba onde procurar os dados e como renderizá-los corretamente.

Para iniciar uma pesquisa direta, selecione **[!UICONTROL Outros]** na lista suspensa **[!UICONTROL Procurar por]** e digite um **[!UICONTROL nome de Source]**, **[!UICONTROL instância de Source]** e **[!UICONTROL ID de Conta]** para a conta que deseja exibir.

![Procurar por outros](images/b2b-account-browse-adhoc.png)

## Exibir detalhes do perfil da conta {#view-account-profile-details}

Depois de usar a guia **[!UICONTROL Procurar]** para localizar um perfil de conta, selecionar a **[!UICONTROL ID do Perfil]** abrirá a guia **[!UICONTROL Detalhes]** para o perfil de conta. As informações do perfil exibidas na guia **[!UICONTROL Detalhes]** foram mescladas de vários fragmentos de perfil para formar uma única visualização da conta individual. Isso inclui detalhes da conta, como atributos básicos e dados de redes sociais.

Os campos padrão mostrados também podem ser alterados em um nível organizacional para exibir atributos de perfil da conta preferencial.

>[!NOTE]
>
>Uma funcionalidade semelhante está disponível para perfis de clientes e um guia passo a passo foi criado com instruções para adicionar e remover atributos, redimensionar painéis, etc. Leia o [guia de personalização de detalhes do perfil](../../profile/ui/profile-customization.md) para saber mais.

![Exibir detalhes do perfil da conta](images/b2b-account-details.png)

É possível exibir detalhes adicionais relacionados à conta selecionando outra das guias disponíveis. Essas guias incluem atributos, pessoas e a guia oportunidades que mostra oportunidades abertas e fechadas relacionadas à conta em todos os sistemas da empresa. Consulte as seções a seguir para obter mais informações sobre cada guia.

## Guia Atributos {#attributes-tab}

A guia **[!UICONTROL Atributos]** lista todas as informações de registro relacionadas à conta. Isso inclui dados de atributos provenientes de várias fontes que foram mesclados para formar uma única visualização da conta.

Além de poder exibir os dados em uma lista, você pode usar a barra de pesquisa para procurar atributos específicos ou exibir os dados de registro como JSON.

![Guia Atributos](images/b2b-account-attributes.png)

## Guia Pessoas {#people-tab}

A guia **[!UICONTROL Pessoas]** fornece uma lista de pessoas individuais associadas à conta. Essas pessoas podem ser contatos e clientes potenciais de diferentes sistemas corporativos gerenciados por equipes diferentes em sua organização, mas no Real-Time CDP, B2B Edition, elas são apresentadas juntas como uma única lista, permitindo que você veja uma visão mais holística dos contatos de sua conta.

>[!NOTE]
>
>A guia [!UICONTROL Pessoas] exibe uma lista de até 25 pessoas associadas à conta. Para contas com mais de 25 pessoas associadas, o sistema mostra uma amostragem aleatória de 25 registros.

Além de mostrar um instantâneo das informações do contato, cada pessoa listada também inclui uma **[!UICONTROL ID do Perfil]**, que é um link clicável que permite explorar o Perfil de Cliente em Tempo Real desse indivíduo. Para saber mais sobre como visualizar perfis de clientes individuais relacionados às suas contas, visite o guia para [procurar perfis no Real-Time CDP, B2B Edition](../profile/profile-browse.md).

![Guia Pessoas](images/b2b-account-people.png)

## Guia Oportunidades {#opportunities-tab}

A guia **[!UICONTROL Oportunidades]** fornece informações sobre oportunidades abertas e fechadas relacionadas à conta. Essas oportunidades podem ser assimiladas no Experience Platform de várias fontes. No entanto, o Real-Time CDP, B2B Edition facilita que os profissionais de marketing vejam todas essas oportunidades em um único local.

>[!NOTE]
>
>A guia [!UICONTROL Oportunidades] exibe uma lista de até 25 oportunidades associadas à conta. Para contas com mais de 25 oportunidades associadas, o sistema mostra uma amostragem aleatória de 25 registros.

Cada oportunidade inclui informações como o nome da oportunidade, sua quantidade, estágio e se a oportunidade está em aberto, fechada, ganha ou perdida.

![Guia de oportunidades da conta](images/b2b-account-opportunities.png)

## Guia Contas relacionadas {#related-accounts-tab}

A guia **[!UICONTROL Contas relacionadas]** fornece informações sobre outras contas que podem estar relacionadas à conta que você está navegando. Para obter informações detalhadas sobre a funcionalidade, leia a [visão geral das contas relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Um grupo de contas relacionadas pode ter no máximo 30 perfis de conta. Se mais de 30 perfis de conta forem encontrados relacionados, eles serão arbitrariamente divididos em vários grupos, cada um com no máximo 30 membros. O grupo Contas relacionadas de um perfil de conta sempre inclui a si mesmo.
>* A guia [!UICONTROL Contas relacionadas] atualmente exibe uma lista de até 25 contas relacionadas associadas à conta que você está navegando. Essa é uma limitação que será abordada em uma atualização futura. Apesar dessa limitação da interface do usuário, quando você usa contas relacionadas nas definições de segmento, para grupos de 30 perfis de conta relacionados, todos os perfis são usados para direcionamento.

Cada conta relacionada inclui informações como a ID e o nome do perfil da conta, sua chave de origem da conta e informações adicionais relacionadas à página inicial, endereço, conta pai, telefone, setor e receita anual.

![Guia de contas relacionadas](images/b2b-account-related-accounts.png)

Você pode usar as contas relacionadas nesta lista para fins de segmentação. Veja um [exemplo de segmentação](/help/rtcdp/segmentation/b2b.md#related-account) para entender como usar contas relacionadas para expandir seu alcance nas definições de segmento.