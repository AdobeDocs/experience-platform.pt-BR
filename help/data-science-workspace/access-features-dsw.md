---
keywords: Experience Platform;home;Data Science Workspace;popular topics;controle de acesso;sandbox;inteligbox;pacote;dsw features;dsw access;Adobe Experience Platform Intelligence;inteligência;pacote de inteligência aep
solution: Experience Platform
title: Acesso e recursos da Data Science Workspace
topic: Access and features for data science workspace
description: 'O documento a seguir descreve as permissões e o acesso aos recursos da Data Science Workspace. '
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---


# Acesso e recursos da Data Science Workspace

O documento a seguir descreve as permissões e o acesso aos recursos da Data Science Workspace.

![Guias DSW](./images/access/platform-tabs.png)

- **Notebooks:** fornece um ambiente de desenvolvimento interativo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analisar e modelar seus dados no Experience Platform.
- **Modelos:** fornece ferramentas usadas para criar, publicar e armazenar fórmulas e modelos avançados de aprendizado de máquina. Para obter mais informações, visite o tutorial [criar e publicar um modelo de aprendizado de máquina](./models-recipes/create-publish-model.md).
- **Serviços:** contém serviços fornecidos pelo Adobe, como  [Serviços ](../intelligent-services/home.md) inteligentes e quaisquer serviços personalizados criados com a Data Science Workspace.

Por que estou apenas vendo a guia Serviços?

- Sua organização pode ter direito somente à Plataforma de dados do cliente em tempo real (RTCDP), que inclui a IA do cliente de serviço inteligente.

Se você não conseguir ver nenhuma das guias **Data Science** e quiser utilizar os recursos da Data Science Workspace, entre em contato com o administrador da empresa para verificar se você tem uma licença do Adobe Experience Platform Intelligence.

## Anúncio de pacote do Adobe Experience Platform Intelligence

A tabela a seguir descreve algumas das principais diferenças para a Data Science Workspace com e sem o complemento do pacote Adobe Experience Platform Intelligence:

>[!NOTE]
>
>Você pode licenciar mais de um complemento do pacote de Inteligência e o aumento da capacidade é adicionado ao seu direito geral. Por exemplo, se você licenciou 2 suplementos de pacote do Adobe Experience Platform Intelligence, terá direito a um total de 20 usuários simultâneos do notebook.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] com adendo de pacote de inteligência |
| --- | :---: | :---: |
| Número de usuários do Bloco de notas suportados. | 5 usuários simultâneos | O primeiro pacote adiciona 5 usuários simultâneos e compras adicionais acrescentam 10 usuários simultâneos por pacote. |
| Permite notebooks Jupyter integrados para análise de dados exploratórios e criação de modelos (R, Python, Scala, PySpark) | X | X |
| Integração nativa com o Serviço de Query. Capacidade de explorar e modelar conjuntos de dados usando SQL em notebooks. | X | X |
| Acesso a modelos de notebook pré-criados para análise preditiva. | X | X |
| Treine manualmente os modelos de pontuação com notebooks Júpiter. | X | X |
| Implante e operacionalize modelos com a capacidade de programar trabalhos de treinamento e dedução. |  | X |
| Estrutura de receita para configurar, avaliar, treinar, pontuar e publicar modelos facilmente na produção. |  | X |
| Experimentação e avaliação de modelos orientados pela interface do usuário. |  | X |
| Suporte a aprendizado profundo para modelos de fluxo de tela (GPU Compute). |  | X |
| Computação distribuída com base em faísca para treinar e pontuar em grandes conjuntos de dados (10MM + linhas). |  | X |

## Controle de acesso

O controle de acesso para Experience Platform é administrado por meio do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Data Science Workspace, a permissão &quot;Gerenciar o Data Science Workspace&quot; deve estar ativada. A tabela a seguir descreve os efeitos da ativação ou desativação dessa permissão:

| Permissão | Ativado | Desativado |
|---|---|---|
| Gerenciar a área de trabalho da análise de dados | Fornece acesso a todos os serviços na Data Science Workspace. | O acesso à API e à interface do usuário a todos os serviços na Data Science Workspace está desativado. Enquanto estiver desativado, a seleção das páginas **Notebooks**, **Modelos** e **Serviços** não é possível. <li>O acesso aos **Serviços** ainda pode estar disponível por meio da Plataforma de Dados de Clientes em Tempo Real (RTCDP).</li> |

## Suporte a sandbox

As caixas de proteção são partições virtuais em uma única instância do Experience Platform. Cada instância da plataforma suporta uma caixa de proteção de produção e várias caixas de proteção de não produção, cada uma mantendo sua própria biblioteca de recursos da plataforma. As caixas de proteção de não-produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua caixa de proteção de produção. Para obter mais informações sobre caixas de proteção, consulte a [visão geral das caixas de proteção](../sandboxes/home.md).

Atualmente, a Data Science Workspace tem a seguinte limitação:

- Os recursos de computação são compartilhados na caixa de proteção de produção e nas caixas de proteção de não produção.

## Próximas etapas

Este documento destacou os diferentes tipos de acesso e recursos disponíveis na Data Science Workspace.

Para saber mais sobre a Data Science Workspace, como um fluxo de trabalho diário completo, comece lendo a documentação do [Data Science Workspace](./walkthrough.md). Para obter informações mais gerais, visite a [visão geral da Data Science Workspace](./home.md).