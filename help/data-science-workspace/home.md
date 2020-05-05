---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Visão geral da Análise do espaço de trabalho da Data Science
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Visão geral da Análise do espaço de trabalho da Data Science

A Adobe Experience Platform Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para liberar insights de seus dados. Integrado à Adobe Experience Platform, a Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe.

Os cientistas de dados de todos os níveis de habilidades encontrarão ferramentas sofisticadas e fáceis de usar que suportam o rápido desenvolvimento, treinamento e ajuste de fórmulas de aprendizado de máquina - todos os benefícios da tecnologia da IA, sem a complexidade.

Com a Data Science Workspace, os cientistas de dados podem criar facilmente APIs de serviços inteligentes - capacitadas pelo aprendizado de máquina. Esses serviços funcionam com outros serviços da Adobe, incluindo o Público alvo da Adobe e a Adobe Analytics Cloud, para ajudá-lo a automatizar experiências digitais personalizadas e direcionadas em aplicativos para Web, desktop e dispositivos móveis.

Este guia fornece uma visão geral dos principais conceitos relacionados à Data Science Workspace.

## Introdução

A empresa atual coloca uma alta prioridade na mineração de grandes dados para previsões e insights que os ajudarão a personalizar experiências de clientes e fornecer mais valor aos clientes - e aos negócios.
Por mais importante que seja, passar dos dados para insights pode ter um custo alto. Normalmente, requer cientistas de dados qualificados que conduzem pesquisas de dados intensivas e demoradas para desenvolver modelos de aprendizado de máquina, ou receitas, que potencializem serviços inteligentes. O processo é longo, a tecnologia é complexa, e dados especializados que os cientistas podem ser difíceis de encontrar.

Com a Data Science Workspace, a Adobe Experience Platform permite que você reúna uma IA voltada para a experiência em toda a empresa, simplificando e acelerando os dados para insights para código com:
- Uma estrutura de aprendizado de máquina e tempo de execução
- Acesso integrado aos seus dados armazenados na Adobe Experience Platform
- Um schema de dados unificado baseado no Experience Data Model (XDM)
- O poder de computação essencial para o aprendizado da máquina/IA e o gerenciamento de grandes conjuntos de dados
- Fórmulas de aprendizado de máquina pré-criadas para acelerar o salto em experiências conduzidas pela IA
- Criação, reutilização e modificação simplificadas de receitas para cientistas de dados de níveis variados de habilidades
- Publicação e compartilhamento de serviços inteligentes em apenas alguns cliques - sem um desenvolvedor - e monitoramento e treinamento para otimização contínua de experiências personalizadas do cliente

Os cientistas de dados de todos os níveis de habilidades obterão insights mais rapidamente e mais eficazes em experiências digitais.

## Introdução

Antes de entrar nos detalhes da Data Science Workspace, veja um breve resumo dos termos principais:

