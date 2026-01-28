---
title: A conexão Trade Desk - CRM
description: Ative perfis para sua conta da Trade Desk para direcionamento e supressão de público com base nos dados do CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# A conexão [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Há dois destinos The Trade Desk - CRM no [catálogo de destinos](/help/destinations/catalog/overview.md).
>
>* Se você originar dados na UE, use o destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Se você originar dados nas regiões APAC ou NAMER, use o destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe *[!DNL Trade Desk]*. Para qualquer consulta ou solicitação de atualização, contate o representante do [!DNL Trade Desk].

## Visão geral {#overview}

Entenda como você pode ativar perfis para sua conta do [!DNL Trade Desk] para direcionamento e supressão de público com base nos dados do CRM.

Este conector envia dados para [!DNL The Trade Desk] para ativação de Dados Primários. [!DNL The Trade Desk] armazene seus emails brutos (sem hash) e números de telefone.

>[!TIP]
>
>Use o destino [!DNL The Trade Desk - CRM] para enviar dados do CRM (como emails e números de telefone) e outros identificadores de dados primários, como cookies e IDs de dispositivos. Você pode continuar usando o [destino da Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) no catálogo do Experience Platform para cookies e mapeamentos de ID de dispositivo.

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Antes de poder ativar públicos para a Trade Desk, você deve entrar em contato com o gerente de conta do [!DNL Trade Desk] para habilitar o recurso. Se estiver enviando emails, números de telefone e UID2/EUID, você deverá compartilhar o contrato UID2/EUID assinado com [!DNL The Trade Desk].

## Requisitos de correspondência de ID {#id-matching-requirements}

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes. Leia a [visão geral do Namespace de Identidade](/help/identity-service/features/namespaces.md) para obter mais informações.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

Os endereços de email e números de telefone com hash e sem hash são compatíveis com o Adobe Experience Platform. Siga as instruções na seção Requisitos de correspondência de ID e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente.

| Identidade de destino | Descrição |
|---|---|
| Email | Endereços de email (texto não criptografado) |
| Email_LC_SHA256 | Os endereços de email precisam ser transformados em hash usando SHA256 e em minúsculas. Você não poderá alterar essa configuração posteriormente. |
| Telefone (E.164) | Telefones que precisam ser normalizados no formato E.164. O formato E.164 inclui um sinal de adição (+), um código de chamada de país internacional, um código de área local e um número de telefone. Por exemplo: (+)(código do país)(código de área)(número de telefone). Esse identificador não está disponível para a Trade Desk - Dados primários (EU). |
| Telefone (SHA256_E.164) | Números de telefone que já foram normalizados para o formato E.164 e depois transformados em hash usando SHA-256, com o hash resultante codificado em Base64. Esse identificador não está disponível para a Trade Desk - Dados primários (EU). |
| TDID | ID de cookie na Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple ID para anunciantes |
| UID2 | O valor bruto de UID2 |
| UID2Token | O token UID2 criptografado, também conhecido como token de publicidade. |
| EUID | O valor bruto da ID da União Europeia |
| TokenUIDE | O token EUID criptografado, também conhecido como token de publicidade. |
| RampID | O RampID de 49 ou 70 caracteres (anteriormente conhecido como IdentityLink ou IDL). Deve ser um RampID do LiveRamp mapeado especificamente para a Trade Desk. |
| netID | A netID do usuário como uma string codificada em base64 de 70 caracteres. Essa ID é compatível somente na Europa. |
| FirstID | O First-id do usuário, um cookie próprio normalmente definido por editores na França. Essa ID é compatível somente na Europa. |

{style="table-layout:auto"}

## Requisitos de hash de email {#email-hashing}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email brutos.

