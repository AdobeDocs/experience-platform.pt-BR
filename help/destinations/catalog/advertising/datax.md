---
title: Conexão Verizon MediaYahoo DataX
description: DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem à Verizon Media/Yahoo trocar dados com seus parceiros externos de maneira segura, automatizada e escalável.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---

# Conexão com o [!DNL Verizon Media/Yahoo DataX]

## Visão geral {#overview}

[!DNL DataX] é um agregado [!DNL Verizon Media/Yahoo] infraestrutura que hospeda vários componentes que permitem [!DNL Verizon Media/Yahoo] Intercâmbio de dados com os seus parceiros externos de forma segura, automatizada e escalável.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos por [!DNL Verizon Media/Yahoo]do [!DNL DataX] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Pré-requisitos {#prerequisites}

**ID MDM**

Este é um identificador exclusivo no [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para esse destino. Se você não souber essa ID, entre em contato com o [!DNL Yahoo DataX] gerente de conta.

**Metadados de taxonomia**

O recurso Taxonomia define uma extensão na Base [!DNL DataX] Estrutura de metadados

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Leia mais sobre [Metadados de taxonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) no [!DNL DataX] documentação do desenvolvedor.

## Limites de tarifa e medidas de proteção {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Ao ativar mais de 100 públicos-alvo para [!DNL Verizon Media/Yahoo DataX], você poderá receber erros de limitação de taxa do destino. Ao ativar públicos-alvo para esse destino, tente ativar menos de 100 públicos-alvo em um fluxo de dados de ativação. Se precisar ativar mais segmentos, crie um novo destino na mesma conta.

[!DNL DataX] é limitada em função dos limites de quota para as publicações de taxonomia e audiência [Documentação do DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de erro | Mensagem de erro | Descrição |
|---------|----------|---------|
| 429 Muitas solicitações | Limite de Taxa excedido por hora **(Limite: 100)** | Número de solicitações permitidas em uma hora por provedor. |

{style="table-layout:auto"}

## Identidades suportadas {#supported-identities}

[!DNL Verizon Media] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| GAID | ID de publicidade do Google | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (Email, GAID, IDFA) usados no destino do Verizon Media. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

[!DNL DataX] As APIs estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico destacado por endereços de email no [!DNL Verizon Media] O (VMG) pode criar rapidamente um novo público-alvo e enviar o grupo de públicos-alvo desejado usando a API quase em tempo real do VMG.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

![Placa de destino Yahoo DataX na interface do usuário da plataforma](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID MDM]**: este é um identificador exclusivo na [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para esse destino. Se você não souber essa ID, entre em contato com o [!DNL Yahoo DataX] gerente de conta.  Com IDs MDM, os dados podem ser restritos para uso somente com um determinado conjunto de usuários exclusivos (como dados primários de anunciantes).

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos-alvo para um destino](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos para destinos.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Para obter mais informações, leia a [!DNL Yahoo/Verizon Media] [documentação sobre [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
