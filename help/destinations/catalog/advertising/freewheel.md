---
title: Conexão FreeWheel
description: Saiba como ativar públicos do Adobe Experience Platform para o FreeWheel para publicidade programática em inventários de TV, exibição e vídeo conectados.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 1f1d3e57-a8ef-4971-b3d1-43521bd158bb
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 8%

---

# [!DNL FreeWheel] conexão {#freewheel}

>[!AVAILABILITY]
>
>O destino [!DNL FreeWheel] está atualmente na Beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe.

## Visão geral {#overview}

[!DNL FreeWheel] é uma plataforma global de tecnologia de publicidade que possibilita compras e vendas programáticas em inventários de CTV (TV conectada), vídeo e exibição. A [!DNL FreeWheel] fornece um mercado orientado por dados que conecta anunciantes com proprietários de mídia premium no mundo inteiro.

Use este destino para enviar públicos de [!DNL Adobe Experience Platform] para [!DNL FreeWheel]. Os públicos são entregues como arquivos de lote diários e disponibilizados para direcionamento em [!DNL FreeWheel] ofertas e campanhas.

## Pré-requisitos {#prerequisites}

Antes de poder ativar públicos para [!DNL FreeWheel], analise os seguintes requisitos:

* **ID de rede do FreeWheel**: você deve ter uma ID de rede [!DNL FreeWheel] válida. Isso é fornecido por [!DNL FreeWheel] quando sua conta é configurada.

## Identidades suportadas {#supported-identities}

[!DNL FreeWheel] dá suporte à ativação das identidades descritas na tabela abaixo. Além dessas identidades, você pode usar qualquer identidade disponível em sua conta do [!DNL FreeWheel]. Consulte [Mapear atributos e identidades](#map) para obter instruções sobre como mapear uma identidade que não esteja na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade do público alvo | Descrição | Considerações |
|---|---|---|
| `idfa` | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| `aaid` | ANDROID ADVERTISING ID | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| `ctv` | ID do dispositivo de TV conectado | Selecione esta identidade de destino ao direcionar dispositivos CTV. |
| `ip` | Endereço IPv4 | Selecione esta identidade de destino para direcionar usuários com base em seus endereços IP. Mapeie um atributo de perfil contendo um endereço IPv4 válido ou use um campo calculado para derivar o valor. |
| `ipv6` | Endereço IPv6 | Selecione esta identidade de destino para direcionar usuários com base em seus endereços IPv6. Mapeie um atributo de perfil contendo um endereço IPv6 válido ou use um campo calculado para derivar o valor. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sim | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | Sim | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li>carregar audiências personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li>públicos-alvo semelhantes,</li><li>públicos federados,</li><li>públicos-alvo gerados em outros aplicativos Experience Platform, como [!DNL Adobe Journey Optimizer],</li><li>e muito mais.</li></ul> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Redirecionamento de CTV, supressão de alcance |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake [!DNL Adobe Experience Platform]. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um público-alvo, juntamente com os campos de identidade desejados, conforme escolhido na etapa de mapeamento do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Batch]** | A primeira exportação é um instantâneo completo de todos os perfis qualificados para os públicos ativados. As exportações subsequentes são atualizações incrementais diárias que incluem novas qualificações de público-alvo (adições) e saídas de público-alvo (remoções). Um intervalo de atualização de público-alvo completo configurável (4, 8 ou 12 semanas) também está disponível, acionando exportações completas periódicas, além dos incrementos diários. Exportações completas contêm apenas perfis qualificados no momento. As saídas de público-alvo não são incluídas e são fornecidas exclusivamente por meio das atualizações incrementais diárias. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

A autenticação para o destino [!DNL FreeWheel] é manipulada automaticamente pela Adobe. Nenhuma credencial ou chave de API é necessária durante a autenticação. O Adobe gerencia a conexão segura com [!DNL FreeWheel] em seu nome.

![Captura de tela da etapa de autenticação para o destino do FreeWheel.](../../assets/catalog/advertising/freewheel/connect-destination.png)

