---
title: Métrica de volume de dados total
description: Saiba mais sobre a nova métrica Volume de dados total e como ela substitui a métrica de riqueza média de perfil anterior.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Métrica Volume de Dados Total

A partir de 24 de setembro de 2024, a métrica Volume total de dados substituirá a métrica anterior Riqueza média de perfil.

Volume de dados total representa a quantidade total de dados disponíveis para o Perfil de cliente em tempo real da Adobe Experience Platform usar em fluxos de trabalho de envolvimento. Este valor é equivalente à métrica de Público-alvo endereçável multiplicada pela Riqueza média do perfil.

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes sobre essa atualização.

### Por que essa mudança foi feita?

Essa alteração foi feita para simplificar o processo de manutenção da conformidade com as métricas de direito de licença. Geralmente, ouvimos dos clientes que eles acham a Riqueza média de perfil difícil de entender e gerenciar. Com essa alteração, esperamos que você seja capaz de entender e gerenciar melhor o uso licenciado do Perfil do cliente em tempo real.

### Essa alteração na métrica altera meu direito de armazenamento de Perfil?

Não. O direito de armazenamento do seu perfil permanecerá o mesmo de antes, já que o Volume total de dados é equivalente ao Público-alvo endereçável multiplicado pela Riqueza média de perfil autorizada.

### Essa alteração afeta os pacotes de direitos que comprei?

Não. Você ainda obterá os benefícios dos pacotes de direitos que adquiriu anteriormente.

### Por que vejo um valor diferente para meu Volume de dados total em comparação ao meu direito de armazenamento de perfil?

Volume de Dados Total representa a quantidade **total** de dados disponíveis para o Perfil usar em fluxos de trabalho de envolvimento. A medição foi atualizada para ser mais determinística e explicável. A maioria dos usuários **não** deve ver uma alteração significativa entre seu Volume de Dados Total e seu armazenamento de perfil total. Se você tiver alguma dúvida, crie um tíquete para o seu representante de atendimento ao cliente.

### Preciso recriar minhas alterações para continuar gerenciando minha riqueza média de perfis?

Não. Quaisquer ações, como filtragem, desativação do perfil para conjuntos de dados, bem como configuração das expirações de evento de experiência e expirações de dados de perfil pseudônimo continuarão a desempenhar um papel no gerenciamento do Volume de dados total.

### Por que o arquivo que eu assimilei na sandbox tem um tamanho diferente em comparação ao Volume total de dados?

O perfil otimiza os dados para um processamento rápido a fim de executar os fluxos de trabalho de personalização e envolvimento para os quais o sistema foi projetado. O tamanho do arquivo no lado do cliente pode ser diferente do Volume de dados total devido a fatores que incluem o tipo de codificação, compactação e formato.

### Essa alteração se aplica às SKUs que têm um limite compartilhado tanto para o Perfil quanto para o data lake?

Os clientes que estão em SKUs que compartilharam a Riqueza média de perfil entre o Perfil e o data lake continuarão a ver a métrica Armazenamento total consumido e **não** verão a métrica Riqueza média de perfil.
