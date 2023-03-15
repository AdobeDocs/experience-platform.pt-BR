---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;identityMap;mapa de identidade;mapa de identidade;Design de esquema;mapa;Mapa;esquema de união;união
solution: Experience Platform
title: Classe de perfil individual XDM
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] é uma classe padrão do Experience Data Model (XDM) que forma uma representação singular (ou &quot;perfil&quot;) de uma pessoa individual. Especificamente, a classe (e seus grupos de campo compatíveis) captura os atributos e interesses de indivíduos identificados e parcialmente identificados que interagem com sua marca.

Os perfis podem variar de sinais comportamentais anônimos (como cookies de navegador) a perfis altamente identificados que contêm informações detalhadas, como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, identidades, detalhes de contato e preferências de comunicação de um indivíduo. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da Platform, consulte o [Visão geral do XDM](../home.md#data-behaviors).

A variável [!DNL XDM Individual Profile] A própria classe fornece vários valores gerados pelo sistema que são automaticamente preenchidos quando os dados são assimilados, enquanto todos os outros campos devem ser adicionados por meio do uso de [grupos de campos de esquema compatíveis](#field-groups):

![](../images/classes/individual-profile.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém o seguinte [!UICONTROL DateTime] campos: <ul><li>`createDate`: a data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: a data e a hora da última modificação do recurso.</li></ul> |
| `_id` | Um identificador de sequência de caracteres exclusivo para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream. Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se você estiver transmitindo dados de uma conexão de origem ou assimilando diretamente de um arquivo do Parquet, é necessário gerar esse valor concatenando uma determinada combinação de campos que tornam o registro exclusivo, como ID principal, carimbo de data e hora, tipo de registro e assim por diante. O valor concatenado deve ser um `uri-reference` string formatada, o que significa que os caracteres de dois pontos devem ser removidos. Posteriormente, o valor concatenado deve ser transformado em hash usando SHA-256 ou outro algoritmo de sua escolha.<br><br>É importante distinguir esse **este campo não representa uma identidade relacionada a uma pessoa individual**, mas sim o próprio registro dos dados. Os dados de identidade relativos a uma pessoa devem ser [campos de identidade](../schema/composition.md#identity) fornecido por grupos de campos compatíveis. |
| `createdByBatchID` | A ID do lote assimilado que causou a criação do registro. |
| `modifiedByBatchID` | A ID do último lote assimilado que causou a atualização do registro. |
| `personID` | Um identificador exclusivo da pessoa individual à qual este registro está relacionado. Este campo não representa necessariamente uma identidade relacionada à pessoa, a menos que também seja designado como um [campo de identidade](../schema/composition.md#identity). |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |

{style="table-layout:auto"}

## Grupos de campos compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com o [!DNL XDM Individual Profile] classe. Veja a seguir uma lista de alguns grupos de campos comumente usados para a classe:

* [[!UICONTROL Consentimentos e preferências]](../field-groups/profile/consents.md)
* [[!UICONTROL Detalhes demográficos]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Detalhes de fidelidade]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Detalhes de contato pessoal]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Detalhes da associação do segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Assinatura de serviço de telecomunicação]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Detalhes de contato comercial]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componentes de pessoa de negócios XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Detalhes de pessoa de negócios XDM]](../field-groups/profile/business-person-details.md)\*

*\*Este grupo de campos só está disponível para organizações com acesso à edição B2B do Adobe Real-time Customer Data Platform.*

Para obter uma lista completa de todos os grupos de campos compatíveis com [!DNL XDM Individual Profile], consulte o [Repositório GitHub XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
