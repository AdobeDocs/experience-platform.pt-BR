---
title: Tags do Mailchimp
description: O destino de Tags do Mailchimp permite exportar os dados da sua conta e ativá-los no Mailchimp para interagir com os contatos.
source-git-commit: b32d619b78502e38e98a410bd14379992543c63c
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] conexão

[[!DNL Mailchimp]](https://mailchimp.com) *(também conhecido como [!DNL Intuit Mailchimp])* é uma plataforma de automação de marketing popular e um serviço de marketing por email usado pelas empresas para gerenciar e conversar com contatos *(clientes, clientes ou outras partes interessadas)* usando listas de endereçamento e campanhas de marketing por email.

[!DNL Mailchimp Tags] usos [públicos](https://mailchimp.com/help/getting-started-audience/) e [tags](https://mailchimp.com/help/getting-started-tags/) para gerenciar suas informações de contato. Tags são rótulos que usam os quais você pode organizar seus contatos e rotulá-los para sua categorização interna dentro do [!DNL Mailchimp].

Comparado a [!DNL Mailchimp Interest Categories] que você usaria para classificar seus contatos com base em seus interesses e preferências, [!DNL Mailchimp Tags] O é destinado a gerenciar assinaturas de tópicos de interesse nos quais seus contatos possam estar interessados. *Observe que o Experience Platform também tem uma conexão para [!DNL Mailchimp Interest Categories], você pode conferir no [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) página.*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) terminal. Você pode **adicionar novos contatos** ou **atualizar tags de existentes [!DNL Mailchimp] contatos** em um existente [!DNL Mailchimp] após ativá-los em um novo público-alvo. [!DNL Mailchimp Tags] O usa os nomes de público-alvo selecionados da Platform como os nomes de tag no [!DNL Mailchimp].

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Mailchimp Tags] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de vendas de uma organização deseja transmitir uma campanha de marketing por email para uma lista de contatos com curadoria. As listas de contato são recebidas em lotes de diferentes fontes offline e, portanto, precisam ser rastreadas. A equipe identifica uma [!DNL Mailchimp] e começa a criar os públicos-alvo do Experience Platform nos quais os contatos de cada lista são adicionados. Depois de enviar esses públicos-alvo para o [!DNL Mailchimp Tags], se algum contato não existir no [!DNL Mailchimp] público-alvo, eles são adicionados com uma tag associada que inclui o nome do público-alvo ao qual o contato pertence. Se algum contato já existir no [!DNL Mailchimp] público-alvo: uma nova tag com o nome do público-alvo é adicionada. Como os rótulos são visíveis no [!DNL Mailchimp] as fontes offline são facilmente identificáveis. Depois que os dados forem enviados para o [!DNL Mailchimp] eles enviam o email da campanha de marketing para o público-alvo.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para obter os pré-requisitos que você precisa configurar no Experience Platform e [!DNL Mailchimp] e para obter as informações que você precisa coletar antes de trabalhar com a [!DNL Mailchimp Tags] destino.

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Mailchimp Tags] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [públicos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) criado em [!DNL Experience Platform].

### Pré-requisitos para a [!DNL Mailchimp Tags] destino {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados da Platform para o seu [!DNL Mailchimp Tags] conta:

#### Você precisa ter um [!DNL Mailchimp] account {#prerequisites-account}

