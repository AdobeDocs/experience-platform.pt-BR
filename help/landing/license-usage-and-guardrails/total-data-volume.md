---
title: Métrica de volume de dados total
description: Saiba mais sobre a nova métrica Volume de dados total e como ela substitui a métrica de riqueza média de perfil anterior.
exl-id: 4b21d25c-b82b-4d1a-83ce-b510f02fd160
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Métrica Volume de Dados Total

O Volume de dados total substitui a métrica Anterior de Riqueza média de perfil como uma maneira mais simples e explicável de rastrear o uso em relação aos direitos do Armazenamento de perfil.

**Volume De Dados Total = Público-Alvo Endereçável × Riqueza Média Do Perfil**

Esta métrica reflete a quantidade total de dados armazenados na **Loja de perfis** e disponíveis para uso nos fluxos de trabalho de envolvimento do Perfil do cliente em tempo real. **não** inclui dados armazenados no **data lake**. Essa alteração fornece uma exibição mais focada e transparente de dados relevantes para a personalização e o envolvimento baseados em perfil.

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

### Como é calculado o Volume total de dados? Ele inclui o armazenamento Data Lake?

O volume de dados total é calculado usando a seguinte fórmula:

**Volume De Dados Total = Público-Alvo Endereçável × Riqueza Média Do Perfil**

Essa métrica reflete a quantidade total de dados armazenados na Loja de perfis que está disponível para o Perfil do cliente em tempo real usar em fluxos de trabalho de envolvimento. **não** inclui dados armazenados no data lake.

Anteriormente, algumas ofertas herdadas usavam uma métrica de &quot;armazenamento total&quot; que combinava o uso do Armazenamento de perfis e do Data Lake. No entanto, o Volume total de dados está limitado apenas ao Armazenamento de perfis, fornecendo uma visualização mais focada de dados relevantes para o engajamento baseado em perfil.

### Preciso recriar minhas alterações para continuar gerenciando minha riqueza média de perfis?

Não. Quaisquer ações, como filtragem, desativação do perfil para conjuntos de dados, bem como configuração das expirações de evento de experiência e expirações de dados de perfil pseudônimo continuarão a desempenhar um papel no gerenciamento do Volume de dados total.

### Por que o arquivo que eu assimilei na sandbox tem um tamanho diferente em comparação ao Volume total de dados?

O perfil otimiza os dados para um processamento rápido a fim de executar os fluxos de trabalho de personalização e envolvimento para os quais o sistema foi projetado. O tamanho do arquivo no lado do cliente pode ser diferente do Volume de dados total devido a fatores que incluem o tipo de codificação, compactação e formato.

### Essa alteração se aplica às SKUs que têm um limite compartilhado tanto para o Perfil quanto para o data lake?

Os clientes que estão em SKUs que compartilharam a Riqueza média de perfil entre o Perfil e o data lake continuarão a ver a métrica Armazenamento total consumido e **não** verão a métrica Riqueza média de perfil.