| Termo | Definição |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Área de trabalho da ciência de dados | A área de trabalho da ciência de dados na plataforma Experience permite que os clientes criem modelos de aprendizado de máquina utilizando dados na plataforma Experience e nas soluções da Adobe para gerar insights e previsões inteligentes para tecer experiências digitais deliciosas para o usuário final. |
| Inteligência artificial | A inteligência artificial é uma teoria e desenvolvimento de sistemas computacionais que são capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de voz, tomada de decisão e tradução entre línguas. |
| Aprendizagem de máquina | O aprendizado de máquina é o campo de estudo que permite aos computadores aprenderem sem serem explicitamente programados. |
| Sensei ML Framework | O Sensei ML Framework é uma estrutura unificada de aprendizado de máquina na Adobe que aproveita os dados na Experience Platform para capacitar os cientistas de dados no desenvolvimento de serviços de inteligência orientados por aprendizado de máquina de modo mais rápido, escalável e reutilizável. |
| Modelo de dados da experiência | O Experience Data Model (XDM) é o esforço de padronização da Adobe para definir schemas padrão, como Perfil e ExperienceEvent, para o Gerenciamento de experiência do cliente. |
| JupyterLab | O JupyterLab é uma interface baseada na Web de código aberto para o Project Júpitter e é totalmente integrado à plataforma Experience. |
| Receitas | Uma fórmula é o termo da Adobe para uma especificação de modelo e é um container de nível superior que representa um aprendizado de máquina específico, algoritmo AI ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas específicos de negócios. |
| Modelo | Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada usando dados históricos e configurações para solucionar um caso de uso comercial. |
| Treinamento | Treinamento é o processo de aprendizado de padrões e insights de dados rotulados. |
| Modelo treinado | Um modelo treinado representa a saída executável de um processo de treinamento modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência para qualquer Serviço Web Inteligente criado a partir dele. O modelo treinado é adequado para pontuação e criação de um serviço Web inteligente. As modificações em um modelo treinado podem ser rastreadas como uma nova versão. |
| Pontuação | A pontuação é o processo de gerar insights a partir de dados usando um modelo treinado. |
| Serviço de | Um serviço implantado expõe a funcionalidade de uma inteligência artificial, modelo de aprendizado de máquina ou algoritmo avançado por meio de uma API, para que possa ser consumido por outros serviços ou aplicativos para criar aplicativos inteligentes. |

O gráfico a seguir descreve a relação hierárquica entre Recebimentos, Modelos, Execuções de treinamento e Execuções de pontuação.

![](./images/home/recipe_hiearchy_ui.png)

## Como entender a área de trabalho da análise de dados

Com a Data Science Workspace, seus cientistas de dados podem simplificar o complicado processo de descoberta de insights em grandes conjuntos de dados. Construída com base em uma estrutura comum de aprendizado de máquina e tempo de execução, a Data Science Workspace oferece gerenciamento avançado de fluxo de trabalho, gerenciamento de modelos e escalabilidade. Os serviços inteligentes suportam a reutilização de fórmulas de aprendizado de máquina para potencializar uma variedade de aplicativos criados usando produtos e soluções da Adobe.

### Acesso único aos dados

Os dados são a pedra angular da IA e do aprendizado da máquina.

A Data Science Workspace é totalmente integrada à Adobe Experience Platform, incluindo o Data Lake, o Perfil do cliente em tempo real e o Unified Edge. Explore todos os dados organizacionais armazenados na Adobe Experience Platform de uma só vez, juntamente com grandes bibliotecas de dados e de aprendizado profundo comuns, como Spark ML e TensorFlow. Se você não encontrar o que precisa, assimile seus próprios conjuntos de dados usando o schema padronizado XDM.

### Fórmulas de aprendizado de máquina pré-criadas

A Data Science Workspace inclui fórmulas pré-criadas de aprendizado de máquina para necessidades comerciais comuns, como previsão de vendas de varejo e detecção de anomalias, de modo que os cientistas e desenvolvedores de dados não precisam start do zero. Atualmente, três fórmulas são oferecidas, previsão [de compra de](./pre-built-recipes/product-purchase-prediction.md)produtos, recomendações [de](./pre-built-recipes/product-recommendations.md)produtos e vendas [de](./pre-built-recipes/retail-sales.md)varejo.

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Se preferir, você pode adaptar uma receita pré-criada às suas necessidades, importar uma receita ou um start do zero para criar uma receita personalizada. Entretanto, quando você treina e hiperajusta uma receita, a criação de um serviço inteligente personalizado não requer um desenvolvedor - apenas alguns cliques e você está pronto para criar uma experiência digital direcionada e personalizada.

### Fluxo de trabalho focado no cientista de dados

Independentemente do seu nível de especialização em ciência de dados, a Data Science Workspace ajuda a simplificar e acelerar o processo de busca de insights em dados e aplicá-los a experiências digitais.

### Exploração de dados

