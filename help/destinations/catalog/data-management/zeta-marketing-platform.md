---
title: Plataforma de marketing Zeta
description: A Zeta Marketing Platform (ZMP) é um sistema baseado em nuvem que ajuda a adquirir, expandir e reter clientes com mais eficiência, alimentado por inteligência (dados proprietários e IA).
hide: true
hidefromtoc: true
exl-id: 291ee60c-aa81-4f1e-9df2-9905a8eeb612
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 1%

---

# Plataforma de marketing Zeta {#zeta-marketing-platform}

## Visão geral {#overview}

A Zeta Marketing Platform (ZMP) é um sistema baseado em nuvem que ajuda a adquirir, expandir e reter clientes com mais eficiência, alimentado por inteligência (dados proprietários e IA). Para obter mais detalhes, consulte [Zeta Global](https://zetaglobal.com/).

Com o conector Zeta Marketing Platform disponível no Adobe Experience Platform, você pode sincronizar facilmente seus públicos do Experience Platform para o ZMP.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe *Zeta Global*. Para qualquer consulta ou solicitação de atualização, entre em contato com a equipe em [Fale conosco](https://zetaglobal.com/about/contact-us/).

## Casos de uso {#use-cases}

### Criar segmentos de público {#use-case-build-audiences}

Um profissional de marketing deseja criar perfis únicos de público-alvo, identificar seus segmentos mais valiosos e usá-los em qualquer canal digital compatível com a Plataforma de marketing Zeta. Eles desejam criar uma visualização verdadeira 360 de um perfil de consumidor, criar e ativar públicos-alvo significativos. Mais detalhes sobre quais canais a Plataforma Zeta Marketing suporta podem ser encontrados [aqui](https://zetaglobal.com/platform/integrations/).

### Direcione usuários com anúncios {#use-case-target-users}

Um anunciante tem como objetivo direcionar os usuários dentro de públicos-alvo específicos por meio do Zeta Demand Side Platform (DSP), já que esses usuários interagem com suas marcas. Para obter mais informações sobre o Zeta DSP, clique [aqui](https://knowledgebase.zetaglobal.com/pug/).

## Pré-requisitos {#prerequisites}

### Pré-requisitos da Zeta Marketing Platform

* Antes de configurar uma nova conexão com o destino Zeta Marketing Platform, você deve criar uma lista de clientes vazia em sua conta Zeta Marketing Platform. Você deve escolher uma dessas listas de clientes como público-alvo designado para receber o público-alvo da Adobe Experience Platform que planeja enviar. Você pode criar uma lista de clientes vazia no ZMP seguindo as instruções [aqui](https://knowledgebase.zetaglobal.com/kb/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Embora o Adobe Experience Platform permita a ativação de vários públicos-alvo para uma instância de destino ZMP específica, é obrigatório que cada instância de destino ZMP receba apenas um público-alvo do Experience Platform. Para lidar com vários públicos-alvo da Experience Platform, crie instâncias de destino ZMP adicionais para cada público-alvo e selecione uma lista de clientes diferente na lista suspensa. Essa abordagem garante que os públicos-alvo do ZMP não sejam substituídos. Consulte [Preencher detalhes do destino](#destination-details) para obter mais detalhes.
* Use as credenciais a seguir para configurar o destino:
   * Nome de usuário: **api**
   * Senha: sua chave de API REST ZMP. Você pode encontrar sua Chave de API REST fazendo logon em sua conta ZMP e navegando até a seção **Configurações** > **Integrações** > **Chaves e Aplicativos**. Consulte a [documentação do ZMP](https://knowledgebase.zetaglobal.com/kb/integrations) para obter mais detalhes.

## Identidades suportadas {#supported-identities}

O [!DNL Zeta Marketing Platform] dá suporte à ativação das IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> O destino Zeta Marketing Platform exige que você mapeie um namespace de identidade de origem para a identidade de destino ZMP `uid`. Isso ajuda a Zeta Marketing Platform a diferenciar cada perfil de forma exclusiva.

| Identidade de destino | Descrição | Considerações | Notas |
|---------|----------|----------|----------|
| uid | Identificador exclusivo que o ZMP usa para diferenciar perfis de clientes | Obrigatório | Escolha o namespace de identidade padrão `Email` se desejar identificar perfis únicos usando seus endereços de email. Como alternativa, você pode optar por mapear seu namespace personalizado para `uid` se os perfis do cliente não tiverem um email. |
| email_md5_id | Email MD5 que representa cada perfil de cliente | Opcional | Escolha essa identidade de público-alvo quando quiser identificar exclusivamente os perfis de clientes usando valores MD5 de email. É essencial que os endereços de email já estejam no formato MD5 no Experience Platform, pois o Experience Platform não converte texto sem formatação em MD5. Nesse cenário, defina `uid` (obrigatório) como os mesmos valores MD5 de email ou outro namespace de identidade apropriado. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | X | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

>[!NOTE]
> À medida que membros individuais são adicionados ou removidos do público-alvo do Experience Platform, as atualizações serão enviadas ao ZMP para garantir que a lista de clientes de destino seja sincronizada adequadamente.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do segmento, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]**: `api`
* **[!UICONTROL Password]**: sua chave de API REST ZMP. Você pode encontrar sua Chave de API REST fazendo logon em sua conta ZMP e navegando até a seção **Configurações** > **Integrações** > **Chaves e Aplicativos**. Consulte a [documentação do ZMP](https://knowledgebase.zetaglobal.com/kb/integrations) para obter mais detalhes.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Imagem mostrando a configuração ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ZMP Account Site Id]**: Seu **ID do Site** do ZMP para o qual você deseja enviar seus públicos-alvo. Você pode exibir sua Id do Site navegando até a seção **Configurações** > **Integrações** > **Chaves e Aplicativos**. Mais informações podem ser encontradas [aqui](https://knowledgebase.zetaglobal.com/kb/integrations).
* **[!UICONTROL ZMP Segment]**: o segmento da lista de clientes na sua conta de ID do site ZMP que você deseja atualizar com o público-alvo da Experience Platform.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e segmentos para destinos de exportação de segmento de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público para este destino.

### Mapear atributos e identidades {#map}

Veja abaixo um exemplo de mapeamento de identidade correto ao exportar perfis para [!DNL Zeta Marketing Platform].

Selecionar campos de origem:

* Selecione um namespace de identidade de origem (personalizado ou padrão, como `Email`) que identifique exclusivamente um perfil no Adobe Experience Platform e [!DNL Zeta Marketing Platform].
* Selecione quaisquer atributos de perfil de origem XDM que precisam ser exportados para e atualizados no [!DNL Zeta Marketing Platform].

Selecionar campos de destino:

* (Obrigatório) Selecione `uid` como a identidade de destino para a qual você mapeia um namespace de identidade de origem.
* (Opcional) Selecione `email_md5_id` como a identidade de destino para a qual você mapeou o namespace de identidade de origem que representa valores md5 de email. É essencial que os endereços de email já estejam no formato MD5 no Experience Platform, pois o Experience Platform não converte texto simples em MD5
* Selecione target mappings adicionais, se necessário.

![Mapeamento de identidade](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Uma ativação bem-sucedida do público-alvo do Experience Platform para a Zeta Marketing Platform atualiza a lista de clientes-alvo no ZMP. A contagem e os perfis de amostra na lista de clientes de destino serão iguais ao número de identidades que foram ativadas com êxito.

![Lista de Clientes no ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Cada membro do público ativado no Experience Platform também estará visível em **Públicos-alvo** > **Pessoas** no ZMP. Você também poderá exibir o segmento **Lista de Clientes** ao qual um perfil pertence na exibição Cliente Único, conforme mostrado abaixo.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [Base de Dados de Conhecimento Zeta](https://knowledgebase.zetaglobal.com/kb/)
