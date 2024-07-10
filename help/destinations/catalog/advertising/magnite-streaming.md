---
title: Magnite Streaming Conexão de destino em tempo real
description: Use esse destino para fornecer públicos-alvo da CDP do Adobe para a plataforma de transmissão Magnite em tempo real.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 2%

---


# (Beta) Magnite Streaming: conexão de destino em tempo real

## Visão geral {#overview}

A variável [!DNL Magnite Streaming: Real-Time] e a Magnite Streaming: os destinos em lote no Adobe Experience Platform ajudam a mapear e exportar públicos para direcionamento e ativação na plataforma Magnite Streaming.

Ativar públicos-alvo para o [!DNL Magnite Streaming] A plataforma do é um processo de duas etapas que requer o uso dos destinos Magnite Streaming: Tempo real e Magnite Streaming: Batch.

Para ativar os públicos para [!DNL Magnite Streaming], você deve:

* Ativar os públicos-alvo no [!DNL Magnite Streaming: Real-Time] como mostrado nesta página.
* Ative o mesmo público no destino Magnite Streaming: Batch. A variável [!DNL Magnite Streaming: Batch] o destino é um componente obrigatório. Falha ao ativar o público-alvo no [!DNL Magnite Streaming] O destino do lote resultará em uma falha de integração, e seus públicos-alvo não serão ativados.

Observação: ao usar o destino em Tempo real, [!DNL Magnite: Streaming] O receberá públicos-alvo em tempo real, mas só poderemos armazenar temporariamente públicos-alvo em tempo real em nossa plataforma e eles serão removidos do nosso sistema em alguns dias. Por isso, se quiser usar o destino Magnite: Streaming em Tempo Real, você *também* Precisar usar a Magnite Streaming: destino do lote - cada público-alvo ativado para o destino em tempo real, você também precisará ativar para o destino do lote.

>[!IMPORTANT]
>
>Este conector de destino está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe.
>
>O conector de destino e a página de documentação são criados e mantidos pelo [!DNL Magnite] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em `adobe-tech@magnite.com`.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Magnite Streaming: Real-Time] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Ativação e direcionamento {#activation-and-targeting}

Essa integração com a Magnite permite que os clientes transmitam seus públicos de CDP do Adobe Experience Platform para a Magnite para direcionamento de publicidade. Os públicos podem ser selecionados no Magnite para direcionamento positivo e negativo (supressão).

## Pré-requisitos {#prerequisites}

Para usar o [!DNL Magnite] destinos no Adobe Experience Platform, você deve primeiro ter uma [!DNL Magnite Streaming] conta. Se você tiver uma [!DNL Magnite Streaming] conta, entre em contato com o [!DNL Magnite] credenciais do gerente de conta a ser fornecido para acessar o [!DNL Magnite's] destinos.
Se você não tiver uma [!DNL Magnite Streaming] conta, entre em contato com adobe-tech@magnite.com

## Identidades suportadas {#supported-identities}

A variável [!DNL Magnite Streaming: Real-Time] o destino oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Um identificador exclusivo de um dispositivo ou identidade. Aceitamos qualquer ID de dispositivo e ID própria, independentemente do tipo. | Os tipos de identidade compatíveis incluem, entre outros, PPUID, GAID, IDFA e IDs de dispositivo de TV. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportação | **[!UICONTROL Exportação de segmentos]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no [!DNL Magnite Streaming: Real-Time] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

![campos de autenticação da configuração de destino não preenchidos](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Nome de usuário]**: o nome de usuário fornecido a você pelo [!DNL Magnite].
* **[!UICONTROL Senha]**: a senha fornecida a você pelo [!DNL Magnite].

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Nome do parceiro de origem]**: O nome do cliente/empresa. Somente compatíveis [!DNL Magnite Streaming] Os clientes do estão disponíveis para seleção.

![campos de autenticação da configuração de destino preenchidos](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Depois de concluído, selecione o **[!UICONTROL Criar]** botão.

![Política de governança e medidas de aplicação opcionais](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

Depois de criar a conexão de destino, você pode prosseguir para o fluxo de ativação de público. A seção a seguir mostra como ativar públicos-alvo usando o destino em tempo real.

### Mapear atributos e identidades {#map}

A próxima etapa é mapear identificadores de origem para o identificador device_id Magnite.

* Você pode adicionar quantos mapeamentos forem necessários selecionando **[!UICONTROL Adicionar novo mapeamento]**.

Este exemplo usando o destino em Tempo real mostra uma linha que contém um identificador de origem deviceId genérico mapeado para o campo de destino Magnite device_id. Quando estiver usando os mapeamentos, selecione [!UICONTROL Próxima].

![Mapeie os campos de dados desejados para o campo device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Defina as IDs de mapeamento para todos os públicos ativados ou defina NENHUM se nenhuma ID de mapeamento estiver presente.

![Defina as IDs de mapeamento para todos os públicos ativados ou defina NENHUM se nenhuma ID de mapeamento estiver presente](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Agora você deve configurar uma Data inicial (obrigatória), uma Data final (opcional) e uma ID de mapeamento para cada público-alvo.

**ID do mapeamento**

* Use o **[!UICONTROL ID do mapeamento]** quando um público-alvo tem uma ID de segmento pré-existente conhecida anteriormente pela Magnite.

* Para adicionar um **[!UICONTROL ID do mapeamento]** para selecionar um público-alvo, selecione cada linha de público-alvo individualmente e insira os dados na coluna à direita (consulte a imagem acima). Se não quiser adicionar uma ID de mapeamento, digite NONE no campo ID de mapeamento.

Selecionar **[!UICONTROL Próxima]** e finalize o fluxo de ativação.

![Selecione Próximo e finalize o fluxo de ativação.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que os públicos-alvo forem carregados, você poderá validar se os públicos-alvo foram criados e carregados corretamente seguindo estas etapas:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Assimilação pela Post, espera-se que os públicos-alvo apareçam em [!DNL Magnite Streaming] dentro de alguns minutos e pode ser aplicado a um acordo. Você pode confirmar isso verificando a ID do segmento que foi compartilhada durante as etapas de ativação no Adobe Experience Platform.

## Ative os mesmos públicos-alvo por meio do [!DNL Magnite Streaming: Batch]destino

Públicos-alvo compartilhados com [!DNL Magnite Streaming] o uso do destino em tempo real também precisará ser compartilhado usando o destino Magnite Streaming: Batch. Quando configurado corretamente, os nomes de segmento no [!DNL Magnite Streaming] A interface é atualizada para refletir aqueles usados na atualização pós-diária do Adobe Experience Platform.

Por fim, se um destino Batch não tiver sido configurado para sua integração, configure-o agora por meio do documento Magnite Streaming: Batch destination.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter a documentação de ajuda adicional, visite o [Magnite Help Center](https://help.magnite.com/help).
