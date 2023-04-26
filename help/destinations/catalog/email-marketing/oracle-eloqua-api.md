---
title: Conexão Eloqua do Oracle (API)
description: O destino Eloqua do Oracle (API) permite exportar os dados da conta e ativá-los no Oracle Eloqua para atender às necessidades de sua empresa.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 3d54b89ab5f956710ad595a0e8d3567e1e773d0a
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite que os profissionais de marketing planejem e executem campanhas, fornecendo uma experiência personalizada para o cliente em potencial. Com o gerenciamento integrado de clientes potenciais e a criação fácil de campanhas, ajuda os profissionais de marketing a engajarem o público certo na hora certa, na jornada do comprador, e dimensionam elegantemente para alcançar públicos-alvo em canais, incluindo email, pesquisa de exibição, vídeo e dispositivos móveis. As equipes de vendas podem fechar mais ofertas a uma taxa mais rápida, aumentando o ROI de marketing por meio de insight em tempo real.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [Atualizar um contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) da [!DNL Oracle Eloqua] REST API, que permite **atualizar identidades** em um segmento em [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] uses [Autenticação básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para comunicar com o [!DNL Oracle Eloqua] REST API. Instruções para autenticação em seu [!DNL Oracle Eloqua] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

O departamento de marketing de uma plataforma online deseja transmitir uma campanha de marketing baseada em email para um público-alvo preparado de clientes potenciais. A equipe de marketing da plataforma pode atualizar informações de clientes potenciais existentes por meio do Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para o [!DNL Oracle Eloqua], que pode ser usada para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Oracle Eloqua] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### [!DNL Oracle Eloqua] pré-requisitos {#prerequisites-destination}

Para exportar dados da Platform para seu [!DNL Oracle Eloqua] conta que você precisa ter uma [!DNL Oracle Eloqua] conta.

Além disso, você precisa, no mínimo, da variável *&quot;Usuários avançados - Permissões de marketing&quot;* para seu [!DNL Oracle Eloqua] instância. Consulte a *&quot;Grupos de segurança&quot;* seção sobre [Acesso seguro do usuário](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) para orientação. O acesso é exigido pelo destino para programaticamente [determinar o URL base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) ao invocar o [!DNL Oracle Eloqua] API.

#### Colete [!DNL Oracle Eloqua] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Oracle Eloqua] destino:

