---
keywords: Experience Platform;página inicial;Data Science Workspace;tópicos populares;controle de acesso;sandbox;pacote de inteligência;recursos do dsw;acesso do dsw;inteligência do Adobe Experience Platform;pacote de inteligência do aep
solution: Experience Platform
title: Acesso e recursos do Data Science Workspace
description: O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# Acesso e recursos do Área de trabalho de ciência de dados

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

O documento a seguir descreve as permissões do Data Science Workspace e o acesso aos recursos.

![guias DSW](./images/access/platform-tabs.png)

- **Notebooks:** fornece um ambiente de desenvolvimento interativo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analisar e modelar seus dados no Experience Platform.
- **Modelos:** fornece ferramentas usadas para criar, publicar e armazenamento receitas e modelos avançados de aprendizado de máquina. Para obter mais informações, visita criar [e publicar um tutorial de modelo](./models-recipes/create-publish-model.md) de aprendizado de máquina.
- **Serviços:** contém serviços fornecidos Adobe Systems, como [serviços](../intelligent-services/home.md) de IA/ML e quaisquer serviços personalizados criados com o Data Science Área de trabalho.

Por que estou vendo apenas a guia Serviços?

- Sua organização só pode ter direito ao Adobe Real-time Customer Data Platform (Real-Time CDP), que inclui o Serviço de IA/ML do cliente.

Se você não conseguir ver nenhuma das guias **Data Science** e quiser utilizar os recursos do Data Science Workspace, entre em contato com o administrador da sua empresa para verificar se você tem uma licença do Adobe Experience Platform Intelligence.

## Pacotes de Área de trabalho de ciência de dados

Os recursos do Área de trabalho de ciência de dados estão disponíveis no pacote Adobe Experience Platform Intelligence e no complemento Avançado Intelligence Pack

A tabela a seguir descreve algumas das principais diferenças nos direitos de Área de trabalho da Data Science com e sem o complemento Avançado Intelligence Pack:

>[!NOTE]
>
>Você pode licenciar mais de um Avançado Intelligence Pack Addon e o aumento da capacidade é adicionado ao seu direito geral. Por exemplo, se você licenciou 2 Adobe Experience Platform Avançado Complementos de Pacote de Inteligência, você tem direito a um total de 20 usuários simultâneos do Notebook.

| Direitos do Área de trabalho de ciência de dados | Somente Pacote do Adobe Experience Platform Intelligence | Complemento Adobe Experience Platform Intelligence mais Advanced Intelligence Pack |
| --- | :---: | :---: |
| Número de usuários do Notebook suportados. | 5 usuários simultâneos | O primeiro pacote adiciona 5 usuários simultâneos e compras adicionais, além de adicionar 10 usuários simultâneos por pacote. |
| Permite notebooks Jupyter integrados para análise de dados exploratórios e criação de modelos. | X (Suporta bibliotecas R, Python e Scala) | X (Adiciona bibliotecas PySpark e Spark ML) |
| Integração nativa com o Serviço de consulta. Capacidade de explorar e moldar conjuntos de dados usando SQL em notebooks. | X | X |
| Acesso a modelos de notebook pré-construído para análise preditiva. | X | X |
| Treinar e pontuar modelos manualmente com o Jupyter Notebooks. | X | X |
| Implante e operacionalize modelos com a capacidade de agendar treinamento e inferir trabalhos. | | X |
| Os estrutura de receita para configurar, avaliar, treinar, treinar, pontuar e publicar modelos na produção. |  | X |
| interface de avaliação e experimentação de modelo orientado. | | X |
| Suporte de aprendizagem profunda para modelos de tensorflow (Cálculo de GPU). | | X |
| Cálculo distribuído com base em spark para treinar e pontuar em relação a grandes conjuntos de dados (10MM + linhas). | | X |

## Controle de acesso

O controle de acesso para o Experience Platform é administrado através da [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita os perfis de produtos em Admin Console, que link os usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Data Science Workspace, a permissão &quot;Gerenciar Data Science Workspace&quot; deve estar ativada. A tabela a seguir descreve os efeitos de ativar ou desativar essa permissão:

| Permissão | Ativado | Desabilitado |
|---|---|---|
| Gerenciar Área de trabalho de ciência de dados | Fornece acesso a todos os serviços no Data Science Área de trabalho. | O acesso da API e interface a todos os serviços na Data Science Área de trabalho está desativado. Enquanto estiver desativado, a seleção das **páginas Notebooks**, **Modelos** e **Serviços** fica impedida. <li>O acesso aos **Serviços** ainda pode estar disponível por meio do Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Suporte à sandbox

As sandboxes são partições virtuais dentro de uma única instância do Experience Platform. Cada instância da Platform é compatível com várias sandboxes de produção e não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar suas sandboxes de produção. Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../sandboxes/home.md).

Atualmente, a Data Science Área de trabalho tem a seguinte limitação da área de segurança:

- Os recursos de computação são compartilhados entre as sandboxes de produção e não produção.

## Próximas etapas

Esse documento descreveu os diferentes tipos de acesso e recursos disponíveis no Data Science Workspace.

Para saber mais sobre o Data Science Workspace, como um fluxo de trabalho diário completo, comece lendo a [documentação de apresentação do Data Science Workspace](./walkthrough.md). Para obter informações mais gerais, visite a [visão geral do Data Science Workspace](./home.md).