Selecione **[!UICONTROL Connect to destination]** para prosseguir para a etapa de detalhes do destino.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_freewheel_backfill"
>title="Intervalo de atualização de público-alvo completo"
>abstract="Selecione o intervalo em que uma exportação de público-alvo completa é enviada para [!DNL FreeWheel], além de atualizações incrementais diárias. Uma exportação de público-alvo completa impede que os membros do público-alvo expirem em [!DNL FreeWheel], de modo que você não experimente quedas nos membros direcionados enquanto suas campanhas estão em execução. As opções disponíveis são 4 semanas, 8 semanas e 12 semanas."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela de exemplo mostrando como preencher detalhes do destino FreeWheel.](../../assets/catalog/advertising/freewheel/destination-details.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Region]**: a região [!DNL FreeWheel] onde sua conta está hospedada. Selecione uma das seguintes opções:
   * **[!UICONTROL US East]**
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Asia Pacific]**
* **[!UICONTROL FreeWheel network ID]**: Sua ID de rede [!DNL FreeWheel]. Este valor é fornecido por [!DNL FreeWheel] e identifica exclusivamente sua organização na plataforma [!DNL FreeWheel].
* **[!UICONTROL Full audience refresh interval]**: a frequência na qual uma exportação de público-alvo completo é enviada para [!DNL FreeWheel] além de atualizações incrementais diárias. Uma exportação de público-alvo completa impede que os membros do público-alvo expirem em [!DNL FreeWheel], de modo que você não experimente quedas nos membros direcionados enquanto suas campanhas estão em execução. Selecione um intervalo na lista suspensa.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Agendar exportações de público {#schedule}

![Captura de tela da etapa Agendamento no fluxo de trabalho de ativação do FreeWheel.](../../assets/catalog/advertising/freewheel/scheduling.png)

Na etapa **[!UICONTROL Scheduling]**, configure o agendamento de exportação para cada público. [!DNL FreeWheel] usa um modelo de exportação híbrido: a primeira exportação para cada público ativado é um instantâneo completo, seguido de atualizações incrementais diárias.

Configure os seguintes campos:

* **[!UICONTROL File export options]**: **[!UICONTROL Export incremental files]** é pré-selecionado e é a única opção com suporte. A primeira exportação inclui automaticamente um instantâneo completo de todos os perfis qualificados. As exportações subsequentes oferecem apenas novas qualificações de público-alvo e saídas desde a última exportação.
* **[!UICONTROL Frequency]**: Selecione **[!UICONTROL Daily]**. [!DNL FreeWheel] espera a entrega diária de arquivos incrementais.
* **[!UICONTROL Scheduled start time]**: Insira a hora em UTC em que a exportação diária deve ser executada.
* **[!UICONTROL Date]**: Defina as datas de início e término da ativação. A data de início determina quando a primeira exportação de instantâneo completo é enviada.

>[!NOTE]
>
>Exportações completas (tanto o instantâneo inicial quanto as renovações completas periódicas) contêm apenas perfis qualificados no momento. As saídas de público-alvo não são incluídas em exportações completas e são entregues exclusivamente por meio de atualizações incrementais diárias.

### Mapear atributos e identidades {#map}

Na etapa de mapeamento, selecione os campos de origem dos perfis do Experience Platform e mapeie-os para os tipos de identidade compatíveis com o [!DNL FreeWheel]. Pelo menos um mapeamento é necessário.

>[!IMPORTANT]
>
>Os tipos de identidade [!DNL FreeWheel] com suporte são apresentados como **atributos de destino** na interface do usuário de mapeamento, não como namespaces de identidade.

Se a sua conta do [!DNL FreeWheel] suportar tipos de identidade que não estão listados na tabela [identidades com suporte](#supported-identities), você poderá mapeá-los inserindo manualmente o nome da identidade no campo de destino em vez de selecionar na lista predefinida.

![Captura de tela mostrando um nome de identidade personalizado digitado diretamente no campo de destino na etapa de mapeamento.](../../assets/catalog/advertising/freewheel/custom-identity.png)

Veja a seguir exemplos de mapeamentos. Os mapeamentos reais dependerão do esquema de perfil e dos tipos de identidade aceitos pela conta [!DNL FreeWheel].

| Campo de origem | Campo de destino |
| --- | --- |
| `identityMap.IDFA` | `idfa` |
| `identityMap.GAID` | `aaid` |
| `homeAddress.ipAddress` | `ip` |

{style="table-layout:auto"}

>[!NOTE]
>
>Nenhum mapeamento obrigatório é aplicado. No entanto, perfis sem pelo menos um mapeamento de identidade válido não serão incluídos nos arquivos exportados.

## Dados exportados / Validar exportação de dados {#exported-data}

[!DNL FreeWheel] recebe dois tipos de arquivos por exportação. Ambos os tipos de arquivos são gerados e entregues automaticamente. Não é necessária nenhuma ação da sua parte.

**Os arquivos de identidade (dados)** contêm os dados de associação de público-alvo. Cada linha mapeia um identificador do usuário para uma ou mais IDs de público-alvo. Os arquivos são entregues para [!DNL FreeWheel] no formato CSV sem cabeçalhos de coluna. Arquivos separados são produzidos para cada tipo de identidade presente na exportação (por exemplo, um arquivo para `aaid` e um arquivo separado para `idfa`).

Exemplo de formato de arquivo de dados:

```csv
aebc1234-56f7-89ab-cdef-0123456789ab,segment_1,segment_2
f7c9a8b0-4d33-11ec-81d3-0242ac130003,segment_1,segment_3
123e4567-e89b-12d3-a456-426614174000,segment_2
```

**Os arquivos de taxonomia** descrevem os públicos-alvo incluídos na exportação. Esses arquivos são entregues junto com os arquivos de dados e incluem a ID de público-alvo, o nome e o TTL (tempo de vida útil) em dias. O TTL máximo para o qual [!DNL FreeWheel] oferece suporte é de 90 dias. Os valores no exemplo abaixo são ilustrativos.

Exemplo de formato de arquivo de taxonomia:

```csv
Segment ID,Segment Name,TTL
segment_1,my_first_segment,30
segment_2,my_second_segment,30
segment_3,my_third_segment,30
```

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter informações adicionais sobre [!DNL FreeWheel] e sua plataforma de tecnologia de publicidade, consulte o [site do FreeWheel](https://www.freewheel.com){target="_blank"}.