| Credencial | Descrição |
| --- | --- |
| `Company Name` | O nome da empresa associado ao [!DNL Oracle Eloqua] conta. <br>Posteriormente, você usará o `Company Name` e [!DNL Oracle Eloqua] `Username` como uma string concatenada a ser usada como a variável **[!UICONTROL Nome do usuário]** when [autenticação no destino](#authenticate). |
| `Username` | O nome de usuário de seu [!DNL Oracle Eloqua] conta. |
| `Password` | A senha de seu [!DNL Oracle Eloqua] conta. |
| `Pod` | [!DNL Oracle Eloqua] O suporta vários data centers, cada um com um nome de domínio exclusivo. [!DNL Oracle Eloqua] refere-se a eles como &quot;pods&quot;, atualmente são sete no total - p01, p02, p03, p04, p06, p07 e p08. Para obter em qual POD você está, faça logon no [!DNL Oracle Eloqua] e observe o URL no seu navegador após ter feito logon com êxito. Por exemplo, se o URL do navegador for `secure.p01.eloqua.com` your `pod` é `p01`. Consulte a [determinar o POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) para obter orientação adicional. |

Consulte a [Fazer logon em [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) para orientação.

## Medidas de proteção {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] os campos de contato personalizados são criados automaticamente usando os nomes dos segmentos selecionados durante a **[!UICONTROL Selecionar segmentos]** etapa.


* [!DNL Oracle Eloqua] O tem um limite máximo de 250 campos de contato personalizados.
* Antes de exportar novos segmentos, verifique se o número de segmentos da Platform e o número de segmentos existentes no [!DNL Oracle Eloqua] não exceda este limite.
* Se esse limite for excedido, você encontrará um erro no Experience Platform. Isso ocorre porque a variável [!DNL Oracle Eloqua] A API falha ao validar a solicitação e responde com um - *400: Ocorreu um erro de validação* - mensagem de erro descrevendo o problema.
* Se você atingiu o limite especificado acima, é necessário remover os mapeamentos existentes do seu destino e excluir os campos de contato personalizado correspondentes em seu [!DNL Oracle Eloqua] antes de exportar mais segmentos.

* Consulte a [[!DNL Oracle Eloqua] Criação de campos de contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obter informações sobre limites adicionais.

## Identidades suportadas {#supported-identities}

[!DNL Oracle Eloqua] O suporta a atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Obrigatório |
|---|---|---|
| `EloquaId` | Identificador exclusivo do contato. | Sim |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada segmento selecionado na Plataforma, a variável correspondente [!DNL Oracle Eloqua] o status do segmento é atualizado com o status do segmento da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL (API) Oracle Eloqua]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL Marketing por email]** categoria .

### Autenticar para destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nome da empresa\Nome de usuário"
>abstract="Preencha este campo com o nome de empresa e nome de usuário do Oracle Eloqua no formulário `{COMPANY_NAME}\{USERNAME}`"

Preencha os campos obrigatórios abaixo. Consulte a [Colete [!DNL Oracle Eloqua] credenciais](#gather-credentials) para quaisquer orientações.
* **[!UICONTROL Senha]**: A senha de seu [!DNL Oracle Eloqua] conta.
* **[!UICONTROL Nome do usuário]**: Uma string concatenada composta por [!DNL Oracle Eloqua] Nome da empresa e [!DNL Oracle Eloqua] Nome de usuário.<br>O valor concatenado assume a forma de `{COMPANY_NAME}\{USERNAME}`.<br> Observe que não use chaves ou espaços e preserve o `\`. <br>Por exemplo, se sua [!DNL Oracle Eloqua] Nome da empresa é `MyCompany` e [!DNL Oracle Eloqua] Nome de usuário é `Username`, o valor concatenado que será usado na variável **[!UICONTROL Nome do usuário]** é `MyCompany\Username`.

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**.
![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** status com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Para encontrar o número do seu pod, faça logon no Oracle Eloqua. Observe o URL no seu navegador após ter feito logon com êxito. "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Base de conhecimento do Oracle - descubra o número do seu pod"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Pod]**: Para obter `pod` estiver em, faça logon no [!DNL Oracle Eloqua] e observe o URL no seu navegador após ter feito logon com êxito. Por exemplo, se o URL do navegador for `secure.p01.eloqua.com` o `pod` o valor que você precisa selecionar é `p01`. Consulte a [Colete [!DNL Oracle Eloqua] credenciais](#gather-credentials) para obter orientação adicional.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Oracle Eloqua] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino.

Para mapear os campos XDM para a [!DNL Oracle Eloqua] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** janela, escolha **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e digite o nome do atributo desejado na função **[!UICONTROL Nome do atributo]** campo. O nome do atributo fornecido deve corresponder a um atributo de contato existente no [!DNL Oracle Eloqua]. Consulte [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) para os nomes exatos dos atributos que você pode usar em [!DNL Oracle Eloqua].
   * Repita essas etapas para adicionar os mapeamentos de atributo necessários e desejados entre seu esquema de perfil XDM e [!DNL Oracle Eloqua]: | Campo de origem | Campo de destino | Obrigatório | |—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Sim | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sim | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * Um exemplo com os mapeamentos acima é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma com mapeamentos de atributo.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Atributos especificados na **[!UICONTROL Campo de destino]** deve ser nomeado exatamente como especificado no [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) como esses atributos formarão o corpo da solicitação.
>* Atributos especificados na **[!UICONTROL Campo de origem]** não seguir tal restrição. Você pode mapeá-lo com base em sua necessidade, no entanto, se o formato de dados não estiver correto quando enviado para o [!DNL Oracle Eloqua] isso resultará em um erro. Por exemplo, você pode mapear a variável **[!UICONTROL Campo de origem]** namespace de identidade `contact key`, `ABC ID` etc. para **[!UICONTROL Campo de destino]** : `EloquaId` depois de garantir que os valores de ID correspondem ao formato aceito por [!DNL Oracle Eloqua].
>* O `EloquaID` o mapeamento é obrigatório para atualizar atributos correspondentes à identidade.
>* O `emailAddress` é necessário mapear. Sem isso, a API gera um erro, como mostrado abaixo:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Quando terminar de fornecer os mapeamentos para a conexão de destino, selecione **[!UICONTROL Próximo]**.

>[!NOTE]
>
>O destino automaticamente faz o sufixo de um identificador exclusivo para os nomes de segmento selecionados em cada execução ao enviar as informações do campo de contato para [!DNL Oracle Eloqua]. Isso garante que os nomes dos campos de contato correspondentes aos nomes dos segmentos não se sobreponham. Consulte a [Validar exportação de dados](#exported-data) captura de tela de seção de um [!DNL Oracle Eloqua] Página Detalhes do contato com o campo de contato personalizado criado usando os nomes de segmento.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e navegue até a lista de destinos.
1. Em seguida, selecione o destino e alterne para a **[!UICONTROL Dados de ativação]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os Dados de ativação de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem no segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Faça logon no [!DNL Oracle Eloqua] e navegue até o **[!UICONTROL Visão geral dos contatos]** para verificar se os perfis do segmento foram adicionados. Para ver o status do segmento, faça uma busca detalhada em um **[!UICONTROL Detalhes do contato]** e verificar se o campo de contato com o nome do segmento selecionado como seu prefixo foi criado.

![Captura de tela da interface do usuário do Oracle Eloqua mostrando a página Detalhes do contato com o campo de contato personalizado criado com o nome do segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Ao criar o destino, você pode receber uma das seguintes mensagens de erro: `400: There was a validation error` ou `400 BAD_REQUEST`. Isso acontece quando você excede o limite de 250 campos de contato personalizados, conforme descrito na [medidas de proteção](#guardrails) seção. Para corrigir esse erro, verifique se você não está excedendo o limite do campo de contato personalizado em [!DNL Oracle Eloqua].
![Captura de tela da interface do usuário da plataforma que mostra o erro.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte a [[!DNL Oracle Eloqua] Códigos de status HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Erros de validação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) páginas para obter uma lista abrangente de códigos de status e erro com explicações.

## Recursos adicionais {#additional-resources}

Para obter mais detalhes, consulte o [!DNL Oracle Eloqua] documentação:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API para o serviço de Marketing Cloud Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Esta seção captura a funcionalidade e atualizações significativas de documentação feitas neste conector de destino.

+++ Exibir log de alterações

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2023 | Atualização da documentação | <ul><li>Atualizamos o [casos de uso](#use-cases) com um exemplo mais claro de quando os clientes se beneficiariam com o uso desse destino.</li> <li>Atualizamos o [mapeamento](#mapping-considerations-example) com exemplos claros de mapeamentos obrigatórios e opcionais.</li> <li>Atualizamos o [Conecte-se ao destino](#connect) com um exemplo de como construir o valor concatenado para a variável **[!UICONTROL Nome do usuário]** usando o [!DNL Oracle Eloqua] Nome da empresa e [!DNL Oracle Eloqua] Nome de usuário. (PLATIR-28343)</li><li>Atualizamos o [Colete [!DNL Oracle Eloqua] credenciais](#gather-credentials) e [Preencha os detalhes do destino](#destination-details) seções com orientação sobre [!DNL Oracle Eloqua] **[!UICONTROL Pod]** seleção. O *&quot;Pod&quot;* é usado pelo destino para criar o URL base para as chamadas de API. O [[!DNL Oracle Eloqua] pré-requisitos](#prerequisites-destination) seção também foi atualizada com orientação sobre atribuição *&quot;Usuários avançados - Permissões de marketing&quot;* , conforme necessário *&quot;Grupos de segurança&quot;* para seu [!DNL Oracle Eloqua] instância.</li></ul> |
| Março de 2023 | Versão inicial | Versão inicial de destino e publicação de documentação. |

{style="table-layout:auto"}

+++