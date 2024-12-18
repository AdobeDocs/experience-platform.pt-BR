---
title: Modelo V2 de dados da área de saúde
description: Saiba mais sobre alguns casos de uso comuns da área de saúde e as melhores classes, grupos de campos relacionados e tipos de dados a serem usados.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# [!UICONTROL Saúde] Modelo De Dados V2

## Grupos de campos e classes {#field-groups}

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos de uso comuns do sistema de saúde.

| Caso de uso | Grupos de campos e classes compatíveis |
| --- | --- |
| **Criar/atualizar paciente**: quando um paciente chega ao front-desk do hospital, um registro de paciente é estabelecido, incluindo detalhes demográficos como um identificador (opcional), o nome do paciente, sua data de nascimento, seu gênero e seu endereço. Isso serve como um componente vital da TI da área de saúde. | <ul><li>**[Perfis individuais XDM](../../classes/individual-profile.md)**:<ul><li>[Paciente](./field-groups/patient.md)</li></ul></li></ul> |
| **Vacinação**: facilitar o processo de vacinação, gerenciar registros de imunização de pacientes e integrar EMRs aos Sistemas de Gerenciamento de Vacinas. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Imunização](./field-groups/immunization.md)</li></ul></li><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Local](./classes/location.md)**:<ul><li>[Localização](./field-groups/location.md)</li></ul><li>**[Medicação](../../classes/medication.md)**:<ul><li>[Medicação](./field-groups/medication.md)</li><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li></ul></li><li>**[Provedor](../../classes/provider.md)**:<ul><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li></ul></li></ul> |
| **Adesão pós-atendimento**: motivar pacientes e cuidadores a concluírem seus planos de tratamento e reduzir as taxas de remessa. | <ul><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Plano de atendimento](./field-groups/care-plan.md)</li><li>[Meta](./field-groups/goal.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Local](./classes/location.md)**:<ul><li>[Localização](./field-groups/location.md)</li></ul><li>**[Provedor](../../classes/provider.md)**:<ul><li>[Meta](./field-groups/goal.md)</li></ul></li></ul> |
| **Experiência do consumidor com o seguro**: melhore a aquisição digital e as experiências entre consumidores que compram seguros. São exemplos: <li> Compreender o comportamento do consumidor para enviar emails promocionais ou anúncios de terceiros direcionados às pessoas que acessam páginas contendo informações gerais (como planos, nomes/níveis de plano, Medicaid ou programas de bem-estar)</li><li> Envio de informações relacionadas à vacina sobre saúde cardíaca para criar conscientização da marca ou solicitações para agendar vacinas para pessoas que procuram informações sobre saúde cardíaca e vacina. </li> | <ul><li>**[Perfil Individual XDM](../../classes/individual-profile.md)**:<ul><li>[Conta](./field-groups/account.md)</li><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li><li>[Paciente](./field-groups/patient.md)</li></ul></li><li>**[Local](./classes/location.md)**:<ul><li>[Localização](./field-groups/location.md)</li></ul><li>**[Medicação](../../classes/medication.md)**:<ul><li>[Medicação](./field-groups/medication.md)</li><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li></ul></li><li>**[Provedor](../../classes/provider.md)**:<ul><li>[Conta](./field-groups/account.md)</li><li>[Dispensa de Medicação](./field-groups/medication-dispense.md)</li><li>[Solicitação de medicação](./field-groups/medication-request.md)</li></ul><li>**[Plano](../../classes/plan.md)**:<ul><li>[Meta](./field-groups/coverage.md)</li></ul></li></ul> |
| **Experiência do provedor aprimorada**: usar os dados do provedor do sistema EMR para sugerir provedores alternativos com base na disponibilidade de compromisso, local e especialidade. <br> <br>Aprimoramento das pesquisas do provedor para mostrar os resultados com a disponibilidade desejada, verificando se o provedor selecionado faz parte da rede do pagador e fornecendo estimativas de custos. | <ul><li>**[Perfis individuais XDM](../../classes/individual-profile.md)**:<ul><li>[Compromisso](./field-groups/appointment.md)</li><li>[Organização](./field-groups/organization.md)</li><li>[Paciente](./field-groups/patient.md)</li><li>[Profissional](./field-groups/practioner.md)</li><li>[Agendar](./field-groups/schedule.md)</li></ul></li><li>**[Local](./classes/location.md)**:<ul><li>[Localização](./field-groups/location.md)</li></ul><li>**[Provedor](../../classes/provider.md)**:<ul><li>[Compromisso](./field-groups/appointment.md)</li><li>[Organização](./field-groups/organization.md)</li><li>[Profissional](./field-groups/practioner.md)</li><li>[Agendar](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:auto"}

## Tipos de dados {#data-types}

A tabela a seguir descreve os tipos de dados criados de acordo com as especificações [!DNL HL7 FHIR Release 5].

| Nome | Descrição |
| --- | --- |
| [[!UICONTROL Endereço]](./data-types/address.md) | Descreve um endereço expresso usando convenções postais (em vez de GPS ou outros formatos de definição de localização). |
| [[!UICONTROL Anotação]](./data-types/annotation.md) | Um nó de texto com atribuição ao autor. |
| [[!UICONTROL Disponibilidade]](./data-types/availability.md) | Dados de disponibilidade de um item. |
| [[!UICONTROL Conceito codificável]](./data-types/codeable-concept.md) | Uma referência de um recurso a outro. |
| [[!UICONTROL Referência codificável]](./data-types/codeable-reference.md) | Uma referência a um recurso ou conceito. |
| [[!UICONTROL Codificação]](./data-types/coding.md) | Uma referência a um código definido por um sistema de terminologia. |
| [[!UICONTROL Ponto de contato]](./data-types/contact-point.md) | Detalhes de contato de uma pessoa. |
| [[!UICONTROL Dosagem]](./data-types/dosage.md) | Como a medicação é/foi tomada ou deve ser tomada. |
| [[!UICONTROL Duração]](./data-types/duration.md) | Um período de tempo. |
| [[!UICONTROL Detalhes Estendidos do Contato]](./data-types/extended-contact-detail.md) | Informações de um contato estendido. |
| [[!UICONTROL Nome Humano]](./data-types/human-name.md) | Informações sobre o nome de uma entidade humana ou outra entidade viva. |
| [[!UICONTROL Identificador]](./data-types/identifier.md) | Um identificador destinado ao cálculo. |
| [[!UICONTROL Dinheiro]](./data-types/money.md) | Uma quantia de utilidade econômica em alguma moeda reconhecida. |
| [[!UICONTROL Período]](./data-types/period.md) | Um período definido por uma data/hora inicial e final. |
| [[!UICONTROL Pessoa]](./data-types/person.md) | Informações sobre um registro de pessoa genérico. |
| [[!UICONTROL Quantidade]](./data-types/quantity.md) | Uma quantia medida ou mensurável. |
| [[!UICONTROL Intervalo]](./data-types/range.md) | Um conjunto de valores vinculados por valores baixo e alto. |
| [[!UICONTROL Taxa]](./data-types/ratio.md) | Uma proporção de dois valores [[!UICONTROL Quantidade]](./data-types/quantity.md) por meio de um numerador e um denominador. |
| [[!UICONTROL Referência]](./data-types/reference.md) | Uma referência de um recurso a outro. |
| [[!UICONTROL Repetir]](./data-types/repeat.md) | Um conjunto de regras que descrevem quando um evento é agendado. |
| [[!UICONTROL Quantidade Simples]](./data-types/simple-quantity.md) | Uma quantia medida ou mensurável. |
| [[!UICONTROL Horário]](./data-types/timing.md) | Informações sobre um evento que pode ocorrer várias vezes. |
| [[!UICONTROL Detalhes do Serviço Virtual]](./data-types/virtual-service-detail.md) | Detalhes de contato do serviço virtual. |

