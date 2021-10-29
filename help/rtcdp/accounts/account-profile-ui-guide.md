---
keywords: perfil rtcdp, perfis rtcdp, identidades rtcdp, políticas de mesclagem rtcdp, perfil do cliente em tempo real
title: Guia da interface do usuário do perfil da conta (Beta)
description: Com o uso de perfis de conta, o Real-time Customer Data Platform B2B Edition permite unificar as informações da conta de várias fontes. Este guia fornece detalhes para interagir com perfis de conta na interface do usuário do Adobe Experience Platform.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 6f421a8ae77318ca2598d640cf7e27ea485ec9db
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 0%

---

# Guia da interface do usuário do perfil da conta (Beta)

>[!IMPORTANT]
>
>Atualmente, o Real-time Customer Data Platform B2B Edition está em beta. A documentação e a funcionalidade estão sujeitas a alterações.

>[!NOTE]
>
>Os perfis da conta só estão disponíveis para clientes do Real-time Customer Data Platform B2B Edition. Para saber mais sobre a CDP em tempo real, incluindo os recursos e funcionalidades disponíveis para cada tipo de licença, comece lendo o [Visão geral da CDP em tempo real](../overview.md).

Os perfis de conta permitem unificar as informações da conta de várias fontes. Essa exibição unificada de uma conta reúne dados de vários canais de marketing e dos diversos sistemas que sua organização está usando atualmente para armazenar informações de conta do cliente. Este documento fornece um guia para interagir com perfis de conta usando os recursos CDP em tempo real, B2B Edition disponíveis na interface do usuário do Adobe Experience Platform (UI).

## Procurar perfis de conta

Para navegar pelos perfis da conta, comece selecionando **[!UICONTROL Perfis]** under [!UICONTROL Contas] na navegação à esquerda.

![](images/b2b-account-browse.png)

No **[!UICONTROL Procurar]** Na guia , é possível explorar perfis de conta usando uma ID de conta de uma fonte corporativa conectada ou inserindo detalhes de origem diretamente.

![](images/b2b-account-browse-by.png)

### Procurar por [!UICONTROL Origem corporativa conectada]

Para procurar perfis de conta por uma origem empresarial conectada, selecione **[!UICONTROL Origem corporativa conectada]** do **[!UICONTROL Procurar por]** , em seguida, escolha uma fonte conectada usando o botão do seletor ao lado do **[!UICONTROL Origem]** campo.

![](images/b2b-account-browse.png)

Isso abre o **[!UICONTROL Selecionar origem]** , onde é possível selecionar uma fonte com base nas conexões estabelecidas pela organização.

>[!NOTE]
>
>Sua organização pode ter várias fontes configuradas para o mesmo provedor de serviços (por exemplo, Marketo), portanto, é importante revisar o nome da conexão, o sistema de origem e a instância do sistema de origem para garantir que você esteja pesquisando pela instância de origem correta.

