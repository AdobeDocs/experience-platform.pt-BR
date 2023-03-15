---
keywords: Experience Platform Adobe Experience Platform;página inicial;Data Science Workspace;tópicos populares;controle de acesso;sandbox;pacote de inteligência;recursos do dsw;acesso do dsw;inteligência;pacote de inteligência do aep
solution: Experience Platform
title: Acesso e recursos do Data Science Workspace
description: O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Acesso e recursos do Data Science Workspace

O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.

![Guias DSW](./images/access/platform-tabs.png)

- **Notebooks:** Oferece um ambiente de desenvolvimento interativo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analisar e modelar seus dados no Experience Platform.
- **Modelos:** Fornece ferramentas usadas para criar, publicar e armazenar receitas e modelos avançados de aprendizado de máquina. Para obter mais informações, visite o [criar e publicar um modelo de aprendizado de máquina](./models-recipes/create-publish-model.md) tutorial.
- **Serviços:** Contém serviços fornecidos pelo Adobe, como [Serviços de IA/ML](../intelligent-services/home.md) e qualquer serviço personalizado que você criou com o Espaço de trabalho de ciência de dados.

Por que estou vendo apenas a guia Serviços?

- Sua organização só pode ter direito ao Adobe Real-time Customer Data Platform (Real-Time CDP), que inclui o Serviço de IA/ML do cliente.

Se você não conseguir visualizar nenhuma das **Ciência de dados** e quiser utilizar os recursos do Data Science Workspace, entre em contato com o administrador da empresa para verificar se você tem uma licença do Adobe Experience Platform Intelligence.

## Empacotamento do Data Science Workspace

Os recursos do Data Science Workspace estão disponíveis no pacote Adobe Experience Platform Intelligence e no complemento Advanced Intelligence Pack

A tabela a seguir descreve algumas das principais diferenças para os direitos do Data Science Workspace com e sem o complemento Advanced Intelligence Pack:

>[!NOTE]
>
>Você pode licenciar mais de um Advanced Intelligence Pack Addon e o aumento da capacidade é adicionado ao seu direito geral. Por exemplo, se você licenciou dois complementos do Adobe Experience Platform Advanced Intelligence Pack, terá direito a um total de 20 usuários simultâneos do Notebook.

| Direito ao Espaço de trabalho de ciência de dados | Somente Pacote do Adobe Experience Platform Intelligence | Complemento Adobe Experience Platform Intelligence mais Advanced Intelligence Pack |
| --- | :---: | :---: |
| Número de usuários do Notebook suportados. | 5 usuários simultâneos | O Primeiro pacote adiciona 5 usuários simultâneos e compras adicionais adicionam 10 usuários simultâneos por pacote. |
| Permite notebooks Jupyter integrados para análise exploratória de dados e criação de modelo. | X (Suporta bibliotecas R, Python e Scala) | X (Adiciona bibliotecas PySpark e Spark ML) |
| Integração nativa com o Serviço de consulta. Capacidade de explorar e moldar conjuntos de dados usando SQL em notebooks. | X | X |
| Acesso a modelos de notebook pré-construídos para análises preditivas. | X | X |
| Treinar e pontuar modelos manualmente com o Jupyter Notebooks. | X | X |
| Implante e operacionalize modelos com a capacidade de programar treinamentos e trabalhos de inferência. |  | X |
| Estrutura de fórmula para configurar, avaliar, treinar, pontuar e publicar modelos na produção com facilidade. |  | X |
| Experimentação e avaliação de modelos orientados pela interface. |  | X |
| Suporte de aprendizagem profunda para modelos de fluxo de sensor (GPU Compute). |  | X |
| Computação distribuída baseada no Spark para treinar e pontuar em relação a grandes conjuntos de dados (10 MM + linhas). |  | X |

## Controle de acesso

O controle de acesso para o Experience Platform é administrado através do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Data Science Workspace, a permissão &quot;Gerenciar Data Science Workspace&quot; deve estar ativada. A tabela a seguir descreve os efeitos de ativar ou desativar essa permissão:

| Permissão | Ativado | Desativado |
|---|---|---|
| Gerenciar o Espaço de trabalho de ciência de dados | Fornece acesso a todos os serviços no Data Science Workspace. | O acesso da API e da interface do usuário a todos os serviços no Espaço de trabalho de ciência de dados está desativado. Enquanto estiver desativado, selecione a variável **Notebooks**, **Modelos**, e **Serviços** páginas é impedida. <li>Acesso a **Serviços** ainda podem estar disponíveis no Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Suporte à sandbox

As sandboxes são partições virtuais dentro de uma única instância do Experience Platform. Cada instância da Platform é compatível com várias sandboxes de produção e não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar suas sandboxes de produção. Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../sandboxes/home.md).

Atualmente, o Data Science Workspace tem a seguinte limitação de sandbox:

- Os recursos de computação são compartilhados entre as sandboxes de produção e não produção.

## Próximas etapas

Este documento descreveu os diferentes tipos de acesso e recursos disponíveis no Espaço de trabalho de ciência de dados.

Para saber mais sobre o Data Science Workspace, como um fluxo de trabalho diário completo, comece lendo o [Apresentação do Data Science Workspace](./walkthrough.md) documentação. Para obter informações mais gerais, visite o [Visão geral do Espaço de trabalho de ciência de dados](./home.md).
