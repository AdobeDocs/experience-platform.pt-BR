---
title: Conexão com Medallia
description: Ative perfis para pesquisas direcionadas do Medallia e coleta de feedback para entender melhor as necessidades e expectativas dos clientes.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---

# Conexão com Medallia

## Visão geral {#overview}

Ative perfis para pesquisas direcionadas do Medallia e coleta de feedback para entender melhor as necessidades e expectativas dos clientes.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe do Medallia. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em adobe-integrations@medallia.com.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino Medallia, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Uma marca B2B deseja avaliar e simplificar seu programa de integração. Eles gostariam de enviar pesquisas personalizadas em tempo real para clientes que acabaram de concluir o processo de integração.

### Caso de uso #2

Um varejista deseja entender melhor as preferências do cliente para o atendimento do pedido. Eles desejam enviar uma breve pesquisa SMS com uma pergunta para clientes que fizeram compras online e na loja no mês passado.

## Pré-requisitos {#prerequisites}

As seguintes informações são necessárias para estabelecer a conexão com Medallia:
* **URL do ponto de extremidade do token OAuth**
* **ID do cliente**
* **Segredo do cliente**
* **URL do gateway da API**
* **Importar nome da API**

Trabalhe com a equipe de entrega da Medallia para obter esses detalhes.

## Identidades suportadas {#supported-identities}

O Medallia suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email | Endereço de email | Selecione a identidade de direcionamento de email quando quiser enviar pesquisas de convite por email. Quando um perfil é associado a vários endereços de email, o Medallia acionará o convite somente para o primeiro email. |
| Telefone | Números de telefone com hash no formato E.164 | Selecione a identidade de direcionamento do telefone quando quiser enviar pesquisas baseadas em SMS. O número de telefone deve estar no formato E.164, que inclui um sinal de adição (+), um código de chamada de país internacional, um código de área local e um número de telefone. Por exemplo: (+)(código do país)(código de área)(número de telefone). Quando um perfil é associado com vários números de telefone, o Medallia acionará o convite somente para o primeiro número de telefone. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros recém-qualificados de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil da [workflow de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL URL do ponto de extremidade do token OAuth]**: normalmente toma a forma de https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID do cliente]**: obtenha junto à equipe de delivery do Medallia.
* **[!UICONTROL Segredo do cliente]**: obtenha junto à equipe de delivery do Medallia.

![Imagem mostrando a tela de autenticação para este destino.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL URL do gateway da API]**: obtenha junto à equipe de delivery do Medallia. Normalmente assume a forma de https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importar nome da API]**: obtenha junto à equipe de delivery do Medallia. Nome da API de importação do Medallia (também conhecido como Feed da Web) a ser usada nesta conexão. Você pode ativar públicos diferentes para APIs de importação diferentes para acionar programas de pesquisa diferentes.

![Imagem mostrando a tela de detalhes do destino para este destino.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos e identidades {#map}

Os seguintes namespaces de identidade de destino devem ser mapeados dependendo do caso de uso:
* Para pesquisas baseadas em email, **email** deve ser mapeado como um campo de destino usando **Campo de destino** > **Selecionar namespace de identidade** > **email**
* Para pesquisas baseadas em SMS, **telefone** deve ser mapeado como um campo de destino usando **Campo de destino** > **Selecionar namespace de identidade** > **telefone**. Os números de telefone devem estar no formato E.164, que inclui um sinal de adição (+), um código de chamada de país internacional, um código de área local e um número de telefone

É altamente recomendável também mapear atributos personalizados adicionais do target para criar pesquisas personalizadas e anexar informações adicionais sobre o cliente ao registro da pesquisa:

* Pesquisas personalizadas geralmente abordam o cliente por nome
   * Mapear o nome do cliente para **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo** > **firstname**
   * Mapear o sobrenome do cliente para **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo** > **sobrenome**
* Adicione mapeamentos para quaisquer outros atributos personalizados do Target, conforme desejado

![Imagem que mostra um mapeamento de amostra para identidades e atributos.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Compartilhe com a equipe de entrega do Medallia o **Nomes de atributo** para cada atributo personalizado do target que você mapear usando **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo**. Talvez você queira fazer uma captura de tela da página de mapeamento para compartilhar diretamente.

## Dados exportados {#exported-data}

Depois de ativar seus segmentos para o destino, informe à equipe de entrega do Medallia, que poderá validar os dados exportados do Adobe Experience Platform para o Medallia. Observe que as pesquisas só podem ser ativadas no Medallia após a verificação bem-sucedida dos dados; antes disso, os dados serão exportados para o Medallia, mas não acionarão pesquisas para os clientes.

Um exemplo de JSON dos dados exportados é fornecido abaixo, que usa o mapeamento de exemplo da captura de tela acima no **Mapear atributos e identidades** seção:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
