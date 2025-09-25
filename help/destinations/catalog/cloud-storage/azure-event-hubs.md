---
keywords: destino do hub de eventos do Azure;hub de eventos do Azure;eventub do Azure
title: Conexão do Azure Event Hubs
description: Crie uma conexão de saída em tempo real com o armazenamento do  [!DNL Azure Event Hubs]  para transmitir dados do Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: d0ee4b30716734b8fce3509a6f3661dfa572cc9f
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 5%

---

# [!DNL Azure Event Hubs] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
> Este destino está disponível somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR).

[!DNL Azure Event Hubs] é uma plataforma de transmissão de big data e um serviço de assimilação de eventos. Ele pode receber e processar milhões de eventos por segundo. Os dados enviados para um hub de eventos podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

Você pode criar uma conexão de saída em tempo real com o armazenamento do [!DNL Azure Event Hubs] para transmitir dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Azure Event Hubs], consulte a [documentação do Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para se conectar a [!DNL Azure Event Hubs] de forma programática, consulte o [Tutorial da API de destinos de streaming](../../api/streaming-destinations.md).
* Para se conectar a [!DNL Azure Event Hubs] usando a interface do usuário do Experience Platform, consulte as seções abaixo.

![AWS Kinesis na interface do usuário](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de transmissão como o [!DNL Azure Event Hubs], é possível alimentar facilmente eventos de segmentação de alto valor e atributos de perfil associados em seus sistemas de escolha.

Por exemplo, um cliente potencial baixou um white paper que os qualifica em um segmento de &quot;alta propensão para conversão&quot;. Ao mapear o público-alvo no qual o cliente potencial se enquadra no destino [!DNL Azure Event Hubs], você receberia esse evento em [!DNL Azure Event Hubs]. Lá, você pode empregar uma abordagem do tipo &quot;faça você mesmo&quot; e descrever a lógica de negócios sobre o evento, pois acha que funcionaria melhor com os sistemas de TI de sua empresa.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allowlist}

Para atender aos requisitos de segurança e conformidade dos clientes, a Experience Platform incluir na lista de permissões fornece uma lista de IPs estáticos que você pode pesquisar pelo destino [!DNL Azure Event Hubs]. Consulte a [lista de permissões de endereço IP para destinos de streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obter a lista completa de IPs a serem incluídos na lista de permissões.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). Ao se conectar a esse destino, você deve fornecer as seguintes informações:

### Informações de autenticação {#authentication-information}

#### Autenticação padrão {#standard-authentication}

![Imagem da tela da interface do usuário mostrando campos concluídos para os detalhes de autenticação padrão dos Hubs de Eventos do Azure](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Se você selecionar o tipo **[!UICONTROL Autenticação padrão]** para se conectar ao seu ponto de extremidade HTTP, insira os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

* **[!UICONTROL Nome da Chave SAS]**: o nome da regra de autorização, que também é conhecido como o nome da chave SAS.
* **[!UICONTROL Chave SAS]**: a chave primária do namespace de Hubs de Eventos. O `sasPolicy` ao qual `sasKey` corresponde deve ter os direitos **manage** configurados para que a lista de Hubs de Eventos seja populada. Saiba mais sobre como autenticar para [!DNL Azure Event Hubs] com chaves SAS na [documentação do Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: preencha seu namespace [!DNL Azure Event Hubs]. Saiba mais sobre os namespaces [!DNL Azure Event Hubs] na [documentação do Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Autenticação SAS (Assinatura de Acesso Compartilhado) {#sas-authentication}

![Imagem da tela da interface do usuário mostrando campos concluídos para os detalhes de autenticação padrão dos Hubs de Eventos do Azure](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Se você selecionar o tipo **[!UICONTROL Autenticação padrão]** para se conectar ao seu ponto de extremidade HTTP, insira os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

* **[!UICONTROL Nome da Chave SAS]**: o nome da regra de autorização, que também é conhecido como o nome da chave SAS.
* **[!UICONTROL Chave SAS]**: a chave primária do namespace de Hubs de Eventos. O `sasPolicy` ao qual `sasKey` corresponde deve ter os direitos **manage** configurados para que a lista de Hubs de Eventos seja populada. Saiba mais sobre como autenticar para [!DNL Azure Event Hubs] com chaves SAS na [documentação do Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: preencha seu namespace [!DNL Azure Event Hubs]. Saiba mais sobre os namespaces [!DNL Azure Event Hubs] na [documentação do Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nome do Hub de Eventos]**: preencha com seu nome [!DNL Azure Event Hub]. Saiba mais sobre os nomes de [!DNL Azure Event Hubs] na [documentação do Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Incluir nomes de segmentos"
>abstract="Ative se quiser que a exportação de dados inclua os nomes dos públicos-alvo que você está exportando. Consulte a documentação para ver um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Incluir carimbos de data e hora do segmento"
>abstract="Ative se quiser que a exportação de dados inclua o carimbo de data e hora UNIX de quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data e hora UNIX de quando os públicos-alvo foram mapeados para o destino para ativação. Consulte a documentação para ver um exemplo de exportação de dados com esta opção selecionada."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Imagem da tela da interface do usuário mostrando campos concluídos para os detalhes de destino do Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nome]**: preencha um nome para a conexão com [!DNL Azure Event Hubs].
* **[!UICONTROL Descrição]**: forneça uma descrição da conexão.  Exemplos: &quot;Clientes de nível Premium&quot;, &quot;Clientes interessados em kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: forneça um nome para o fluxo ao seu destino [!DNL Azure Event Hubs].
* **[!UICONTROL Incluir nomes de segmentos]**: alterne se quiser que a exportação de dados inclua os nomes dos públicos-alvo que você está exportando. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte a seção [Dados exportados](#exported-data), mais abaixo.
* **[!UICONTROL Incluir carimbos de data/hora do segmento]**: ative se desejar que a exportação de dados inclua o carimbo de data/hora UNIX quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data/hora UNIX quando os públicos-alvo foram mapeados para o destino para ativação. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte a seção [Dados exportados](#exported-data), mais abaixo.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* [A avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) não tem suporte atualmente em exportações para o destino dos Hubs de Eventos do Azure. [Leia mais](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consulte [Ativar dados de público-alvo para destinos de exportação de perfil de streaming](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação de perfis para o seu destino [!DNL Azure Event Hubs], a fim de exportar dados somente para o seu destino quando atualizações relevantes para um perfil tiverem ocorrido após a qualificação de público-alvo ou outros eventos significativos. Os perfis são exportados para seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração na associação de público-alvo para pelo menos um dos públicos-alvo mapeados para o destino. Por exemplo, o perfil se qualificou para um dos públicos mapeados para o destino ou saiu de um dos públicos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos públicos-alvo mapeados para o destino recebeu uma nova identidade no atributo de mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos de pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis em que ocorreram atualizações relevantes são exportados para o seu destino. Por exemplo, se um público-alvo mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde estejam as alterações. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#what-determines-export-what-is-included}

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para seu [!DNL Azure Event Hubs] destino* e *quais dados são incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como dica para uma exportação de destino. Isso significa que se o status `segmentMembership` de um perfil for alterado para `realized` ou `exiting` ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como atualmente as identidades não podem ser mapeadas para [!DNL Azure Event Hubs] destinos, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração em um atributo é definida como qualquer atualização no atributo, seja ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração, mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>**Observação**: o comportamento de exportação para destinos do Azure Event Hubs foi atualizado com a versão de setembro de 2025. O novo comportamento destacado abaixo atualmente se aplica somente aos novos destinos do Azure Event Hubs criados após esta versão. Para destinos existentes do Hub de Eventos do Azure, você pode continuar usando o comportamento de exportação antigo ou entrar em contato com a Adobe para migrar para o novo comportamento em que somente os públicos mapeados são exportados. Todas as organizações serão migradas gradualmente para o novo comportamento em 2026. <br><br> <span class="preview"> **Novo comportamento de exportação**: os segmentos mapeados para o destino e alterados serão incluídos no objeto segmentMembership. Em alguns cenários, eles podem ser exportados usando várias chamadas. Além disso, em alguns cenários, alguns segmentos que não foram alterados também podem ser incluídos na chamada do. Em qualquer caso, somente segmentos mapeados no fluxo de dados serão exportados.</span></li><br>**Comportamento antigo**: o objeto `segmentMembership` inclui o segmento mapeado no fluxo de dados de ativação, para o qual o status do perfil foi alterado após um evento de qualificação ou saída de segmento. Outros segmentos não mapeados para os quais o perfil qualificado pode fazer parte da exportação de destino, se esses segmentos pertencerem à mesma [política de mesclagem](/help/profile/merge-policies/overview.md) que o segmento mapeado no fluxo de dados de ativação. <li>Todas as identidades no objeto `identityMap` também estão incluídas (no momento, o Experience Platform não oferece suporte ao mapeamento de identidade no destino [!DNL Azure Event Hubs]).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

>[!BEGINSHADEBOX]

Por exemplo, considere esse fluxo de dados para um destino [!DNL Azure Event Hubs] onde três públicos-alvo são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![Fluxo de dados de destino do Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para ou saindo dos *três segmentos mapeados*. Na exportação de dados, no objeto `segmentMembership` (consulte a seção [Dados Exportados](#exported-data) abaixo), outros públicos mapeados poderão aparecer se esse perfil específico for membro deles e se eles compartilharem a mesma política de mesclagem que o público-alvo que acionou a exportação. Se um perfil se qualificar para o segmento **Cliente com Carros DeLoree** e também for membro dos segmentos **Ativo do Site Básico e Cidade - Dallas**, esses outros dois públicos-alvo também estarão presentes no objeto `segmentMembership` da exportação de dados, porque eles são mapeados no fluxo de dados, se compartilharem a mesma política de mesclagem com o segmento **Cliente com Carros DeLosands**.

Do ponto de vista dos atributos de perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

>[!ENDSHADEBOX]

## Preenchimento retroativo de dados históricos {#historical-data-backfill}

Quando você adiciona um novo público a um destino existente ou cria um novo destino e mapeia públicos a ele, o Experience Platform exporta dados históricos de qualificação de público para o destino. Os perfis qualificados para o público-alvo *antes* de o público-alvo ser adicionado ao destino são exportados para o destino em aproximadamente uma hora.

## Dados exportados {#exported-data}

Os dados exportados do [!DNL Experience Platform] chegam ao destino [!DNL Azure Event Hubs] no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento, é um membro de outros dois segmentos e saiu de outro segmento. A exportação também inclui o nome, sobrenome, data de nascimento e endereço de email pessoal do atributo de perfil. As identidades para esse perfil são ECID e email.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

Abaixo estão mais exemplos de dados exportados, dependendo das configurações de interface do usuário que você selecionar no fluxo de destino de conexão para as opções **[!UICONTROL Incluir nomes de segmento]** e **[!UICONTROL Incluir carimbos de data/hora de segmento]**:

+++ A amostra de exportação de dados abaixo inclui nomes de público na seção `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ A amostra de exportação de dados abaixo inclui carimbos de data/hora de público-alvo na seção `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Política de limites e novas tentativas {#limits-retry-policy}

Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência de menos de 10 minutos para mensagens enviadas com êxito, com uma taxa de menos de 10 mil solicitações por segundo para cada fluxo de dados a um destino HTTP.

No caso de solicitações com falha para o destino da API HTTP, o Experience Platform armazena as solicitações com falha e tenta enviar as solicitações duas vezes para o seu endpoint.

>[!MORELIKETHIS]
>
>* [Conecte-se aos Hubs de Eventos do Azure e ative os dados usando a API de Serviço de Fluxo](../../api/streaming-destinations.md)
>* [Destino do AWS Kinesis](./amazon-kinesis.md)
>* [Tipos e categorias de destino](../../destination-types.md)
