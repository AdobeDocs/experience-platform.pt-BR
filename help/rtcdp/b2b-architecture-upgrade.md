---
title: Atualizações de arquitetura para o Real-Time CDP B2B edition
description: Leia este documento para saber mais sobre as atualizações abrangentes da arquitetura do Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Atualizações de arquitetura no Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Este documento descreve as atualizações de arquitetura das edições B2B e B2P do Real-Time CDP. **Nenhuma ação é necessária** neste momento. Consulte este documento para obter informações sobre como as atualizações afetarão os recursos existentes do Adobe Experience Platform. Em caso de dúvidas, entre em contato com a equipe de conta da Adobe.

A Adobe reprojetou as edições B2B e B2P do Real-Time CDP para aprimorar a escalabilidade, o desempenho e a confiabilidade, além de oferecer suporte a casos de uso B2B mais avançados. Para garantir que todos os clientes se beneficiem dessas melhorias, a Adobe atualizará todos os clientes B2B e B2P existentes para a nova arquitetura.

Use a arquitetura aprimorada para obter os seguintes benefícios:

* **Escalabilidade da assimilação de dados**: melhoria do suporte para relações B2B de alta cardinalidade, como contas conectadas a milhares de pessoas.
* **Avaliação de público-alvo confiável e eficiente**: segmentação mais rápida e resiliente para públicos-alvo B2B complexos.
* **resolução da entidade**: resolução de identidade aprimorada para entidades B2B, qualidade de dados aprimorada e duplicação reduzida para permitir segmentação e agregação mais precisas.

## Novos recursos

Leia a seguir os principais aprimoramentos incluídos na atualização de arquitetura.

### Instantâneos de conta para associação de público-alvo

Com a nova arquitetura B2B, os detalhes de associação de público-alvo agora são incluídos para entidades de conta em exportações de instantâneo. Esse recurso permite acessar o status do público-alvo no nível da conta, carimbos de data e hora e indicadores de associação.

Com essa atualização, agora é possível:

* Permita que as equipes de marketing e operações validem diretamente a associação ao público-alvo da conta.
* Obtenha paridade de recursos entre seus modelos de segmentação de perfil (pessoa) e conta, garantindo uma experiência consistente em todas as entidades.

Leia a documentação em [públicos-alvo da conta](../segmentation/types/account-audiences.md) para obter mais informações.

### Contagens de público-alvo para públicos-alvo que incluem entidades B2B

As estimativas de tamanho do público-alvo para públicos-alvo com entidades B2B agora são calculadas com precisão exata. Essas estimativas estão disponíveis durante a pré-visualização e fornecem insights mais precisos e confiáveis para públicos-alvo que envolvem relacionamentos B2B complexos.

Com essa atualização, agora é possível:

* Use insights de estimativas precisas de tamanho do público-alvo para melhorar o planejamento e a tomada de decisões durante o processo de criação do público-alvo.
* Projete públicos-alvo complexos B2B com confiança, sabendo de uma estimativa de público-alvo mais precisa.
* Permita um planejamento de campanha mais inteligente, um direcionamento mais preciso e uma melhor alocação de recursos.

Leia a documentação em [públicos-alvo da conta](../segmentation/types/account-audiences.md) para obter mais informações.

### Pesquisa completa de eventos de nível de pessoa em públicos-alvo de conta

Os públicos-alvo da conta agora podem aproveitar todo o histórico de eventos no nível da pessoa, expandindo além da janela de pesquisa anterior de 30 dias.

Com essa atualização, agora é possível:

* Crie públicos-alvo mais abrangentes com base no histórico completo de eventos de nível de pessoa associados.
* Permita definições de público-alvo mais ricas e precisas aproveitando dados comportamentais de longo prazo.
* Identifique contas de alto valor com base em padrões de envolvimento mais profundos ao longo do tempo.
* Casos de uso de suporte que exigem insights de ações históricas, como aquelas que envolvem ciclos de vendas longos ou sinais de compras atrasadas.

Leia a documentação em [públicos-alvo da conta](../segmentation/types/account-audiences.md) para obter mais informações.

## Atualizações para recursos existentes

Os seguintes recursos foram atualizados como parte das atualizações de arquitetura B2B.

### Atualizações para público-alvo de várias entidades com atributos B2B e eventos de experiência

Como parte da nova atualização da arquitetura, os filtros de Evento de experiência não podem mais ser usados em um único público de várias entidades que inclui atributos B2B.

Para obter a mesma lógica de público-alvo, use a abordagem de segmento de segmento:

1. Criar um público-alvo do evento de experiência: defina a condição comportamental separadamente. Por exemplo: &quot;Pessoas que visitaram a página de preços nos últimos três dias&quot;.
2. Criar um público-alvo com várias entidades com atributos B2B: faça referência ao público-alvo do evento de experiência como parte dos critérios deste público-alvo. Por exemplo: &quot;Pessoas que são **&#39;Tomador de Decisão&#39;** de qualquer oportunidade em que a conta esteja no setor **&#39;Finanças&#39;** e membro do público-alvo de pessoas que visitou a página de preços nos últimos três dias.

