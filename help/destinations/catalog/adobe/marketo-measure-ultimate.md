---
title: Destino do Marketo Measure Ultimate
description: Saiba como conectar e ativar dados ao destino do Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
source-git-commit: c2c7a4cd860fed2c8124fe46fe3fd405ba49ecf4
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Destino do Marketo Measure Ultimate {#mmu-destination}

## Visão geral {#overview}

O Marketo Measure (anteriormente Bizible) fornece aos profissionais de marketing informações sobre quais esforços de marketing são os mais eficientes na geração de receita e na maximização do retorno sobre o investimento para sua empresa. O Marketo Measure é uma solução de atribuição de marketing que rastreia e cria relatórios sobre o desempenho do canal automaticamente, fornecendo visibilidade de quais canais estão gerando mais engajamento do cliente e permitindo otimizar adequadamente seus gastos com marketing.

O destino permite que os dados B2B (business-to-business) fluam do Adobe Experience Platform para o Marketo Measure. O cartão só está disponível para clientes do Marketo Measure Ultimate.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do Marketo Measure, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino. Essa integração:

* Satisfaz os complexos requisitos de emissão de relatórios de dados e desempenho de grandes empresas.
* Permite relatórios de atribuição B2B com vários sistemas de CRM e automação de marketing.
* Fornece facilidade para trazer dados de ponto de contato offline de terceiros.

## Pré-requisitos {#prerequisites}

Observe os seguintes pré-requisitos para o destino do Marketo Measure:

* O mapeamento da sandbox Experience Platform deve ser concluído na página de configurações do Marketo Measure pelo administrador. Sem o mapeamento de sandbox, não é possível concluir o fluxo de trabalho para se conectar ao destino salvar e ativar dados.
* Somente conjuntos de dados de classes XDM B2B podem ser exportados (consulte, por exemplo, as classes Conta de negócios XDM e Oportunidade de negócios XDM). Você não pode trazer vários conjuntos de dados da mesma classe XDM B2B para uma determinada fonte de dados.
* Cada conjunto de dados só pode ser incluído em um fluxo de dados para o destino do Marketo Measure.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação do conjunto de dados]** | Você está exportando conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações de público-alvo. Leia mais sobre [exportações do conjunto de dados](/help/destinations/destination-types.md#dataset-export-destinations). |
| Frequência de exportação | **[!UICONTROL Lote]** | Esse destino do lote exporta arquivos para a plataforma do Marketo Measure a cada duas horas. Leia mais sobre [agendamento de exportações de conjunto de dados](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados na seção abaixo.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

![O workflow Conectar ao destino para o destino do Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Exportar conjuntos de dados para este destino {#export-datasets}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Leia o [(Beta) Exportar conjuntos de dados](/help/destinations/ui/export-datasets.md) tutorial para obter instruções abrangentes sobre como exportar conjuntos de dados para este destino.

## Validar exportação de dados {#exported-data}

Para validar uma exportação bem-sucedida do conjunto de dados, você pode verificar se o conjunto de dados foi enviado com êxito para a [data warehouse do Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=en).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).


