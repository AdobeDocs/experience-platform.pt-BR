---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Correspondência de segmentos;correspondência de segmentos
solution: Experience Platform
title: Visão geral da correspondência de segmentos
description: A Correspondência de segmentos é um serviço de compartilhamento de segmentos no Adobe Experience Platform que permite que dois ou mais usuários da Platform troquem dados de segmento de maneira segura, controlada e compatível com a privacidade.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 2%

---

# Visão geral do [!DNL Segment Match]

A correspondência de segmentos do Adobe Experience Platform é um serviço de compartilhamento de segmentos que permite que dois ou mais usuários da Platform troquem dados de segmento de maneira segura, controlada e compatível com a privacidade. [!DNL Segment Match] O usa padrões de privacidade da Platform e identificadores pessoais, como emails com hash, números de telefone com hash e identificadores de dispositivos, como IDFAs e GAIDs.

Com [!DNL Segment Match] você pode:

* Gerencie o processo de sobreposição de identidade.
* Exibir estimativas pré-compartilhamento.
* Aplique rótulos de uso de dados para controlar se os dados podem ser compartilhados com parceiros.
* Mantenha o gerenciamento do ciclo de vida do público compartilhado após a publicação de um feed e continue uma troca dinâmica de dados por meio das capacidades de adicionar, excluir e cancelar o compartilhamento.

[!DNL Segment Match] O usa um processo de sobreposição de identidade para garantir que o compartilhamento de segmentos seja feito de maneira segura e com foco na privacidade. Um **identidade sobreposta** é uma identidade que tem uma correspondência no segmento e no segmento do parceiro selecionado. Antes de compartilhar um segmento entre um remetente e um destinatário, o processo de sobreposição de identidade verifica se há uma sobreposição nos namespaces e verificações de consentimento entre o remetente e o(s) destinatário(s). Ambas as verificações de sobreposição devem ser aprovadas para que um segmento seja compartilhado.

As seções a seguir fornecem mais informações sobre [!DNL Segment Match], incluindo detalhes sobre a configuração e seu fluxo de trabalho completo.

## Configuração

As seções a seguir descrevem como instalar e configurar [!DNL Segment Match]:

### Configurar namespaces e dados de identidade {#namespaces}

O primeiro passo para começar a usar o [!DNL Segment Match] é para garantir que você esteja assimilando dados nos namespaces de identidade compatíveis.

