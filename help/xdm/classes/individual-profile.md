---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, Esquemas, identityMap, mapa de identidade, mapa de identidade, design de esquema, mapa, mapa, mapa, esquema de união, união
solution: Experience Platform
title: Classe de Perfil Individual XDM
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] é uma classe padrão do Experience Data Model (XDM) que forma uma representação singular (ou &quot;perfil&quot;) de uma pessoa individual. Especificamente, a classe (e seus grupos de campos compatíveis) captura os atributos e interesses de indivíduos identificados e parcialmente identificados que interagem com sua marca.

Os perfis podem variar de sinais comportamentais anônimos (como cookies do navegador) a perfis altamente identificados que contêm informações detalhadas, como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, identidades, detalhes de contato e preferências de comunicação para um indivíduo. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte [Visão geral do XDM](../home.md#data-behaviors).

O [!DNL XDM Individual Profile] A própria classe fornece vários valores gerados pelo sistema que são preenchidos automaticamente quando os dados são assimilados, enquanto todos os outros campos devem ser adicionados através do uso de [grupos de campos de esquema compatíveis](#field-groups):

![](../images/classes/individual-profile.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto contendo o seguinte [!UICONTROL DateTime] campos: <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de string exclusivo para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream. Em alguns casos, `_id` pode ser um [Identificador universal exclusivo (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se você estiver fazendo streaming de dados de uma conexão de origem ou assimilando diretamente de um arquivo Parquet, deverá gerar esse valor concatenando uma determinada combinação de campos que tornam o registro exclusivo, como ID primária, carimbo de data e hora, tipo de registro e assim por diante. O valor concatenado deve ser um `uri-reference` sequência de caracteres formatada, ou seja, qualquer caractere de dois pontos deve ser removido. Depois disso, o valor concatenado deve ser colocado em hash usando SHA-256 ou outro algoritmo de sua escolha.<br><br>É importante distinguir que **este campo não representa uma identidade relacionada a uma pessoa**, mas o registro dos dados em si. Os dados de identidade relativos a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity) fornecido por grupos de campos compatíveis. |
| `createdByBatchID` | A ID do lote assimilado que fez com que o registro fosse criado. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `personID` | Um identificador exclusivo para a pessoa a que este registro se refere. Este campo não representa necessariamente uma identidade relacionada com a pessoa, a menos que também seja designado como [campo de identidade](../schema/composition.md#identity). |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |

{style=&quot;table-layout:auto&quot;}

## Grupos de campos compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento em [atualizações de nome do grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com a variável [!DNL XDM Individual Profile] classe . Esta é uma lista de alguns grupos de campos comumente usados para a classe :

* [[!UICONTROL Consentimentos e preferências]](../field-groups/profile/consents.md)
* [[!UICONTROL Detalhes demográficos]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Detalhes da Fidelidade]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Detalhes de contato pessoal]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Detalhes da associação ao segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Subscrição Telecom]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Detalhes do Contato do Trabalho]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componentes de Pessoa Comercial XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Detalhes da Pessoa Comercial XDM]](../field-groups/profile/business-person-details.md)\*

*\*Este grupo de campos está disponível somente para organizações com acesso à edição B2B do Adobe Real-time Customer Data Platform.*

Para obter uma lista completa de todos os grupos de campos compatíveis de [!DNL XDM Individual Profile], consulte o [XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
