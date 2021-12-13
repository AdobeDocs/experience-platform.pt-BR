---
title: Grupo de Campos de Esquema Componentes da Pessoa Comercial XDM
description: Este documento fornece uma visão geral do grupo de campos Componentes de pessoa comercial do XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 83329002a1fe51e49818a203191c7082f9589037
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL Componentes de Pessoa Comercial XDM] grupo de campos de esquema

[!UICONTROL Componentes de Pessoa Comercial XDM] é um grupo de campos de esquema padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura vários registros de origem de uma pessoa e outros atributos necessários para a segmentação de pessoa.

Quando um perfil é criado para uma pessoa por meio de [Perfil do cliente em tempo real](../../../profile/home.md) na edição B2B da CDP em tempo real, as informações usadas para criar esse perfil podem vir de muitos registros de origem. Por exemplo, se uma pessoa trabalha para duas empresas diferentes, muitos sistemas de CRM criariam uma cópia intencionalmente duplicada dessa pessoa para que uma cópia estivesse vinculada à Empresa A, enquanto a outra estivesse vinculada à Empresa B. Ao trazer esses dados para o Adobe Experience Platform, esse grupo de campos é usado para unir esses diferentes registros de origem em uma única representação.

O grupo de campos fornece um nível raiz `personComponents` , que é uma matriz de objetos. Cada objeto na matriz representa um registro de origem diferente.

>[!IMPORTANT]
>
>Você deve seguir os padrões de ingestão conforme descrito no [documentação das fontes](../../../rtcdp/sources/b2b.md). Não há garantias de que outros métodos de mapeamento de campo funcionem.
>
>Por exemplo, cada objeto da variável `personComponents` A matriz é enviada individualmente durante os padrões de ingestão padrão e, em seguida, adicionada à matriz por plataforma. A adição manual de uma matriz de objetos ao Componente de pessoa comercial retornará um erro.
>Você deve usar o utilitário de geração automática ao criar esquemas para seus dados B2B. Consulte a documentação para obter instruções sobre como usar o [Utilitário de geração automática de esquema e namespace B2B](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Se você não estiver usando o utilitário de geração automática e pretende mapear manualmente o modelo de dados, leia a documentação em [as classes Real-time Customer Data Platform B2B Edition Experience Data Model (XDM)](../../../rtcdp/schemas/b2b.md) antes de mapear os dados.
>
>Consulte a [tutorial completo](../../../rtcdp/b2b-tutorial.md) para obter informações sobre workflows recomendados para dados B2B.

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
