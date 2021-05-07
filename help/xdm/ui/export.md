---
solution: Experience Platform
title: Exportar esquemas XDM na interface do usuário
description: Saiba como exportar um esquema existente para uma sandbox ou Organização IMS diferente na interface do usuário do Adobe Experience Platform.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Exportar esquemas XDM na interface do usuário

Todos os recursos da Biblioteca de esquemas estão contidos em uma sandbox específica de uma Organização IMS. Em alguns casos, você pode compartilhar recursos do Experience Data Model (XDM) entre sandboxes e Orgs do IMS.

Para atender a essa necessidade, o espaço de trabalho [!UICONTROL Schemas] na interface do usuário do Adobe Experience Platform permite gerar uma carga de exportação para qualquer schema na Biblioteca de Esquemas. Essa carga útil pode ser usada em uma chamada para a API do Registro de Schema para importar o esquema (e todos os recursos dependentes) para uma sandbox de destino e a Organização IMS.

>[!NOTE]
>
>Você também pode usar a API do Registro de Schema para exportar outros recursos além de schemas, incluindo classes, grupos de campos de esquema e tipos de dados. Consulte o guia em [exportar/importar endpoints](../api/export-import.md) para obter mais informações.

## Pré-requisitos

Embora a interface do usuário da plataforma permita exportar recursos do XDM, você deve usar a API do Registro de Schema para importar esses recursos para outras sandboxes ou Orgs do IMS para concluir o fluxo de trabalho. Consulte o guia sobre [introdução à API do Registro de Schema](../api/getting-started.md) para obter informações importantes sobre cabeçalhos de autenticação necessários antes de seguir este guia.

## Gerar uma carga de exportação

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo. No espaço de trabalho [!UICONTROL Schemas], localize o schema que deseja exportar e abra-o no [!DNL Schema Editor].

>[!TIP]
>
>Consulte o guia em [explorar recursos XDM](./explore.md) para obter detalhes sobre como encontrar o recurso XDM que você está procurando.

Depois que o esquema for aberto, selecione o ícone **[!UICONTROL Copy JSON]** (![Copiar Ícone](../images/ui/export/icon.png)) na parte superior direita da tela.

![](../images/ui/export/copy-json.png)

Isso copia uma carga JSON para a área de transferência, gerada com base na estrutura do esquema. Para o schema &quot;[!DNL Loyalty Members]&quot; mostrado acima, o seguinte JSON é gerado:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.fieldgroups.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "fieldgroups",
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
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/fieldgroups/profile-consents",
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
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/fieldgroups/profile-consents"
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

A carga assume a forma de uma matriz, com cada item de matriz sendo um objeto que representa um recurso XDM personalizado a ser exportado. No exemplo acima, o grupo de campos personalizados &quot;[!DNL Loyalty details]&quot; e o schema &quot;[!DNL Loyalty Members]&quot; são incluídos. Quaisquer recursos principais empregados pelo schema não são incluídos na exportação, pois esses recursos estão disponíveis em todas as sandboxes e Organizações de IMS.

Observe que cada instância da ID de locatário da sua organização aparece como `<XDM_TENANTID_PLACEHOLDER>` no payload. Esses espaços reservados serão substituídos automaticamente pelo valor de ID de locatário apropriado, dependendo de onde você importa o esquema na próxima etapa.

## Importe o recurso usando a API

Depois de copiar o JSON de exportação para o esquema, você pode usá-lo como carga para uma solicitação POST para o endpoint `/import` na API do Registro de Schema. Consulte a seção sobre [importar um recurso XDM na API](../api/export-import.md#import) para obter detalhes sobre como configurar a chamada para enviar o esquema para a Org do IMS e a sandbox desejadas.

## Próximas etapas

Ao seguir este guia, você exportou com êxito um esquema XDM para uma Organização IMS ou sandbox diferente. Para obter mais informações sobre os recursos da interface do usuário [!UICONTROL Schemas], consulte a [[!UICONTROL Schemas] visão geral da interface do usuário](./overview.md).
