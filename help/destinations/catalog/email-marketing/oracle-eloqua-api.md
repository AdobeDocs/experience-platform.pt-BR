---
title: (API) Conexão Oracle Eloqua
description: O destino (API) Oracle Eloqua permite exportar os dados da conta e ativá-los no Oracle Eloqua para as necessidades comerciais.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: cf7ad18fa3d8f074371a0f03e09e218d37be5e01
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 3%

---


# [!DNL (API) Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite que os profissionais de marketing planejem e executem campanhas enquanto fornecem uma experiência personalizada para seus clientes potenciais. Com o gerenciamento integrado de leads e a fácil criação de campanhas, o modelo ajuda os profissionais de marketing a engajarem o público-alvo certo na hora certa da jornada do comprador e é dimensionado elegantemente para alcançar os públicos-alvo em todos os canais, incluindo email, pesquisa de exibição, vídeo e dispositivos móveis. As equipes de vendas podem fechar mais negócios a uma taxa mais rápida, aumentando o ROI do marketing por meio de insights em tempo real.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aproveita a operação [Atualizar um contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) da API REST [!DNL Oracle Eloqua], que permite **atualizar identidades** de um público para [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] usa [Autenticação Básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para se comunicar com a API REST [!DNL Oracle Eloqua]. As instruções para autenticar na sua instância do [!DNL Oracle Eloqua] estão mais abaixo, na seção [Autenticar no destino](#authenticate).

## Casos de uso {#use-cases}

O departamento de marketing de uma plataforma online deseja transmitir uma campanha de marketing por email para um público-alvo com curadoria de clientes potenciais. A equipe de marketing da plataforma pode atualizar as informações de clientes potenciais existentes por meio do Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para [!DNL Oracle Eloqua], que pode ser usado para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar dados para o destino [!DNL Oracle Eloqua], você deve ter um [esquema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) criados em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos do esquema de Detalhes da associação do público-alvo](/help/xdm/field-groups/profile/segmentation.md) se precisar de orientação sobre os status do público-alvo.

### [!DNL Oracle Eloqua] pré-requisitos {#prerequisites-destination}

Para exportar dados da Platform para sua conta [!DNL Oracle Eloqua], é necessário ter uma conta [!DNL Oracle Eloqua].

Além disso, você precisa, no mínimo, dos *&quot;Usuários avançados - Permissões de marketing&quot;* para sua instância do [!DNL Oracle Eloqua]. Consulte a seção *&quot;Grupos de Segurança&quot;* na página [Acesso de usuário protegido](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) para obter orientação. O acesso é exigido pelo destino para [determinar programaticamente a URL base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) ao invocar a API [!DNL Oracle Eloqua].

#### Obter credenciais de [!DNL Oracle Eloqua] {#gather-credentials}

Anote os itens abaixo antes de autenticar no destino [!DNL Oracle Eloqua]:

