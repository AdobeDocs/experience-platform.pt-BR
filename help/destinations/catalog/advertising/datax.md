---
title: Conexão Verizon MediaYahoo DataX
description: O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# Conexão Verizon Media/Yahoo DataX

## Visão geral {#overview}

O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela equipe DataX da Verizon Media/Yahoo. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Pré-requisitos {#prerequisites}

**ID MDM**

Esse é um identificador exclusivo no Yahoo DataX e é um campo obrigatório para configurar exportações de dados para esse destino. Se não souber essa ID, entre em contato com o gerente de conta do Yahoo Data X.

**Limite da taxa**

O DataX é limitado por taxa de acordo com os limites de cota para postagens de taxonomia e público-alvo descritos na variável [Documentação do DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de erro | Mensagem de erro | Descrição |
|---------|----------|---------|
| 429 Demasiados pedidos | Limite de taxa excedido por hora **(Limite: 100)** | Número de solicitações permitidas em uma hora por provedor. |

{style=&quot;table-layout:auto&quot;}

**Metadados de taxonomia**

O recurso Taxonomia define uma extensão sobre a estrutura de Metadados DataX Base

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

Leia mais sobre [Metadados de taxonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) na documentação do desenvolvedor do DataX.

## Identidades suportadas {#supported-identities}

O Verizon Media oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

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

As APIs DataX estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico desconectado de endereços de email no Verizon Media (VMG) podem criar rapidamente um novo segmento e encaminhar o grupo de público-alvo desejado usando a API quase em tempo real do VMG.

## Ligar ao destino {#connect}

![Cartão de destino do Yahoo DataX na interface do usuário da plataforma](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID MDM]**: Esse é um identificador exclusivo no Yahoo DataX e é um campo obrigatório para configurar exportações de dados para esse destino. Se você não souber essa ID, entre em contato com o gerente de conta do Yahoo Data X.  Com as IDs MDM, os dados podem ser restritos para uso somente com um determinado conjunto de usuários exclusivos (como dados primários para anunciantes).

## Ativar segmentos para este destino {#activate}

Ler [Ativar perfis e segmentos para um destino](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Para obter mais informações, leia a Mídia Yahoo/Verizon [documentação sobre o DataX](https://developer.verizonmedia.com/datax/guide/).
