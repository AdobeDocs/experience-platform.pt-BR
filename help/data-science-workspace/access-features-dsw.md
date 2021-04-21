---
keywords: Experience Platform, home, Data Science Workspace, tópicos populares, controle de acesso, sandbox, pacote de inteligência, recursos dsw, acesso ao dsw, Adobe Experience Platform Intelligence, inteligência, pacote de inteligência aep
solution: Experience Platform
title: Acesso e recursos do Data Science Workspace
topic-legacy: Access and features for data science workspace
description: O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# Acesso e recursos da Data Science Workspace

O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.

![Guias DSW](./images/access/platform-tabs.png)

- **Notebooks:** oferece um ambiente de desenvolvimento interativo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analisar e modelar seus dados no Experience Platform.
- **Modelos:** fornece ferramentas usadas para criar, publicar e armazenar fórmulas e modelos avançados de aprendizado de máquina. Para obter mais informações, visite o tutorial [criar e publicar um modelo de aprendizado de máquina](./models-recipes/create-publish-model.md).
- **Serviços:** contém serviços fornecidos pelo Adobe, como Serviços  [inteligentes ](../intelligent-services/home.md) e quaisquer serviços personalizados criados com o Data Science Workspace.

Por que estou vendo apenas a guia Serviços?

- Sua organização só pode ter direito à Plataforma de dados do cliente em tempo real (RTCDP), que inclui a API do cliente de serviço inteligente.

Se não conseguir ver nenhuma das guias **Data Science** e quiser usar os recursos do Data Science Workspace, entre em contato com o administrador da empresa para verificar se você tem uma licença Adobe Experience Platform Intelligence.

## Aditamento de pacote Adobe Experience Platform Intelligence

A tabela a seguir descreve algumas das principais diferenças para o Data Science Workspace com e sem o complemento do pacote Adobe Experience Platform Intelligence :

>[!NOTE]
>
>Você pode licenciar mais de um pacote de Inteligência e o aumento da capacidade é adicionado ao seu direito geral. Por exemplo, se você licenciou 2 adjuntos de pacotes Adobe Experience Platform Intelligence, terá direito a um total de 20 usuários simultâneos de Notebook.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] com o complemento de pacote de inteligência |
| --- | :---: | :---: |
| Número de usuários do Notebook suportados. | 5 usuários simultâneos | O primeiro pacote adiciona 5 usuários simultâneos e compras adicionais e adiciona 10 usuários simultâneos por pacote. |
| Permite notebooks Jupyter integrados para análise de dados exploratórios e criação de modelos (R, Python, Scala, PySpark) | X | X |
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

As sandboxes são partições virtuais em uma única instância do Experience Platform. Cada instância da Platform é compatível com uma sandbox de produção e várias sandboxes de não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar a sandbox de produção. Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../sandboxes/home.md).

Atualmente, o Data Science Workspace tem a seguinte limitação de sandbox:

- Os recursos de computação são compartilhados nas sandbox de produção e nas sandboxes de não produção.

## Próximas etapas

Este documento descrevia os diferentes tipos de acesso e recursos disponíveis no Data Science Workspace.

Para saber mais sobre o Data Science Workspace, como um fluxo de trabalho diário completo, comece lendo a documentação do [Data Science Workspace](./walkthrough.md). Para obter informações mais gerais, visite a [Visão geral do Data Science Workspace](./home.md).