Antes de criar um [!DNL Mailchimp Tags] destino, você deve primeiro garantir que tenha um [!DNL Mailchimp] conta. Se você ainda não tiver um, visite o [[!DNL Mailchimp] página de inscrição](https://login.mailchimp.com/signup/) para registrar e criar sua conta.

#### Coletar [!DNL Mailchimp] Chave de API {#gather-credentials}

Você precisa do seu [!DNL Mailchimp] **Chave de API** para autenticar o [!DNL Mailchimp Interest Categories] destino em relação ao seu [!DNL Mailchimp] conta. A variável **Chave de API** serve como **Senha** quando você [autenticar o destino](#authenticate).

Se você não tiver seu **Chave de API**, faça logon no [!DNL Mailchimp] conta e consulte o [!DNL Mailchimp] documentação sobre [como gerar sua chave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Um exemplo de uma chave de API é `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se você gerar a variável **Chave de API**, anote-o, pois você não poderá acessá-lo após a geração.

#### Identifique o seu [!DNL Mailchimp] data center {#identify-data-center}

Em seguida, você deve identificar o [!DNL Mailchimp] data center. Para fazer isso, faça logon no [!DNL Mailchimp] e navegue até a página **Seção de chaves de API** da sua conta.

A ID do data center é a primeira seção do URL que você vê no navegador. Se o URL for *https://`us14`.mailchimp.com/account/api/*, o data center será `us14`.

A ID do data center também é anexada à sua chave de API no formulário *key-dc*; Por exemplo, se sua chave de API for `0123456789abcdef0123456789abcde-us14`, o data center será `us14`.

Anote o valor do data center *(`us14` neste exemplo)*. Você precisará desse valor quando [preencher os detalhes do destino](#destination-details).

Se precisar de mais orientação, consulte o [[!DNL Mailchimp] Documentação de fundamentos](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Medidas de proteção {#guardrails}

Consulte a [!DNL Mailchimp] [limites de taxa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) para obter informações detalhadas sobre os limites impostos pela [!DNL Mailchimp] API.

## Identidades suportadas {#supported-identities}

[!DNL Mailchimp] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | O endereço de email do contato. | Obrigatório |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um público-alvo, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada público selecionado na Platform, a variável correspondente [!DNL Mailchimp Tags] O status do segmento é atualizado com o status do público-alvo da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar [!DNL Mailchimp Tags]. Como alternativa, você pode localizá-lo na **[!UICONTROL Marketing por email]** categoria.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Conectar ao destino]**.

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome de usuário]** | Seu [!DNL Mailchimp] usuário. |
| **[!UICONTROL Senha]** | Seu [!DNL Mailchimp] **Chave de API**, que você anotou na [Coletar [!DNL Mailchimp] credenciais](#gather-credentials) seção.<br> Sua chave de API assume a forma de `{KEY}-{DC}`, em que o `{KEY}` porção refere-se ao valor anotado na variável [[!DNL Mailchimp] Chave de API](#gather-credentials) seção e o `{DC}` parte refere-se à [[!DNL Mailchimp] data center](#identify-data-center). <br>Você pode fornecer a variável `{KEY}` parte ou o formulário inteiro.<br> Por exemplo, se sua chave de API for <br>*`0123456789abcdef0123456789abcde-us14`*,<br> você pode fornecer *`0123456789abcdef0123456789abcde`*ou *`0123456789abcdef0123456789abcde-us14`*como o valor. |

{style="table-layout:auto"}

![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | Um nome pelo qual você reconhecerá este destino no futuro. |
| **[!UICONTROL Descrição]** | Uma descrição que ajudará você a identificar esse destino no futuro. |
| **[!UICONTROL Centro de dados]** | Seu [!DNL Mailchimp] account `data center`. Consulte a [Identificar [!DNL Mailchimp] data center](#identify-data-center) para obter orientação. |
| **[!UICONTROL Nome do público-alvo (insira o data center primeiro)]** | Depois de inserir seu **[!UICONTROL Centro de dados]**, essa lista suspensa é preenchida automaticamente com os nomes dos públicos-alvo da [!DNL Mailchimp] conta. Selecione o público que deseja atualizar com os dados da Platform. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar públicos para destinos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Mailchimp Tags] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL Mailchimp Tags] campos de destino, siga as etapas abaixo:

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha **[!UICONTROL Selecionar namespace de identidade]** e selecione o `Email` namespace de identidade.

   ![Captura de tela da interface do usuário da plataforma com o campo Origem como Email do namespace de identidade.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. No **[!UICONTROL Selecionar campo de destino]** escolha **[!UICONTROL Selecionar namespace de identidade]** e selecione o `Email` namespace de identidade.

   ![Captura de tela da interface do usuário da plataforma com o campo Target como email do namespace de identidade.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Os mapeamentos entre o esquema de perfil XDM e o [!DNL Mailchimp Tags] será conforme abaixo: | Campo de origem | Campo de destino | Obrigatório | | — | — | — | |`IdentityMap: Email`|`Identity: Email`| Sim |

   Um exemplo com os mapeamentos concluídos é mostrado abaixo:
   ![Exemplo de captura de tela da interface do usuário do Platform mostrando mapeamentos de campo.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Faça logon no [[!DNL Mailchimp]](https://login.mailchimp.com/) conta. Em seguida, navegue até o **[!DNL Audience]** > **[!DNL All Contacts]** e verifique se os contatos do público foram adicionados e se os contatos do público foram atualizados com o nome do público.
   ![Captura de tela da interface do usuário do Mailchimp mostrando a página Público-alvo.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Consulte a [[!DNL Mailchimp] página de erros](https://mailchimp.com/developer/marketing/docs/errors/) para obter uma lista abrangente de códigos de erro e status com explicações.

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [!DNL Mailchimp] A documentação do está abaixo:
* [Introdução ao [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Introdução ao Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Criar um público-alvo](https://mailchimp.com/help/create-audience/)
* [Introdução às tags](https://mailchimp.com/help/getting-started-tags/)
* [API de marketing](https://mailchimp.com/developer/marketing/api/)
