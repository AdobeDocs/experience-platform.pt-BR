---
title: Conexão Verizon MediaYahoo DataX
description: O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: f61771ec11b8bd2d19e303b39e57e82da8f11ead
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] conexão

## Visão geral {#overview}

[!DNL DataX] é um agregado [!DNL Verizon Media/Yahoo] infraestrutura que hospeda vários componentes que permitem [!DNL Verizon Media/Yahoo] Trocar dados com os seus parceiros externos de forma segura, automatizada e escalável.

>[!IMPORTANT]
>
>Esta página de documentação foi criada por [!DNL Verizon Media/Yahoo]&#39;s [!DNL DataX] equipe. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Pré-requisitos {#prerequisites}

**ID MDM**

Esse é um identificador exclusivo em [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para esse destino. Caso não saiba essa ID, entre em contato com seu [!DNL Yahoo DataX] gerente de conta.

**Metadados de taxonomia**

O recurso Taxonomia define uma extensão sobre a Base [!DNL DataX] Estrutura de metadados

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

## Limites de taxa e medidas de proteção {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Ao ativar mais de 100 segmentos para [!DNL Verizon Media/Yahoo DataX], você pode receber erros de limite de taxa do destino. Ao ativar segmentos para a [!DNL Yahoo/DataX] no destino, é recomendável ativar menos de 100 segmentos em um fluxo de dados de ativação. Se precisar ativar mais segmentos, crie um novo destino na mesma conta.

[!DNL DataX] é limitada por taxa de acordo com os limites de cota para postagens de taxonomia e público-alvo descritas no [Documentação do DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de erro | Mensagem de erro | Descrição |
|---------|----------|---------|
| 429 Demasiados pedidos | Limite de taxa excedido por hora **(Limite: 100)** | Número de solicitações permitidas em uma hora por provedor. |

{style=&quot;table-layout:auto&quot;}

## Identidades suportadas {#supported-identities}

[!DNL Verizon Media] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| GAID | Google Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (Email, GAID, IDFA) usados no destino de Mídia Verizon. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

[!DNL DataX] As APIs estão disponíveis para anunciantes que desejam direcionar a um grupo de público-alvo específico endereços de email destacados em [!DNL Verizon Media] (VMG) pode criar rapidamente um novo segmento e impulsionar o grupo de público-alvo desejado usando a API quase em tempo real da VMG.

## Ligar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

![Cartão de destino do Yahoo DataX na interface do usuário da plataforma](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID MDM]**: Esse é um identificador exclusivo em [!DNL Yahoo DataX] e é um campo obrigatório para configurar exportações de dados para esse destino. Caso não saiba essa ID, entre em contato com seu [!DNL Yahoo DataX] gerente de conta.  Com as IDs MDM, os dados podem ser restritos para uso somente com um determinado conjunto de usuários exclusivos (como dados primários para anunciantes).

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para um destino](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Para obter mais informações, leia a [!DNL Yahoo/Verizon Media] [documentação sobre [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
