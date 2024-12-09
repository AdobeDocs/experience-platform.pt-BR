---
title: Modelo V2 de dados da área de saúde
description: Saiba mais sobre alguns casos de uso comuns da área de saúde e as melhores classes, grupos de campos relacionados e tipos de dados a serem usados.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 4d4e68376af914fbfcb005ad950e643f9407ad47
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 12%

---

# [!UICONTROL Saúde] Modelo De Dados V2

## Grupos de campos e classes {#field-groups}

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos de uso comuns do sistema de saúde.

<table>
  <thead>
    <tr>
      <th>Casos de uso</th>
      <th>Grupos de campos</th>
      <th>Classes compatíveis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Criar/atualizar paciente</strong>: quando um paciente chega ao front-desk do hospital, um registro de paciente é estabelecido, incluindo detalhes demográficos como um identificador (opcional), o nome do paciente, sua data de nascimento, seu gênero e seu endereço. Isso serve como um componente vital da TI da área de saúde.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vacinação</strong>: facilitar o processo de vacinação, gerenciar registros de imunização de pacientes e integrar EMRs aos Sistemas de Gerenciamento de Vacinas.</td>
      <td><a href="../field-groups/event/healthcare-immunization.md">Imunização</a></td>
      <td>
        <li><a href="../classes/experienceevent.md">Evento de experiência XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Localização</a></td>
      <td>
        <li><a href="../classes/location.md">Localização</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Dispensa de medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Solicitação de medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Adesão pós-atendimento</strong>: motivar pacientes e cuidadores a concluírem seus planos de tratamento e reduzir as taxas de remessa.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Localização</a></td>
      <td>
        <li><a href="../classes/location.md">Localização</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-care-plan.md">Plano de atendimento</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-goal.md">Meta</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Experiência do consumidor com o seguro</strong>: melhore a aquisição digital e as experiências entre consumidores que compram seguros. São exemplos: 
        <li> Compreender o comportamento do consumidor para enviar emails promocionais ou anúncios de terceiros direcionados às pessoas que acessam páginas contendo informações gerais (como planos, nomes/níveis de plano, Medicaid ou programas de bem-estar)
        </li> 
        <li> Envio de informações relacionadas à vacina sobre saúde cardíaca para criar conscientização da marca ou solicitações para agendar vacinas para pessoas que procuram informações sobre saúde cardíaca e vacina.
        </li>
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/plan/healthcare-coverage.md">Cobertura</a></td>
      <td>
        <li><a href="../classes/plan.md">Plano</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-account.md">Conta</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Localização</a></td>
      <td>
        <li><a href="../classes/location.md">Localização</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Dispensa de medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Solicitação de medicação</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicação</a></li>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Experiência do provedor aprimorada</strong>: usar os dados do provedor do sistema EMR para sugerir provedores alternativos com base na disponibilidade de compromisso, local e especialidade. <br> <br>Aprimoramento das pesquisas do provedor para mostrar os resultados com a disponibilidade desejada, verificando se o provedor selecionado faz parte da rede do pagador e fornecendo estimativas de custos.
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Paciente</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Localização</a></td>
      <td>
        <li><a href="../classes/location.md">Localização</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-organization.md">Organização</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-practioner.md">Profissional</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-schedule.md">Agendar</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Perfil individual XDM</a></li>
        <li><a href="../classes/provider.md">Provedor</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Tipos de dados {#data-types}

A tabela a seguir descreve os tipos de dados criados de acordo com as especificações [!DNL HL7 FHIR Release 5].

| Nome | Descrição |
| --- | --- |
| [[!UICONTROL Endereço]](../data-types/healthcare/address.md) | Descreve um endereço expresso usando convenções postais (em vez de GPS ou outros formatos de definição de localização). |
| [[!UICONTROL Anotação]](../data-types/healthcare/annotation.md) | Um nó de texto com atribuição ao autor. |
| [[!UICONTROL Disponibilidade]](../data-types/healthcare/availability.md) | Dados de disponibilidade de um item. |
| [[!UICONTROL Conceito codificável]](../data-types/healthcare/codeable-concept.md) | Uma referência de um recurso a outro. |
| [[!UICONTROL Referência codificável]](../data-types/healthcare/codeable-reference.md) | Uma referência a um recurso ou conceito. |
| [[!UICONTROL Codificação]](../data-types/healthcare/coding.md) | Uma referência a um código definido por um sistema de terminologia. |
| [[!UICONTROL Ponto de contato]](../data-types/healthcare/contact-point.md) | Detalhes de contato de uma pessoa. |
| [[!UICONTROL Dosagem]](../data-types/healthcare/dosage.md) | Como a medicação é/foi tomada ou deve ser tomada. |
| [[!UICONTROL Duração]](../data-types/healthcare/duration.md) | Um período de tempo. |
| [[!UICONTROL Detalhes Estendidos do Contato]](../data-types/healthcare/extended-contact-detail.md) | Informações de um contato estendido. |
| [[!UICONTROL Nome Humano]](../data-types/healthcare/human-name.md) | Informações sobre o nome de uma entidade humana ou outra entidade viva. |
| [[!UICONTROL Identificador]](../data-types/healthcare/identifier.md) | Um identificador destinado ao cálculo. |
| [[!UICONTROL Dinheiro]](../data-types/healthcare/money.md) | Uma quantia de utilidade econômica em alguma moeda reconhecida. |
| [[!UICONTROL Período]](../data-types/healthcare/period.md) | Um período definido por uma data/hora inicial e final. |
| [[!UICONTROL Pessoa]](../data-types/healthcare/person.md) | Informações sobre um registro de pessoa genérico. |
| [[!UICONTROL Quantidade]](../data-types/healthcare/quantity.md) | Uma quantia medida ou mensurável. |
| [[!UICONTROL Intervalo]](../data-types/healthcare/range.md) | Um conjunto de valores vinculados por valores baixo e alto. |
| [[!UICONTROL Taxa]](../data-types/healthcare/ratio.md) | Uma proporção de dois valores [[!UICONTROL Quantidade]](../data-types/healthcare/quantity.md) por meio de um numerador e um denominador. |
| [[!UICONTROL Referência]](../data-types/healthcare/reference.md) | Uma referência de um recurso a outro. |
| [[!UICONTROL Repetir]](../data-types/healthcare/repeat.md) | Um conjunto de regras que descrevem quando um evento é agendado. |
| [[!UICONTROL Quantidade Simples]](../data-types/healthcare/simple-quantity.md) | Uma quantia medida ou mensurável. |
| [[!UICONTROL Horário]](../data-types/healthcare/timing.md) | Informações sobre um evento que pode ocorrer várias vezes. |
| [[!UICONTROL Detalhes do Serviço Virtual]](../data-types/healthcare/virtual-service-detail.md) | Detalhes de contato do serviço virtual. |
