---
keywords: Experience Platform;espelhamento de dados;esquema relacional;alterar captura de dados;sincronização de banco de dados;chave primária;relacionamentos
solution: Experience Platform
title: Visão geral do Data Mirror
description: Saiba como o Data Mirror permite a assimilação de alterações no nível da linha de bancos de dados externos na Adobe Experience Platform usando esquemas relacionais com exclusividade, relações e controle de versão imposto.
badge: Disponibilidade limitada
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---

# Visão geral do Data Mirror

>[!AVAILABILITY]
>
>O Data Mirror e esquemas relacionais estão disponíveis para os **titulares de licença de campanhas orquestradas** da Adobe Journey Optimizer. Eles também estão disponíveis como uma **versão limitada** para usuários do Customer Journey Analytics, dependendo da sua licença e da ativação de recursos. Entre em contato com o representante da Adobe para obter acesso.

>[!NOTE]
>
>Esquemas relacionais eram anteriormente chamados de esquemas baseados em modelo em versões anteriores da documentação do Adobe Experience Platform. A funcionalidade permanece a mesma.

O Data Mirror é um recurso do Adobe Experience Platform que permite a assimilação de alterações no nível da linha de bancos de dados externos no data lake usando esquemas relacionais. Ele preserva os relacionamentos de dados, impõe exclusividade e oferece suporte ao controle de versão sem exigir processos de extração, transformação e carregamento (ETL) de upstream.

Use o Data Mirror para sincronizar inserções, atualizações e exclusões (dados mutáveis) de sistemas externos como [!DNL Snowflake], [!DNL Databricks] ou [!DNL BigQuery] diretamente no Experience Platform. Isso ajuda a preservar a estrutura do modelo de banco de dados existente e a integridade dos dados conforme você traz os dados para a Platform.

## Recursos e benefícios

O Data Mirror fornece os seguintes recursos essenciais para a sincronização do banco de dados:

* **Imposição de chave primária**: garante a exclusividade nos conjuntos de dados e impede registros duplicados durante a assimilação.
* **Assimilação de alteração no nível da linha**: suporta alterações granulares de dados, incluindo substituições e exclusões com controle de precisão.
* **Relacionamentos de esquema**: permite relacionamentos de chave estrangeira e primária entre conjuntos de dados por meio de descritores.
* **Manipulação de eventos fora de ordem**: processa eventos de alteração usando descritores de versão e carimbo de data/hora, mesmo quando eles chegam fora de sequência.
* **Integração direta de warehouse**: conecta-se a data warehouses de nuvem com suporte para sincronização de alterações quase em tempo real.

Use o Data Mirror para assimilar alterações diretamente de seus sistemas de origem, impor a integridade do esquema e disponibilizar os dados para análises, orquestração de jornadas e workflows de conformidade. O Data Mirror elimina processos complexos de ETL upstream e acelera a implementação, permitindo o espelhamento direto dos modelos de banco de dados existentes.

Planeje a exclusão e os requisitos de higiene de dados ao implementar esquemas relacionais com o Data Mirror. Todos os aplicativos devem considerar como as exclusões afetam os conjuntos de dados relacionados, os fluxos de trabalho de conformidade e os processos downstream antes da implantação.

## Pré-requisitos {#prerequisites}

Antes de começar, você deve entender os seguintes componentes do Experience Platform e confirmar se o ambiente atende aos requisitos técnicos e estruturais:

