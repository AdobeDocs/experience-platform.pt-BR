---
title: Tags do Mailchimp
description: O destino de Tags do Mailchimp permite exportar os dados da sua conta e ativá-los no Mailchimp para interagir com os contatos.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] conexão

[[!DNL Mailchimp]](https://mailchimp.com) *(também conhecido como [!DNL Intuit Mailchimp])* é uma plataforma de automação de marketing popular e um serviço de marketing por email usado pelas empresas para gerenciar e conversar com os contatos *(clientes, clientes ou outros interessados)* usando listas de endereçamento e campanhas de marketing por email.

[!DNL Mailchimp Tags] usa [públicos-alvo](https://mailchimp.com/help/getting-started-audience/) e [marcas](https://mailchimp.com/help/getting-started-tags/) para gerenciar suas informações de contato. As marcas são etiquetas com as quais você pode organizar seus contatos e rotular para sua categorização interna em [!DNL Mailchimp].

Comparado ao [!DNL Mailchimp Interest Categories], que você usaria para classificar seus contatos com base em seus interesses e preferências, o [!DNL Mailchimp Tags] deve gerenciar assinaturas de tópicos de interesse nos quais seus contatos possam estar interessados. *Observação: a Experience Platform também tem uma conexão para [!DNL Mailchimp Interest Categories]. Você pode fazer o check-out na página [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md).*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aproveita o ponto de extremidade [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/). Você pode **adicionar novos contatos** ou **atualizar marcas de [!DNL Mailchimp] contatos** existentes em um público-alvo [!DNL Mailchimp] existente depois de ativá-los em um novo público-alvo. [!DNL Mailchimp Tags] usa os nomes de público selecionados do Experience Platform como os nomes de marca em [!DNL Mailchimp].

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Mailchimp Tags], veja um exemplo de caso de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de vendas de uma organização deseja transmitir uma campanha de marketing por email para uma lista de contatos com curadoria. As listas de contato são recebidas em lotes de diferentes fontes offline e, portanto, precisam ser rastreadas. A equipe identifica um público-alvo [!DNL Mailchimp] existente e começa a criar os públicos-alvo da Experience Platform aos quais os contatos de cada lista são adicionados. Depois de enviar esses públicos-alvo para [!DNL Mailchimp Tags], se algum contato não existir no público-alvo [!DNL Mailchimp] selecionado, ele será adicionado com uma marca associada que inclui o nome do público ao qual o contato pertence. Se já existirem contatos no público-alvo [!DNL Mailchimp], uma nova tag com o nome do público-alvo será adicionada. Como os rótulos estão visíveis no [!DNL Mailchimp], as fontes offline são facilmente identificáveis. Depois que os dados são enviados para [!DNL Mailchimp], eles enviam o email da campanha de marketing para o público.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para quaisquer pré-requisitos que você precise configurar no Experience Platform e [!DNL Mailchimp] e para obter as informações que você precisa coletar antes de trabalhar com o destino [!DNL Mailchimp Tags].

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar dados para o destino [!DNL Mailchimp Tags], você deve ter um [esquema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) e [públicos-alvo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=pt-BR) criados em [!DNL Experience Platform].

### Pré-requisitos para o destino [!DNL Mailchimp Tags] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados do Experience Platform para sua conta do [!DNL Mailchimp Tags]:

#### Você precisa ter uma conta [!DNL Mailchimp] {#prerequisites-account}

Antes de criar um destino [!DNL Mailchimp Tags], primeiro verifique se você tem uma conta [!DNL Mailchimp]. Caso ainda não tenha uma, visite a [[!DNL Mailchimp] página de inscrição](https://login.mailchimp.com/signup/) para registrar-se e criar sua conta.

#### Coletar a chave de API [!DNL Mailchimp] {#gather-credentials}

Você precisa da sua [!DNL Mailchimp] **chave de API** para autenticar o destino [!DNL Mailchimp Interest Categories] em relação à sua conta [!DNL Mailchimp]. A **chave de API** serve como **senha** quando você [autentica o destino](#authenticate).

Se você não tiver a **chave de API**, entre na sua conta [!DNL Mailchimp] e consulte a documentação do [!DNL Mailchimp] sobre [como gerar a sua chave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Um exemplo de uma chave de API é `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se você gerar a **chave de API**, anote-a, pois não será possível acessá-la após a geração.

#### Identificar o data center do [!DNL Mailchimp] {#identify-data-center}

Em seguida, você deve identificar seu data center do [!DNL Mailchimp]. Para fazer isso, faça logon na sua conta do [!DNL Mailchimp] e navegue até a **seção de chaves de API** da sua conta.

A ID do data center é a primeira seção do URL que você vê no navegador. Se a URL for *https://`us14`.mailchimp.com/account/api/*, o data center será `us14`.

A ID do data center também é anexada à sua chave de API no formato *key-dc*; Por exemplo, se sua chave de API for `0123456789abcdef0123456789abcde-us14`, o data center será `us14`.

Anote o valor do data center *(`us14` neste exemplo)*. Você precisará desse valor quando [preencher os detalhes de destino](#destination-details).

Se você precisar de mais orientação, consulte a [[!DNL Mailchimp] documentação sobre fundamentos](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Medidas de proteção {#guardrails}

Consulte os [!DNL Mailchimp] [limites de taxa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) para obter informações detalhadas sobre os limites impostos pela API [!DNL Mailchimp].

## Identidades suportadas {#supported-identities}

[!DNL Mailchimp] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | O endereço de email do contato. | Obrigatório |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | <ul><li>Você está exportando todos os membros de um público-alvo, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campos.</li><li> Para cada público selecionado no Experience Platform, o status do segmento [!DNL Mailchimp Tags] correspondente é atualizado com o status do público do Experience Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Em **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, procure por [!DNL Mailchimp Tags]. Como alternativa, você pode localizá-lo na categoria **[!UICONTROL Email marketing]**.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Connect to destination]**.

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Username]** | Seu nome de usuário [!DNL Mailchimp]. |
| **[!UICONTROL Password]** | Sua [!DNL Mailchimp] **chave de API**, que você anotou na seção [Coletar [!DNL Mailchimp] credenciais](#gather-credentials).<br> Sua chave de API assume a forma de `{KEY}-{DC}`, em que a parte `{KEY}` se refere ao valor anotado na seção [[!DNL Mailchimp] chave de API](#gather-credentials) e a parte `{DC}` se refere ao [[!DNL Mailchimp] data center](#identify-data-center). <br>Você pode fornecer a parte `{KEY}` ou todo o formulário.<br> Por exemplo, se a sua chave de API for <br>*`0123456789abcdef0123456789abcde-us14`*,<br> você pode fornecer *`0123456789abcdef0123456789abcde`*ou *`0123456789abcdef0123456789abcde-us14`*como o valor. |

{style="table-layout:auto"}

![Captura de tela da interface do Experience Platform mostrando como autenticar.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá um status **[!UICONTROL Connected]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela da interface do Experience Platform mostrando os detalhes do destino.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Name]** | Um nome pelo qual você reconhecerá este destino no futuro. |
| **[!UICONTROL Description]** | Uma descrição que ajudará você a identificar esse destino no futuro. |
| **[!UICONTROL Data center]** | Sua conta [!DNL Mailchimp] do `data center`. Consulte a seção [Identificar [!DNL Mailchimp] data center](#identify-data-center) para obter qualquer orientação. |
| **[!UICONTROL Audience Name (Please enter Data center first)]** | Após inserir sua **[!UICONTROL Data center]**, essa lista suspensa é preenchida automaticamente com os nomes de público-alvo da sua conta [!DNL Mailchimp]. Selecione o público que deseja atualizar com os dados do Experience Platform. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar públicos-alvo para destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente seus dados de público-alvo do Adobe Experience Platform para o destino [!DNL Mailchimp Tags], é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste na criação de um link entre os campos do esquema do Experience Data Model (XDM) na sua conta do Experience Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para os campos de destino [!DNL Mailchimp Tags], siga as etapas abaixo:

1. Na etapa **[!UICONTROL Mapping]**, selecione **[!UICONTROL Add new mapping]**. Você verá uma nova linha de mapeamento na tela.
1. Na janela **[!UICONTROL Select source field]**, escolha **[!UICONTROL Select identity namespace]** e selecione o namespace de identidade `Email`.

   ![Captura de tela da interface do usuário do Experience Platform com o campo do Source como Email do namespace de identidade.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. Na janela **[!UICONTROL Select target field]**, escolha **[!UICONTROL Select identity namespace]** e selecione o namespace de identidade `Email`.

   ![Captura de tela da interface do usuário do Experience Platform com o campo Direcionamento como Email do namespace de identidade.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Os mapeamentos entre seu esquema de perfil XDM e [!DNL Mailchimp Tags] serão como abaixo:

   | Campo de origem | Campo de público alvo | Obrigatório |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | Sim |

   Um exemplo com os mapeamentos concluídos é mostrado abaixo:
   ![Exemplo de captura de tela da interface do Experience Platform mostrando mapeamentos de campo.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Next]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Faça logon em sua conta do [[!DNL Mailchimp]](https://login.mailchimp.com/). Em seguida, navegue até a página **[!DNL Audience]** > **[!DNL All Contacts]** e verifique se os contatos do público foram adicionados e se os contatos do público foram atualizados com o nome do público.
   ![Captura de tela da interface do usuário do Mailchimp mostrando a página Público-alvo.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Consulte a [[!DNL Mailchimp] página de erros](https://mailchimp.com/developer/marketing/docs/errors/) para obter uma lista abrangente do status e dos códigos de erro com explicações.

## Recursos adicionais {#additional-resources}

Informações adicionais úteis da documentação do [!DNL Mailchimp] estão abaixo:

* [Introdução ao [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Introdução aos públicos-alvo](https://mailchimp.com/help/getting-started-audience/)
* [Criar um público-alvo](https://mailchimp.com/help/create-audience/)
* [Introdução às Tags](https://mailchimp.com/help/getting-started-tags/)
* [API de marketing](https://mailchimp.com/developer/marketing/api/)
