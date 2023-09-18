---
title: Categorias de interesse do Mailchimp
description: O Mailchimp (também conhecido como Intuit Mailchimp) é uma plataforma de automação de marketing popular e um serviço de marketing por email usado pelas empresas para gerenciar e conversar com contatos (clientes, clientes ou outras partes interessadas) usando listas de endereçamento e campanhas de marketing por email. Use esse conector para classificar seus contatos com base em seus interesses e preferências.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 2%

---

# Conexão com o [!DNL Mailchimp Interest Categories]

[[!DNL Mailchimp]](https://mailchimp.com) é uma plataforma de automação de marketing popular e um serviço de marketing por email usado pelas empresas para gerenciar e conversar com contatos *(clientes, clientes ou outras partes interessadas)* usando listas de endereçamento e campanhas de marketing por email. Use esse conector para classificar seus contatos com base em seus interesses e preferências.

[!DNL Mailchimp Interest Categories] usos [públicos](https://mailchimp.com/help/getting-started-audience/), [grupos](https://mailchimp.com/help/getting-started-with-groups/), e categorias de juros *(também conhecidos como nomes de grupo ou títulos de grupo)*. Each [!DNL Mailchimp] grupo é uma lista de categorias de interesse. Os contatos são associados a uma categoria de interesse quando assinam uma ou mais categorias de interesse por meio de um formulário de inscrição em seu site. Em um público-alvo, você também pode organizar os contatos em grupos e associá-los a categorias de interesse, que podem ser usadas para criar segmentos. Você pode usar esses públicos para transmitir emails de campanha direcionados aos contatos inscritos.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) usa o [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API a ser criada [categorias de juros](https://mailchimp.com/developer/marketing/api/interest-categories/) e, em seguida, adicione contatos de cada um dos públicos-alvo selecionados da Platform em uma categoria de interesse correspondente. Você pode **adicionar novos contatos** ou **atualizar as informações de [!DNL Mailchimp] contatos**, depois **adicione-os ou remova-os dos grupos desejados** em um existente [!DNL Mailchimp] público-alvo depois de ativá-los em um novo segmento. [!DNL Mailchimp Interest Groups] O usa os nomes de público-alvo selecionados da Platform como categorias de interesse no [!DNL Mailchimp].

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Mailchimp Interest Categories] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de vendas de um site de artigos esportivos quer transmitir uma campanha de marketing por email para uma lista de contatos que se identificaram como interessados em futebol. As listas de contatos são segregadas como lotes na exportação de dados recebida da equipe de desenvolvimento do site e, portanto, precisam ser rastreadas. A equipe identifica uma [!DNL Mailchimp] e começa a criar os públicos-alvo do Experience Platform nos quais os contatos de cada lista são adicionados. Depois de enviar esses públicos-alvo para o [!DNL Mailchimp Interest Categories], se algum contato não existir no [!DNL Mailchimp] público ao qual são adicionados em um grupo com o nome do público ao qual o contato pertence. Se algum contato já existir no [!DNL Mailchimp] público-alvo ou grupo, então as informações são atualizadas. Depois que os dados forem enviados para [!DNL Mailchimp Interest Categories], a equipe de Vendas pode selecionar e enviar o email da campanha de marketing para o grupo de interesse de futebol na [!DNL Mailchimp] público-alvo.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para obter os pré-requisitos que você precisa configurar no Experience Platform e [!DNL Mailchimp] e para informações que você deve coletar antes de trabalhar com a [!DNL Mailchimp Interest Categories] destino.

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Mailchimp Interest Categories] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

### Pré-requisitos para a [!DNL Mailchimp Interest Categories] destino {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados da Platform para o seu [!DNL Mailchimp] conta:

#### Você deve ter um [!DNL Mailchimp] account {#prerequisites-account}

