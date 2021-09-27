---
title: Grupo de Campos de Esquema Componentes da Pessoa Comercial XDM
description: Este documento fornece uma visão geral do grupo de campos Componentes de pessoa comercial do XDM.
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] Componentes da Pessoa Comercial XDM

>[!NOTE]
>
>Esse grupo de campos só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real (CDP em tempo real).

[!UICONTROL O Componente de pessoa comercial do XDM ] é um grupo de campo de esquema padrão para a  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe que captura vários registros de origem de uma pessoa e outros atributos necessários para a segmentação da pessoa.

Quando um perfil é criado para uma pessoa por meio do [Real-time Customer Profile](../../../profile/home.md) na edição B2B da CDP em tempo real, as informações usadas para criar esse perfil podem vir de muitos registros de origem. Por exemplo, se uma pessoa trabalha para duas empresas diferentes, muitos sistemas de CRM criariam uma cópia intencionalmente duplicada dessa pessoa para que uma cópia estivesse vinculada à Empresa A, enquanto a outra estivesse vinculada à Empresa B. Ao trazer esses dados para o Adobe Experience Platform, esse grupo de campos é usado para unir esses diferentes registros de origem em uma única representação.

O grupo de campos fornece um campo `personComponents` de nível raiz, que é uma matriz de objetos. Cada objeto na matriz representa um registro de origem diferente.

![](../../images/field-groups/business-person-components.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta associada à pessoa. |
| `sourceConvertedContactKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para o contato relacionado se esse lead foi convertido. |
| `sourceExternalKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto do sistema de origem a partir do qual os dados da pessoa se originaram. |
| `sourcePersonKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da pessoa. |
| `workEmail` | [[!UICONTROL Endereço de email]](../../data-types/b2b-source.md) | A ID do email de trabalho da pessoa. |
| `personGroupID` | String | Um identificador de grupo para a pessoa. |
| `personScore` | String | Uma pontuação gerada para a pessoa por um sistema de CRM. |
| `personSource` | String | Um identificador exclusivo baseado em sequência para o sistema de origem a partir do qual os dados da pessoa se originaram. |
| `personStatus` | String | O status atual de marketing ou vendas da pessoa. |
| `personType` | String | O tipo de pessoa em um contexto B2B. |
| `sourceAccountID` | String | Um identificador exclusivo baseado em sequência para a conta no sistema de origem associado à pessoa. Esse campo é usado como chave estrangeira pelo sistema para buscar as diferentes empresas para as quais essa pessoa trabalha. |
| `sourceConvertedContactID` | String | Um identificador exclusivo baseado em sequência para o contato relacionado, se este cliente potencial foi convertido. |
| `sourceExternalID` | String | Um identificador exclusivo baseado em sequência para o sistema de origem a partir do qual os dados da pessoa se originaram. |
| `sourcePersonID` | String | Um identificador exclusivo baseado em sequência para a pessoa. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