Os namespaces de identidade são um componente de [Serviço de identidade da Adobe Experience Platform](../../../identity-service/home.md). Cada identidade do cliente contém um namespace associado que indica o contexto da identidade. Por exemplo, um namespace pode distinguir um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Ao corresponder dados de registro em fragmentos de perfil (como quando [!DNL Real-Time Customer Profile] mescla (Dados do perfil), o valor da identidade e o namespace devem corresponder.

No contexto da [!DNL Segment Match], os namespaces são usados no processo de sobreposição ao compartilhar dados.

A lista de namespaces compatíveis é a seguinte:

| Namespace | Descrição |
| --------- | ----------- |
| Emails (SHA256, em letras minúsculas) | Um namespace para o endereço de email com hash prévio. Os valores fornecidos neste namespace são convertidos em minúsculas antes do hash com SHA256. Espaços à esquerda e à direita precisam ser cortados antes da normalização de um endereço de email. Esta configuração não pode ser alterada retroativamente. A Platform oferece dois métodos de suporte a hash na coleta de dados, por meio de [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) e até [preparação de dados](../../../data-prep/functions.md#hashing). |
| Telefone (SHA256_E.164) | Um namespace que representa números de telefone brutos que precisam de hash usando os formatos SHA256 e E.164. |
| ECID | Um namespace que representa um valor de ID de Experience Cloud (ECID). Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte a [Visão geral da ECID](../../../identity-service/ecid.md) para obter mais informações. |
| Apple IDFA (ID para anunciantes) | Um namespace que representa a Apple ID para anunciantes. Consulte o seguinte documento em [anúncios baseados em interesses](https://support.apple.com/en-us/HT202074) para obter mais informações. |
| ID de anúncio do Google | Um namespace que representa uma ID de anúncio do Google. Consulte o seguinte documento em [ID de publicidade do Google](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obter mais informações. |

### Definir configuração de consentimento

Você deve fornecer uma configuração de consentimento e definir seu valor padrão como `opt-in` ou `opt-out` para verificar o consentimento.

A verificação de consentimento de aceitação e recusa determina se você pode operar com o consentimento para compartilhar dados do usuário por padrão. Se o padrão de configuração de consentimento estiver definido como `opt-out`, os dados do usuário poderão ser compartilhados, a menos que um usuário recuse explicitamente o uso. Se o padrão estiver definido como `opt-in`, os dados do usuário não poderão ser compartilhados, a menos que um usuário faça o opt-in explicitamente.

A configuração de consentimento padrão para [!DNL Segment Match] está definida como `opt-out`. Para aplicar um modelo de aceitação para seus dados, envie uma solicitação por email para a equipe de conta do Adobe.

Para obter mais informações sobre o `share` atributo usado para definir o valor de consentimento de compartilhamento de dados, consulte a seguinte documentação sobre [grupo de campos privacidade e consentimentos](../../../xdm/field-groups/profile/consents.md). Para obter informações sobre o grupo de campos específico usado para registrar o consentimento do consumidor para a coleta e uso de dados relacionados à privacidade, personalização e preferências de marketing, consulte o seguinte [Consentimento para privacidade, personalização e preferências de marketing Exemplo do GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configurar rótulos de uso de dados

O último pré-requisito que você deve estabelecer é configurar um novo rótulo de uso de dados para impedir o compartilhamento de dados. Por meio dos rótulos de uso de dados, é possível gerenciar quais dados podem ser compartilhados por meio do [!DNL Segment Match].

Os rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles forem assimilados no Experience Platform ou assim que os dados estiverem disponíveis para uso na plataforma.

[!DNL Segment Match] usa o rótulo C11, um rótulo de contrato específico para [!DNL Segment Match] que você pode adicionar manualmente a qualquer conjunto de dados ou atributo para garantir que eles sejam excluídos da [!DNL Segment Match] processo de compartilhamento de parceiros. O rótulo C11 indica dados que não devem ser usados em [!DNL Segment Match] processos. Depois de determinar de quais conjuntos de dados e/ou campos você deseja excluir [!DNL Segment Match] e adicionada a etiqueta C11 de acordo, a etiqueta é automaticamente aplicada pela [!DNL Segment Match] fluxo de trabalho. [!DNL Segment Match] ativa automaticamente a variável [!UICONTROL Restringir compartilhamento de dados] política principal. Para obter instruções específicas sobre como aplicar rótulos de uso de dados a conjuntos de dados, consulte o tutorial em [gerenciamento de rótulos de uso de dados na interface](../../../data-governance/labels/user-guide.md).

Para obter uma lista de rótulos de uso de dados e suas definições, consulte [glossário de rótulos de uso de dados](../../../data-governance/labels/reference.md). Para obter informações sobre políticas de uso de dados, consulte a [visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

### Noções básicas [!DNL Segment Match] permissões

Há duas permissões associadas a [!DNL Segment Match]:

| Permissão | Descrição |
| --- | --- |
| Gerenciar conexões de compartilhamento de público | Essa permissão permite concluir o processo de handshake de parceiro, que conecta duas organizações para habilitar o [!DNL Segment Match] fluxos. |
| Gerenciar compartilhamentos de público | Essa permissão permite criar, editar e publicar feeds (o pacote de dados usado para [!DNL Segment Match]) com parceiros ativos (parceiros que foram conectados pelo usuário administrador com **[!UICONTROL Conexões de compartilhamento de público]** acesso). |

Consulte a [visão geral do controle de acesso](../../../access-control/home.md) para obter mais informações sobre controle de acesso e permissões.

## [!DNL Segment Match] fluxo de trabalho completo

Após configurar os dados de identidade e namespaces, a configuração de consentimento e o rótulo de uso de dados, você pode começar a trabalhar com [!DNL Segment Match] e seus recursos.

### Gerenciar parceiro

Na interface do usuário da Platform, selecione **[!UICONTROL Segmentos]** no menu de navegação esquerdo e selecione **[!UICONTROL Feeds]** no cabeçalho superior.

![segments-feed.png](./images/segments-feed.png)

A variável [!UICONTROL Feeds] A página contém uma lista de feeds recebidos de parceiros do, bem como feeds compartilhados. Para exibir uma lista de parceiros existentes ou estabelecer uma conexão com um novo parceiro, selecione **[!UICONTROL Gerenciar parceiros]**.

![manage-partners.png](./images/manage-partners.png)

Uma conexão entre dois parceiros é um &quot;handshake bidirecional&quot; que atua como um método de autoatendimento para que os usuários conectem suas organizações da Platform em conjunto no nível da sandbox. A conexão é necessária para informar à Platform que um contrato foi estabelecido e que a Platform pode facilitar o compartilhamento de serviços entre você e seu(s) parceiro(s).

>[!NOTE]
>
>O &quot;aperto de mão bidirecional&quot; entre você e seu parceiro é estritamente uma conexão. Nenhum dado é trocado durante esse processo.

Você pode exibir uma lista de conexões com parceiros existentes na interface principal do [!UICONTROL Gerenciar parceiros] tela. No painel direito está a variável [!UICONTROL Configuração de compartilhamento] painel, que oferece a opção de gerar uma nova [!UICONTROL ID de conexão] bem como uma caixa de entrada onde você pode inserir o nome de um parceiro [!UICONTROL ID de conexão].

![estabelecer-conexão.png](./images/establish-connection.png)

Para criar um novo [!UICONTROL ID de conexão], selecione **[!UICONTROL Regenerar]** em [!UICONTROL Configuração de compartilhamento] e selecione o ícone copiar ao lado da ID recém-gerada.

![share-setting.png](./images/share-setting.png)

Para conectar um parceiro usando sua [!UICONTROL ID de conexão], insira o valor do identificador exclusivo na caixa de entrada em [!UICONTROL Conectar parceiro] e selecione **[!UICONTROL Solicitação]**.

![connect-partner.png](./images/connect-partner.png)

### Criar feed {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Casos de uso de marketing restritos"
>abstract="Casos de uso restritos de marketing ajudam a fornecer orientação aos parceiros para garantir que os segmentos compartilhados sejam usados adequadamente de acordo com as restrições de governança de dados."
>text="Learn more in documentation"

A **feed** é um agrupamento de dados (segmentos), as regras de como esses dados podem ser expostos ou usados e as configurações que determinam como os dados são comparados com os dados de seus parceiros. Um feed pode ser gerenciado de forma independente e trocado com outros usuários da Platform por meio de [!DNL Segment Match].

Para criar um novo feed, selecione **[!UICONTROL Criar feed]** do [!UICONTROL Feeds] painel.

![create-feed.png](./images/create-feed.png)

A configuração básica de um feed inclui um nome, uma descrição e configurações relacionadas a casos de uso de marketing e configurações de identidade. Forneça um nome e uma descrição para o feed e aplique os casos de uso de marketing dos quais deseja que os dados sejam excluídos. Você pode selecionar mais de um caso de uso em uma lista que inclui:

* [!UICONTROL Analytics]
* [!UICONTROL Combinar com PII]
* [!UICONTROL Direcionamento entre sites]
* [!UICONTROL Ciência de dados]
* [!UICONTROL Direcionamento de email]
* [!UICONTROL Exportar para terceiros]
* [!UICONTROL Publicidade no local]
* [!UICONTROL Personalização no local]
* [!UICONTROL Correspondência de segmentos]
* [!UICONTROL Personalização de identidade única]

Por fim, selecione os namespaces de identidade apropriados para seu feed. Para obter informações sobre os namespaces específicos compatíveis com o [!DNL Segment Match], consulte o [dados de identidade e tabela de namespaces](#namespaces). Quando terminar, selecione **[!UICONTROL Próxima]**.

![audience-sharing.png](./images/audience-sharing.png)

Depois de estabelecer as configurações do feed, selecione os segmentos que deseja compartilhar na lista de segmentos primários. É possível selecionar mais de um segmento na lista e usar o painel direito para gerenciar a lista de segmentos selecionados. Quando terminar, selecione **[!UICONTROL Próxima]**.

![select-segments.png](./images/select-segments.png)

A variável [!UICONTROL Compartilhar] é exibida, fornecendo uma interface para selecionar os parceiros com os quais deseja compartilhar o feed. Durante essa etapa, você também pode exibir o relatório de estimativas de sobreposição pré-compartilhamento e ver o número de identidades sobrepostas por namespace entre você e seu parceiro, o número de identidades sobrepostas que têm consentimento para compartilhar dados.

Selecionar **[!UICONTROL Analisar por segmento]** para ver o relatório de estimativas.

![analyze.png](./images/analyze.png)

O relatório de estimativas de sobreposição permite gerenciar verificações de sobreposição e consentimento por parceiro e por segmento antes de compartilhar o feed.

| Métricas | Descrição |
| ------- | ----------- |
| Estimativa de identidades com consentimento | O número total de identidades sobrepostas que atendem aos requisitos de consentimento configurados para sua organização. |
| Estimativa de identidades sobrepostas | O número de identidades qualificadas para o segmento selecionado e que também têm uma correspondência com o parceiro selecionado. Essas identidades são exibidas por namespace e não representam identidades de perfil individuais. As estimativas de sobreposição se baseiam em rascunhos de perfil. |

Quando terminar, selecione **[!UICONTROL Fechar]**.

![overlap-report.png](./images/overlap-report.png)

Depois de selecionar seus parceiros e visualizar seu relatório de estimativas de sobreposição, selecione **[!UICONTROL Próxima]** para continuar.

![share.png](./images/share.png)

A variável [!UICONTROL Revisão] é exibida, permitindo que você revise o novo feed antes que ele seja compartilhado e publicado. Esta etapa inclui detalhes sobre a configuração de identidade aplicada, bem como informações sobre os casos de uso de marketing, segmentos e parceiros selecionados.

Selecionar **[!UICONTROL Concluir]** para continuar.

![review.png](./images/review.png)

### Atualizar feed

Para adicionar ou remover segmentos, selecione **[!UICONTROL Criar feed]** do [!UICONTROL Feeds] e selecione **[!UICONTROL Feed existente]**. Na lista de feeds existentes exibida, selecione o feed que deseja atualizar e selecione **[!UICONTROL Próxima]**.

![lista de feeds](./images/feed-list.png)

A lista de segmentos é exibida. Aqui, você pode adicionar novos segmentos ao feed e usar o painel direito para remover os segmentos que não são mais necessários. Quando terminar de gerenciar os segmentos no feed, selecione **[!UICONTROL Próxima]** e siga as etapas descritas acima para concluir o feed atualizado.

![update](./images/update.png)

>[!NOTE]
>
>Quando você adiciona ou remove um segmento de um feed compartilhado, o parceiro destinatário deve confirmar a alteração reativando o [!DNL Profile] alternar na lista de feeds recebidos.

### Aceitar um feed recebido

Para exibir um feed de entrada, selecione **[!UICONTROL Recebido]** no cabeçalho do [!UICONTROL Feeds] e selecione o feed que deseja exibir na lista. Para aceitar o feed, selecione **[!UICONTROL Ativar para perfil]** e aguarde alguns instantes para que o status seja atualizado de [!UICONTROL Pending] para [!UICONTROL Ativado].

![received.png](./images/received.png)

Depois de aceitar um feed compartilhado, você pode começar a usar os dados compartilhados para criar novos segmentos.

## Próximas etapas

Ao ler este documento, você compreendeu o [!DNL Segment Match], seus recursos e seu fluxo de trabalho completo. Consulte os seguintes documentos para saber mais sobre outros serviços da plataforma:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [Visão geral do [!DNL Real-Time Customer Profile]](../../../profile/home.md)
