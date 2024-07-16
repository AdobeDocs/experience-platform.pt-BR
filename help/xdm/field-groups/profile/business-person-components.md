---
title: Grupo de campos Esquema de componentes de pessoa de negócios XDM
description: Saiba mais sobre o grupo de campos de esquema Componentes de pessoas de negócios XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 2%

---

# [!UICONTROL Componentes de pessoa de negócios XDM] grupo de campos de esquema

[!UICONTROL Componentes de Pessoa de Negócios XDM] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura vários registros de origem para uma pessoa e outros atributos que são necessários para a segmentação de pessoas.

Quando um perfil é criado para uma pessoa por meio do [Perfil de cliente em tempo real](../../../profile/home.md) na edição B2B do Real-Time CDP, as informações usadas para criar esse perfil podem vir de muitos registros de origem. Por exemplo, se uma pessoa trabalha para duas empresas diferentes, muitos sistemas de CRM criariam uma cópia intencionalmente duplicada dessa pessoa para que uma cópia seja vinculada à Empresa A, enquanto a outra é vinculada à Empresa B. Ao trazer esses dados para a Adobe Experience Platform, esse grupo de campos é usado para mesclar esses diferentes registros de origem em uma única representação.

O grupo de campos fornece um campo `personComponents` de nível raiz, que é uma matriz de objetos. Cada objeto na matriz representa um registro de origem diferente.

>[!IMPORTANT]
>
>Você deve seguir os padrões de assimilação conforme descrito na [documentação de origens](../../../rtcdp/sources/b2b.md). Não há garantias de que outros métodos de mapeamento de campo funcionarão.
>
>Por exemplo, cada objeto da matriz `personComponents` é enviado individualmente durante os padrões de assimilação padrão e adicionado à matriz pela Platform. Adicionar manualmente uma matriz de objetos ao Componente de pessoa de negócios retornará um erro.
>Você deve usar o utilitário de geração automática ao criar esquemas para seus dados B2B. Consulte a documentação para obter instruções sobre como usar o [utilitário de geração automática de namespace e esquema B2B](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Se você não estiver usando o utilitário de geração automática e pretende mapear manualmente seu modelo de dados, leia a documentação sobre as [classes XDM do Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) antes de mapear seus dados.
>
>Consulte o [tutorial completo](../../../rtcdp/b2b-tutorial.md) para obter informações sobre fluxos de trabalho recomendados para dados B2B.

![](../../images/field-groups/business-person-components.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a conta associada à pessoa. |
| `sourceConvertedContactKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para o contato relacionado se este cliente em potencial tiver sido convertido. |
| `sourceExternalKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto do sistema de origem de onde os dados da pessoa se originaram. |
| `sourcePersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a pessoa. |
| `workEmail` | [[!UICONTROL Endereço de email]](../../data-types/b2b-source.md) | A ID do email comercial da pessoa. |
| `personGroupID` | String | Um identificador de grupo da pessoa. |
| `personScore` | String | Uma pontuação gerada para a pessoa por um sistema CRM. |
| `personSource` | String | Um identificador exclusivo baseado em sequência para o sistema de origem de onde os dados da pessoa se originaram. |
| `personStatus` | String | O status atual de marketing ou vendas da pessoa. |
| `personType` | String | O tipo de pessoa em um contexto B2B. |
| `sourceAccountID` | String | Um identificador exclusivo baseado em sequência para a conta no sistema de origem associado à pessoa. Este campo é usado como uma chave estrangeira pelo sistema para procurar as diferentes empresas para as quais essa pessoa trabalha. |
| `sourceConvertedContactID` | String | Um identificador exclusivo baseado em sequência para o contato relacionado se este lead for convertido. |
| `sourceExternalID` | String | Um identificador exclusivo baseado em sequência para o sistema de origem de onde os dados da pessoa se originaram. |
| `sourcePersonID` | String | Um identificador exclusivo baseado em sequência para a pessoa. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
