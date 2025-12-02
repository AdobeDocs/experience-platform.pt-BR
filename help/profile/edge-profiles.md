---
title: Perfis do Edge
description: Saiba mais sobre perfis de borda, bem como terminologia relacionada, regiões disponíveis para perfis de borda, bem como serviços disponíveis para perfis de borda.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Perfis do Edge

No Adobe Experience Platform, o Perfil do cliente em tempo real é a única fonte da verdade para dados de entidade. Esses dados do perfil ficam em um hub central e atendem a casos de uso que dependem da abrangência e da integridade de seus dados. No entanto, em casos de uso mais em tempo real, onde a sensibilidade ao tempo é mais importante, os perfis de borda são a opção preferida. Os perfis do Edge são perfis leves que se baseiam em bordas e ajudam nos casos de uso de personalização em tempo real.

Por exemplo, aplicativos da Adobe como o Adobe Target, Custom Personalization Destination e Adobe Campaign usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção que define a borda para a qual os dados serão enviados.

## Terminologia {#terminology}

Ao trabalhar com bordas, compreenda os seguintes conceitos:

- **Edge**: uma borda é um servidor geograficamente posicionado que armazena dados e os torna prontamente acessíveis aos aplicativos.
- **Projeção do Edge**: uma projeção de borda é a exibição de projeção do sistema do perfil em uma borda específica para representar os dados do perfil com uma ID exclusiva em conformidade com um determinado esquema para um determinado cliente. Por exemplo, uma entidade que respeita o esquema de Perfil com ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visitante do site Luma, replicou para o data center VA6, contendo os campos `age = 35` e `gender = male`.

Em outros termos, os dados são roteados para uma borda por uma projeção, com o **destino da projeção** definindo **para qual** borda os dados serão enviados.

## Regiões disponíveis {#regions}

As seguintes regiões estão disponíveis para uso com o Edge:

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Todas essas regiões são opções válidas para que os perfis cheguem ao.

## Serviços disponíveis {#services}

Os seguintes serviços estão habilitados para a Pesquisa de perfil na borda:

- [Serviço de Trabalho de Projeção](#mepw)
- [Serviço de perfil expresso](#xps)

### Serviço de Trabalho de Projeção {#mepw}

O serviço de trabalhador de projeção (MEPW) monitora as alterações que ocorrem no hub nos perfis. Após examinar as alterações nas configurações, esse serviço prepara as projeções e as envia para as regiões de borda especificadas anteriormente. Além disso, esse serviço processa as solicitações de atualização da entidade e envia as projeções necessárias para as regiões necessárias. As atualizações de entidade são usadas para garantir que a entidade possa ser acessada com alta disponibilidade.

### Serviço de perfil expresso {#xps}

O Serviço de perfil expresso (XPS) recupera os perfis em bordas diferentes. Esse serviço recebe solicitações de soluções downstream, como destinos Adobe Target ou Custom Personalization, pesquisa os perfis nos bancos de dados nas bordas e envia o perfil solicitado para a solução solicitante. Se o perfil não for encontrado, uma solicitação de atualização será enviada para o hub associado.

## Próximas etapas

Depois de ler este manual, você deve ter uma compreensão básica dos perfis de borda, incluindo informações sobre as regiões e serviços disponíveis para perfis de borda. Para obter mais informações sobre o Adobe Experience Edge, consulte [Visão geral da coleção de dados](/help/collection/home.md).

## Apêndice

A seção a seguir lista as perguntas frequentes sobre perfis de borda do:

### Em que regiões os perfis de borda podem chegar?

Os perfis do Edge podem chegar a diferentes regiões, dependendo da situação atual.

Além disso, cada perfil de borda tem um atributo de esquema chamado de Região de atividade do usuário (UAR). Todas as bordas que este perfil visitou nos últimos 14 dias estão listadas neste atributo de perfil. Como resultado, quando esse atributo está presente em um perfil, todas as alterações no perfil também são enviadas para todas as regiões listadas no UAR.

### Como as expirações de dados funcionam com perfis de borda?

Para perfis de borda, a expiração de dados determina quanto tempo o perfil permanecerá na borda antes de ser removido. A expiração dos dados é **em andamento**, o que significa que sempre que o perfil é acessado na borda, o tempo de expiração dos dados é redefinido. Por padrão, a expiração dos dados dura 14 dias.

### Quais dados são armazenados no perfil de borda?

O Perfil do Edge armazena os atributos do perfil, as IDs do perfil, bem como as IDs de público-alvo qualificado. Por padrão, a expiração dos dados dura 14 dias.
