---
title: Visão geral de Executar e operar
description: Inspecione, solucione problemas e otimize suas implementações do Experience Platform com as ferramentas Executar e Operar. Obtenha visibilidade sobre ativações programadas em lote, identifique problemas de configuração e melhore a confiabilidade do sistema.
solution: Experience Platform
type: Documentation
role: Admin, User
exl-id: 7f44cdf3-4db1-47f9-bcde-401f6dcfc551
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# Visão geral de Executar e operar

Quando os processos em lote falham ou fornecem dados incompletos, é necessário entender rapidamente o que causou o problema. A causa básica pode ser problemas de disponibilidade de dados, tempo incorreto, problemas de configuração ou restrições de capacidade do sistema. Sem uma visibilidade clara, você pode passar horas investigando vários sistemas antes de encontrar a resposta.

Com as ferramentas do [!UICONTROL Run and Operate], você pode:

* **Inspecionar suas operações de dados**: obtenha uma exibição completa do status de execução do trabalho e da integridade em todos os seus fluxos de trabalho.
* **Solucionar problemas com mais rapidez**: acesse as informações detalhadas de diagnóstico e o histórico de execução para identificar rapidamente as causas básicas e reduzir o tempo médio de resolução.
* **Evite problemas de forma proativa**: analise padrões de trabalho, detecte problemas de configuração antes que eles causem falhas e otimize suas operações de dados.

## Públicos-alvo {#target-audiences}

As ferramentas do [!UICONTROL Run and Operate] foram projetadas para atender a vários públicos em toda a organização:

* **Equipes de dados e TI**: administradores de sistema e engenheiros de dados que mantêm pipelines de dados confiáveis e solucionam problemas técnicos.
* **Operações de marketing**: tecnólogos de marketing que inspecionam a entrega de dados em plataformas de marketing e resolvem problemas de ativação.
* **Implementadores**: profissionais que validam a eficiência e a confiabilidade da implementação e que solucionam problemas técnicos.

## Pré-requisitos {#prerequisites}

Para acessar as ferramentas Executar e Operar, você precisa das **[!UICONTROL View Job Schedules]** e **[!UICONTROL View Profile Management]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Entre em contato com o administrador do sistema para garantir que você tenha as permissões apropriadas.

## Introdução {#getting-started}

Para acessar as ferramentas Executar e Operar na interface do usuário do Experience Platform:

1. Faça logon em sua conta do Experience Platform e selecione **[!UICONTROL Run and Operate]** na navegação à esquerda.
2. Selecione a ferramenta que corresponde às suas necessidades de inspeção ou solução de problemas.

![Interface do usuário do Experience Platform mostrando a navegação à esquerda de Executar e Operar](assets/overview/run-and-operate.png)

## Ferramentas disponíveis {#available-tools}

As ferramentas a seguir ajudam a inspecionar e otimizar as operações de dados.

### Cronogramas do processo {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] estão disponíveis no momento apenas para os seguintes trabalhos do Real-Time CDP:
>
> * Assimilação em lote de data lake
> * Assimilação de perfil em lote
> * Segmentação em lote
> * Ativação do destino de lote

Com [Agendamentos de trabalho](job-schedules.md), você pode inspecionar todas as operações em lote agendadas em sua organização, por sandbox, incluindo assimilação de data lake, assimilação de perfil, segmentação e ativação de destino. Visualize o status de execução do job, as métricas de desempenho e o histórico de execução para identificar padrões e diagnosticar problemas de configuração que afetam a confiabilidade.

![Interface do Experience Platform mostrando a tela de Agendamentos de Trabalho.](assets/overview/job-schedules-interface.png)

As Programações de Trabalho fornecem três níveis de investigação:

* **[Inspecionar agendas de trabalho](job-schedules.md)**: visualize todos os conjuntos de dados e seus trabalhos agendados em uma linha do tempo para identificar padrões e conflitos de agendamento em todo o pipeline.
* **[Identificar antipadrões](job-schedules-anti-patterns.md)**: saiba como detectar e resolver problemas comuns de configuração, como sobreposição de agendamento, empilhamento denso de lotes e lotes excessivos que afetam o desempenho.
* **[Exibir detalhes do trabalho](job-schedules-details.md)**: aprofunde-se em conjuntos de dados específicos e execuções de trabalho individuais para investigar falhas, verificar o tempo e verificar os registros processados.

Você também pode entender as dependências entre os estágios de processamento de dados, ajudando a garantir um fluxo de dados confiável em todos os workflows do Experience Platform.

### Verificações de integridade {#health-checks}

Com as [Verificações de integridade](health-checks.md), você pode detectar proativamente problemas de configuração de esquema e identidade antes que eles afetem as operações comerciais. Atualmente, as verificações de integridade executam verificações estáticas diárias nos esquemas e namespaces de identidade, identificando práticas recomendadas, configurações incorretas e padrões que levam a falhas downstream.

Atualmente, as verificações de integridade avaliam cinco áreas fundamentais:

* **[Validação do campo de identidade](health-checks.md#identity-field-validation)**: verifique se os campos de identidade têm restrições de comprimento e padrão adequadas.
* **[Regras de vinculação de gráfico de identidade](health-checks.md#identity-graph-linking-rules)**: confirme se as regras de vinculação estão configuradas para impedir o recolhimento do perfil.
* **[Configuração de identidade de pessoas e não pessoas](health-checks.md#people-non-people-identity)**: valide o uso do tipo de identidade correto em classes de esquema.
* **[Descrição do namespace de identidade personalizado](health-checks.md#namespace-missing-description)**: verifique se os metadados do namespace estão completos.
* **[Namespaces de identidade obsoletos](health-checks.md#deprecated-namespace)**: detectar namespaces obsoletos para limpeza.

## Próximas etapas {#next-steps}

Agora que você entende a finalidade e os recursos das ferramentas do [!UICONTROL Run and Operate], explore os seguintes recursos para aprofundar seu conhecimento:

* Saiba como usar as [verificações de integridade](health-checks.md) para detectar problemas de configuração de esquema e identidade
* Saiba como [inspecionar agendas de trabalho](job-schedules.md) para sua assimilação e ativações em lote
* Saiba mais sobre a [assimilação em lote](../ingestion/batch-ingestion/overview.md) para entender como os dados são assimilados na Experience Platform
* Entenda como [configurar ativações agendadas](../destinations/ui/activate-batch-profile-destinations.md) para destinos em lote
* Explorar [monitoramento de fluxo de dados](../dataflows/ui/monitor-destinations.md) para destinos
