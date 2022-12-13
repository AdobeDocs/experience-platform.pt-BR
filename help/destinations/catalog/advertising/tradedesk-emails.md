---
title: (Beta) A conexão do Trade Desk - CRM
description: Ative perfis para sua conta do Trade Desk para direcionamento e supressão de público-alvo com base em dados de CRM.
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---

# (Beta) O [!DNL Trade Desk] - Conexão CRM

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] no Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

>[!IMPORTANT]
>
> Esta página de documentação foi criada pela *[!DNL Trade Desk]* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato com seu [!DNL Trade Desk] representante.

Este documento foi projetado para ajudar você a ativar perfis para sua [!DNL Trade Desk] considere o direcionamento e a supressão do público-alvo com base nos dados do CRM.

>[!TIP]
>
>Use [!DNL The Trade Desk] Destino do CRM para mapeamento de dados do CRM, como email ou endereço de email com hash. Use o [outro destino do Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) no catálogo do Adobe Experience Platform para obter cookies e mapeamentos de ID de dispositivo.

[!DNL The Trade Desk] O (TTD) não lida diretamente com o arquivo de upload de endereços de email a qualquer momento, nem [!DNL The Trade Desk] armazene seus emails brutos (sem hash).

## Pré-requisitos {#prerequisites}

Antes de poder ativar segmentos para [!DNL The Trade Desk], você deve entrar em contato com seu [!DNL The Trade Desk] gerente de conta para assinar o contrato de integração do CRM. [!DNL The Trade Desk] O concederá permissão e compartilhará sua ID do anunciante para configurar seu destino.

## Requisitos de correspondência de ID {#id-matching-requirements}

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes. Leia o [Visão geral do Namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR) para obter mais informações.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções na seção Requisitos de correspondência da ID e use os namespaces apropriados para endereços de email com texto simples e com hash, respectivamente.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| Email | Endereços de email (texto limpo) | Selecione o `Email` identidade do target quando sua identidade de origem for um namespace ou atributo de email. |
| Email_LC_SHA256 | Os endereços de email precisam ser transformados em hash usando SHA256 e em minúsculas. Certifique-se de seguir qualquer [normalização de email](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regras necessárias. Você não poderá alterar essa configuração posteriormente. | Selecione o `Email_LC_SHA256` identidade do target quando sua identidade de origem for um namespace ou atributo Email_LC_SHA256. |

{style=&quot;table-layout:auto&quot;}

## Requisitos de hash de email {#hashing-requirements}

Você pode fazer hash de endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email brutos.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte o [visão geral da ingestão em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os seguintes requisitos:

* Remova os espaços à esquerda e à direita.
* Converta todos os caracteres ASCII em minúsculas.
* Em `gmail.com` endereços de email, remova os seguintes caracteres da parte do nome de usuário do endereço de email:
   * O período (. (Código ASCII 46). Por exemplo, normalize `jane.doe@gmail.com` para `janedoe@gmail.com`.
   * O sinal de mais (+ (código ASCII 43)) e todos os caracteres subsequentes. Por exemplo, normalize `janedoe+home@gmail.com` para `janedoe@gmail.com`.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (email ou email com hash) usados no destino do Trade Desk. |
| Frequência de exportação | **[!UICONTROL Lote diário]** | Como um perfil é atualizado no Experience Platform com base na avaliação de segmento, ele é atualizado uma vez por dia, a partir da plataforma de destino. Leia mais sobre [uploads em lote](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

### Autenticar para destino {#authenticate}

[!DNL The Trade Desk] O Destino do CRM é um upload diário de arquivos em lote e não requer autenticação do usuário.

### Preencha os detalhes do destino {#fill-in-details}

Antes de enviar ou ativar os dados do público-alvo para um destino, você deve configurar uma conexão com sua própria plataforma de destino. Ao [configuração](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Tipo de conta]**: Escolha a **[!UICONTROL Conta existente]** opção.
* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante]**: your [!DNL Trade Desk Advertiser ID], que pode ser compartilhado pelo [!DNL Trade Desk] Gerente de conta ou localizado em [!DNL Advertiser Preferences] no [!DNL Trade Desk] IU.

Ao se conectar ao destino, a configuração de uma política de governança de dados é totalmente opcional. Revise o Experience Platform [visão geral de governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) para obter mais detalhes.

## Ativar segmentos para este destino {#activate}

Consulte [ativar dados do público-alvo para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) para obter instruções sobre como ativar segmentos de público-alvo para um destino.

No **[!UICONTROL Agendamento]** você pode configurar o agendamento e os nomes de arquivo para cada segmento que está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

>[!NOTE]
>
>Todos os segmentos ativados para [!DNL The Trade Desk] O Destino do CRM é automaticamente definido para uma frequência diária e exportação completa de arquivos.

No **[!UICONTROL Mapeamento]** na página, você deve selecionar atributos ou namespaces de identidade da coluna de origem e mapear para a coluna de destino.

Abaixo está um exemplo do mapeamento de identidade correto ao ativar segmentos para [!DNL The Trade Desk] Destino do CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] O Destino do CRM não aceita endereços de email brutos e com hash como identidades no mesmo fluxo de ativação. Crie fluxos de ativação separados para endereços de email brutos e com hash.

Seleção de campos de origem:

* Selecione o `Email` namespace ou atributo como identidade de origem, se estiver usando o endereço de email bruto na assimilação de dados.
* Selecione o `Email_LC_SHA256` namespace ou atributo como identidade de origem se você tiver hash nos endereços de email do cliente na assimilação de dados no Platform.

Seleção de campos de destino:

* Selecione o `Email` namespace como identidade de destino quando o namespace ou atributo de origem for `Email`.
* Selecione o `Email_LC_SHA256` namespace como identidade de destino quando o namespace ou atributo de origem for `Email_LC_SHA256`.

## Validar exportação de dados {#validate}

Para validar se os dados são exportados corretamente do Experience Platform e para [!DNL The Trade Desk], encontre os segmentos no bloco de dados Adobe 1PD dentro [!DNL The Trade Desk] Plataforma de gerenciamento de dados (DMP). Estas são as etapas para encontrar a ID correspondente na variável [!DNL Trade Desk] IU:

1. Primeiro, clique no botão **[!UICONTROL Dados]** Guia e revisão **[!UICONTROL Primários]**.
2. Role a página para baixo, em **[!UICONTROL Dados importados]**, você encontrará o **[!UICONTROL Bloco Adobe 1PD]**.
3. Clique no link**[!UICONTROL Adobe 1PD]** bloco e listará todos os segmentos ativados para o [!DNL Trade Desk] destino do seu anunciante. Você também pode usar a função de pesquisa.
4. O ID do segmento # from Experience Platform será exibido como o Nome do segmento no [!DNL Trade Desk] IU.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).
