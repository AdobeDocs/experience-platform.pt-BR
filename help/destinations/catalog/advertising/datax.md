---
title: Integração com o Verizon MediaYahoo DataX
description: O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável.
source-git-commit: 07c8a7afaf6cd2af249ad52eabfbc5f8cd6689ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Verizon Media/Yahoo DataX

## Visão geral {#overview}

O DataX é uma infraestrutura agregada da Verizon Media/Yahoo que hospeda vários componentes que permitem que o Verizon Media/Yahoo troque dados com seus parceiros externos de forma segura, automatizada e escalável.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela equipe DataX da Verizon Media/Yahoo. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com elas em [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Pré-requisitos {#prerequisites}

**ID MDM**

Esse é um identificador exclusivo no Yahoo DataX e é um campo obrigatório para configurar exportações de dados para esse destino. Se não souber essa ID, entre em contato com o gerente de conta do Yahoo Data X.

**Limite da taxa**

O DataX é limitado por taxa de acordo com os limites de cota para postagens de taxonomia e público-alvo descritos na [documentação do DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de erro | Mensagem de erro | Descrição |
|---------|----------|---------|
| 429 Demasiados pedidos | Limite de taxa excedido por hora **(Limite: 100)** | Número de solicitações permitidas em uma hora por provedor. |

{style=&quot;table-layout:auto&quot;}

**Metadados de taxonomia**

O recurso Taxonomia define uma extensão sobre a estrutura de Metadados DataX Base

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
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
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação. |
| GAID | ID de publicidade do Google | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportação {#export-type}

**Exportação de segmento**  - você está exportando todos os membros de um segmento (público) com os identificadores (Email) usados no destino Mídia de versão.

## Casos de uso {#use-cases}

As APIs DataX estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico desconectado de endereços de email no Verizon Media (VMG) podem criar rapidamente um novo segmento e encaminhar o grupo de público-alvo desejado usando a API quase em tempo real do VMG.

## Ligar ao destino {#connect}

![Cartão de destino do Yahoo DataX na interface do usuário da plataforma](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** MDM: Esse é um identificador exclusivo no Yahoo DataX e é um campo obrigatório para configurar exportações de dados para esse destino. Se você não souber essa ID, entre em contato com o gerente de conta do Yahoo Data X.  Com as IDs MDM, os dados podem ser restritos para uso somente com um determinado conjunto de usuários exclusivos (como dados primários para anunciantes).

## Ativar segmentos para este destino {#activate}

Leia [Ativar perfis e segmentos para um destino](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Para obter mais informações, leia a documentação do Yahoo/Verizon Media [em DataX](https://developer.verizonmedia.com/datax/guide/).