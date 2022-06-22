---
title: Ligação Medallia
description: Ative perfis para pesquisas direcionadas da Medallia e coleta de feedback para entender melhor as necessidades e expectativas do cliente.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 2%

---


# Ligação Medallia

## Visão geral {#overview}

Ative perfis para pesquisas direcionadas da Medallia e coleta de feedback para entender melhor as necessidades e expectativas do cliente.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela equipe Medallia. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em adobe-integrations@medallia.com.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino Medallia, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Uma marca B2B deseja avaliar e simplificar seu programa de integração. Eles gostariam de enviar pesquisas personalizadas em tempo real para clientes que acabaram de concluir o processo de integração.

### Caso de uso nº 2

Um varejista deseja entender melhor as preferências do cliente para o cumprimento de pedidos. Eles desejam enviar uma breve pesquisa por SMS de 1 pergunta para clientes que fizeram compras online e na loja no mês passado.

## Pré-requisitos {#prerequisites}

Para estabelecer a ligação Medallia são necessárias as seguintes informações:
* **URL do Endpoint de token OAuth**
* **ID do cliente**
* **Segredo do cliente**
* **URL do gateway da API**
* **Importar nome da API**

Entre em contato com a equipe de entrega de Medallia para obter esses detalhes.

## Identidades suportadas {#supported-identities}

Medallia suporta a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| email | Endereço de email | Selecione a identidade de destino do email quando desejar enviar pesquisas por convite por email. Quando um perfil é associado a vários endereços de email, o Media acionará o convite somente para o primeiro email. |
| Telefone | Números de telefone com hash no formato E.164 | Selecione a identidade de destino do telefone quando quiser enviar pesquisas baseadas em SMS. O número de telefone deve estar no formato E.164, que inclui um sinal de mais (+), um código de chamada internacional, um código de área local e um número de telefone. Por exemplo: (+)(código do país)(código da área)(número de telefone). Quando um perfil é associado a vários números de telefone, Medallia acionará o convite somente para o primeiro número de telefone. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros recém-qualificados de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!UICONTROL URL do Endpoint de token OAuth]**: Normalmente assume a forma de https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID do cliente]**: Obtenha da equipe de entrega de Medallia.
* **[!UICONTROL Segredo do cliente]**: Obtenha da equipe de entrega de Medallia.

![Imagem que mostra a tela de autenticação para esse destino.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL URL do gateway da API]**: Obtenha da equipe de entrega de Medallia. Normalmente assume a forma de https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importar nome da API]**: Obtenha da equipe de entrega de Medallia. Nome da API de importação do Medallia (também conhecida como Feed da Web) a ser usada nesta conexão. É possível ativar diferentes segmentos para diferentes APIs de Importação para acionar diferentes programas de pesquisa.

![Imagem que mostra a tela de detalhes do destino para esse destino.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Mapear atributos e identidades {#map}

Os seguintes namespace de identidade de destino devem ser mapeados, dependendo do caso de uso:
* Para pesquisas por email, **email** deve ser mapeado como um campo de destino usando **Campo de destino** > **Selecionar namespace de identidade** > **email**
* Para pesquisas baseadas em SMS, **Telefone** deve ser mapeado como um campo de destino usando **Campo de destino** > **Selecionar namespace de identidade** > **Telefone**. Os números de telefone devem estar no formato E.164, que inclui um sinal de adição (+), um código internacional de chamada do país, um código de área local e um número de telefone

É altamente recomendável também mapear atributos personalizados do target adicionais para criar pesquisas personalizadas e anexar informações adicionais sobre o cliente ao registro da pesquisa:

* As pesquisas personalizadas geralmente abordam o cliente por nome
   * Mapeie o nome do cliente para **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo** > **firstname**
   * Mapeie o sobrenome do cliente para **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo** > **lastname**
* Adicione mapeamentos para qualquer outro atributo personalizado de destino, conforme desejado

![Imagem que mostra um exemplo de mapeamento de identidades e atributos.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Compartilhe com sua equipe de entrega da Medallia os detalhes exatos **Nomes dos atributos** para cada atributo personalizado do target que você mapeia usando **Campo de destino** > **Selecionar atributos personalizados** > **Nome do atributo**. É possível capturar a tela da página de mapeamento para compartilhar diretamente.

## Dados exportados {#exported-data}

Depois de ativar seus segmentos no destino, informe a equipe de delivery de Medallia, que poderá validar os dados exportados do Adobe Experience Platform para Medallia. Note-se que os inquéritos só podem ser ativados em Medallia após verificação bem sucedida dos dados; antes disso, os dados serão exportados para Medallia, mas não acionarão pesquisas para os clientes.

Um exemplo de JSON dos dados exportados é fornecido abaixo, que usa o exemplo de mapeamento da captura de tela acima no **Mapear atributos e identidades** seção:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).
