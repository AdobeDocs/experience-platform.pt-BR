---
title: Conexão Verizon MediaYahoo DataX
description: DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem à Verizon Media/Yahoo trocar dados com seus parceiros externos de maneira segura, automatizada e escalável.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 65809628e8535027edb08e54e84b308777036ab2
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] conexão

## Visão geral {#overview}

[!DNL DataX] é uma infraestrutura [!DNL Verizon Media/Yahoo] agregada que hospeda vários componentes que permitem que o [!DNL Verizon Media/Yahoo] troque dados com seus parceiros externos de maneira segura, automatizada e escalonável.

>[!IMPORTANT]
>
>Este conector de destino e página de documentação são criados e mantidos pela equipe [!DNL Verizon Media/Yahoo] de [!DNL DataX]. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em [dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)

## Pré-requisitos {#prerequisites}

**ID DO MDM**

Este é um identificador exclusivo em [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para este destino. Se você não souber essa ID, contate o gerente de conta do [!DNL Yahoo DataX].

**Metadados de taxonomia**

O recurso Taxonomia define uma extensão na estrutura de Metadados Base [!DNL DataX]

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

Leia mais sobre [Metadados de taxonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) na documentação para desenvolvedores do [!DNL DataX].

## Limites de tarifa e medidas de proteção {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Ao ativar mais de 100 públicos-alvo para [!DNL Verizon Media/Yahoo DataX], você poderá receber erros de limitação de taxa do destino. Ao ativar públicos-alvo para esse destino, tente ativar menos de 100 públicos-alvo em um fluxo de dados de ativação. Se precisar ativar mais segmentos, crie um novo destino na mesma conta.

[!DNL DataX] tem taxa limitada de acordo com os limites de cota para publicações de taxonomia e público-alvo descritos na [documentação do DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de erro | Mensagem de erro | Descrição |
|---------|----------|---------|
| 429 Muitas solicitações | Limite de Taxa excedido por hora **(Limite: 100)** | Número de solicitações permitidas em uma hora por provedor. |

{style="table-layout:auto"}

## Identidades suportadas {#supported-identities}

[!DNL Verizon Media] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| GAID | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público-alvo com os identificadores (Email, GAID, IDFA) usados no destino do Verizon Media. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

As APIs [!DNL DataX] estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico digitado de endereços de email no [!DNL Verizon Media] (VMG), e podem criar rapidamente um novo público-alvo e enviar por push o grupo de público-alvo desejado usando a API quase em tempo real do VMG.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

![Cartão de destino do Yahoo DataX na interface do usuário do Experience Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ID do MDM]**: é um identificador exclusivo em [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para este destino. Se você não souber essa ID, contate o gerente de conta do [!DNL Yahoo DataX].  Com IDs MDM, os dados podem ser restritos para uso somente com um determinado conjunto de usuários exclusivos (como dados primários de anunciantes).

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para um destino](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para destinos.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Para obter mais informações, leia a documentação [!DNL Yahoo/Verizon Media] [em [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
