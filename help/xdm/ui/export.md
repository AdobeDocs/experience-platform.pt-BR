---
solution: Experience Platform
title: Exportar esquemas XDM na interface do
description: Saiba como exportar um esquema existente para uma sandbox ou organização diferente na interface do usuário do Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 11%

---

# Exportar esquemas XDM na interface {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Copiar estrutura JSON"
>abstract="Gere um conteúdo de exportação para o esquema escolhido copiando a estrutura JSON para a área de transferência. Use este recurso para exportar os detalhes de qualquer esquema na Biblioteca de esquemas. Esse JSON exportado pode ser usado para importar o esquema e recursos relacionados para uma sandbox ou organização diferente. Isso torna simples e eficiente o compartilhamento e a reutilização de esquemas entre diferentes ambientes."

Todos os recursos na Biblioteca de esquemas estão contidos em uma sandbox específica em uma organização. Em alguns casos, é possível compartilhar recursos do Experience Data Model (XDM) entre sandboxes e organizações.

Para atender a essa necessidade, o espaço de trabalho [!UICONTROL Schemas] na interface do usuário do Adobe Experience Platform permite gerar uma carga de exportação para qualquer esquema na Biblioteca de Esquemas. Essa carga pode ser usada em uma chamada à API do Registro de esquema para importar o esquema (e todos os recursos dependentes) para uma sandbox e organização de destino.

>[!NOTE]
>
>Você também pode usar a API do Registro de esquema para exportar outros recursos além de esquemas, incluindo classes, grupos de campos de esquema e tipos de dados. Consulte o [manual do ponto de extremidade de exportação](../api/export.md) para obter mais informações.

## Pré-requisitos

Embora a interface do Experience Platform permita exportar recursos XDM, você deve usar a API do registro de esquema para importar esses recursos para outras sandboxes ou organizações para concluir o fluxo de trabalho. Consulte o manual sobre [introdução à API do Registro de Esquema](../api/getting-started.md) para obter informações importantes sobre cabeçalhos de autenticação necessários antes de seguir este guia.

## Gerar uma carga de exportação {#generate-export-payload}

As cargas de exportação podem ser geradas na interface do usuário do Experience Platform a partir do painel de detalhes na guia [!UICONTROL Browse] ou diretamente da tela do esquema no Editor de esquemas.

Para gerar uma carga de exportação, selecione **[!UICONTROL Schemas]** na navegação à esquerda. No espaço de trabalho [!UICONTROL Schemas], selecione a linha do esquema que deseja exportar para exibir os detalhes do esquema na barra lateral direita.

>[!TIP]
>
>Consulte o guia em [explorando recursos XDM](./explore.md) para obter detalhes sobre como encontrar o recurso XDM que você está procurando.

Em seguida, selecione o ícone **[!UICONTROL Copy JSON]** (![Copiar Ícone](/help/images/icons/copy.png)) nas opções disponíveis.

![O espaço de trabalho Esquemas com uma linha de esquema e [!UICONTROL Copy to JSON] realçado.](../images/ui/export/copy-json.png)

Isso copia uma carga JSON para a área de transferência, gerada com base na estrutura do esquema. Para o esquema &quot;[!DNL Loyalty Members]&quot; mostrado acima, o seguinte JSON é gerado:

+++Selecione para expandir um exemplo de carga JSON

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

+++

A carga também pode ser copiada selecionando [!UICONTROL More] na parte superior direita do Editor de esquemas. Um menu suspenso fornece duas opções, [!UICONTROL Copy JSON structure] e [!UICONTROL Delete schema].

>[!NOTE]
>
>Um esquema não pode ser excluído quando está habilitado para o Perfil ou tem conjuntos de dados associados.

![O Editor de Esquemas com [!UICONTROL More] e [!UICONTROL Copy to JSON] realçados.](../images/ui/export/schema-editor-copy-json.png)

A carga assume a forma de uma matriz, com cada item de matriz sendo um objeto que representa um recurso XDM personalizado a ser exportado. No exemplo acima, o grupo de campos personalizados &quot;[!DNL Loyalty details]&quot; e o esquema &quot;[!DNL Loyalty Members]&quot; foram incluídos. Quaisquer recursos principais empregados pelo esquema não são incluídos na exportação, pois esses recursos estão disponíveis em todas as sandboxes e organizações.

Observe que cada instância da ID de locatário da sua organização aparece como `<XDM_TENANTID_PLACEHOLDER>` na carga. Esses espaços reservados serão substituídos automaticamente pelo valor de ID do locatário apropriado, dependendo de onde você importa o esquema na próxima etapa.

## Importar o recurso usando a API {#import-resource-with-api}

Depois de copiar o JSON de exportação para o esquema, você pode usá-lo como carga para uma solicitação POST para o ponto de extremidade `/rpc/import` na API do Registro de Esquema. Consulte o [manual de ponto de extremidade de importação](../api/import.md) para obter detalhes sobre como configurar a chamada para enviar o esquema para a organização e a sandbox desejadas.

## Próximas etapas

Ao seguir este guia, você exportou com êxito um esquema XDM para uma organização ou sandbox diferente. Para obter mais informações sobre os recursos da interface do usuário do [!UICONTROL Schemas], consulte a visão geral da interface do usuário do [[!UICONTROL Schemas]](./overview.md).
