---
solution: Experience Platform
title: Exportar Schemas XDM na interface do usuário
description: Saiba como exportar um schema existente para uma caixa de proteção ou Organização IMS diferente na interface do usuário do Adobe Experience Platform.
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 8d6916890a94300dc68d018d56579df9616c177c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Exportar schemas XDM na interface do usuário

Todos os recursos dentro da Biblioteca de Schemas estão contidos em uma caixa de proteção específica dentro de uma Organização IMS. Em alguns casos, você pode compartilhar recursos do Experience Data Model (XDM) entre caixas de proteção e Organizações IMS.

Para atender a essa necessidade, a área de trabalho [!UICONTROL Schemas] na interface do usuário do Adobe Experience Platform permite gerar uma carga de exportação para qualquer schema na Biblioteca de Schemas. Essa carga pode ser usada em uma chamada para a API do Registro do Schema para importar o schema (e todos os recursos dependentes) em uma caixa de proteção do público alvo e uma Organização IMS.

>[!NOTE]
>
>Você também pode usar a API do Registro do Schema para exportar outros recursos além de schemas, incluindo classes, mixins e tipos de dados. Consulte o guia nos [pontos finais de exportação/importação](../api/export-import.md) para obter mais informações.

## Pré-requisitos

Embora a interface do usuário da plataforma permita exportar recursos XDM, é necessário usar a API do Registro do Schema para importar esses recursos para outras caixas de proteção ou Organizações IMS para concluir o fluxo de trabalho. Consulte o guia de introdução à API do Registro de Schemas](../api/getting-started.md) para obter informações importantes sobre os cabeçalhos de autenticação necessários antes de seguir este guia.[

## Gerar uma carga de exportação

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo. Na área de trabalho [!UICONTROL Schemas], localize o schema que deseja exportar e abra-o no [!DNL Schema Editor].

>[!TIP]
>
>Consulte o guia em [exploração de recursos XDM](./explore.md) para obter detalhes sobre como localizar o recurso XDM que você está procurando.

Depois de abrir o schema, selecione o ícone **[!UICONTROL Copiar JSON]** (![Copiar ícone](../images/ui/export/icon.png)) no canto superior direito da tela.

![](../images/ui/export/copy-json.png)

Isso copia uma carga JSON para a área de transferência, gerada com base na estrutura do schema. Para o schema &quot;[!DNL Loyalty Members]&quot; mostrado acima, o seguinte JSON é gerado:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

A carga assume a forma de uma matriz, com cada item de matriz sendo um objeto que representa um recurso XDM personalizado a ser exportado. No exemplo acima, a combinação personalizada &quot;[!DNL Loyalty details]&quot; e o schema &quot;[!DNL Loyalty Members]&quot; estão incluídos. Os recursos principais empregados pelo schema não são incluídos na exportação, pois estão disponíveis em todas as caixas de proteção e organizações IMS.

Observe que cada instância da ID de locatário de sua organização aparece como `<XDM_TENANTID_PLACEHOLDER>` na carga. Esses espaços reservados serão automaticamente substituídos pelo valor de ID do locatário apropriado, dependendo de onde você importa o schema na próxima etapa.

## Importe o recurso usando a API

Depois de copiar o JSON de exportação para o schema, você pode usá-lo como carga de uma solicitação de POST para o terminal `/import` na API do Registro do Schema. Consulte a seção sobre [importar um recurso XDM na API](../api/export-import.md#import) para obter detalhes sobre como configurar a chamada para enviar o schema para a Organização IMS e caixa de proteção desejadas.

## Próximas etapas

Ao seguir este guia, você exportou com êxito um schema XDM para uma Organização IMS ou caixa de proteção diferente. Para obter mais informações sobre os recursos da interface do usuário [!UICONTROL Schemas], consulte [[!UICONTROL Schemas] Visão geral da interface do usuário](./overview.md).