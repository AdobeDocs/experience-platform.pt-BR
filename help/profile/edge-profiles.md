---
title: Perfis de borda
description: Saiba mais sobre perfis de borda, bem como terminologia relacionada, regiões disponíveis para perfis de borda, bem como serviços disponíveis para perfis de borda.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: 6a17febf845d2b9566e49423fc68491315b2d4d7
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Perfis de borda

No Adobe Experience Platform, o Perfil do cliente em tempo real é a única fonte da verdade para dados de entidade. Esses dados do perfil ficam em um hub central e atendem a casos de uso que dependem da abrangência e da integridade de seus dados. No entanto, em casos de uso mais em tempo real, onde a sensibilidade ao tempo é mais importante, os perfis de borda são a opção preferida. Os perfis de borda são perfis leves que se baseiam em bordas e ajudam nos casos de uso de personalização em tempo real.

Por exemplo, aplicativos Adobe como Adobe Target, Custom Personalization Destination e Adobe Campaign usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção que define a borda para a qual os dados serão enviados e uma configuração de projeção que define as informações específicas que serão disponibilizadas na borda.

## Terminologia {#terminology}

Ao trabalhar com bordas, compreenda os seguintes conceitos:

- **Edge**: uma borda é um servidor localizado geograficamente que armazena dados e os torna prontamente acessíveis aos aplicativos.
- **Configuração de projeção**: uma configuração de projeção descreve como uma determinada entidade deve ser replicada nas bordas de um determinado cliente e sob quais condições. Por exemplo, para o Luma (um cliente de amostra), somente os campos idade e gênero do conjunto de dados após o esquema de Perfil devem se propagar para as bordas.
- **Projeção de borda**: uma projeção de borda é a aplicação de uma configuração de projeção em uma borda específica para um pedaço de dados com uma ID exclusiva em conformidade com um determinado esquema para um determinado cliente. Por exemplo, uma entidade que respeita o schema do perfil com ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visitante do site Luma, replicado para o data center VA6, contendo os campos `age = 35` e `gender = male`.

Em outros termos, os dados são roteados para uma borda por uma projeção, com a variável **destino da projeção** definindo **que** borda os dados serão enviados para o e a variável **configuração de projeção** definindo **o que** os dados serão enviados para a borda especificada.

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

- [Serviço de configuração de perfil de borda](#edge-profile-configuration-service)
- [Serviço de Trabalho de Projeção](#mepw)
- [Serviço de perfil expresso](#xps)

### Serviço de configuração de perfil de borda {#edge-profile-configuration-service}

O Serviço de configuração de perfil de borda expõe APIs para soluções e aplicativos downstream para criar configurações de projeção. Você pode usar essas APIs para especificar os atributos e os públicos-alvo de um perfil que deve ser enviado para as bordas, bem como as regiões de borda para as quais a projeção deve ser enviada. Nesse momento, é possível especificar **qualquer** das regiões periféricas para as projeções.

### Serviço de Trabalho de Projeção {#mepw}

O serviço de trabalhador de projeção (MEPW) monitora as alterações que ocorrem no hub nos perfis. Após examinar as alterações nas configurações, esse serviço prepara as projeções e as envia para as regiões de borda especificadas anteriormente. Além disso, esse serviço processa as solicitações de atualização da entidade e envia as projeções necessárias para as regiões necessárias. As atualizações de entidade são usadas para garantir que a entidade possa ser acessada com alta disponibilidade.

### Serviço de perfil expresso {#xps}

O Serviço de perfil expresso (XPS) recupera os perfis em bordas diferentes. Esse serviço recebe solicitações de soluções downstream, como destinos de Adobe Target ou Personalização personalizada, pesquisa os perfis nos bancos de dados nas bordas e envia o perfil solicitado para a solução solicitante. Se o perfil não for encontrado, uma solicitação de atualização será enviada para o hub associado.

## Próximas etapas

Depois de ler este manual, você deve ter uma compreensão básica dos perfis de borda, incluindo informações sobre as regiões e serviços disponíveis para perfis de borda. Para obter mais informações sobre o Adobe Experience Edge, leia o [Visão geral da rede de borda](../web-sdk/home.md#edge-network).

## Apêndice

A seção a seguir lista as perguntas frequentes sobre perfis de borda do:

### Em que regiões os perfis de borda podem chegar?

Os perfis de borda podem aterrissar em diferentes regiões, dependendo da situação atual.

Para configurações de projeção, quaisquer alterações no perfil serão propagadas para todas as regiões mencionadas na configuração do perfil.

Além disso, cada perfil de borda tem um atributo de esquema chamado de Região de atividade do usuário (UAR). Todas as bordas que este perfil visitou nos últimos 14 dias estão listadas neste atributo de perfil. Como resultado, quando esse atributo está presente em um perfil, todas as alterações no perfil também são enviadas para todas as regiões listadas no UAR.

### Como as expirações de dados funcionam com perfis de borda?

Para perfis de borda, a expiração de dados determina quanto tempo o perfil permanecerá na borda antes de ser removido. A expiração dos dados é **rolagem**, o que significa que sempre que o perfil é acessado na borda, o tempo de expiração dos dados é redefinido. Por padrão, a expiração dos dados dura 14 dias.

### Quais dados são armazenados no perfil de borda?

O perfil do Edge armazena os atributos do perfil, as IDs do perfil, bem como as IDs de público-alvo qualificado. Por padrão, a expiração dos dados dura 14 dias.
