---
title: Destino do Marketo Measure Ultimate
description: Saiba como conectar e ativar dados ao destino do Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 2%

---

# Destino do Marketo Measure Ultimate {#mmu-destination}

## Visão geral {#overview}

A Marketo Measure (anteriormente Bizible) fornece aos profissionais de marketing da insight quais esforços de marketing são os mais eficientes na geração de receita e na maximização do retorno sobre o investimento para sua empresa. O Marketo Measure é uma solução de atribuição de marketing que rastreia e cria relatórios sobre o desempenho do canal automaticamente, fornecendo visibilidade de quais canais estão gerando mais engajamento do cliente e permitindo otimizar adequadamente seus gastos com marketing.

O destino permite que os dados B2B (business-to-business) fluam do Adobe Experience Platform para o Marketo Measure. O cartão está disponível somente para clientes do Marketo Measure Ultimate.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do Marketo Measure, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino. Essa integração:

* Satisfaz os complexos requisitos de emissão de relatórios de dados e desempenho de grandes empresas.
* Permite relatórios de atribuição B2B com vários sistemas de CRM e automação de marketing.
* Fornece facilidade para trazer dados de ponto de contato offline de terceiros.

## Pré-requisitos {#prerequisites}

Observe os seguintes pré-requisitos para o destino do Marketo Measure:

* O mapeamento da sandbox da Experience Platform deve ser concluído na página de configurações do Marketo Measure pelo administrador. Sem o mapeamento de sandbox, não é possível concluir o fluxo de trabalho para se conectar ao destino salvar e ativar dados.
* Somente conjuntos de dados de classes XDM B2B podem ser exportados (consulte, por exemplo, as classes Conta de negócios XDM e Oportunidade de negócios XDM). Você não pode trazer vários conjuntos de dados da mesma classe XDM B2B para uma determinada fonte de dados.
* Cada conjunto de dados só pode ser incluído em um fluxo de dados para o destino do Marketo Measure.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Dataset export]** | Você está exportando conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações de público-alvo. Leia mais sobre [exportações do conjunto de dados](/help/destinations/destination-types.md#dataset-export-destinations). |
| Frequência de exportação | **[!UICONTROL Batch]** | Esse destino do lote exporta arquivos para a plataforma do Marketo Measure a cada duas horas. Leia mais sobre [agendando exportações do conjunto de dados](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage and Activate Dataset Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados na seção abaixo.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.

![O fluxo de trabalho Conectar ao destino do Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Exportar conjuntos de dados para este destino {#export-datasets}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa de **[!UICONTROL View Destinations]** e **[!UICONTROL Manage and Activate Dataset Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia o [Tutorial de exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md) para obter instruções detalhadas sobre como exportar conjuntos de dados para este destino.

## Validar exportação de dados {#exported-data}

Para validar uma exportação bem-sucedida do conjunto de dados, você pode verificar se o conjunto de dados foi enviado com êxito para o seu [data warehouse do Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=pt-BR).

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).