Antes de criar um [!DNL Mailchimp Interest Categories] destino, você deve primeiro garantir que tenha um [!DNL Mailchimp] conta. Se ainda não tiver um, visite o [[!DNL Mailchimp] página de inscrição](https://login.mailchimp.com/signup/) para registrar e criar sua conta.

#### Coletar [!DNL Mailchimp] Chave de API {#gather-credentials}

Você precisa do seu [!DNL Mailchimp] **Chave de API** para autenticar o [!DNL Mailchimp Interest Categories] destino em relação ao seu [!DNL Mailchimp] conta. A variável **Chave de API** serve como **Senha** quando você [autenticar o destino](#authenticate).

Se você não tiver seu **Chave de API**, Faça logon em sua conta e consulte a [[!DNL Mailchimp] Gerar sua chave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) documentação para criar uma.

Um exemplo de uma chave de API é `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se você gerar a variável **Chave de API**, anote-o, pois você não poderá acessá-lo após a geração.

#### Identificar [!DNL Mailchimp] data center {#identify-data-center}

Em seguida, você deve identificar o [!DNL Mailchimp] data center. Para fazer isso, faça logon no [!DNL Mailchimp] e navegue até a página **Seção de chaves de API** da sua conta.

O valor é a primeira parte do URL que você vê no navegador. Se o URL for *https://`us14`.mailchimp.com/account/api/*, o data center será `us14`.

Ele também está anexado à sua chave de API no formulário *key-dc*; se sua chave de API for `0123456789abcdef0123456789abcde-us14`, o data center será `us14`.

Anote o valor do data center *(`us14` neste exemplo)*, esse valor é necessário quando você [preencher detalhes do destino](#destination-details).

Se precisar de mais orientação, consulte o [[!DNL Mailchimp] Documentação de fundamentos](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Medidas de proteção {#guardrails}

Cada um dos seus [!DNL Mailchimp] os públicos-alvo podem conter até 60 nomes de grupo (ou categorias de interesse) em um único grupo ou em vários grupos no mesmo público-alvo. Consulte [!DNL Mailchimp] [grupos](https://mailchimp.com/help/getting-started-with-groups/) para quaisquer esclarecimentos necessários. Ao atingir esse limite, você obtém uma `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` mensagem como uma resposta de erro do [!DNL Mailchimp] API.

Além disso, consulte o [!DNL Mailchimp] [limites de taxa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) para obter informações detalhadas sobre os limites impostos pela [!DNL Mailchimp] API.

## Identidades suportadas {#supported-identities}

[!DNL Mailchimp] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | Endereço de email do contato | Obrigatório |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada público selecionado na Platform, a variável correspondente [!DNL Mailchimp Interest Categories] O status do segmento é atualizado com o status de público-alvo da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar [!DNL Mailchimp Interest Categories]. Como alternativa, você pode localizá-lo na **[!UICONTROL Marketing por email]** categoria.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Conectar ao destino]**.

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome de usuário]** | Seu [!DNL Mailchimp Interest Categories] usuário. |
| **[!UICONTROL Senha]** | Seu [!DNL Mailchimp] **Chave de API**, que você anotou na [Coletar [!DNL Mailchimp] credenciais](#gather-credentials) seção.<br> Sua chave de API assume a forma de `{KEY}-{DC}`, em que o `{KEY}` porção refere-se ao valor anotado na variável [[!DNL Mailchimp] Chave de API](#gather-credentials) seção e o `{DC}` parte refere-se à [[!DNL Mailchimp] data center](#identify-data-center). <br>Você pode fornecer a variável `{KEY}` parte ou o formulário inteiro.<br> Por exemplo, se sua chave de API for <br>*`0123456789abcdef0123456789abcde-us14`*,<br> você pode fornecer *`0123456789abcdef0123456789abcde`*ou *`0123456789abcdef0123456789abcde-us14`*como o valor. |

{style="table-layout:auto"}

![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | Um nome pelo qual você reconhecerá este destino no futuro. |
| **[!UICONTROL Descrição]** | Uma descrição que ajudará você a identificar esse destino no futuro. |
| **[!UICONTROL Centro de dados]** | Seu [!DNL Mailchimp] account `data center`. Consulte a [Identificar [!DNL Mailchimp] data center](#identify-data-center) para obter orientação. |
| **[!UICONTROL Nome do público-alvo (selecione o data center primeiro)]** | Depois de selecionar o **[!UICONTROL Centro de dados]**, essa lista suspensa é preenchida automaticamente com os nomes dos públicos-alvo da [!DNL Mailchimp] conta. Selecione o público que deseja atualizar com os dados da Platform. |
| **[!UICONTROL Categoria de interesse (selecione primeiro o data center e o nome do público-alvo)]** | Depois de selecionar o **[!UICONTROL Nome do público]**, essa lista suspensa será preenchida automaticamente com os nomes das categorias dos grupos de interesse [!DNL Mailchimp] conta. Selecione o nome da categoria que você deseja atualizar com os dados da Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Se a chave de API fornecida na variável **[!UICONTROL Senha]** ou a variável **[!UICONTROL Centro de dados]** estiverem incorretos, a interface exibirá um [!DNL Mailchimp] Resposta de erro da API: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* conforme mostrado abaixo. Nesse caso, não será possível selecionar um valor no **[!UICONTROL Nome do público-alvo (selecione o data center primeiro)]** campo. Para corrigir esse erro, forneça os valores corretos.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Mailchimp Interest Categories] destino, você deve passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL Mailchimp Interest Categories] campos de destino, siga as etapas abaixo:

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Agora você pode ver uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o atributo **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos]** e selecione na lista de atributos preenchida na variável [!DNL Mailchimp] API. *Quaisquer atributos personalizados adicionados aos selecionados [!DNL Mailchimp] O público-alvo também estará disponível para seleção como campos de direcionamento.*

   Os mapeamentos disponíveis entre o esquema de perfil XDM e [!DNL Mailchimp Interest Categories] são as seguintes: | Campo de origem | Campo de destino | Notas | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Obrigatório: Sim | |`xdm: person.name.firstName`|`Attribute: FNAME`| | |`xdm: person.name.lastName`|`Attribute: LNAME`| | |`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   Além disso, `ADDRESS` é um campo de público alvo especial conhecido como `merge field` no seu [!DNL Mailchimp] público-alvo. A variável [[!DNL Mailchimp] documentação](https://mailchimp.com/developer/marketing/docs/merge-fields/) define as chaves necessárias como `addr1`, `city`, `state`, e `zip`e as teclas opcionais `addr2` e `country`. Os valores desses campos devem ser cadeias de caracteres. Se qualquer um dos `ADDRESS` os mapeamentos de campo estiverem presentes, o destino passará a variável `ADDRESS` objeto para o [!DNL Mailchimp] API para atualização. Qualquer `ADDRESS` os campos que não estão mapeados têm seu valor padrão `NULL` exceto para o país cujo padrão é `US`.

   Os mapeamentos disponíveis para o `ADDRESS` são os seguintes:

   | Campo de origem | Campo de destino |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Por exemplo, você deseja atualizar o valor de `country` com o campo de endereço existente do contato `addr1`, `city`, `state`, e `zip` valores como `132, My Street, Kingston`, `New York`, `New York` e `12401`. Para atualizar o `country` você deve passar os valores existentes com alterações *(se houver)* e o novo valor para o país. Portanto, os valores no conjunto de dados devem ser `132, My Street, Kingston`, `New York`, `New York`, `12401`, e `US`. Em outras palavras, se você apenas passar `country` e não fornecem valores para `addr1`, `city`, `state`, e `zip` eles serão substituídos por `NULL`.

   Um exemplo com os mapeamentos concluídos é mostrado abaixo:
   ![Exemplo de captura de tela da interface do usuário do Platform mostrando mapeamentos de campo.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

* Faça logon no [[!DNL Mailchimp]](https://login.mailchimp.com/) conta. Em seguida, navegue até o **[!DNL Audience]** página. Em seguida, expanda a variável **[!DNL Manage Contacts]** e selecione **[!DNL Groups]**.

![Captura de tela da interface do usuário do Mailchimp mostrando a página do grupo de público-alvo.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Selecione o Grupo e verifique se os públicos-alvo selecionados são criados como categorias com o nome do público-alvo da Platform, que pode ser seguido por um sufixo gerado automaticamente.
   * Esse destino usa os nomes dos segmentos selecionados para criar a categoria de interesse usando o [[!DNL Mailchimp] Adicionar API de categoria de juros](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Se você criar um novo destino e ativar os mesmos públicos-alvo novamente, [!DNL Mailchimp] adiciona um sufixo para distinguir entre os segmentos existentes e os novos.
* Contatos cujos emails não existiam no grupo são adicionados à categoria recém-criada.
* Para contatos que já existem no grupo, os dados do campo de atributo são atualizados e o contato é adicionado à categoria recém-criada.

![Captura de tela da interface do usuário do Mailchimp mostrando as categorias do grupo de público-alvo.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erro encontrado se [!DNL Mailchimp] Os valores da chave de API ou do data center estão incorretos {#incorrect-credentials-error}

Se a chave de API fornecida na variável **[!UICONTROL Senha]** ou a variável **[!UICONTROL Centro de dados]** estiverem incorretos, a interface exibirá um [!DNL Mailchimp] Resposta de erro da API: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* conforme mostrado abaixo. Nesse caso, não é possível selecionar um valor do **[!UICONTROL Nome do público-alvo (selecione o data center primeiro)]** campo.

![Captura de tela da interface do usuário do Platform mostrando erro se os valores da chave da API do Mailchimp ou do data center estiverem incorretos.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Para corrigir esse erro e prosseguir para a próxima etapa, você deve fornecer os valores corretos. Consulte a [Identificar [!DNL Mailchimp] data center](#identify-data-center) e
[Coletar [!DNL Mailchimp] Chave de API](#gather-credentials) seções se precisar de orientação.

### Erro encontrado se [!DNL Mailchimp] o limite do nome do grupo foi excedido {#group-name-limits-error}

Ao criar o destino, você pode receber as seguintes mensagens de erro: *`Cannot have more than 60 interests per list (Across all categories)`* ou *`400 BAD_REQUEST`*. Isso acontece quando você excede os 60 nomes de grupo (ou categorias de interesse) em um único grupo ou em vários grupos dentro do mesmo limite de público-alvo, conforme descrito na seção [grades de proteção](#guardrails) seção. Para corrigir esse erro, verifique se você não está excedendo o limite de nome de grupo no [!DNL Mailchimp].

### [!DNL Mailchimp] Códigos de status e erro

Consulte a [[!DNL Mailchimp] página de erros](https://mailchimp.com/developer/marketing/docs/errors/) para obter uma lista abrangente de códigos de erro e status com explicações.

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [!DNL Mailchimp] A documentação do está abaixo:
* [Introdução ao [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Introdução ao Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Criar um público-alvo](https://mailchimp.com/help/create-audience/)
* [Introdução aos grupos](https://mailchimp.com/help/getting-started-with-groups/)
* [Criar um novo grupo de público-alvo](https://mailchimp.com/help/create-new-audience-group/)
* [Categorias de juros](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [API de marketing](https://mailchimp.com/developer/marketing/api/)
