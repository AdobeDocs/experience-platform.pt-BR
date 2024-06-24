---
title: Plataforma de marketing Zeta
description: A Zeta Marketing Platform (ZMP) é um sistema baseado em nuvem que ajuda a adquirir, expandir e reter clientes com mais eficiência, alimentado por inteligência (dados proprietários e IA).
hide: true
hidefromtoc: true
source-git-commit: bf553371316d9d9cb368fc4d1be14196201ef680
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Plataforma de marketing Zeta {#zeta-marketing-platform}

## Visão geral {#overview}

A Zeta Marketing Platform (ZMP) é um sistema baseado em nuvem que ajuda a adquirir, expandir e reter clientes com mais eficiência, alimentado por inteligência (dados proprietários e IA). Para obter mais detalhes, consulte [Zeta Global](https://zetaglobal.com/).

Com o conector Zeta Marketing Platform disponível no Adobe Experience Platform, você pode sincronizar facilmente seus públicos do Experience Platform para o ZMP.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pelo *Zeta Global* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato com a equipe em [Entre em contato](https://zetaglobal.com/about/contact-us/).

## Casos de uso {#use-cases}

### Criar segmentos de público {#use-case-build-audiences}

Um profissional de marketing deseja criar perfis únicos de público-alvo, identificar seus segmentos mais valiosos e usá-los em qualquer canal digital compatível com a Plataforma de marketing Zeta. Eles desejam criar uma visualização verdadeira 360 de um perfil de consumidor, criar e ativar públicos-alvo significativos. Mais detalhes sobre quais canais a Plataforma de marketing Zeta suporta podem ser encontrados [aqui](https://zetaglobal.com/platform/integrations/).

### Direcione usuários com anúncios {#use-case-target-users}

Um anunciante tem como objetivo direcionar os usuários dentro de públicos-alvo específicos por meio do Demand Side Platform Zeta (DSP), já que esses usuários interagem com suas marcas. Para obter mais informações sobre o DSP Zeta, clique em [aqui](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## Pré-requisitos {#prerequisites}

### Pré-requisitos da Zeta Marketing Platform

* Antes de configurar uma nova conexão com o destino Zeta Marketing Platform, você deve criar uma lista de clientes vazia em sua conta Zeta Marketing Platform. Você deve escolher uma dessas listas de clientes como público-alvo designado para receber o público-alvo da Adobe Experience Platform que planeja enviar. Você pode criar uma lista de clientes vazia no ZMP seguindo as instruções [aqui](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Embora o Adobe Experience Platform permita a ativação de vários públicos-alvo para uma instância de destino ZMP específica, é obrigatório que cada instância de destino ZMP receba apenas um público-alvo Experience Platform. Para lidar com vários públicos-alvo do Experience Platform, crie instâncias de destino ZMP adicionais para cada público-alvo e selecione uma lista de clientes diferente na lista suspensa. Essa abordagem garante que os públicos-alvo do ZMP não sejam substituídos. Consulte [Preencher detalhes do destino](#destination-details) para obter mais detalhes.
* Use as credenciais a seguir para configurar o destino:
   * Nome de usuário: **api**
   * Senha: sua chave de API REST ZMP. Você pode encontrar sua chave de API REST fazendo logon em sua conta ZMP e navegando até **Configurações** > **Integrações** > **Chaves e aplicativos** seção. Consulte a [Documentação ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) para obter mais detalhes.

## Identidades suportadas {#supported-identities}

[!DNL Zeta Marketing Platform] O é compatível com a ativação de IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> O destino da Zeta Marketing Platform exige que você mapeie um namespace de identidade de origem para o ZMP `uid` identidade do público alvo. Isso ajuda a Zeta Marketing Platform a diferenciar cada perfil de forma exclusiva.

| Identidade de destino | Descrição | Considerações | Notas |
---------|----------|----------|----------|
| uid | Identificador exclusivo que o ZMP usa para diferenciar perfis de clientes | Obrigatório | Escolha o `Email` namespace de identidade padrão se quiser identificar perfis únicos usando seus endereços de email. Como alternativa, você pode optar por mapear o namespace personalizado para `uid` se os perfis do cliente não tiverem um email. |
| email_md5_id | Email MD5 que representa cada perfil de cliente | Opcional | Escolha essa identidade de público-alvo quando quiser identificar exclusivamente os perfis de clientes usando valores MD5 de email. É essencial que os endereços de email já estejam no formato MD5 no Experience Platform, pois a Plataforma não converte texto sem formatação em MD5. Neste cenário, defina `uid` (obrigatório) para os mesmos valores MD5 de email ou outro namespace de identidade apropriado. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | X | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

>[!NOTE]
> À medida que membros individuais são adicionados ou removidos do público-alvo da Platform, as atualizações serão enviadas ao ZMP para garantir que a lista de clientes de destino seja sincronizada adequadamente.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL Nome de usuário]**: `api`
* **[!UICONTROL Senha]**: sua chave de API REST ZMP. Você pode encontrar sua chave de API REST fazendo logon em sua conta ZMP e navegando até **Configurações** > **Integrações** > **Chaves e aplicativos** seção. Consulte a [Documentação ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) para obter mais detalhes.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Imagem mostrando a configuração ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID do site da conta ZMP]**: Seu ZMP **ID do site** para onde você deseja enviar seus públicos-alvo. Você pode exibir sua ID do site navegando até **Configurações** > **Integrações** > **Chaves e aplicativos** seção. Mais informações podem ser encontradas [aqui](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL Segmento ZMP]**: o segmento da lista de clientes na conta da ZMP Site Id que você deseja atualizar com o público-alvo da Platform.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

Veja abaixo um exemplo do mapeamento de identidade correto ao exportar perfis para o [!DNL Zeta Marketing Platform].

Selecionar campos de origem:
* Selecione um namespace de identidade de origem (personalizado ou padrão, como `Email`) que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL Zeta Marketing Platform].
* Selecione quaisquer atributos de perfil de origem XDM que precisam ser exportados para e atualizados no [!DNL Zeta Marketing Platform].

Selecionar campos de destino:
* (Obrigatório) Selecionar `uid` como a identidade de destino para a qual você mapeia um namespace de identidade de origem.
* (Opcional) Selecione `email_md5_id` como a identidade de destino para a qual você mapeou o namespace de identidade de origem que representa valores md5 de email. É essencial que os endereços de email já estejam no formato MD5 no Experience Platform, pois a Plataforma não converte texto simples em MD5
* Selecione target mappings adicionais, se necessário.

![Mapeamento de identidade](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Uma ativação de público-alvo bem-sucedida do Experience Platform para a Plataforma de marketing Zeta atualiza a lista de clientes-alvo no ZMP. A contagem e os perfis de amostra na lista de clientes de destino serão iguais ao número de identidades que foram ativadas com êxito.

![Lista de clientes no ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Cada membro do público ativado pelo Experience Platform também estará visível em **Públicos-alvo** > **Pessoas** no ZMP. Você também poderá exibir a variável **Lista de Clientes** segmento ao qual um perfil pertence na visualização Cliente único, conforme mostrado abaixo.

![ExibiçãoÚnicaDoClienteNoZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [Base de conhecimento Zeta](https://knowledgebase.zetaglobal.com/zmp/)
