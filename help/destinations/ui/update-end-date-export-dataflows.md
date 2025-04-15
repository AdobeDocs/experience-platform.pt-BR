---
title: Atualizar a data de término dos fluxos de dados de exportação do conjunto de dados (Ação necessária para 1 de maio de 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Saiba como atualizar a data de término dos fluxos de dados de exportação do conjunto de dados com uma data de término atual em 1º de maio de 2025.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Atualizar a data de término dos fluxos de dados de exportação do conjunto de dados (Ação necessária para 1 de maio de 2025)

>[!IMPORTANT]
>
>Os itens de ação nessa página se aplicam se sua organização configurar fluxos de dados de exportação do conjunto de dados antes da versão de setembro de 2024 do Experience Platform.

## O que está acontecendo?

A versão de [setembro de 2024 do Experience Platform](/help/release-notes/latest/latest.md#destinations) introduziu a opção de definir uma data `endTime` para fluxos de dados do conjunto de dados de exportação. A Adobe também introduziu uma data de término padrão em 1 de maio de 2025 para todos os fluxos de dados de exportação do conjunto de dados criados *antes da versão de setembro de 2024*. No momento, esses fluxos de dados exibem uma mensagem semelhante à mostrada abaixo.

![Notificação da interface do usuário sobre a necessidade de atualizar a data de término do fluxo de dados do conjunto de dados de exportação.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Item de ação**: para qualquer um desses fluxos de dados, você deve atualizar manualmente a data final antes que ela expire; caso contrário, suas exportações serão interrompidas. Use a interface do Experience Platform para identificar quais fluxos de dados estão definidos para serem interrompidos em 1º de maio de 2025.

## Por que estou sendo notificado?

Sua organização foi identificada como tendo fluxos de dados de exportação do conjunto de dados ativos com uma data de término em 1º de maio de 2025.

## Usar a interface do para atualizar a data de término

Use a interface do usuário do Experience Platform para identificar fluxos de dados com uma data de término em 1º de maio de 2025 e atualizá-los para uma data futura.

### Encontre os fluxos de dados que precisam de atualização

Navegue até **Destinos > Procurar** e procure o tipo de dados **Conjuntos de Dados** na coluna **Tipo de Dados**, conforme mostrado abaixo. Selecione os fluxos de dados desejados para inspecioná-los.

![Fluxos de dados de exportação do conjunto de dados destacados na guia Procurar.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Atualizar a data final dos fluxos de dados

Para atualizar a data final dos fluxos de dados:

1. Nos fluxos de dados selecionados para inspeção na etapa anterior, selecione **Exportar conjuntos de dados**.
   ![Controle de exportação de conjuntos de dados realçado na guia Procurar.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. No fluxo de trabalho, continue na etapa **Agendamento** e selecione **Editar agendamento**.
   ![Controle de edição de agendamento realçado na etapa Agendamento.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Escolha uma data de término desejada após 1º de maio de 2025 e selecione **Salvar**.
   ![Selecione o controle de data de término realçado na etapa de Agendamento.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Passe para o final do workflow e salve as atualizações.

Para obter informações abrangentes sobre a etapa de agendamento, leia o [tutorial sobre a interface do usuário de conjuntos de dados de exportação](/help/destinations/api/export-datasets.md#scheduling).

## Usar a API para atualizar a data de término

### Encontre os fluxos de dados que precisam de atualização

### Atualizar a data final dos fluxos de dados