Para saber mais sobre como assimilar endereços de email no Experience Platform, leia a [visão geral de assimilação em lote](/help/ingestion/batch-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Remova espaços à esquerda e à direita.
* Converta todos os caracteres ASCII em minúsculas.
* Em `gmail.com` endereços de email, remova os seguintes caracteres da parte do nome de usuário do endereço de email:

      * O período (`.`) (código ASCII 46). Por exemplo, normalize &quot;jane.doe@gmail.com&quot; para &quot;janedoe@gmail.com&quot;.
     * O caractere de sinal de mais (`+`) (código ASCII 43) e todos os caracteres subsequentes. Por exemplo, normalize `janedoe+home@gmail.com` para `janedoe@gmail.com`.
  

## Requisitos de normalização e hash do número de telefone {#phone-hashing}

Veja o que você precisa saber sobre o upload de números de telefone:

* Você deve normalizar os números de telefone antes de enviá-los em uma solicitação, independentemente de você enviá-los com hash ou sem hash em uma solicitação.
* Para carregar dados normalizados, com hash e codificados, você deve enviar números de telefone como hashes SHA-256 codificados em Base64 dos números de telefone normalizados.

Se você deseja carregar números de telefone brutos ou com hash, é necessário normalizá-los.

>[!IMPORTANT]
>
>A normalização antes do hash garante que o valor da ID gerada sempre seja o mesmo e que os dados possam ser correspondidos com precisão.

Veja o que você precisa saber sobre os requisitos de normalização de números de telefone:

* O Operador UID2 aceita números de telefone no formato E.164, que é o formato de número de telefone internacional que garante a exclusividade global.
* Os números de telefone E.164 podem ter no máximo 15 dígitos.
* Números de telefone E.164 normalizados usam a seguinte sintaxe: `[+][country code][subscriber number including area code]` sem espaços, hifens, parênteses ou outros caracteres especiais. Veja alguns exemplos:

      * EUA: 1 (234) 567-8901 é normalizado para +12345678901.
     * Cingapura: 65 1243 5678 é normalizado para +6512345678.
     * Austrália: número de telefone celular 0491 570 006 é normalizado para adicionar o código do país e eliminar o zero à esquerda: +61491570006.
     * Reino Unido: o número de telefone celular 07812 345678 foi normalizado para adicionar o código do país e eliminar o zero à esquerda: +447812345678.
  
Verifique se o número de telefone normalizado é UTF-8, não outro sistema de codificação, como UTF-16.

Um hash de número de telefone é um hash SHA-256 codificado na Base64 de um número de telefone normalizado. O número de telefone é primeiro normalizado, depois é hash usando o algoritmo de hash SHA-256 e, em seguida, os bytes resultantes do valor de hash são codificados usando a codificação Base64. Observe que a codificação Base64 é aplicada aos bytes do valor de hash, não à representação de string codificada em hexadecimal.
A tabela a seguir mostra um exemplo de um número de telefone de entrada simples, e o resultado como cada etapa é aplicado para chegar a um valor seguro e opaco.

| Tipo | Exemplo | Comentários e uso |
|---|---|---|
| Número de telefone bruto | 1 (234) 567-8901 | Este é o ponto de partida. |
| Número de telefone normalizado | +12345678901 | A normalização é sempre o primeiro passo. |
| Hash SHA-256 do número de telefone normalizado | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Essa string de 64 caracteres é uma representação codificada hexadecimal do SHA-256 de 32 bytes. |
| Codificação hexadecimal para Base64 SHA-256 de número de telefone normalizado e com hash | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | Essa string de 44 caracteres é uma representação codificada na Base64 do SHA-256 de 32 bytes. O hash SHA-256 é um valor hexadecimal. Você deve usar um codificador Base64 que use um valor hexadecimal como entrada. Use essa codificação para valores phone_hash enviados no corpo da solicitação. |

>[!IMPORTANT]
>
>Ao aplicar a codificação Base64, certifique-se de usar uma função que use um valor hexadecimal como entrada. Se você usar uma função que usa texto como entrada, o resultado será uma string mais longa, inválida para os fins de UID2.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (email ou email com hash) usados no destino da Trade Desk. |
| Frequência de exportação | **[!UICONTROL Daily Batch]** | Como um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o perfil (identidades) é atualizado uma vez por dia downstream para a plataforma de destino. Leia mais sobre [exportações de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

### Autenticar no destino {#authenticate}

O Destino do CRM [!DNL The Trade Desk] é um carregamento diário de arquivo em lotes e não requer autenticação do usuário.

### Preencher Detalhes do Destino {#fill-in-details}

Antes de enviar ou ativar dados de público-alvo para um destino, você deve configurar uma conexão com sua própria plataforma de destino. Ao [configurar](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Account Type]**: Escolha a opção **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Advertiser ID]**: seu [!DNL Trade Desk Advertiser ID], que pode ser compartilhado pelo seu Gerente de Conta do [!DNL Trade Desk] ou ser encontrado em [!DNL Advertiser Preferences] na interface do usuário do [!DNL Trade Desk].

![Captura de tela da interface do Experience Platform mostrando como preencher os detalhes do destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Ao se conectar ao destino, definir uma política de governança de dados é totalmente opcional. Revise a [visão geral da governança de dados](/help/data-governance/policies/overview.md) da Experience Platform para obter mais detalhes.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para um destino.

Na página **[!UICONTROL Scheduling]**, é possível configurar o agendamento e os nomes de arquivo para cada público-alvo que você está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

![Captura de tela da interface do Experience Platform para agendar a ativação de públicos-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todos os públicos-alvo ativados para o Destino do CRM [!DNL The Trade Desk] são definidos automaticamente para uma frequência diária e uma exportação de arquivo completa.

![Captura de tela da interface do Experience Platform para agendar a ativação de públicos-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Na página **[!UICONTROL Mapping]**, você deve selecionar atributos ou namespaces de identidade na coluna de origem e mapear para a coluna de destino.

![Captura de tela da interface do Experience Platform para mapear a ativação de público-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Veja abaixo um exemplo de mapeamento de identidade correto ao ativar públicos para o destino do CRM [!DNL The Trade Desk].

Selecionar campos de origem e destino:

| Campo de origem | Campo de destino |
|---|---|
| Email | email |
| Email_LC_SHA256 | hash_email |
| Telefone (E.164) | telefone |
| Telefone (SHA256_E.164) | hash_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| TokenUIDE | euid_token |
| RampID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Validar exportação de dados {#validate}

Para validar se os dados foram exportados corretamente do Experience Platform para o [!DNL The Trade Desk], localize os públicos-alvo na guia 1PD do Adobe na biblioteca &quot;Dados e identidade do anunciante&quot; do [!DNL The Trade Desk]. Estas são as etapas para encontrar a ID correspondente na interface do usuário do [!DNL Trade Desk]:

1. Primeiro, selecione a guia **[!UICONTROL Libraries]** e revise a seção **[!UICONTROL Advertiser data and identity]**.
2. Clique no **[!UICONTROL Adobe 1PD]** e ele listará todos os públicos ativados para [!DNL The Trade Desk].
3. O Nome do segmento ou a ID do segmento da Experience Platform serão exibidos como o Nome do segmento na interface do usuário do [!DNL Trade Desk].

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).
