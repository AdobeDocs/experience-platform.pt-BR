---
keywords: Experience Platform, página inicial, tópicos populares, segmentação, Segmentação, Correspondência de segmentos, correspondência de segmentos
solution: Experience Platform
title: Visão geral da correspondência de segmentos
topic-legacy: overview
description: Correspondência de segmentos é um serviço de compartilhamento de segmentos no Adobe Experience Platform que permite que dois ou mais usuários da plataforma troquem dados de segmento de maneira segura, regida e amigável à privacidade.
source-git-commit: ee59da6c075573af366403e1059b5318fb924d21
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 1%

---


# (Beta) [!DNL Segment Match] visão geral

>[!IMPORTANT]
>
>[!DNL Segment Match] está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

A Correspondência de segmentos do Adobe Experience Platform é um serviço de compartilhamento de segmentos que permite que dois ou mais usuários da plataforma troquem dados de segmento de maneira segura, regida e amigável à privacidade. [!DNL Segment Match] O usa padrões de privacidade da plataforma e identificadores pessoais, como emails com hash, números de telefone com hash e identificadores de dispositivos, como IDFAs e GAIDs.

Com [!DNL Segment Match] você pode:

* Gerencie o processo de sobreposição de identidade.
* Exibir estimativas de pré-compartilhamento.
* Aplique rótulos de uso de dados para controlar se os dados podem ser compartilhados com parceiros.
* Manter o gerenciamento compartilhado do ciclo de vida do público-alvo após a publicação de um feed e continuar uma troca dinâmica de dados por meio de recursos para adicionar, excluir e cancelar o compartilhamento.

[!DNL Segment Match] O usa um processo de sobreposição de identidade para garantir que o compartilhamento de segmentos seja feito de maneira segura e com foco na privacidade. Uma **identidade sobreposta** é uma identidade que tem uma correspondência no segmento e no segmento do parceiro selecionado. Antes de compartilhar um segmento entre um remetente e um destinatário, o processo de sobreposição de identidade verifica se há sobreposição nos namespaces e nas verificações de consentimento entre o remetente e o destinatário. Ambas as verificações de sobreposição devem ser transmitidas para que um segmento seja compartilhado.

As seções a seguir fornecem mais informações sobre [!DNL Segment Match], incluindo detalhes sobre a configuração e seu fluxo de trabalho completo.

## Configuração

As seções a seguir descrevem como configurar e configurar [!DNL Segment Match]:

### Configurar dados de identidade e namespaces {#namespaces}

A primeira etapa para começar a usar [!DNL Segment Match] é garantir que você esteja assimilando dados nos namespaces de identidade compatíveis.

Os namespaces de identidade são um componente do [Adobe Experience Platform Identity Service](../../identity-service/home.md). Cada identidade do cliente contém um namespace associado que indica o contexto da identidade. Por exemplo, um namespace pode distinguir um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Ao corresponder dados de registro em fragmentos de perfil (como quando [!DNL Real-time Customer Profile] mescla dados de Perfil), o valor de identidade e o namespace devem corresponder.

No contexto de [!DNL Segment Match], os namespaces são usados no processo de sobreposição ao compartilhar dados.

A lista de namespaces suportados é a seguinte:

| Namespace | Descrição |
| --------- | ----------- |
| Emails (SHA256, em minúsculas) | Um namespace para endereço de email com hash prévio. Os valores fornecidos neste namespace são convertidos em minúsculas antes do hash com SHA256. Os espaços à esquerda e à direita precisam ser cortados antes que um endereço de email seja normalizado. Esta configuração não pode ser alterada retroativamente. Consulte o seguinte documento em [SHA256 hash support](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) para obter mais informações. |
| Telefone (SHA256_E.164) | Um namespace que representa números brutos de telefone que precisam ser atribuídos a hash usando os formatos SHA256 e E.164. |
| ECID | Um namespace que representa um valor de Experience Cloud ID (ECID). Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte a [Visão geral da ECID](../../identity-service/ecid.md) para obter mais informações. |
| Apple IDFA (ID para anunciantes) | Um namespace que representa Apple ID para anunciantes. Consulte o seguinte documento sobre [anúncios baseados em juros](https://support.apple.com/en-us/HT202074) para obter mais informações. |
| ID de anúncio do Google | Um namespace que representa uma ID de publicidade do Google. Consulte o seguinte documento em [ID de anúncio do Google](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obter mais informações. |

### Configurar configuração de consentimento

Você deve fornecer uma configuração de consentimento e definir seu valor padrão como `opt-in` ou `opt-out` para uma verificação de consentimento.

A verificação de consentimento de aceitação e recusa determina se você pode operar com o consentimento para compartilhar dados do usuário por padrão. Se o padrão de configuração de consentimento for definido como `opt-in`, os dados do usuário poderão ser compartilhados, a menos que um usuário recuse explicitamente a adesão. Se o padrão estiver definido como `opt-out`, os dados do usuário não poderão ser compartilhados, a menos que um usuário opte explicitamente por participar.

A configuração de consentimento padrão para [!DNL Segment Match] é definida como `opt-out`. Para aplicar um modelo de aceitação aos seus dados, envie uma solicitação por email para seu Gerente de conta do Adobe.

Para obter mais informações sobre o atributo `share` usado para definir o valor de consentimento de compartilhamento de dados, consulte a seguinte documentação sobre o [grupo de campos privacidade e consentimento](../../xdm/field-groups/profile/consents.md). Para obter informações sobre o grupo de campos específico usado para capturar o consentimento do consumidor para a coleta e o uso de dados relacionados à privacidade, personalização e preferências de marketing, consulte o seguinte [Consentimento para privacidade, personalização e preferências de marketing - exemplo do GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configurar rótulos de uso de dados

O último pré-requisito que você deve estabelecer é configurar um novo rótulo de uso de dados para impedir o compartilhamento de dados. Por meio de rótulos de uso de dados, você pode gerenciar quais dados podem ser compartilhados por meio de [!DNL Segment Match].

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados no Experience Platform ou assim que os dados forem disponibilizados para uso na plataforma.

[!DNL Segment Match] O usa o rótulo C11, um rótulo de contrato específico para o  [!DNL Segment Match] qual você pode adicionar manualmente a qualquer conjunto de dados ou atributo para garantir que eles sejam excluídos do processo de compartilhamento de  [!DNL Segment Match] parceiros. O rótulo C11 indica dados que não devem ser usados em processos [!DNL Segment Match]. Depois de determinar quais conjuntos de dados e/ou campos você deseja excluir de [!DNL Segment Match] e adicionar o rótulo C11 de acordo, o rótulo é aplicado automaticamente pelo workflow [!DNL Segment Match]. [!DNL Segment Match] ativa automaticamente a política  [!UICONTROL Restrict data ] Sharingcore . Para obter instruções específicas sobre como aplicar rótulos de uso de dados a conjuntos de dados, consulte o tutorial em [gerenciar rótulos de uso de dados na interface do usuário](../../data-governance/labels/user-guide.md).

Para obter uma lista de rótulos de uso de dados e suas definições, consulte o glossário de [rótulos de uso de dados](../../data-governance/labels/reference.md). Para obter informações sobre políticas de uso de dados, consulte a [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md).

### Como entender as permissões [!DNL Segment Match]

Há duas permissões associadas a [!DNL Segment Match]:

| Permissão | Descrição |
| --- | --- |
| Gerenciar conexões de compartilhamento de público-alvo | Essa permissão permite concluir o processo de handshake do parceiro, que conecta duas Organizações IMS para ativar os fluxos [!DNL Segment Match]. |
| Gerenciar compartilhamentos de público-alvo | Essa permissão permite criar, editar e publicar feeds (o pacote de dados usado para [!DNL Segment Match]) com parceiros ativos (parceiros que foram conectados pelo usuário administrador com acesso a **[!UICONTROL Conexões de compartilhamento de público-alvo]**). |

Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre controle de acesso e permissões.

## [!DNL Segment Match] fluxo de trabalho completo

Depois de configurar seus dados de identidade e namespaces, a configuração de consentimento e o rótulo de uso de dados, você pode começar a trabalhar com [!DNL Segment Match] e seus recursos.

### Gerenciar parceiro

Na interface do usuário da plataforma, selecione **[!UICONTROL Segmentos]** na navegação à esquerda e selecione **[!UICONTROL Feeds]** no cabeçalho superior.

![segment-feed.png](../images/ui/segment-match/segments-feed.png)

A página [!UICONTROL Feeds] contém uma lista de feeds recebidos de parceiros, bem como feeds que você compartilhou. Para exibir uma lista de parceiros existentes ou estabelecer uma conexão com um novo parceiro, selecione **[!UICONTROL Gerenciar parceiros]**.

![manage-partner.png](../images/ui/segment-match/manage-partners.png)

Uma conexão entre dois parceiros é um &quot;handshake bidirecional&quot; que funciona como um método de autoatendimento para os usuários conectarem suas organizações da Platform em um nível de sandbox. A conexão é necessária para informar à Platform que um contrato foi estabelecido e que a Platform pode facilitar o compartilhamento de serviços entre você e seu(s) parceiro(s).

>[!NOTE]
>
>O &quot;aperto de mão bidirecional&quot; entre você e seu parceiro é estritamente uma conexão. Nenhum dado é trocado durante este processo.

Você pode exibir uma lista de conexões com parceiros existentes na interface principal da tela [!UICONTROL Gerenciar parceiros]. No painel direito está o painel [!UICONTROL Compartilhar configuração], que fornece a opção de gerar um novo [!UICONTROL conectar ID], bem como uma caixa de entrada onde você pode inserir o [!UICONTROL connect ID] de um parceiro.

![estabeleça-connection.png](../images/ui/segment-match/establish-connection.png)

Para criar um novo [!UICONTROL connect ID], selecione **[!UICONTROL Restaurar]** em [!UICONTROL Compartilhar configuração] e selecione o ícone copiar ao lado do ID recém-gerado.

![share-setting.png](../images/ui/segment-match/share-setting.png)

Para conectar um parceiro usando seu [!UICONTROL connect ID], digite seu valor de ID exclusivo na caixa de entrada em [!UICONTROL Connect partner] e selecione **[!UICONTROL Request]**.

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### Criar feed

Um **feed** é um agrupamento de dados (segmentos), as regras de como esses dados podem ser expostos ou usados e as configurações que determinam como seus dados são comparados com os dados de seus parceiros. Um feed pode ser gerenciado independentemente e trocado com outros usuários da plataforma por meio de [!DNL Segment Match].

Para criar um novo feed, selecione **[!UICONTROL Criar feed]** no painel [!UICONTROL Feeds].

![create-feed.png](../images/ui/segment-match/create-feed.png)

A configuração básica de um feed inclui um nome, uma descrição e configurações relacionadas a casos de uso de marketing e configurações de identidade. Forneça um nome e uma descrição para o feed e aplique os casos de uso de marketing dos quais deseja que os dados sejam excluídos. Você pode selecionar mais de um caso de uso em uma lista que inclui:

* [!UICONTROL Analytics]
* [!UICONTROL Combinar com PII]
* [!UICONTROL Direcionamento entre sites]
* [!UICONTROL Ciência de dados]
* [!UICONTROL Direcionamento de email]
* [!UICONTROL Exportar para terceiros]
* [!UICONTROL Anúncios no site]
* [!UICONTROL Personalização no site]
* [!UICONTROL Correspondência de segmentos]
* [!UICONTROL Personalização de identidade única]

Finalmente, selecione os namespaces de identidade apropriados para seu feed. Para obter informações sobre namespaces específicos suportados por [!DNL Segment Match], consulte a [tabela de dados e namespaces de identidade](#namespaces). Quando terminar, selecione **[!UICONTROL Next]**.

![audience-sharing.png](../images/ui/segment-match/audience-sharing.png)

Depois de estabelecer as configurações do feed, selecione os segmentos que deseja compartilhar da lista de segmentos primários. É possível selecionar mais de um segmento na lista e usar o painel direito para gerenciar a lista de segmentos selecionados. Quando terminar, selecione **[!UICONTROL Next]**.

![select-segments.png](../images/ui/segment-match/select-segments.png)

A página [!UICONTROL Compartilhar] é exibida, fornecendo uma interface para selecionar os parceiros com os quais deseja compartilhar seu feed. Durante essa etapa, você também pode exibir o relatório de estimativas de sobreposição de compartilhamento anterior e ver o número de identidades sobrepostas por namespace entre você e seu parceiro, o número de identidades sobrepostas que consentiram em compartilhar dados.

Selecione **[!UICONTROL Analisar por segmento]** para ver o relatório de estimativas.

![analyze.png](../images/ui/segment-match/analyze.png)

O relatório de estimativas de sobreposição permite gerenciar verificações de sobreposição e consentimento por parceiro e por segmento antes de compartilhar o feed.

| Métricas | Descrição |
| ------- | ----------- |
| Identidades estimadas com consentimento | O número total de identidades sobrepostas que atendem aos requisitos de consentimento configurados para sua organização. |
| Estimativa de identidades sobrepostas | O número de identidades qualificadas para o segmento selecionado e que também têm uma correspondência com o parceiro selecionado. Essas identidades são exibidas pelo namespace e não representam identidades de perfil individuais. As estimativas de sobreposição são baseadas em Rascunhos de perfil. |

Quando terminar, selecione **[!UICONTROL Fechar]**.

![overlap-report.png](../images/ui/segment-match/overlap-report.png)

Após selecionar seus parceiros e visualizar seu relatório de estimativas de sobreposição, selecione **[!UICONTROL Next]** para continuar.

![share.png](../images/ui/segment-match/share.png)

A etapa [!UICONTROL Revisar] é exibida, permitindo que você revise seu novo feed antes que ele seja compartilhado e publicado. Esta etapa inclui detalhes sobre a configuração de identidade aplicada, bem como informações sobre casos de uso de marketing, segmentos e parceiros selecionados.

Selecione **[!UICONTROL Finish]** para continuar.

![review.png](../images/ui/segment-match/review.png)

### Atualizar feed

Para adicionar ou remover segmentos, selecione **[!UICONTROL Criar feed]** na página [!UICONTROL Feeds] e selecione **[!UICONTROL Feed existente]**. Na lista de feed existentes que aparece, selecione o feed que deseja atualizar e selecione **[!UICONTROL Next]**.

![lista de feeds](../images/ui/segment-match/feed-list.png)

A lista de segmentos é exibida. A partir daqui, você pode adicionar novos segmentos ao seu feed e pode usar o painel direito para remover quaisquer segmentos que não sejam mais necessários. Depois de concluir o gerenciamento dos segmentos no feed, selecione **[!UICONTROL Next]** e siga as etapas descritas acima para concluir o feed atualizado.

![atualizar](../images/ui/segment-match/update.png)

>[!NOTE]
>
>Ao adicionar ou remover um segmento de um feed compartilhado, o parceiro de recebimento deve confirmar a alteração, habilitando novamente o botão [!DNL Profile] em sua lista de feeds recebidos.

### Aceitar um feed de entrada

Para exibir um feed de entrada, selecione **[!UICONTROL Received]** no cabeçalho da página [!UICONTROL Feeds] e selecione o feed que deseja visualizar na lista. Para aceitar o feed, selecione **[!UICONTROL Ativar para perfil]** e aguarde alguns instantes para que o status seja atualizado de [!UICONTROL Pendente] para [!UICONTROL Ativado].

![receive.png](../images/ui/segment-match/received.png)

Depois de aceitar um feed compartilhado, você pode começar a usar os dados compartilhados para criar novos segmentos.

## Próximas etapas

Ao ler este documento, você aprendeu a entender [!DNL Segment Match], seus recursos e seu fluxo de trabalho completo. Consulte os seguintes documentos para saber mais sobre outros serviços da plataforma:

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] visão geral](../../profile/home.md)