* [Criar esquemas na interface do Experience Platform](../ui/resources/schemas.md) ou [API](../api/schemas.md)
* [Configurar conexões de origem na nuvem](../../sources/home.md#cloud-storage)
* [Aplicar conceitos de captura de dados de alteração](../../sources/tutorials/api/change-data-capture.md) (substituições, exclusões)
* Distinguir entre [padrão](../schema/composition.md) e [esquemas relacionais](../schema/relational.md)
* [Definir relações estruturais com descritores](../api/descriptors.md)

### Requisitos de implementação

A instância da Platform e os dados de origem devem atender a requisitos específicos para que o Data Mirror funcione corretamente. O Data Mirror requer **esquemas relacionais**, que são estruturas de dados flexíveis com restrições impostas.

Inclua uma **chave primária e um descritor de versão** em todos os esquemas. Se você estiver trabalhando com um esquema de série temporal, também é necessário um **descritor de carimbo de data/hora**.

Seu banco de dados externo deve oferecer suporte à captura de dados de alteração ou fornecer metadados que identificam inserções, atualizações e exclusões. Os dados do Source devem incluir **identificadores exclusivos**, um único campo ou uma chave primária composta e **informações de versão** para que o sistema possa aplicar as atualizações na ordem correta.

Para detectar exclusões, adicione uma coluna `_change_request_type` que especifique se cada registro é uma substituição ou uma exclusão.

## Implementar o Data Mirror {#implementation-workflow}

Diferentemente das abordagens de assimilação padrão, o Data Mirror preserva sua estrutura de modelo de banco de dados no data lake da Experience Platform. Essa consistência da estrutura de dados elimina a necessidade de pré-processamento externo. Veja a seguir um fluxo de trabalho de implementação de alto nível do Data Mirror. Escolha o método de implementação com base no fluxo de trabalho da equipe e no sistema de origem.

### Definir a estrutura do esquema

Crie [esquemas relacionais](../schema/relational.md) com descritores necessários (metadados que definem o comportamento e as restrições do esquema). Escolha um método que se ajuste ao fluxo de trabalho da sua equipe, por meio da interface do usuário ou diretamente pela API.

* **Abordagem da interface**: [Criar esquemas relacionais no Editor de Esquemas](../ui/resources/schemas.md#create-relational-schema)
* **Abordagem da API**: [Criar esquemas por meio da API do Registro de Esquemas](../api/schemas.md#create-relational-schema)

### Mapear relacionamentos e definir o gerenciamento de dados

Defina conexões entre conjuntos de dados usando descritores de relacionamento. Gerencie relacionamentos e mantenha a qualidade dos dados em conjuntos de dados. Essas tarefas garantem associações consistentes e oferecem suporte à conformidade com os requisitos de higiene de dados.

* **Relacionamentos de esquema**: [Defina relações entre conjuntos de dados usando descritores](../api/descriptors.md)
* **Higiene de registros**: [Gerenciar exclusões de registros de precisão para conjuntos de dados com base em esquemas relacionais](../../hygiene/ui/record-delete.md#relational-record-delete)

### Configurar a conexão de origem

Selecione um método de assimilação com base no sistema de origem e caso de uso. Cada opção aceita diferentes níveis de automação, transformação e escalabilidade.

* [**Configurar conexões de origem na nuvem**](../../sources/home.md#cloud-storage)
* **Assimilação de SQL**: usar o Data Distiller para gravar em conjuntos de dados relacionais
* [**Carregamento de arquivo**](../ui/resources/schemas.md#upload-ddl-file): carregar arquivos manualmente para assimilação em lote ou única

### Habilitar assimilação de captura de dados de alteração

Configure conexões de captura de dados de alteração com data warehouses de nuvem compatíveis. Assimilar alterações no nível da linha, mantendo a exclusividade e aplicando atualizações na ordem correta.

* **Alterar captura de dados**: [Habilitar captura de dados de alteração em conexões de origem](../../sources/tutorials/api/change-data-capture.md)

## Casos de uso comuns {#use-cases}

Revise os casos de uso comuns listados abaixo, nos quais o Data Mirror oferece suporte à sincronização de dados precisa e à preservação de relacionamentos. Cada cenário mostra como a Data Mirror oferece suporte a necessidades comerciais comuns em análises, orquestração e conformidade.

### Modelagem de dados relacionais

Use [esquemas relacionais](../schema/relational.md) no Data Mirror para representar entidades, processar inserções, atualizações e exclusões no nível da linha e manter as relações de chave primária e estrangeira existentes nas suas fontes de dados. Essa abordagem traz princípios de modelagem de dados relacionais para a Experience Platform e garante a consistência estrutural entre conjuntos de dados.

### Sincronização de warehouse para lake

Espelhe dados de eventos, logs de interação com o cliente, eventos de campanha e dados auxiliares de data warehouses da nuvem compatíveis com a Experience Platform. Isso oferece suporte à qualificação de campanha, precisão de direcionamento e sequenciamento de mensagens. O Journey Optimizer e o Real-Time CDP B2B dependem disso para a lógica de orquestração quase em tempo real.

### Integração do Customer Journey Analytics

Sincronizar eventos de série temporal, como cliques na Web, visualizações de produtos, compras e interações de suporte de sistemas como centrais de atendimento ou logs de bate-papo. Um histórico completo de alterações permite uma análise de tendências e uma segmentação comportamental precisas. O Experience Platform Data Mirror for Customer Journey Analytics usa isso para refletir substituições e exclusões dos sistemas de origem.

### Modelagem de relacionamento B2B

Preservar relações como hierarquias de conta para contato, de assinatura para conta ou de contato para região. Eles oferecem suporte à segmentação, pontuação de leads, rastreamento de oportunidades e coordenação multicanal. Diferentemente da assimilação padrão que nivela os relacionamentos, o Data Mirror os mantém nativamente usando descritores para uma modelagem mais precisa.

### Gerenciamento de assinaturas

Rastreie eventos como renovações, cancelamentos, atualizações, downgrades e alterações de plano com o histórico completo de versões. Isso oferece suporte a campanhas de retenção, previsão de churn e segmentação baseada no ciclo de vida. O histórico completo permite insights comportamentais e direcionamento preciso.

### Operações de higiene de dados

Use a captura de dados de alteração para permitir exclusões precisas no nível de registro para workflows de conformidade (por exemplo, setores regulamentados) e limpeza. A Data Mirror aplica exclusões com precisão, preservando os dados relacionados nos conjuntos de dados conectados.

## Considerações importantes {#considerations}

Revise essas considerações principais para garantir que sua implementação esteja alinhada aos comportamentos de esquema, métodos de assimilação e padrões de relacionamento compatíveis. O planejamento adequado ajuda a evitar problemas de integração e garante uma modelagem de dados precisa.

### Exclusão de dados e requisitos de higiene

Todos os aplicativos que usam esquemas relacionais e o Data Mirror devem entender as implicações da exclusão de dados. Os esquemas relacionais permitem exclusões precisas no nível do registro que podem afetar os dados relacionados nos conjuntos de dados conectados. Esses recursos de exclusão afetam a integridade dos dados, a conformidade e o comportamento downstream do aplicativo, independentemente do caso de uso específico. Revise [os requisitos de higiene de dados para conjuntos de dados com base em esquemas relacionais](../../hygiene/ui/record-delete.md#relational-record-delete) e planeje cenários de exclusão antes da implementação.

### Seleção do comportamento do esquema

Esquemas relacionais padrão para **registrar comportamento**, que captura o estado da entidade (clientes, contas, etc.). Se você precisar de **comportamento de série temporal** para o rastreamento de eventos, configure-o explicitamente.

### Comparação do método de assimilação

Use essa tabela de comparação para escolher o melhor método de assimilação para suas necessidades de dados, se você precisar de sincronização em tempo real, transformação baseada em SQL ou uploads manuais de arquivos.

| Método de assimilação | Caso de uso |
| ----------------------- | -------------------------------------------------------------- |
| **Alterar captura de dados** | Sincronização em tempo real de depósitos na nuvem compatíveis |
| **Distiller de dados** | Workflows de assimilação e transformação baseados em SQL |
| **Carregamento de arquivo** | Assimilação em lote/manual quando a integração de origem não está disponível |

### Limitações de relacionamento

O Data Mirror oferece suporte a relações **um para um** e **muitos para um** usando descritores. As relações **De muitos para muitos** exigem modelagem adicional e não têm suporte direto.

## Próximas etapas

Depois de revisar esta visão geral, você poderá determinar se o Data Mirror se adapta ao seu caso de uso e entender os requisitos de implementação. Para começar:

1. Os **arquitetos de dados** devem avaliar seu modelo de dados para garantir que ele aceite chaves primárias, controle de versão e recursos de controle de alterações.
2. As **partes interessadas do negócio** devem confirmar se sua licença inclui suporte a esquema relacional e as edições necessárias do Experience Platform.
3. **Os designers de esquema** devem planejar sua estrutura de esquema para identificar os descritores, as relações de campo e as necessidades de governança de dados necessários.
4. As **equipes de implementação** devem escolher um método de assimilação com base nos seus sistemas de origem, requisitos em tempo real e fluxos de trabalho operacionais.

Para obter detalhes sobre a implementação, consulte a [documentação sobre esquemas relacionais](../schema/relational.md).
