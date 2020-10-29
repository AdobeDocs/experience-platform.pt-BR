---
product: experience-platform
audience: user
user-guide-title: Ajuda do sistema do Experience Data Model (XDM)
breadcrumb-title: Guia do Data Model (XDM)
user-guide-description: Use as classes e as combinações do Experience Data Model (XDM) para padronizar os dados de experiência.
translation-type: tm+mt
source-git-commit: 0a5b6bab6a0a11a572a4cd5de95b33f8d61d34bc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 20%

---


# Experience Data Model (XDM) System {#xdm}

* [Visão geral do sistema XDM](home.md)
* Esquemas {#schema}
   * [Noções básicas da composição do schema](schema/composition.md)
   * [Práticas recomendadas para modelagem de dados](schema/best-practices.md)
   * [Restrições de tipo de campo XDM](schema/field-constraints.md)
   * [Dicionário de campos XDM](schema/field-dictionary.md)
   * Casos de uso do schema {#use-cases}
      * [Mistura de consentimento de privacidade](schema/privacy-consent.md)
* Classes {#classes}
   * [Perfil individual XDM](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Misturas {#mixins}
   * Misturas de perfis {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Detalhes demográficos](./mixins/profile/person-details.md)
      * [Detalhes do contato pessoal](./mixins/profile/personal-details.md)
      * [Detalhes da associação ao segmento](./mixins/profile/segmentation.md)
      * [Detalhes do contato de trabalho](./mixins/profile/work-details.md)
   * Misturas de eventos {#event}
      * [Detalhes da ID do usuário final](./mixins/event/enduserids.md)
      * [Detalhes do ambiente](./mixins/event/environment-details.md)
   * [Misturar atualizações de nomes](./mixins/name-updates.md)
* Tipos de dados {#data-types}
   * [Beacon](./data-types/beacon.md)
   * [Detalhes do navegador](./data-types/browser-details.md)
   * [Dispositivo](./data-types/device.md)
   * [Endereço de email](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Geografia](./data-types/geo.md)
   * [Círculo geográfico](./data-types/geo-circle.md)
   * [Coordenadas geográficas](./data-types/geo-coordinates.md)
   * [Detalhes da interação geográfica](./data-types/geo-interaction-details.md)
   * [Forma geográfica](./data-types/geo-shape.md)
   * [Identidade](./data-types/identity.md)
   * [Nome da pessoa](./data-types/person-name.md)
   * [Número de telefone](./data-types/phone-number.md)
   * [Inserir contexto](./data-types/place-context.md)
   * [Detalhes do POI](./data-types/poi-details.md)
   * [Interação POI](./data-types/poi-interaction.md)
   * [Endereço postal](./data-types/postal-address.md)
* API de registro do schema {#api}
   * [Introdução](api/getting-started.md)
   * [Recursos de lista](api/list-resources.md)
   * [Pesquisar um recurso](api/look-up-resource.md)
   * [Atualizar um recurso](api/update-resource.md)
   * [Substituir um recurso](api/replace-resource.md)
   * [Excluir um recurso](api/delete-resource.md)
   * [Criar uma classe](api/create-class.md)
   * [Criar uma mistura](api/create-mixin.md)
   * [Criar um tipo de dados](api/create-data-type.md)
   * [Criar um schema](api/create-schema.md)
   * [Uniões](api/unions.md)
   * [Descritores](api/descriptors.md)
   * [Schemas Ad-hoc](api/ad-hoc.md)
   * [Apêndice](api/appendix.md)
* Tutoriais {#tutorials}
   * [Criar um schema (API)](tutorials/create-schema-api.md)
   * [Criar um schema (UI)](tutorials/create-schema-ui.md)
   * [Definir uma relação entre dois schemas (API)](tutorials/relationship-api.md)
   * [Definir uma relação entre dois schemas (UI)](tutorials/relationship-ui.md)
   * [Criar um schema ad-hoc (API)](tutorials/ad-hoc.md)
* [Guia de solução de problemas](troubleshooting-guide.md)
* [Referência da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)