Encontrar os dados certos e prepará-los é a parte mais trabalhosa da construção de uma receita eficaz. A Data Science Workspace e a Adobe Experience Platform o ajudarão a obter dos dados para insights mais rapidamente.

Na Adobe Experience Platform, seus dados entre canais são centralizados e armazenados no schema padronizado XDM, para que os dados sejam mais fáceis de encontrar, entender e limpar. Um único armazenamento de dados baseado em um schema comum pode salvar inúmeras horas de exploração e preparação de dados.

Ao navegar, use R, Python ou Scala com o notebook Jupyter integrado e hospedado para navegar pelo catálogo de dados na plataforma. Usando um desses idiomas, também é possível aproveitar o Spark ML e o TensorFlow. Start do zero ou use um dos modelos de notebook fornecidos para problemas específicos da empresa.

Como parte do fluxo de trabalho da exploração de dados, você também pode assimilar novos dados ou usar recursos existentes para ajudar na preparação dos dados.

### Criação  

Com a Data Science Workspace, você decide como deseja criar receitas.

- Economize tempo ao procurar uma fórmula pré-criada que atenda às suas necessidades comerciais, que você pode usar como está ou configurar para atender aos seus requisitos específicos.
- Crie uma receita do zero, usando o tempo de execução de criação no Jupyter Notebook para desenvolver e registrar a receita.
- Faça upload de uma receita criada fora da Adobe Experience Platform para a Data Science Workspace ou importe o código da receita de um repositório, como o Git, usando a autenticação e a integração disponíveis entre o Git e a Data Science Workspace.

### Experimentação

A Data Science Workspace proporciona uma grande flexibilidade ao processo de experimentação. Start com a sua receita. Em seguida, crie uma instância separada, usando o mesmo algoritmo principal emparelhado com características exclusivas, como parâmetros de hiperajuste. É possível criar quantas instâncias forem necessárias, treinando e pontuando cada instância quantas vezes desejar. À medida que você os treina, a Data Science Workspace rastreia receitas, instâncias de receitas e instâncias treinadas, juntamente com métricas de avaliação, para que você não precise.

### Operacionalização

Quando você está feliz com sua receita, é só alguns cliques para criar um serviço inteligente. Não é necessário programação - você pode fazer isso sozinho, sem se inscrever em um desenvolvedor ou engenheiro. Por fim, publique o serviço inteligente no Adobe IO e ele estará pronto para ser consumido pela sua equipe de experiência digital.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Melhoria contínua

A Data Science Workspace rastreia onde os serviços inteligentes são chamados e como estão se saindo. À medida que os dados entram, você pode avaliar a precisão do serviço inteligente para fechar o loop e retreinar as fórmulas conforme necessário para melhorar o desempenho. O resultado é um refinamento contínuo na precisão da personalização do cliente.

### Acesso a novos recursos e conjuntos de dados

Os cientistas de dados podem aproveitar as novas tecnologias e conjuntos de dados assim que estiverem disponíveis por meio dos serviços da Adobe. Através de atualizações frequentes, fazemos o trabalho de integração de conjuntos de dados e tecnologias na plataforma, para que você não precise.

### Controle de acesso na Data Science Workspace

