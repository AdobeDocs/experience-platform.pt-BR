---
title: (Beta) A conexão Trade Desk - CRM
description: Ative perfis para sua conta da Trade Desk para direcionamento e supressão de público com base nos dados do CRM.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 4%

---

# (Beta) A [!DNL Trade Desk] - Conexão CRM

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] O destino na Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.
>
>Com o lançamento da EUID (European Unified ID), você verá agora dois destinos do [!DNL The Trade Desk - CRM] no [catálogo de destinos](/help/destinations/catalog/overview.md).
>* Se seus dados se originarem da UE, use o destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Se seus dados se originarem das regiões da Ásia-Pacífico ou América do Norte, use o destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Ambos os destinos em Experience Platform estão atualmente em beta. Esse conector de destino e a página de documentação são criados e mantidos pelo *[!DNL Trade Desk]* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato com o [!DNL Trade Desk] representante da, a documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

Este documento foi criado para ajudar você a ativar perfis para o seu [!DNL Trade Desk] conta para direcionamento e supressão de público com base nos dados do CRM.

[!DNL The Trade Desk(TTD)] não manipula diretamente o arquivo de upload de endereços de email a qualquer momento, nem [!DNL The Trade Desk] armazene seus emails brutos (sem hash).

>[!TIP]
>
>Uso [!DNL The Trade Desk] Destinos do CRM para mapeamento de dados do CRM, como email ou email com hash. Use o [outro destino da Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) no catálogo do Adobe Experience Platform para cookies e mapeamentos de ID de dispositivo.

## Pré-requisitos {#prerequisites}

Antes de poder ativar públicos para [!DNL The Trade Desk], você deve entrar em contato com [!DNL The Trade Desk] Gerente de conta para assinar o contrato de integração do CRM. [!DNL The Trade Desk] O fornecerá permissão e compartilhará sua ID de anunciante para configurar seu destino.

## Requisitos de correspondência de ID {#id-matching-requirements}

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes. Leia as [Visão geral do namespace de identidade](/help/identity-service/namespaces.md) para obter mais informações.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções na seção Requisitos de correspondência de ID e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | Endereços de email (texto não criptografado) | Entrada `email` como a identidade de destino quando sua identidade de origem for um atributo ou namespace de email. |
| Email_LC_SHA256 | Os endereços de email precisam ser transformados em hash usando SHA256 e em minúsculas. Certifique-se de seguir qualquer [normalização de email](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regras necessárias. Você não poderá alterar essa configuração posteriormente. | Entrada `hashed_email` como a identidade de destino quando sua identidade de origem for um namespace ou atributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisitos de hash de email {#hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email brutos.

Para saber mais sobre como assimilar endereços de email no Experience Platform, leia o [visão geral da assimilação em lote](/help/ingestion/batch-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Remova espaços à esquerda e à direita.
* Converta todos os caracteres ASCII em minúsculas.
* Entrada `gmail.com` endereços de email, remova os seguintes caracteres da parte do nome de usuário do endereço de email:
   * O ponto (. (código ASCII 46). Por exemplo, normalize `jane.doe@gmail.com` para `janedoe@gmail.com`.
   * O sinal de mais (+ (código ASCII 43)) e todos os caracteres subsequentes. Por exemplo, normalize `janedoe+home@gmail.com` para `janedoe@gmail.com`.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (email ou email com hash) usados no destino da Trade Desk. |
| Frequência de exportação | **[!UICONTROL Lote diário]** | Como um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o perfil (identidades) é atualizado uma vez por dia downstream para a plataforma de destino. Leia mais sobre [exportações em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

### Autenticar no destino {#authenticate}

[!DNL The Trade Desk] O Destino do CRM é um carregamento diário de arquivo em lotes e não requer autenticação do usuário.

### Preencher Detalhes do Destino {#fill-in-details}

Antes de enviar ou ativar dados de público-alvo para um destino, você deve configurar uma conexão com sua própria plataforma de destino. Enquanto [configuração](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Tipo de conta]**: Escolha o **[!UICONTROL Conta existente]** opção.
* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante]**: seu [!DNL Trade Desk Advertiser ID], que podem ser compartilhados pelo seu [!DNL Trade Desk] Gerente de conta ou em [!DNL Advertiser Preferences] no [!DNL Trade Desk] IU.

![Captura de tela da interface do usuário da Platform mostrando como preencher detalhes do destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Ao se conectar ao destino, definir uma política de governança de dados é totalmente opcional. Revise o Experience Platform [visão geral da governança de dados](/help/data-governance/policies/overview.md) para obter mais detalhes.

## Ativar públicos para este destino {#activate}

Ler [ativar dados do público-alvo para destinos de exportação de perfis em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para um destino.

No **[!UICONTROL Agendamento]** você pode configurar o agendamento e os nomes de arquivo para cada público-alvo que está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

![Captura de tela da interface do usuário da Platform para agendar a ativação do público-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todos os públicos-alvo ativados para [!DNL The Trade Desk] O Destino do CRM é automaticamente definido como uma frequência diária e exportação completa de arquivo.

![Captura de tela da interface do usuário da Platform para agendar a ativação do público-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

No **[!UICONTROL Mapeamento]** , você deve selecionar atributos ou namespaces de identidade na coluna de origem e mapear para a coluna de destino.

![Captura de tela da interface do usuário da Platform para mapear a ativação de público-alvo.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Veja abaixo um exemplo do mapeamento de identidade correto ao ativar públicos para [!DNL The Trade Desk] Destino do CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] O Destino do CRM não aceita endereços de email brutos e com hash como identidades no mesmo fluxo de ativação. Crie fluxos de ativação separados para endereços de email brutos e com hash.

Selecionar campos de origem:

* Selecione o `Email` namespace ou atributo como identidade de origem se estiver usando o endereço de email bruto na assimilação de dados.
* Selecione o `Email_LC_SHA256` namespace ou atributo como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados na Platform.

Selecionar campos de destino:

* Entrada  `email` como identidade de destino quando o namespace ou atributo de origem é `Email`.
* Entrada  `hashed_email` como identidade de destino quando o namespace ou atributo de origem é `Email_LC_SHA256`.

## Validar exportação de dados {#validate}

Para validar se os dados foram exportados corretamente do Experience Platform e para [!DNL The Trade Desk], encontre os públicos-alvo no bloco de dados Adobe 1PD em [!DNL The Trade Desk] Plataforma de gerenciamento de dados (DMP). Estas são as etapas para encontrar a ID correspondente no [!DNL Trade Desk] Interface do usuário:

1. Primeiro, clique no link **[!UICONTROL Dados]** Guia e revisar **[!UICONTROL Primário]**.
2. Role para baixo na página, em **[!UICONTROL Dados importados]**, você encontrará a **[!UICONTROL Mosaico Adobe 1PD]**.
3. Clique no **[!UICONTROL Adobe 1PD]** bloco e listará todos os públicos-alvo ativados para o [!DNL Trade Desk] destino do seu anunciante. Você também pode usar a função de pesquisa.
4. O ID de segmento nº do Experience Platform será exibido como o Nome do segmento na [!DNL Trade Desk] IU.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
