---
title: Modelo de autoatendimento de documentação // Substituir pelo nome do seu destino
description: Use este modelo para criar documentação pública para seu destino no catálogo do Adobe Experience Platform. // Substitua pelo parágrafo na seção Visão geral
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# Conexão YourDestination {#your-destination}

*Conforme você passa por esse modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias do UICONTROL nesta página. Esta é uma tag que ajuda nossos processos de tradução automática a traduzir a página corretamente para os vários idiomas suportados. Adicionaremos tags à sua documentação após enviá-la.*

>[!IMPORTANT]
>
>* Preencha todas as seções neste template, na ordem em que são descritas no template.
>* Este modelo é atualizado com pouca frequência, com base no feedback do parceiro. Antes de começar a criar a documentação para o seu destino, baixe o [versão mais recente do modelo](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## Visão geral {#overview}

*Forneça uma breve visão geral da empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto para mais leitura.*

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela *YourDestination* equipe. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em *Insira o link ou endereço de email, onde você pode acessar para obter atualizações, por exemplo `support@YourDestination.com`.*

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável *YourDestination* destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1 {#use-case-1}

*Para plataformas de mensagens móveis:*

*Uma plataforma residencial de aluguel e vendas deseja enviar notificações móveis para os dispositivos Android e iOS dos clientes para que saibam que há 100 listas atualizadas na área em que eles buscaram anteriormente um aluguel.*

### Caso de uso nº 2 {#use-case-2}

*Para plataformas de rede social:*

*Uma marca de vestuário atlético quer alcançar clientes existentes por meio de suas contas de mídia social. A marca de vestuário pode assimilar endereços de email do próprio CRM para o Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para o Seu destino, para exibir anúncios nos feeds de mídia social de seus clientes.*

## Pré-requisitos {#prerequisites}

*Adicione informações nesta seção sobre qualquer coisa que os clientes precisam saber antes de começar a configurar o destino na interface do usuário do Adobe Experience Platform. Isso pode ser sobre:*

* *precisar ser adicionado a uma lista de permissões*
* *requisitos para hash de email*
* *qualquer conta específica do seu lado*
* *como obter uma chave de API para se conectar à sua plataforma*

*Você pode vincular à sua documentação relevante se isso for útil para os clientes.*

## Identidades suportadas {#supported-identities}

*Adicione informações nesta seção sobre as identidades suportadas pelo seu destino. Preenchemos previamente a tabela com alguns valores padrão. Exclua os valores que não se aplicam ao seu destino e quaisquer valores que não são pré-preenchidos.*

*YourDestination* O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | Google Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |
| ECID | Experience Cloud ID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Leia o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| external_id | IDs de usuário personalizadas | Selecione essa identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

*Na tabela , mantenha somente as linhas que correspondem ao seu destino. Você deve ter uma linha para o tipo Export e uma linha para a frequência Export . Exclua os valores que não se aplicam ao seu destino.*

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na *YourDestination* destino. |
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Tipo de exportação | **[!UICONTROL Exportação do conjunto de dados]** | Você está exportando conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações do público-alvo. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |
| Frequência de exportação | **[!UICONTROL Lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

*Adicione os campos que os clientes devem preencher ao autenticar para o destino. Esses campos são específicos do destino e dependem da sua configuração no Destination SDK. Os campos do seu destino podem não ser os mesmos listados abaixo. Por favor, inclua também uma captura de tela semelhante à captura de tela mostrada abaixo.*

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

![Exemplo de captura de tela mostrando como autenticar no destino](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Token de portador]**: Preencha o token portador para autenticar para o destino.

### Preencha os detalhes do destino {#destination-details}

*Adicione os campos que os clientes devem preencher ao configurar um novo destino. Esses campos são específicos do destino e dependem da sua configuração no Destination SDK. Os campos do seu destino podem não ser os mesmos listados abaixo. Por favor, inclua também uma captura de tela semelhante à captura de tela mostrada abaixo.*

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Exemplo de captura de tela mostrando como preencher os detalhes do seu destino](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu *YourDestination* ID da conta.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

*Exclua conforme apropriado - Se você estiver documentando um novo destino de transmissão, mantenha o primeiro parágrafo abaixo. Se você estiver documentando um novo destino baseado em arquivo, mantenha o segundo parágrafo. Se você estiver documentando um destino que exporta conjuntos de dados, mantenha o terceiro parágrafo.*

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

Ler [(Beta) Exportar conjuntos de dados](/help/destinations/ui/export-datasets.md) para obter instruções detalhadas sobre como exportar conjuntos de dados para esse destino.

### Mapear atributos e identidades {#map}

*Adicione informações sobre mapeamentos compatíveis entre campos de origem e de destino na etapa Mapeamento do fluxo de trabalho de ativação. Seu destino pode ser compatível com a exportação de atributos de perfil, namespaces de identidade ou ambos. Alguns campos podem ser obrigatórios. Os atributos do Target podem ser predefinidos ou personalizados. Chame os avisos importantes e use exemplos, de preferência com capturas de tela. Dois exemplos de páginas de destino que você pode usar como referência são:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Dados exportados / Validar exportação de dados {#exported-data}

*Adicione um parágrafo sobre como os dados são exportados para seu destino. Isso ajudaria o cliente a garantir que ele tenha integrado corretamente com seu destino. Por exemplo, você pode fornecer um JSON de amostra como o abaixo. Ou você pode fornecer capturas de tela e informações da interface do seu destino que mostram como os clientes devem esperar que os segmentos sejam preenchidos na plataforma de destino.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
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

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

*Você pode fornecer outros links para a documentação do seu produto ou outros recursos que você considere importantes para o sucesso do cliente.*