Para saber mais sobre como conectar-se às fontes corporativas, consulte [visão geral das fontes](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Você pode escolher uma fonte selecionando o botão de opção ao lado do nome da conexão e usando **[!UICONTROL Selecionar]** para retornar ao [!UICONTROL Procurar] guia .

Com uma fonte selecionada, agora você deve inserir um **[!UICONTROL ID da conta]** relacionado à origem. Por exemplo, selecionar uma origem do Salesforce exigiria que você informasse uma ID de conta da instância do Salesforce para exibir o perfil de conta vinculado a essa ID.

>[!NOTE]
>
>Para IDs de conta do Marketo, há duas tabelas de conta possíveis que podem ser referenciadas. Portanto, você deve usar uma sintaxe específica para garantir que esteja visualizando a conta correta.
>
>A sintaxe padrão mais comum é a ID da conta do Marketo anexada por `.mkto_org` (por exemplo, `1234567.mkto_org`). Os clientes de marketing baseado em conta do Marketo podem ter valores adicionais que podem ser encontrados usando a ID de conta do Marketo anexada por `.mkto_account`. Se não tiver certeza de qual sintaxe usar, verifique com o administrador do Marketo.

![](images/b2b-account-browse-id.png)

### Procurar por [!UICONTROL Outros]

A CDP em tempo real, B2B Edition, suporta a capacidade de realizar uma pesquisa direta permitindo que você insira um **[!UICONTROL Nome da origem]**, **[!UICONTROL Instância de origem]** e **[!UICONTROL ID da conta]** para uma conta que você deseja visualizar. Ao inserir o nome de origem e a instância diretamente, você fornece o contexto necessário para o Experience Platform procurar e exibir os dados corretos do perfil da conta.

A capacidade de executar uma pesquisa direta é útil em circunstâncias em que uma conexão de origem diretamente aos dados não é possível. Por exemplo, se sua organização tiver políticas de governança de dados em vigor que impedem a conexão diretamente com um CRM, você poderá exportar esses dados para um sistema de armazenamento em nuvem e assimilá-los no Experience Platform.

Outro exemplo pode ser que você está realizando uma transformação nos dados entre o momento em que sai de um sistema e entra na Plataforma. Você pode usar a funcionalidade de pesquisa direta para fornecer contexto para os dados (como especificar que são dados do Marketo, apesar de provirem de um bucket do Amazon S3, por exemplo), para que o sistema saiba onde procurar e como renderizar corretamente os dados.

Para iniciar uma pesquisa direta, selecione **[!UICONTROL Outros]** do **[!UICONTROL Procurar por]** , em seguida, insira um **[!UICONTROL Nome da origem]**, **[!UICONTROL Instância de origem]** e **[!UICONTROL ID da conta]** para a conta que deseja visualizar.

![](images/b2b-account-browse-adhoc.png)

## Exibir detalhes do perfil da conta

Depois de usar o **[!UICONTROL Procurar]** para localizar um perfil de conta, selecione a guia **[!UICONTROL ID do perfil]** abre o **[!UICONTROL Detalhe]** para o perfil da conta. As informações do perfil são exibidas no **[!UICONTROL Detalhe]** A guia foi unida de vários fragmentos de perfil para formar uma única visualização da conta individual. Isso inclui detalhes da conta, como atributos básicos e dados de mídia social.

Os campos padrão mostrados também podem ser alterados em nível organizacional para exibir os atributos preferenciais do perfil da conta.

>[!NOTE]
>
>Uma funcionalidade semelhante está disponível para perfis de clientes e um guia passo a passo foi criado com instruções para adicionar e remover atributos, redimensionar painéis etc. Leia o [guia de personalização de detalhes do perfil](../../profile/ui/profile-customization.md) para saber mais.

![](images/b2b-account-details.png)

Você pode visualizar detalhes adicionais relacionados à conta selecionando outra das guias disponíveis. Essas guias incluem atributos, pessoas e a guia oportunidades que mostra oportunidades abertas e fechadas relacionadas à conta em todos os sistemas empresariais. Consulte as seções a seguir para obter mais informações sobre cada guia.

## Guia Atributos

O **[!UICONTROL Atributos]** lista todas as informações de registro relacionadas à conta. Isso inclui dados de atributos provenientes de várias fontes que foram mescladas para formar uma única visualização da conta.

Além de poder exibir os dados em uma lista, você pode usar a barra de pesquisa para procurar atributos específicos ou exibir os dados de registro como JSON.

![](images/b2b-account-attributes.png)

## Guia Pessoas

O **[!UICONTROL Pessoas]** A guia fornece uma lista de pessoas individuais associadas à conta. Essas pessoas podem ser contatos e leads de diferentes sistemas empresariais gerenciados por diferentes equipes em sua organização, mas na Real-time CDP, B2B Edition são apresentados juntos como uma única lista, permitindo que você veja uma visão mais holística dos contatos de sua conta.

>[!NOTE]
>
>O [!UICONTROL Pessoas] exibe uma lista de até 25 pessoas associadas à conta. Para contas com mais de 25 pessoas associadas, o sistema mostra uma amostragem aleatória de 25 registros.

Além de mostrar um instantâneo das informações do contato, cada pessoa listada também inclui um **[!UICONTROL ID do perfil]**, que é um link clicável que permite explorar o Perfil do cliente em tempo real para esse indivíduo. Para saber mais sobre como visualizar perfis de clientes individuais relacionados a suas contas, visite o guia para [navegar pelos perfis na Real-time CDP, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Guia Oportunidades

O **[!UICONTROL Oportunidades]** A guia fornece informações para oportunidades abertas e fechadas relacionadas à conta. Essas oportunidades podem ser assimiladas em Experience Platform de várias fontes, no entanto, a CDP em tempo real, a B2B Edition, facilita para os profissionais de marketing verem todas essas oportunidades juntas em um único lugar.

>[!NOTE]
>
>O [!UICONTROL Oportunidades] exibe uma lista de até 25 oportunidades associadas à conta. Para contas com mais de 25 oportunidades associadas, o sistema mostra uma amostragem aleatória de 25 registros.

Cada oportunidade inclui informações como o nome da oportunidade, sua quantidade, estágio e se a oportunidade está aberta, fechada, ganha ou perdida.

![](images/b2b-account-opportunities.png)
