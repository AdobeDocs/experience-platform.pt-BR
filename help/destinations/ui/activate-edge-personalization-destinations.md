---
title: Ativar públicos para destinos de personalização de borda
description: Saiba como ativar públicos do Adobe Experience Platform para destinos de personalização de borda para casos de uso de personalização de mesma página e próxima página.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: afcb5f80edaa4d68ba167123feb2ba9060469243
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---


# Ativar públicos para destinos de personalização de borda

## Visão geral {#overview}

O Adobe Experience Platform usa [segmentação de borda](../../segmentation/ui/edge-segmentation.md) junto com destinos de borda para permitir que os clientes criem e direcionem públicos-alvo em alta escala, em tempo real. Esse recurso ajuda a configurar casos de uso de personalização de mesma página e próxima página.

Exemplos de destinos de borda são os [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e a variável [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) conexões.

>[!NOTE]
>
>Quando [configuração da conexão do Adobe Target](../catalog/personalization/adobe-target-connection.md) sem usar uma ID de fluxo de dados, os casos de uso descritos neste artigo não são compatíveis. Somente casos de uso de personalização da próxima sessão são compatíveis na ausência de um fluxo de dados.

>[!IMPORTANT]
> 
> * Para ativar os dados e habilitar a [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para ativar os dados sem passar pelo [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar segmento sem mapeamento]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}
> 
> Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Este artigo explica o fluxo de trabalho necessário para ativar públicos-alvo em destinos de borda do Adobe Experience Platform. Quando usado junto com [segmentação de borda](../../segmentation/ui/edge-segmentation.md) e a opção [mapeamento de atributos de perfil](#mapping), esses destinos permitem casos de uso de personalização de mesma página e próxima página nas propriedades da Web e móveis.

Para obter uma breve visão geral sobre como configurar a conexão do Adobe Target para personalização de borda, assista ao vídeo abaixo.

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter mudado desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte as etapas de configuração descritas nas seções abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Para obter uma breve visão geral de como compartilhar públicos-alvo e atributos de perfil com a Adobe Target e destinos de personalização personalizados, assista ao vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Casos de uso {#use-cases}

Os destinos de personalização de borda permitem usar soluções de personalização de Adobe, como o Adobe Target, ou suas próprias plataformas de parceiros de personalização (por exemplo, [!DNL Optimizely], [!DNL Pega]), bem como sistemas proprietários (por exemplo, CMS interno) para potencializar uma experiência mais profunda de personalização do cliente por meio da [Personalização personalizada](../catalog/personalization/custom-personalization.md) destino. Tudo isso enquanto também aproveita os recursos de coleta de dados e segmentação da Rede de borda do Experience Platform.

Os casos de uso descritos abaixo incluem personalização do site e publicidade direcionada no site.

Para habilitar esses casos de uso, os clientes precisam de uma maneira rápida e simplificada de recuperar informações de públicos-alvo e atributos de perfil do Experience Platform e de enviar essas informações para a [Adobe Target](../catalog/personalization/adobe-target-connection.md) ou o [Personalização personalizada](../catalog/personalization/custom-personalization.md) conexões na interface do Experience Platform.

### Personalização da mesma página {#same-page}

Um usuário visita uma página do site. O cliente pode usar as informações de visita da página atual (por exemplo, URL de referência, idioma do navegador, informações do produto incorporadas) para selecionar a próxima ação/decisão (por exemplo, personalização), usando o [Personalização personalizada](../catalog/personalization/custom-personalization.md) para plataformas não-Adobe (por exemplo, [!DNL Pega], [!DNL Optimizely], etc.).

### Personalização da próxima página {#next-page}

Um usuário visita a Página A em seu site. Com base nessa interação, o usuário se qualificou para um conjunto de públicos-alvo. O usuário clica em um link que o leva da Página A para a Página B. Os públicos para os quais o usuário se qualificou durante a interação anterior na Página A, juntamente com as atualizações de perfil determinadas pela visita atual do site, serão usados para potencializar a próxima ação/decisão (por exemplo, qual banner de publicidade exibir para o visitante ou, no caso de testes A/B, qual versão da página exibir).

### Personalização da próxima sessão {#next-session}

Um usuário visita várias páginas do site. Com base nessas interações, o usuário se qualificou para um conjunto de públicos-alvo. O usuário então encerra a sessão de navegação atual.

No dia seguinte, o usuário retorna ao mesmo site do cliente. Os públicos para os quais eles se qualificaram durante a interação anterior com todas as páginas do site visitadas, juntamente com as atualizações de perfil determinadas pela visita atual do site, serão usados para selecionar a próxima ação/decisão (por exemplo, qual banner de publicidade exibir para o visitante ou, no caso de testes A/B, qual versão da página exibir).

### Personalização de um banner de página inicial {#home-page-banner}

Uma empresa de vendas e aluguel de residências quer personalizar sua página inicial com um banner, com base nas qualificações de público-alvo no Adobe Experience Platform. A empresa pode selecionar quais públicos-alvo devem obter uma experiência personalizada e enviá-los para o Adobe Target como critérios de direcionamento para sua oferta do Target.

## Pré-requisitos {#prerequisites}

### Configurar um fluxo de dados na interface da coleção de dados {#configure-datastream}

A primeira etapa na configuração do destino de personalização é configurar um fluxo de dados para o SDK da Web do Experience Platform. Isso é feito na interface da Coleção de dados.

Ao configurar o fluxo de dados, em **[!UICONTROL Adobe Experience Platform]** verifique se ambos **[!UICONTROL Segmentação de borda]** e **[!UICONTROL Destinos de personalização]** são selecionados.

![Configuração da sequência de dados](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Para obter mais detalhes sobre como configurar um fluxo de dados, siga as instruções descritas em [Documentação do SDK da Web da Platform](../../datastreams/configure.md#aep).

### Criar um [!DNL Active-On-Edge] política de mesclagem {#create-merge-policy}

Depois de criar a conexão de destino, você deve criar um [!DNL Active-On-Edge] política de mesclagem. A variável [!DNL Active-On-Edge] a política de mesclagem garante que os públicos-alvo sejam avaliados constantemente [na borda](../../segmentation/ui/edge-segmentation.md) e estão disponíveis para caso de uso de personalização em tempo real e na próxima página.

>[!IMPORTANT]
>
>Atualmente, os destinos de borda só oferecem suporte à ativação de públicos-alvo que usam o [Política de mesclagem ativa na borda](../../segmentation/ui/segment-builder.md#merge-policies) defina como padrão. Se você mapear públicos-alvo que usam uma política de mesclagem diferente para destinos de borda, esses públicos-alvo não serão avaliados.

Siga as instruções em [criação de uma política de mesclagem](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)e certifique-se de ativar o **[!UICONTROL Política de mesclagem ativa na borda]** alternar.

### Criar um novo público na Platform {#create-audience}

Depois de criar o [!DNL Active-On-Edge] política de mesclagem, você deve criar um novo público na Platform.

Siga as [audience builder](../../segmentation/ui/segment-builder.md) para criar seu novo público-alvo e certifique-se de [atribuir](../../segmentation/ui/segment-builder.md#merge-policies) o [!DNL Active-On-Edge] política de mesclagem criada na etapa 3.

### Criar uma conexão de destino {#connect-destination}

Após configurar o fluxo de dados, você pode começar a configurar o destino de personalização.

Siga as [tutorial de criação de conexão de destino](../ui/connect-destination.md) para obter instruções detalhadas sobre como criar uma nova conexão de destino.

Dependendo do destino que você estiver configurando, consulte os seguintes artigos para obter os pré-requisitos específicos do destino e informações relacionadas:

* [Conexão com o Adobe Target](../catalog/personalization/adobe-target-connection.md#parameters)
* [Conexão de personalização personalizada](../catalog/personalization/custom-personalization.md##parameters)

## Selecione seu destino {#select-destination}

Após concluir os pré-requisitos, agora é possível selecionar o destino de personalização de borda a ser usado para personalização de mesma página e próxima página.

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar públicos]** no cartão correspondente ao destino de personalização em que você deseja ativar os públicos-alvo, conforme mostrado na imagem abaixo.

   ![Ativar botões](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Selecione a conexão de destino que deseja usar para ativar os públicos-alvo e selecione **[!UICONTROL Próxima]**.

   ![Selecionar destino](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Mover para a próxima seção para [selecionar seus públicos](#select-audiences).

## Selecione seus públicos-alvo {#select-audiences}

Use as caixas de seleção à esquerda dos nomes dos públicos-alvo para selecionar os públicos-alvo que você deseja ativar para o destino e selecione **[!UICONTROL Próxima]**.

Para selecionar os públicos que deseja ativar para o destino, use as caixas de seleção à esquerda dos nomes dos públicos e selecione **[!UICONTROL Próxima]**.

Você pode selecionar entre vários tipos de públicos-alvo, dependendo de sua origem:

* **[!UICONTROL Serviço de segmentação]**: públicos-alvo gerados no Experience Platform pelo serviço de segmentação. Consulte a [documentação de segmentação](../../segmentation/ui/overview.md) para obter mais detalhes.
* **[!UICONTROL Upload personalizado]**: públicos gerados fora do Experience Platform e carregados na Platform como arquivos CSV. Para saber mais sobre públicos-alvo externos, consulte a documentação em [importação de um público](../../segmentation/ui/overview.md#import-audience).
* Outros tipos de públicos-alvo, provenientes de outras soluções de Adobe, como [!DNL Audience Manager].

![Selecionar públicos](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Mapear atributos {#mapping}

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, a variável **[!UICONTROL Personalização personalizada]** o destino exige que você use o [API do servidor de rede de borda](../../server-api/overview.md) ao configurar o destino para personalização baseada em atributo. Todas as chamadas à API do servidor devem ser feitas em um [contexto autenticado](../../server-api/authentication.md).
>
><br>Se você já estiver usando o SDK da Web ou o SDK móvel para a integração, poderá recuperar atributos por meio da API do servidor adicionando uma integração do lado do servidor.
>
><br>Se você não seguir os requisitos acima, a personalização será baseada somente na associação ao público-alvo.

Selecione os atributos com base nos quais você deseja habilitar os casos de uso de personalização para seus usuários. Isso significa que se o valor de um atributo mudar ou se um atributo for adicionado a um perfil, esse perfil se tornará um membro do público-alvo e será ativado para o destino de personalização.

A adição de atributos é opcional, e você ainda pode prosseguir para a próxima etapa e ativar a personalização de mesma página e próxima página sem selecionar atributos. Se você não adicionar atributos nesta etapa, a personalização ainda ocorrerá com base na associação de público e nas qualificações do mapa de identidade para perfis.

![Imagem mostrando a etapa de mapeamento com um atributo selecionado](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Selecionar atributos de origem {#select-source-attributes}

Para adicionar atributos de origem, selecione o **[!UICONTROL Adicionar novo campo]** controle no **[!UICONTROL Campo de origem]** e pesquise ou navegue até o campo de atributo XDM desejado, conforme mostrado abaixo.

![Gravação de tela mostrando como selecionar um atributo de direcionamento na etapa de mapeamento](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Selecionar atributos de destino {#select-target-attributes}

Para adicionar atributos de destino, selecione a variável **[!UICONTROL Adicionar novo campo]** controle no **[!UICONTROL Campo de destino]** e digite o nome do atributo personalizado para o qual você deseja mapear o atributo de origem.

>[!NOTE]
>
>A seleção de atributos do target se aplica somente ao [Personalização personalizada](../catalog/personalization/custom-personalization.md) fluxo de trabalho de ativação, para oferecer suporte ao mapeamento de campos de nome amigável na plataforma de destino.

![Gravação de tela mostrando como selecionar um atributo XDM na etapa de mapeamento](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Agendar exportação de público {#scheduling}

Por padrão, a variável [!UICONTROL Programação de público] A página mostra apenas os públicos-alvo recém-selecionados que você escolheu no fluxo de ativação atual.

Para ver todos os públicos-alvo sendo ativados para o seu destino, use a opção de filtragem e desative a variável **[!UICONTROL Mostrar somente novos públicos-alvo]** filtro.

![Todos os públicos-alvo](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

No **[!UICONTROL Programação de público]** selecione cada público e use a variável **[!UICONTROL Data inicial]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

![Programação de público](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Selecionar **[!UICONTROL Próxima]** para acessar o [!UICONTROL Revisão] página.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Avaliação de política de consentimento {#consent-policy-evaluation}

Se sua organização adquiriu o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Ler sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** etapa, o Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de público-alvo até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

### Filtrar públicos {#filter-audiences}

Nesta etapa, é possível usar os filtros disponíveis na página para exibir somente os públicos-alvo cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho. Você também pode alternar quais colunas da tabela deseja visualizar.

![Gravação de tela mostrando os filtros de público-alvo disponíveis na etapa de revisão.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Se estiver satisfeito com a sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
