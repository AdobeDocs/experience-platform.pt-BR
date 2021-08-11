---
keywords: Experience Platform, home, Data Science Workspace, tópicos populares, controle de acesso, sandbox, pacote de inteligência, recursos dsw, acesso ao dsw, Adobe Experience Platform Intelligence, inteligência, pacote de inteligência aep
solution: Experience Platform
title: Acesso e recursos do Data Science Workspace
topic-legacy: Access and features for data science workspace
description: O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 2ff2721f5420483ddc5caffd1eb0532df729e01b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# Acesso e recursos da Data Science Workspace

O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.

![Guias DSW](./images/access/platform-tabs.png)

- **Notebooks:** oferece um ambiente de desenvolvimento interativo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analisar e modelar seus dados no Experience Platform.
- **Modelos:** fornece ferramentas usadas para criar, publicar e armazenar fórmulas e modelos avançados de aprendizado de máquina. Para obter mais informações, visite o tutorial [criar e publicar um modelo de aprendizado de máquina](./models-recipes/create-publish-model.md).
- **Serviços:** contém serviços fornecidos pelo Adobe, como serviços de  [AI/ML e ](../intelligent-services/home.md) quaisquer serviços personalizados criados com o Data Science Workspace.

Por que estou vendo apenas a guia Serviços?

- Sua organização só pode ter direito à Plataforma de dados do cliente em tempo real (RTCDP), que inclui o Serviço de IA/ML do cliente.

Se não conseguir ver nenhuma das guias **Data Science** e quiser usar os recursos do Data Science Workspace, entre em contato com o administrador da empresa para verificar se você tem uma licença Adobe Experience Platform Intelligence.

## Embalagem da Data Science Workspace

Os recursos do Data Science Workspace estão disponíveis no pacote Adobe Experience Platform Intelligence e no complemento Advanced Intelligence Pack

A tabela a seguir descreve algumas das principais diferenças para os direitos do Data Science Workspace com e sem o complemento Advanced Intelligence Pack:

>[!NOTE]
>
>Você pode licenciar mais de um Addon do Advanced Intelligence Pack e o aumento da capacidade é adicionado ao seu direito geral. Por exemplo, se você licenciou 2 Adobe Experience Platform Advanced Intelligence Pack Addons, tem direito a um total de 20 usuários simultâneos de Notebook.

| Direito do Data Science Workspace | Somente Pacote de inteligência Adobe Experience Platform | Adobe Experience Platform Intelligence mais complemento de pacote de inteligência avançada |
| --- | :---: | :---: |
| Número de usuários do Notebook suportados. | 5 usuários simultâneos | O primeiro pacote adiciona 5 usuários simultâneos e compras adicionais e adiciona 10 usuários simultâneos por pacote. |
| Permite notebooks Jupyter integrados para análise de dados exploratórios e criação de modelos. | X (Suporta bibliotecas R, Python e Scala) | X (adiciona bibliotecas PySpark e Spark ML) |
| Integração nativa com o Serviço de query. Capacidade de explorar e modelar conjuntos de dados usando SQL em notebooks. | X | X |
| Acesso a modelos de notebook pré-criados para análises preditivas. | X | X |
| Treine e marque manualmente modelos com notebooks Jupyter. | X | X |
| Implante e operacionalize modelos com a capacidade de agendar trabalhos de treinamento e inferência. |  | X |
| Estrutura de receita para configurar, avaliar, treinar, pontuar e publicar modelos facilmente na produção. |  | X |
| Experimentação e avaliação de modelo orientada pela interface do usuário. |  | X |
| Suporte para aprendizado profundo para modelos de Tensorflow (GPU Compute). |  | X |
| Computação distribuída baseada em Spark para treinar e pontuar em relação a grandes conjuntos de dados (10MM + linhas). |  | X |

## Controle de acesso

O controle de acesso para Experience Platform é administrado por meio do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Data Science Workspace, a permissão &quot;Gerenciar Data Science Workspace&quot; deve estar habilitada. A tabela a seguir descreve os efeitos da ativação ou desativação dessa permissão:

| Permissão | Ativado | Desativado |
|---|---|---|
| Gerenciar o Data Science Workspace | Fornece acesso a todos os serviços no Data Science Workspace. | O acesso da API e da interface do usuário a todos os serviços no Data Science Workspace está desativado. Enquanto estiver desativado, a seleção das páginas **Notebooks**, **Modelos** e **Serviços** é impedida. <li>O acesso a **Services** ainda pode estar disponível por meio da Plataforma de dados do cliente em tempo real (RTCDP).</li> |

## Suporte a sandbox

As sandboxes são partições virtuais em uma única instância do Experience Platform. Cada instância da Platform é compatível com várias sandboxes de produção e não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar as sandboxes de produção. Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../sandboxes/home.md).

Atualmente, o Data Science Workspace tem a seguinte limitação de sandbox:

- Os recursos de computação são compartilhados nas sandboxes de produção e não produção.

## Próximas etapas

Este documento descrevia os diferentes tipos de acesso e recursos disponíveis no Data Science Workspace.

Para saber mais sobre o Data Science Workspace, como um fluxo de trabalho diário completo, comece lendo a documentação do [Data Science Workspace](./walkthrough.md). Para obter informações mais gerais, visite a [Visão geral do Data Science Workspace](./home.md).