O Controle de acesso for Experience Platform é administrado pelo [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produtos no Admin Console, que vinculam usuários com permissões e caixas de proteção. Consulte a visão geral [do](../access-control/home.md) controle de acesso para obter mais informações.

>[!IMPORTANT] Para usar o Data Science Workspace, a permissão &quot;Gerenciar o Data Science Workspace&quot; deve estar ativada.

A tabela a seguir descreve os efeitos da ativação ou desativação dessa permissão:

| Permissão | Ativado | Desabilitado |
|---|---|---|
| Gerenciar a área de trabalho da análise de dados | Fornece acesso a todos os serviços na Data Science Workspace. | O acesso à API e à interface do usuário a todos os serviços na Data Science Workspace está desativado. Enquanto estiver desativado, o roteamento das páginas *Modelos* e *Serviços* da Data Science é impedido. |

### Segurança e paz de espírito

A segurança de seus dados é uma das principais prioridades da Adobe. A Adobe protege seus dados com processos e controles de segurança desenvolvidos para ajudar a cumprir padrões, regulamentos e certificações aceitos pelo setor.

A segurança é integrada ao software e aos serviços como parte do Adobe Secure Product Lifecycle.
Para saber mais sobre a segurança, conformidade e outros dados do software e dados da Adobe, visite a página de segurança em https://www.adobe.com/security.html.

### Suporte a sandbox

As caixas de proteção são partições virtuais em uma única instância da Experience Platform. Cada instância da plataforma suporta uma caixa de proteção de produção e várias caixas de proteção de não produção, cada uma mantendo sua própria biblioteca de recursos da plataforma. As caixas de proteção de não-produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua caixa de proteção de produção. Para obter mais informações sobre caixas de proteção, consulte a visão geral [das](../sandboxes/home.md)caixas de proteção.

Atualmente, a Data Science Workspace tem algumas limitações:

- Os recursos de computação são compartilhados na caixa de proteção de produção e nas caixas de proteção de não produção. O isolamento para caixas de proteção de produção está definido para ser fornecido no futuro.
- Atualmente, as cargas de trabalho Scala/Spark e PySpark para notebooks e fórmulas são compatíveis apenas na área de segurança de produção. O suporte para caixas de proteção que não sejam de produção está definido para ser fornecido no futuro.

## Data Science Workspace em ação

As previsões e insights fornecem as informações necessárias para fornecer uma experiência altamente personalizada a cada cliente que visita seu site, entra em contato com sua central de atendimento ou participa de outras experiências digitais. Veja como seu trabalho diário acontece com a Data Science Workspace.

### Definir o problema

Tudo start com um problema de negócios. Por exemplo, uma central de atendimento on-line precisa de contexto para ajudá-los a tornar positivo o sentimento negativo do cliente.

Há muitos dados sobre o cliente. Eles navegaram pelo site, colocaram itens no carrinho e até fizeram pedidos. Eles podem ter recebido e-mails, usado cupons ou contatado a central de atendimento anteriormente. A receita, portanto, precisa usar os dados disponíveis sobre o cliente e suas atividades para determinar a propensão para comprar e recomendar uma oferta que o cliente provavelmente apreciará e usará.

![](./images/home/example_problem.png)

No momento do contato da central de atendimento, o cliente ainda tem dois pares de sapatos no carrinho, mas removeu uma camisa. Com essas informações, o serviço inteligente pode recomendar que o agente da central de atendimento oferta um cupom por 20% de desconto nos sapatos durante a chamada. Se o cliente usar o cupom, essas informações serão adicionadas ao conjunto de dados e as previsões se tornarão ainda melhores na próxima vez que o cliente fizer uma chamada.

### Explore e prepare os dados

Com base no problema de negócios definido, você sabe que a receita deve analisar todas as transações da Web do cliente, incluindo visitas ao site, pesquisas, visualizações de página, links clicados, ações de carrinho, ofertas recebidas, e-mails recebidos, interações de call center e assim por diante.

Um cientista de dados geralmente gasta até 75% do tempo necessário para criar uma receita explorando e transformando os dados. Os dados geralmente vêm de vários repositórios e são salvos em schemas diferentes - eles devem ser combinados e mapeados antes de poderem ser usados para criar uma fórmula.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Se você estiver começando do zero ou configurando uma fórmula existente, você começará a pesquisa de dados em um catálogo de dados centralizado e padronizado para sua organização, o que simplifica consideravelmente a busca. Você pode até descobrir que outro cientista de dados em sua organização já identificou um conjunto de dados semelhante e optar por ajustar esse conjunto de dados em vez de start do zero.
Todos os dados na Adobe Experience Platform estão em conformidade com um schema XDM padronizado, eliminando a necessidade de criar um modelo complexo para unir dados ou obter ajuda de um engenheiro de dados.

Se você não encontrar imediatamente os dados necessários, mas eles existem fora da Adobe Experience Platform, é uma tarefa relativamente simples de assimilar conjuntos de dados adicionais, que também se transformará no schema XDM padronizado.\
Você pode usar o Notebook Júpiter para simplificar o pré-processamento de dados - possivelmente começando com um modelo de notebook ou um notebook usado anteriormente para a propensão a comprar.

![](./images/home/notebook_templates.png)

### Aumentar a receita

Se você já encontrar uma fórmula que atenda a todas as suas necessidades, poderá passar para a experimentação. Ou você pode modificar um pouco a receita ou criar uma do zero - aproveitando o tempo de execução da criação da Data Science Workspace no Notebook de Júpiter. O uso do tempo de execução de criação garante que você possa usar o treinamento e o fluxo de trabalho de pontuação da Data Science Workspace e converter a fórmula posteriormente, para que possa ser armazenada e reutilizada por outras pessoas em sua organização.

Você também pode importar uma receita para a Data Science Workspace e aproveitar os workflows de experimentação ao criar seu serviço inteligente.

### Experimente com a receita

Com uma receita que incorpora os algoritmos principais de aprendizado de máquina, muitas instâncias de fórmula podem ser criadas com uma única receita. Essas instâncias de fórmula são chamadas de modelos. Um modelo requer treinamento e avaliação para otimizar sua eficiência e eficácia operacional, um processo normalmente composto de tentativa e erro.

![](./images/home/recipe_hiearchy_ui.png)

À medida que você treina seus modelos, as execuções de treinamento e as avaliações são geradas. A Data Science Workspace acompanha as métricas de avaliação de cada modelo único e suas execuções de treinamento. As métricas de avaliação geradas por meio de experimentação permitirão determinar a execução de treinamento que tem melhor desempenho.

![](./images/home/evaluation_metrics.png)

Visite [esta seção](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) para obter tutoriais sobre como treinar e avaliar modelos na Data Science Workspace.

### Operacionalizar o modelo

Quando você seleciona a melhor fórmula treinada para atender às necessidades de sua empresa, pode criar um serviço inteligente na Data Science Workspace sem a ajuda do desenvolvedor. São apenas alguns cliques - sem necessidade de codificação. Um serviço inteligente publicado é acessível a outros membros de sua organização sem a necessidade de recriar o modelo.

Um serviço inteligente publicado é configurável para se treinar automaticamente de vez em quando usando novos dados conforme eles se tornam disponíveis. Isso garante que seu serviço mantenha sua eficiência e eficácia enquanto o tempo continua.

## Próximas etapas

A Data Science Workspace ajuda a otimizar e simplificar o fluxo de trabalho da ciência de dados, desde a coleta de dados até os algoritmos até serviços inteligentes, para cientistas de dados de todos os níveis de habilidades. Com as ferramentas sofisticadas que a Data Science Workspace oferece, você pode reduzir significativamente o tempo dos dados para insights.

Mais importante, a Data Science Workspace coloca os recursos de ciência de dados e otimização algorítmica da plataforma de marketing líder da Adobe nas mãos dos cientistas de dados da empresa. Pela primeira vez, as empresas podem trazer algoritmos proprietários para a plataforma, aproveitando os poderosos recursos de aprendizado de máquina e AI da Adobe para oferecer experiências altamente personalizadas aos clientes em larga escala.

Com o casamento entre a experiência em marca e o aprendizado de máquina da Adobe e a proeza em IA, as empresas têm o poder de gerar mais valor comercial e fidelidade à marca, dando aos clientes o que eles querem, antes que eles peçam.

Para obter informações adicionais, como um fluxo de trabalho diário completo, comece lendo a documentação de navegação da [Data Science Workspace](./walkthrough.md) .

## Recursos adicionais

O vídeo a seguir foi criado para oferecer suporte à sua compreensão da Data Science Workspace.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

