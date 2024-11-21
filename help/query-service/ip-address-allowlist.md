---
keywords: Endereço IP, intervalo IP, lista de permissões, inclui na lista de permissões, Serviço de consulta, acesso à rede
title: INCLUI NA LISTA DE PERMISSÕES de endereço IP para o serviço de consulta
description: Esta página fornece intervalos IP atualizados que você pode adicionar ao incluo na lista de permissões para obter acesso seguro ao Serviço de consulta.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * A partir de 15 de outubro de 2024, somente os novos intervalos IP serão válidos para acesso ao Serviço de consulta. Endereços IP desatualizados não funcionam mais. Certifique-se de que a inclui na lista de permissões inclua apenas os novos IPs para evitar interrupções do serviço.

## Visão geral {#overview}

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o acesso ao Serviço de consulta.

Como parte das melhorias contínuas, o Adobe atualizou os intervalos IP para acesso de rede ao Serviço de consulta. Os endereços IP anteriores agora estão obsoletos e somente os novos endereços IP são válidos. É essencial atualizar sua inclui na lista de permissões para incluir os novos intervalos de IP a seguir para manter o serviço ininterrupto.

A Adobe recomenda adicionar os seguintes intervalos IP específicos da região a um incluo na lista de permissões, dependendo da sua região. Falha ao adicionar esses intervalos de IP específicos da região pode levar a erros ou interrupções do serviço.

## VA7: clientes dos EUA e da América {#us-americas}

**Novo IP:** 4.152.211.251

## NLD2: clientes EMEA {#emea}

**Novo IP:** 108.141.12.47

## AUS5: clientes da APAC {#apac}

**Novo IP:** 40.82.220.111

## CAN2: Clientes canadenses {#can2}

**Novo IP:** 4.172.28.20

## GBR9: Clientes do Reino Unido {#gbr9}

**Novo IP:** 20.254.80.141

## Configurar restrições baseadas em IP {#set-ip-restrictions}

Use os [Guias de API de autorização do Data Distiller](./auth-api/overview.md) para configurar restrições baseadas em IP. Essas restrições baseadas em IP garantem que somente redes aprovadas e máquinas clientes possam acessar dados via SQL no Adobe Experience Platform. Saiba como configurar, aplicar e monitorar restrições de IP para manter altos padrões de segurança, com recursos para rastreamento e alertas de acesso em tempo real.

* [Guia de introdução](./auth-api/getting-started.md)
* [Guia de Ponto de Extremidade de Acesso IP](./auth-api/ip-access.md)
* [Guia de Endpoint de validação de IP](./auth-api/validate.md)