| Credencial | Descrição |
| --- | --- |
| `Company Name` | O nome da empresa associado à sua conta [!DNL Oracle Eloqua]. <br>Posteriormente, você usará `Company Name` e [!DNL Oracle Eloqua] `Username` como uma cadeia de caracteres concatenada a ser usada como **[!UICONTROL Nome de Usuário]** ao [autenticar no destino](#authenticate). |
| `Username` | O nome de usuário da sua conta [!DNL Oracle Eloqua]. |
| `Password` | A senha da sua conta [!DNL Oracle Eloqua]. |
| `Pod` | O [!DNL Oracle Eloqua] oferece suporte a vários data centers, cada um com um nome de domínio exclusivo. [!DNL Oracle Eloqua] refere-se a eles como &quot;pods&quot;, existem atualmente sete no total - p01, p02, p03, p04, p06, p07 e p08. Para obter o POD em que você está, faça logon no [!DNL Oracle Eloqua] e anote a URL no navegador depois de fazer logon com êxito. Por exemplo, se a URL do navegador for `secure.p01.eloqua.com`, `pod` será `p01`. Consulte a página [determinando seu POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) para obter orientação adicional. |

Consulte [Entrando em [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) para obter orientação.

## Medidas de proteção {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] campos de contato personalizados são criados automaticamente usando os nomes dos públicos selecionados durante a etapa **[!UICONTROL Selecionar segmentos]**.

* [!DNL Oracle Eloqua] tem um limite máximo de 250 campos de contatos personalizados.
* Antes de exportar novos públicos, verifique se o número de públicos da Platform e o número de públicos existentes em [!DNL Oracle Eloqua] não excedem esse limite.
* Se esse limite for excedido, você encontrará um erro no Experience Platform. Isso ocorre porque a API [!DNL Oracle Eloqua] falha ao validar a solicitação e responde com - *400: Erro de validação* - mensagem de erro descrevendo o problema.
* Se você atingiu o limite especificado acima, é necessário remover os mapeamentos existentes do destino e excluir os campos de contato personalizados correspondentes na conta do [!DNL Oracle Eloqua] antes de exportar mais segmentos.

* Consulte a página [[!DNL Oracle Eloqua] Criando Campos de Contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obter informações sobre limites adicionais.

## Identidades suportadas {#supported-identities}

[!DNL Oracle Eloqua] oferece suporte à atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Obrigatório |
|---|---|---|
| `EloquaId` | Identificador exclusivo do contato. | Sim |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campos.</li><li> Para cada público selecionado na Platform, o status de segmento [!DNL Oracle Eloqua] correspondente é atualizado com seu status de público da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquise por [!DNL (API) Oracle Eloqua]. Como alternativa, você pode localizá-lo na categoria **[!UICONTROL Email Marketing]**.

### Autenticar para o destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nome da empresa\nome de usuário"
>abstract="Preencha este campo com o nome da empresa e o nome de usuário do Oracle Eloqua no formulário `{COMPANY_NAME}\{USERNAME}`"

Preencha os campos obrigatórios abaixo. Consulte a seção [Coletar [!DNL Oracle Eloqua] credenciais](#gather-credentials) para obter qualquer orientação.
* **[!UICONTROL Senha]**: a senha da sua conta [!DNL Oracle Eloqua].
* **[!UICONTROL Nome de Usuário]**: uma cadeia de caracteres concatenada composta pelo Nome da Empresa [!DNL Oracle Eloqua] e pelo Nome de Usuário [!DNL Oracle Eloqua].<br>O valor concatenado assume a forma de `{COMPANY_NAME}\{USERNAME}`.<br> Observe que não use chaves ou espaços e preserve a `\`. <br>Por exemplo, se o Nome da Empresa [!DNL Oracle Eloqua] for `MyCompany` e o Nome de Usuário [!DNL Oracle Eloqua] for `Username`, o valor concatenado que você usará no campo **[!UICONTROL Nome de Usuário]** será `MyCompany\Username`.

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá um status **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Para encontrar o número do seu pod, faça logon no Oracle Eloqua. Observe o URL no seu navegador após relizar o logon com sucesso. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da Interface do Usuário da Plataforma mostrando os detalhes de destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Pod]**: para saber em qual `pod` você está, faça logon no [!DNL Oracle Eloqua] e anote a URL no navegador depois de fazer logon com êxito. Por exemplo, se a URL do navegador for `secure.p01.eloqua.com` o valor `pod` necessário para selecionar é `p01`. Consulte a seção [Coletar [!DNL Oracle Eloqua] credenciais](#gather-credentials) para obter orientação adicional.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente seus dados de público-alvo do Adobe Experience Platform para o destino [!DNL Oracle Eloqua], é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Para mapear seus campos XDM para os campos de destino [!DNL Oracle Eloqua], siga estas etapas:

1. Na etapa **[!UICONTROL Mapeamento]**, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. Na janela **[!UICONTROL Selecionar campo de origem]**, escolha a categoria **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. Na janela **[!UICONTROL Selecionar campo de destino]**, escolha **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e digite o nome do atributo desejado no campo **[!UICONTROL Nome do atributo]**. O nome do atributo fornecido deve corresponder a um atributo de contato existente em [!DNL Oracle Eloqua]. Consulte [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) para obter os nomes de atributos exatos que você pode usar em [!DNL Oracle Eloqua].
   * Repita essas etapas para adicionar os mapeamentos de atributos necessários e desejados entre seu esquema de perfil XDM e [!DNL Oracle Eloqua]:
| Campo do Source | Campo de destino | Obrigatório |
|—|—|—|
`IdentityMap: Eid`|`Identity: EloquaId`| Sim |
`xdm: personalEmail.address`|`Attribute: emailAddress`| Sim |
`xdm: personName.firstName`|`Attribute: firstName`| |
|`xdm: personName.lastName`|`Attribute: lastName`| |
|`xdm: workAddress.street1`|`Attribute: address1`| |
`xdm: workAddress.street2`|`Attribute: address2`| |
`xdm: workAddress.street3`|`Attribute: address3`| |
`xdm: workAddress.postalCode`|`Attribute: postalCode`| |
`xdm: workAddress.country`|`Attribute: country`| |
`xdm: workAddress.city`|`Attribute: city`| |

   * Um exemplo com os mapeamentos acima é mostrado abaixo:
     ![Exemplo de captura de tela da interface do usuário da plataforma com mapeamentos de atributos.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Os atributos especificados no **[!UICONTROL campo de Destino]** devem ser nomeados exatamente como especificado em [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html), pois esses atributos formarão o corpo da solicitação.
>* Os atributos especificados no **[!UICONTROL campo Source]** não seguem nenhuma restrição desse tipo. Você pode mapeá-lo com base na sua necessidade. No entanto, se o formato dos dados não estiver correto quando enviado para o [!DNL Oracle Eloqua], ocorrerá um erro. Por exemplo, você pode mapear o **[!UICONTROL campo do Source]** namespace de identidade `contact key`, `ABC ID` etc. para **[!UICONTROL Campo de destino]**: `EloquaId` depois de verificar se os valores de ID correspondem ao formato aceito por [!DNL Oracle Eloqua].
>* O mapeamento `EloquaID` é obrigatório para atualizar atributos correspondentes à identidade.
>* O mapeamento `emailAddress` é necessário. Sem ela, a API lança um erro, como mostrado abaixo:
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

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Avançar]**.

>[!NOTE]
>
>O destino coloca automaticamente um identificador exclusivo entre os nomes de público selecionados em cada execução ao enviar as informações do campo de contato para [!DNL Oracle Eloqua]. Isso garante que os nomes de campo de contato correspondentes aos nomes de público-alvo não se sobreponham. Consulte o exemplo de tela da seção [Validar exportação de dados](#exported-data) de uma página de Detalhes do Contato [!DNL Oracle Eloqua] com um campo de contato personalizado criado usando os nomes de público-alvo.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecione **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e navegue até a lista de destinos.
1. Em seguida, selecione o destino e alterne para a guia **[!UICONTROL Dados de ativação]** e selecione um nome de público-alvo.
   ![Exemplo de captura de tela da interface do usuário da plataforma mostrando Dados de Ativação de Destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitore o resumo do público-alvo e verifique se a contagem de perfis corresponde à contagem no segmento.
   ![Exemplo de captura de tela da Interface do Usuário da Plataforma mostrando o Segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Faça logon no site [!DNL Oracle Eloqua] e navegue até a página **[!UICONTROL Visão geral dos contatos]** para verificar se os perfis do público-alvo foram adicionados. Para ver o status do público-alvo, vá para uma página de **[!UICONTROL Detalhes do contato]** e verifique se o campo de contato com o nome do público-alvo selecionado como seu prefixo foi criado.

![Captura de tela da interface do usuário do Oracle Eloqua mostrando a página Detalhes do Contato com o campo de contato personalizado criado com o nome do público-alvo.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Ao criar o destino, você pode receber uma das seguintes mensagens de erro: `400: There was a validation error` ou `400 BAD_REQUEST`. Isso acontece quando você excede o limite de 250 campos de contato personalizados, conforme descrito na seção [medidas de proteção](#guardrails). Para corrigir esse erro, verifique se você não está excedendo o limite do campo de contato personalizado em [!DNL Oracle Eloqua].
![Captura de tela da Interface do Usuário da Plataforma mostrando erro.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte as páginas [[!DNL Oracle Eloqua] Códigos de status HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Erros de validação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) para obter uma lista abrangente de códigos de status e de erro com explicações.

## Recursos adicionais {#additional-resources}

Para obter detalhes adicionais, consulte a documentação do [!DNL Oracle Eloqua]:

* [Automação de Marketing do Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST para o Serviço de Marketing Cloud Eloqua do Oracle](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Esta seção captura a funcionalidade e as atualizações de documentação significativas feitas neste conector de destino.

+++ Exibir changelog

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2023 | Atualização da documentação | <ul><li>Atualizamos a seção [casos de uso](#use-cases) com um exemplo mais claro de quando os clientes se beneficiariam com o uso desse destino.</li> <li>Atualizamos a seção [mapping](#mapping-considerations-example) com exemplos claros de mapeamentos obrigatórios e opcionais.</li> <li>Atualizamos a seção [Conectar ao destino](#connect) com um exemplo sobre como construir o valor concatenado para o campo **[!UICONTROL Nome de Usuário]** usando o Nome da Empresa [!DNL Oracle Eloqua] e o Nome de Usuário [!DNL Oracle Eloqua]. (PLATIR-28343)</li><li>Atualizamos as seções [Coletar [!DNL Oracle Eloqua] credenciais](#gather-credentials) e [Preencher detalhes do destino](#destination-details) com orientações sobre a seleção do [!DNL Oracle Eloqua] **[!UICONTROL Pod]**. O valor *&quot;Pod&quot;* é usado pelo destino para construir a URL base para as chamadas de API. A seção [[!DNL Oracle Eloqua] pré-requisitos](#prerequisites-destination) também foi atualizada com orientação sobre como atribuir *&quot;Usuários Avançados - Permissões de marketing&quot;* como um *&quot;Grupos de segurança&quot;* necessário para sua instância [!DNL Oracle Eloqua].</li></ul> |
| Março de 2023 | Versão inicial | Versão inicial de destino e publicação da documentação. |

{style="table-layout:auto"}

+++