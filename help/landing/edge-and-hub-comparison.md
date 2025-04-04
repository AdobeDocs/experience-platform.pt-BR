---
solution: Experience Platform
title: Comparação entre Edge Network e hub
description: Saiba mais sobre os diferentes caminhos de processamento disponíveis para uso no Adobe Experience Platform.
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---

# Comparação entre Edge Network e hub

A Adobe Experience Platform é o sistema mais poderoso, flexível e aberto do mercado para criar e gerenciar soluções completas que impulsionam a experiência do cliente. Você pode usar o Experience Platform para centralizar e padronizar dados e conteúdo de clientes de qualquer sistema e aplicar a ciência de dados e o aprendizado de máquina para melhorar consideravelmente o design e o delivery de experiências personalizadas. Como resultado, a Experience Platform tem várias maneiras de processar seus dados, permitindo que você avalie seus dados da melhor maneira possível.

## Tipos de servidor

No Experience Platform, os dados podem ser processados em dois caminhos diferentes: hub do Adobe Experience Platform para workflows em lote e de transmissão e Edge Network para experiências em tempo real.

### hub do Adobe Experience Platform

O Hub é um data center principal localizado centralmente e contém todos os dados históricos e o contexto avançado do perfil que foi coletado no Adobe Experience Platform. Isso permite enviar e receber dados mais robustos e completos para seus serviços downstream. Como resultado, o hub deve ser usado em cenários nos quais a **integridade** dos dados é mais importante.

Os serviços disponíveis no hub incluem o seguinte:

- Segmentação em lote
- Segmentação de transmissão
- Perfis
- Destinos
- Gráfico de identidade
- Data Distiller - Serviço de consulta
- Conectores do Source

### Experience Platform Edge Network

O Edge Network é um servidor que está fisicamente localizado mais próximo a diferentes localizações geográficas. Esses data centers processam todos os dados coletados por meio das extensões do SDK e das APIs do Edge Network. Os únicos dados que residem no Edge Network são as associações de público-alvo, identidades de perfil e atributos necessários para personalização.

O Edge Network permite enviar e receber dados para seus clientes mais rapidamente devido à proximidade deles com o usuário final. Além disso, você pode usar o Edge Network para processar solicitações de encaminhamento de eventos e solicitações de gerenciamento de tags. No entanto, o Edge Network processa apenas dados **comportamentais**. Como resultado, o Edge Network deve ser usado em cenários nos quais a **velocidade** dos dados é mais importante.

Os serviços disponíveis no Edge Network incluem:

- Segmentação de borda
- Perfis do Edge
- Destinos do Edge
- Coleção de dados
- Extensões do SDK

## Localizações

A seção a seguir lista os locais para hub e Edge Network.

![Um diagrama que lista os locais diferentes para servidores hub e Edge Network.](./images/servers/platform-server-locations.png)

Hub **1**

- VA7 (Virgínia, EUA)
- NLD2 (Países Baixos)
- AUS5 (Austrália)
- CAN2 (Canadá)
- GBR9 (Reino Unido)
- IND1 (Índia)

**Edge Network**

- OR2 (Oregon, EUA)
- VA6 (Virgínia, EUA)
- IRL1 (Irlanda)
- IND1 (Índia)
- SGP3 (Cingapura)
- AUS3 (Austrália)
- JPN3 (Japão)

Informações mais detalhadas sobre os locais de servidor disponíveis podem ser encontradas na [visão geral sobre várias nuvens](./multi-cloud.md#available-cloud-regions).

## Próximas etapas

Depois de ler esta visão geral, você compreende as diferenças entre o processamento de dados no hub do Adobe Experience Platform e no Adobe Experience Platform Edge Network.

## Apêndice

A seção a seguir lista informações adicionais sobre o processamento de dados no Adobe Experience Platform.

### Perguntas frequentes

A seção a seguir lista as perguntas frequentes sobre hub e Edge Network:

#### Quais cenários são mais apropriados para o hub?

O hub é mais adequado em cenários em que a **integridade** dos dados é mais importante. Por exemplo, digamos que você queira criar uma campanha de marketing para direcionar todos os clientes que abandonaram os carrinhos. Nesse caso de uso, você pode usar a segmentação em lote, criando um público-alvo que corresponda aos usuários do carrinho abandonado e exportando-o para um destino em lote.

#### Quais cenários são mais apropriados para o Edge Network?

O Edge Network é mais adequado para cenários em que a **velocidade** dos dados é mais importante. Por exemplo, digamos que você precise criar uma venda rápida limitada para direcionar um cliente que está navegando em seu site com um produto em seu carrinho. Nesse caso de uso, você pode usar a segmentação de borda, permitindo direcionar imediatamente e enviar uma notificação personalizada aos usuários com um produto em seu carrinho com uma &quot;venda rápida&quot;.

#### Quais dados vão do hub para o Edge Network?

Somente os dados necessários para fornecer experiências em tempo real na borda são carregados do hub para o Edge Network. Esses dados são enviados automaticamente do hub para a Edge Network para mantê-los consistentes no futuro e são retidos por até 14 dias. No entanto, **não** significa que os dados são mantidos perfeitamente sincronizados com os dados no hub. Como resultado, pode haver diferenças nos dados disponíveis entre o hub e o Edge Network.