Quando a atualização for concluída, quaisquer novos públicos-alvo de várias entidades com atributos B2B e eventos de experiência deverão ser criados usando a abordagem de segmento de segmento. Além disso, você deve validar a associação de público-alvo para garantir o comportamento esperado.

### Mesclagem de resolução de entidade e precedência de tempo em públicos B2B

Como parte da atualização da arquitetura, a Adobe introduziu a resolução de entidades para contas e oportunidades, que é executada diariamente. Esse aprimoramento permite que a Experience Platform identifique e consolide vários registros que representam a mesma entidade real, melhorando assim a consistência dos dados e permitindo uma segmentação mais precisa do público-alvo.

Com essa atualização, agora é possível:

* Use as APIs [!DNL Profile Access] para exibir os perfis de mesclagem mais recentes assim que os trabalhos diários de resolução de entidade forem concluídos.
* Utilize a precisão e a consistência aprimoradas dos dados da conta e da oportunidade para segmentação, ativação e análise.

Leia a [[!DNL Profile Access] API](../profile/api/entities.md) para obter mais informações.

### Suporte a políticas de mesclagem em públicos B2B de várias entidades

Públicos-alvo de várias entidades com atributos B2B agora oferecem suporte a uma única política de mesclagem - a política de mesclagem padrão que você configura - em vez de várias políticas de mesclagem.

Os públicos que dependiam anteriormente de uma política de mesclagem não padrão podem produzir resultados diferentes. Para entender as possíveis alterações na composição do público-alvo, analise e teste qualquer um dos públicos-alvo que depende de uma política de mesclagem não padrão. Além disso, monitore os resultados de ativação para detectar qualquer mudança na composição do público-alvo devido à alteração da política de mesclagem.

Leia o [guia de caso de uso de segmentação do Real-Time CDP B2B edition](./segmentation/b2b.md) para obter mais informações.

### Substituição de pesquisa e exclusão de entidade B2B na API [!DNL Profile Access]

As seguintes funcionalidades de pesquisa para entidades B2B que usam a API [!DNL Profile Access] estão sendo descontinuadas:

* Relação Conta-Pessoa
* Relação oportunidade-pessoa
* Campaign
* Membro da campanha
* Lista de marketing
* Membros da lista de marketing

As solicitações de exclusão das seguintes entidades B2B usando a API [!DNL Profile Access] estão sendo descontinuadas:

* Conta
* Relação Conta-Pessoa
* Oportunidade
* Relação oportunidade-pessoa
* Campaign
* Membro da campanha
* Lista de marketing
* Membros da lista de marketing

Leia a [[!DNL Profile Access] API](../profile/api/entities.md) para obter mais informações.

### Pesquisas de conta e perfil de oportunidade

Agora você pode recuperar esquemas de conta e de oportunidade como entidades de dimensão de pesquisa somente após eles terem concluído o processo diário de resolução da entidade. Os registros assimilados recentemente não estarão disponíveis para enriquecimento de perfil ou definições de segmento até que o próximo ciclo de resolução da entidade seja concluído (normalmente a cada 24 horas).

É recomendável analisar todos os casos de uso que exigem acesso em tempo real aos dados da conta e da oportunidade. Além disso, é recomendável planejar um período de latência de até 24 horas ao projetar ou atualizar workflows que dependem de segmentação baseada em pesquisa ou personalização com entidades de conta e oportunidade.

### Substituição da criação de público-alvo por meio da API para entidades B2B

A criação de públicos-alvo usando entidades B2B por meio da API está sendo descontinuada. A lista de entidades B2B afetadas inclui:

* Conta
* Oportunidade
* Relação Conta-Pessoa
* Relação oportunidade-pessoa
* Campaign
* Membro da campanha
* Lista de marketing
* Membro da lista de marketing

Leia o [manual de API do ponto de extremidade de definições de segmento](../segmentation/api/segment-definitions.md) para obter mais informações.

### Alterações nas importações de público-alvo de várias entidades na ferramenta sandbox

Com as atualizações de arquitetura, você não poderá mais importar públicos-alvo de várias entidades com atributos B2B e eventos de experiência se eles tiverem sido exportados antes da atualização. Esses públicos-alvo não serão importados e não poderão ser convertidos automaticamente para a nova arquitetura. Para contornar essa limitação, você deve reexportar esses públicos-alvo e importá-los para suas respectivas sandboxes de destino usando as ferramentas da sandbox.

Leia o [guia de ferramentas de sandbox](../sandboxes/ui/sandbox-tooling.md) para obter mais informações.