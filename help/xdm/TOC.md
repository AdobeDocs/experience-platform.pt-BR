---
product: experience-platform
audience: user
user-guide-title: Ajuda do sistema do Experience Data Model (XDM)
breadcrumb-title: Guia do Experience Data Model (XDM)
user-guide-description: Use as classes e as combinações do Experience Data Model (XDM) para padronizar os dados de experiência.
translation-type: tm+mt
source-git-commit: b735e5f7eb8d1f0526d8786430c844b4d36fa09d
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 24%

---


# Sistema do Modelo de Dados de Experiência (XDM) {#xdm}

* [Visão geral do sistema XDM](home.md)
* Esquemas {#schema}
   * [Noções básicas da composição do schema](schema/composition.md)
   * [Práticas recomendadas para modelagem de dados](schema/best-practices.md)
   * [Restrições de tipo de campo XDM](schema/field-constraints.md)
   * [Dicionário de campos XDM](schema/field-dictionary.md)
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
   * [aplicação](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Detalhes do navegador](./data-types/browser-details.md)
   * [Comércio](./data-types/commerce.md)
   * [Consentimentos e preferências](./data-types/consents.md)
   * [Dispositivo](./data-types/device.md)
   * [Endereço de email](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Geografia](./data-types/geo.md)
   * [Círculo geográfico](./data-types/geo-circle.md)
   * [Coordenadas geográficas](./data-types/geo-coordinates.md)
   * [Detalhes da interação geográfica](./data-types/geo-interaction-details.md)
   * [Forma geográfica](./data-types/geo-shape.md)
   * [Identidade](./data-types/identity.md)
   * [Medição](./data-types/measure.md)
   * [Pedido](./data-types/order.md)
   * [Item de Pagamento](./data-types/payment-item.md)
   * [Pessoa](./data-types/person.md)
   * [Nome da pessoa](./data-types/person-name.md)
   * [Número de telefone](./data-types/phone-number.md)
   * [Inserir contexto](./data-types/place-context.md)
   * [Detalhes do POI](./data-types/poi-details.md)
   * [Interação POI](./data-types/poi-interaction.md)
   * [Endereço postal](./data-types/postal-address.md)
   * [Pesquisa](./data-types/search.md)
   * [Subscrição](./data-types/subscription.md)
   * [Interação Web](./data-types/web-interactions.md)
   * [Detalhes da página da Web](./data-types/webpage-details.md)
*  SchemasUI  {#ui}
   * [Visão geral](./ui/overview.md)
   * [Explore os recursos do XDM](./ui/explore.md)
   * Criar e editar recursos {#resources}
      * [Esquemas](./ui/resources/schemas.md)
      * [Classes](./ui/resources/classes.md)
      * [Misturas](./ui/resources/mixins.md)
      * [Tipos de dados](./ui/resources/data-types.md)
   * Definir campos {#fields}
      * [Visão geral](./ui/fields/overview.md)
      * [Campos obrigatórios](./ui/fields/required.md)
      * [Campos de objeto](./ui/fields/object.md)
      * [Campos de matriz](./ui/fields/array.md)
      * [Campos Enum](./ui/fields/enum.md)
      * [Campos de identidade](./ui/fields/identity.md)
      * [Campos de relacionamento](./ui/fields/relationship.md)
   * [Gerar dados XDM de amostra](./ui/sample.md)
   * [Exportar schemas XDM](./ui/export.md)
* API de Registro do schema {#api}
   * [Visão geral](api/overview.md)
   * [Introdução](api/getting-started.md)
   * [Esquemas](api/schemas.md)
   * [Comportamentos](api/behaviors.md)
   * [Classes](api/classes.md)
   * [Misturas](api/mixins.md)
   * [Tipos de dados](api/data-types.md)
   * [Descritores](api/descriptors.md)
   * [Uniões](api/unions.md)
   * [Exportar/Importar](api/export-import.md)
   * [Dados de amostra](api/sample-data.md)
   * [Log de auditoria](api/audit-log.md)
   * [Schemas Ad-hoc](api/ad-hoc.md)
   * [Apêndice](api/appendix.md)
* Tutoriais {#tutorials}
   * [Criar um schema (UI)](tutorials/create-schema-ui.md)
   * [Criar um schema (API)](tutorials/create-schema-api.md)
   * [Definir uma relação entre dois schemas (UI)](tutorials/relationship-ui.md)
   * [Definir uma relação entre dois schemas (API)](tutorials/relationship-api.md)
   * [Criar um schema ad-hoc (API)](tutorials/ad-hoc.md)
* [Guia de solução de problemas](troubleshooting-guide.md)
* [Referência da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Notas de versão da plataforma](https://www.adobe.com/go/platform-release-notes-en)