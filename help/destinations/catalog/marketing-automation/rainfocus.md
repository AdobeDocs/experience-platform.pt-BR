---
title: Perfis dos participantes do RainFocus
description: Saiba como usar o conector de destino Perfis de participantes RainFocus para sincronizar perfis de público-alvo com o Perfil de participante global RainFocus.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# Perfis dos participantes do RainFocus {#rainfocus-destination}

## Visão geral {#overview}

Use o destino [!DNL RainFocus Attendee Profiles] para transmitir perfis de clientes do Adobe Experience Platform para a plataforma [!DNL RainFocus] para criar e atualizar perfis de participantes.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL RainFocus]. Para fazer consultas ou solicitações de atualização, contate-os diretamente em `clientcare@rainfocus.com` ou visite a [Central de ajuda](https://help.rainfocus.com/hc/en-us) da RainFocus.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino RainFocus, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1 {#use-case-1}

Uma grande empresa de tecnologia corporativa está prestes a abrir um registro para sua exposição global e gostaria de encaminhar os perfis do cliente para [!DNL RainFocus] a fim de simplificar o processo de registro.

### Caso de uso #2 {#use-case-2}

Uma marca de serviços financeiros deve hospedar uma série de apresentações voltadas para clientes novos e existentes. Eles têm uma série de segmentos de público-alvo com clientes-alvo na Adobe Experience Platform. Usando o Conector de Destino do [!DNL RainFocus], é possível enviar facilmente esses perfis para o [!DNL RainFocus] para ativação.

## Pré-requisitos {#prerequisites}

Antes de usar o destino [!DNL RainFocus], atenda aos seguintes pré-requisitos:

* Crie um Perfil de API [!DNL RainFocus] com OAuth (Global).
   * O ponto de extremidade **Repositório de Participantes** deve estar habilitado.
   * Será necessário gerar uma **ID do Cliente** e um **Segredo do Cliente**.

Você também deve ter um identificador RainFocus **código de evento**, para o qual deseja que os perfis sejam enviados.

## Identidades suportadas {#supported-identities}

[!DNL RainFocus] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do segmento, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

![Fornecer detalhes de autenticação para o Conector de Destino RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**: preencha o [!DNL Client ID] fornecido pelo Perfil de API RainFocus.
* **[!UICONTROL Client secret]**: preencha o [!DNL Client Secret] fornecido pelo Perfil de API RainFocus.
* **[!UICONTROL Environment]**: especifique o ambiente RainFocus ao qual você está se conectando, por exemplo `dev`, `prod`.
* **[!UICONTROL Org ID]**: Forneça o `orgid` exclusivo para sua instância do RainFocus.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Fornecer detalhes de conexão para o Conector de Destino RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Event ID]**: Seu identificador de código de evento [!DNL RainFocus], para o qual você deseja que os perfis sejam enviados.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e segmentos para destinos de exportação de segmento de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público para este destino.

### Mapear atributos e identidades {#map}

Os seguintes namespaces de identidade de destino devem ser mapeados dependendo do caso de uso:

* **O email** deve ser mapeado como um campo de destino usando **Campo de destino > Selecionar namespace de identidade > email**

![Como mapear campos de perfil e identidade](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

É recomendável mapear campos de perfil adicionais, pois isso garantirá que o perfil de participante em [!DNL RainFocus] seja totalmente preenchido. Os seguintes campos de destino estão disponíveis em [!DNL RainFocus]:

| Campo de público alvo | Descrição |
|------------|-------------|
| `address1` | A primeira linha do endereço |
| `address2` | A segunda linha do endereço (se aplicável) |
| `city` | O nome da cidade |
| `companyname` | O nome da empresa |
| `countryid` | Um identificador de código de país ISO 3166-1 alpha-2 para o país |
| `email` | O endereço de email |
| `firstname` | O nome da pessoa |
| `lastname` | O sobrenome da pessoa |
| `jobtitle` | O cargo da pessoa |
| `phone` | O número de telefone |
| `state` | O código alfa de estado FIPS do estado ou província |
| `zip` | O CEP ou código postal |

{style="table-layout:auto"}

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que um conjunto de perfis for enviado para [!DNL RainFocus], use o log do Perfil de API em [!DNL RainFocus] para validar se os perfis foram assimilados com êxito.

![Exibir logs no Perfil de API em RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Validar se os perfis foram assimilados com êxito](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [Conector de Source de Streaming RainFocus](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/analytics/rainfocus)
