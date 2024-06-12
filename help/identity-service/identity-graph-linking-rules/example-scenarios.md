---
title: Exemplos De Cenários Para Definir Configurações De Identidade
description: Saiba mais sobre exemplos de cenários para definir configurações de identidade.
badge: Beta
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: f1779ee75c877649a69f9fa99f3872aea861beca
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# Exemplos de cenários para configurar regras de vinculação de gráficos de identidade

>[!AVAILABILITY]
>
>Esse recurso ainda não está disponível; o programa beta para regras de vinculação de gráficos de identidade deve começar em julho nas sandboxes de desenvolvimento. Entre em contato com a equipe de conta do Adobe para obter informações sobre os critérios de participação.

Este documento descreve cenários de exemplo que você pode considerar ao configurar regras de vinculação de gráficos de identidade.

## Dispositivo compartilhado

Há instâncias em que vários logons podem ocorrer em um único dispositivo:

| Dispositivo compartilhado | Descrição |
| --- | --- |
| Computadores e tablets da família | O marido e a esposa fazem logon em suas respectivas contas bancárias. |
| Quiosque público | Os viajantes que fazem logon em um aeroporto usam sua ID de fidelidade para fazer check-in de malas e imprimir cartões de embarque. |
| Central de atendimento | A equipe da central de atendimento faz logon em um único dispositivo em nome dos clientes, ligando para o suporte ao cliente para resolver problemas. |

![dispositivos compartilhados](../images/identity-settings/shared-devices.png)

Nesses casos, do ponto de vista do gráfico, sem limites ativados, uma única ECID será vinculada a várias IDs de CRM.

Com as regras de vinculação do gráfico de identidade, você pode:

* Configure a ID usada para fazer logon como identificador exclusivo. Por exemplo, você pode limitar um gráfico para armazenar apenas uma identidade com um namespace de ID de CRM e, portanto, definir essa ID de CRM como o identificador exclusivo de um dispositivo compartilhado.
   * Ao fazer isso, você pode garantir que as IDs do CRM não sejam mescladas pela ECID.

## Cenários de email/telefone inválidos

Também há instâncias de usuários que fornecem valores falsos como números de telefone e/ou endereços de email ao se registrar. Nesses casos, se os limites não estiverem ativados, as identidades relacionadas a telefone/email acabarão sendo vinculadas a várias IDs de CRM diferentes.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Com as regras de vinculação do gráfico de identidade, você pode:

* Configure a ID de CRM, o número de telefone ou o endereço de email como o identificador exclusivo e, portanto, limite uma pessoa a apenas uma ID de CRM, número de telefone e/ou endereço de email associado à conta.

## Valores de identidade incorretos ou incorretos

Há casos em que valores de identidade incorretos e não exclusivos são assimilados no sistema, independentemente do namespace. São exemplos:

* Namespace IDFA com o valor de identidade de &quot;user_null&quot;.
   * Os valores de identidade do IDFA devem ter 36 caracteres: 32 caracteres alfanuméricos e quatro hifens.
* Namespace de número de telefone com o valor de identidade de &quot;não especificado&quot;.
   * Os números de telefone não devem ter caracteres alfabéticos.

Essas identidades podem resultar nos gráficos a seguir, nos quais várias IDs de CRM são mescladas com a identidade &quot;incorreta&quot;:

![dados incorretos](../images/identity-settings/bad-data.png)

Com as regras de vinculação do gráfico de identidade, você pode configurar a ID do CRM como identificador exclusivo para impedir o colapso de perfis indesejados devido a esse tipo de dados.

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Visão geral das regras de vinculação do gráfico de identidade](./overview.md)
* [Algoritmo de otimização de identidade](./identity-optimization-algorithm.md)
* [Serviço de identidade e perfil do cliente em tempo real](../identity-and-profile.md)
* [Lógica de vinculação de identidade](../features/identity-linking-logic.md)
