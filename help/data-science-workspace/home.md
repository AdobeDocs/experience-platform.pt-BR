---
keywords: Experience Platform;página inicial;Espaço de trabalho de ciência de dados;tópicos populares;espaço de trabalho de ciência de dados;ciência de dados
solution: Experience Platform
title: Visão geral do Data Science Workspace
description: Este guia fornece uma visão geral dos principais conceitos relacionados ao Espaço de trabalho de ciência de dados na Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: fa52aa668d21f71c0da6b35c933713f068e36b28
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---

# Visão geral do Espaço de trabalho de ciência de dados

>[!NOTE]
>
>Observe que a presença da documentação sobre um recurso no Experience League não garante sua disponibilidade para todos os clientes. Esse recurso só está disponível para clientes existentes que compraram uma licença do Adobe Experience Platform ou do Adobe Experience Platform Intelligence. Consulte a descrição oficial do produto para entender os recursos e outros detalhes associados aos SKUs/produtos comprados.


Adobe Experience Platform [!DNL Data Science Workspace] O usa aprendizagem de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, [!DNL Data Science Workspace] O ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções do Adobe.

Os cientistas de dados de todos os níveis de habilidade encontrarão ferramentas sofisticadas e fáceis de usar que oferecem suporte ao rápido desenvolvimento, treinamento e ajuste de receitas de aprendizado de máquina - todos os benefícios da tecnologia de IA, sem a complexidade.

Com [!DNL Data Science Workspace], os cientistas de dados podem criar facilmente APIs de serviços inteligentes - viabilizadas pelo aprendizado de máquina. Esses serviços funcionam com outros serviços da Adobe, incluindo o Adobe Target e o Adobe Analytics Cloud, para ajudar você a automatizar experiências digitais personalizadas e direcionadas em aplicativos da Web, da área de trabalho e móveis.

Este guia fornece uma visão geral dos principais conceitos relacionados ao [!DNL Data Science Workspace].

## Introdução

As empresas atuais dão alta prioridade à mineração de big data para previsões e insights que as ajudarão a personalizar as experiências dos clientes e a agregar mais valor aos clientes - e aos negócios.
Mesmo sendo importante, a obtenção de dados para insights pode ter um custo alto. Normalmente, ela requer cientistas de dados qualificados que realizam pesquisas de dados intensivas e demoradas para desenvolver modelos ou receitas de aprendizado de máquina que alimentam os serviços inteligentes. O processo é longo, a tecnologia é complexa e cientistas de dados qualificados podem ser difíceis de encontrar.

Com [!DNL Data Science Workspace], o Adobe Experience Platform permite trazer IA com foco em experiência para toda a empresa, simplificando e acelerando a integração de dados e insights ao código com:
- Uma estrutura de aprendizado de máquina e tempo de execução
- Acesso integrado aos dados armazenados no Adobe Experience Platform
- Um esquema de dados unificado baseado em [!DNL Experience Data Model] (XDM)
- A potência computacional essencial para o aprendizado de máquina/IA e o gerenciamento de grandes conjuntos de dados
- Receitas de aprendizado de máquina pré-criadas para acelerar o salto para experiências orientadas por IA
- Criação, reutilização e modificação simplificadas de receitas para cientistas de dados de vários níveis de habilidade
- Publicação e compartilhamento inteligentes de serviços com apenas alguns cliques, sem um desenvolvedor, e monitoramento e novo treinamento para otimização contínua de experiências personalizadas do cliente

Cientistas de dados de todos os níveis de habilidade obterão insights mais rapidamente e experiências digitais mais eficazes.

## Introdução

Antes de mergulhar nos detalhes de [!DNL Data Science Workspace], aqui está um breve resumo dos termos principais:

| Termo | Definição |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] no prazo de [!DNL Experience Platform] permite que os clientes criem modelos de aprendizado de máquina utilizando dados em [!DNL Experience Platform] e Adobe Soluções para gerar insights e previsões inteligentes para tecer experiências digitais deliciosas para o usuário final. |
| Inteligência artificial | Inteligência artificial é uma teoria e desenvolvimento de sistemas computacionais que são capazes de executar tarefas que normalmente exigem inteligência humana, como percepção visual, reconhecimento de fala, tomada de decisão e tradução entre línguas. |
| Aprendizado de Máquina | O aprendizado de máquina é o campo de estudo que permite aos computadores a capacidade de aprender sem ser explicitamente programado. |
| [!DNL Sensei] Estrutura de ML | [!DNL Sensei] A estrutura de ML é uma estrutura unificada de aprendizado de máquina no Adobe que utiliza dados sobre [!DNL Experience Platform] capacitar os cientistas de dados no desenvolvimento de serviços de inteligência orientados para o aprendizado de máquina de maneira mais rápida, escalável e reutilizável. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) é o esforço de padronização liderado pelo Adobe para definir esquemas padrão, como [!DNL Profile] e [!DNL ExperienceEvent], para Gerenciamento de experiência do cliente. |
| [!DNL JupyterLab] | [!DNL JupyterLab] é uma interface web de código aberto para o Project Jupyter e está totalmente integrada ao [!DNL Experience Platform]. |
| Receitas | Uma fórmula é um termo de Adobe para uma especificação de modelo e é um contêiner de nível superior que representa um aprendizado de máquina específico, algoritmo de IA ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas comerciais específicos. |
| Modelo | Um modelo é uma instância de uma fórmula de aprendizado de máquina treinada com dados históricos e configurações para resolver em um caso de uso comercial. |
| Treinamento | Treinamento é o processo de padrões de aprendizado e insights de dados rotulados. |
| Modelo treinado | Um modelo treinado representa a saída executável de um processo de treinamento de modelo, no qual um conjunto de dados de treinamento foi aplicado à instância do modelo. Um modelo treinado manterá uma referência a qualquer serviço inteligente da Web criado a partir dele. O modelo treinado é adequado para pontuar e criar um serviço web inteligente. As modificações em um modelo treinado podem ser rastreadas como uma nova versão. |
| Pontuação | A pontuação é o processo de gerar insights dos dados usando um modelo treinado. |
| Serviço | Um serviço implantado expõe a funcionalidade de uma inteligência artificial, de um modelo de aprendizado de máquina ou de um algoritmo avançado por meio de uma API, para que possa ser consumido por outros serviços ou aplicativos para criar aplicativos inteligentes. |

O gráfico a seguir descreve a relação hierárquica entre Receitas, Modelos, Execuções de Treinamento e Execuções de Pontuação.

![](./images/home/recipe_hiearchy_ui.png)

## Noções básicas do [!DNL Data Science Workspace]

Com [!DNL Data Science Workspace], seus cientistas de dados podem simplificar o complicado processo de descoberta de insights em grandes conjuntos de dados. Baseado em uma estrutura e um tempo de execução comuns de aprendizado de máquina, [!DNL Data Science Workspace] O oferece gerenciamento avançado de fluxo de trabalho, gerenciamento de modelos e escalabilidade. Os serviços inteligentes suportam a reutilização de receitas de aprendizado de máquina para potencializar uma variedade de aplicativos criados com produtos e soluções Adobe.

### Acesso aos dados em um único local

Os dados são a base da IA e do aprendizado de máquina.

[!DNL Data Science Workspace] O é totalmente integrado ao Adobe Experience Platform, incluindo o Data Lake, [!DNL Real-Time Customer Profile], e [!DNL Unified Edge]. Explore todos os dados organizacionais armazenados no Adobe Experience Platform de uma só vez, juntamente com os big data comuns e as bibliotecas de deep learning, como [!DNL Spark] ML e [!DNL TensorFlow]. Se não encontrar o que precisa, assimile seus próprios conjuntos de dados usando o esquema padronizado XDM.

### Receitas de aprendizado de máquina pré-criadas

[!DNL Data Science Workspace] O inclui receitas de aprendizado de máquina pré-criadas para necessidades comerciais comuns, como previsão de vendas de varejo e detecção de anomalias, para que cientistas e desenvolvedores de dados não precisem começar do zero. Atualmente, são oferecidas três receitas, [previsão de compra do produto](./pre-built-recipes/product-purchase-prediction.md), [recomendações de produto](./pre-built-recipes/product-recommendations.md), e [vendas de varejo](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Se preferir, você poderá adaptar uma fórmula pré- criada às suas necessidades, importar uma fórmula ou começar do zero para criar uma fórmula personalizada. No entanto, você começa, depois de treinar e hiperajustar uma fórmula, criar um serviço inteligente personalizado não requer um desenvolvedor, apenas alguns cliques e você está pronto para criar uma experiência digital direcionada e personalizada.

### Fluxo de trabalho focado no cientista de dados

Qualquer que seja o seu nível de conhecimento em ciência de dados, [!DNL Data Science Workspace] O ajuda a simplificar e acelerar o processo de encontrar insights em dados e aplicá-los a experiências digitais.

### Exploração de dados

Encontrar os dados certos e prepará-los é a parte mais trabalhosa para criar uma fórmula eficaz. [!DNL Data Science Workspace] O e o Adobe Experience Platform ajudarão você a passar do data para o insights mais rapidamente.

No Adobe Experience Platform, os dados entre canais são centralizados e armazenados no esquema padronizado do XDM, de modo que os dados são mais fáceis de encontrar, entender e limpar. Um único armazenamento de dados com base em um esquema comum pode economizar inúmeras horas de exploração e preparação de dados.

À medida que você navega, use R, [!DNL Python]ou Scala com o aplicativo integrado, hospedado [!DNL Jupyter Notebook] para procurar o catálogo de dados em [!DNL Platform]. Usando uma dessas linguagens, você também pode aproveitar [!DNL Spark] ML e TensorFlow. Comece do zero ou use um dos modelos de bloco de anotações fornecidos para problemas comerciais específicos.

Como parte do fluxo de trabalho de exploração de dados, você também pode assimilar novos dados ou usar recursos existentes para ajudar na preparação dos dados.

### Criação

Com [!DNL Data Science Workspace], você decide como deseja criar receitas.

- Economize tempo procurando uma fórmula pré-criada que atenda às suas necessidades comerciais, que você pode usar como está ou configurar para atender aos seus requisitos específicos.
- Crie uma fórmula do zero, usando o tempo de execução de criação no Jupyter Notebook para desenvolver e registrar a fórmula.
- Fazer upload de uma fórmula criada fora do Adobe Experience Platform para [!DNL Data Science Workspace] ou importar código de fórmula de um repositório, como [!DNL Git], utilizando a autenticação e a integração disponíveis entre [!DNL Git] e [!DNL Data Science Workspace].

### Experimentação

O Data Science Workspace oferece tremenda flexibilidade ao processo de experimentação. Comece com sua fórmula. Em seguida, crie uma instância separada, usando o mesmo algoritmo principal combinado com características exclusivas, como parâmetros de hiperajuste. Você pode criar quantas instâncias forem necessárias, treinando e pontuando cada instância quantas vezes desejar. Ao treiná-los, [!DNL Data Science Workspace] O rastreia receitas, instâncias de receitas e instâncias treinadas, além de métricas de avaliação, para que você não precise fazê-lo.

### Operacional

Quando estiver satisfeito com a sua receita, basta alguns cliques para criar um serviço inteligente. Nenhuma codificação necessária - você mesmo pode fazer isso sem inscrever um desenvolvedor ou engenheiro. Por fim, publique o serviço inteligente no Adobe IO e ele estará pronto para ser consumido pela sua equipe de experiência digital.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Aprimoramento contínuo

[!DNL Data Science Workspace] rastreia onde os serviços inteligentes são chamados e como estão se saindo. À medida que os dados são acumulados, você pode avaliar a precisão do serviço inteligente para fechar o loop e treinar novamente as receitas, conforme necessário, para melhorar o desempenho. O resultado é um refinamento contínuo na precisão da personalização do cliente.

### Acesso a novos recursos e conjuntos de dados

Os cientistas de dados podem aproveitar as novas tecnologias e conjuntos de dados assim que estiverem disponíveis pelos serviços da Adobe. Por meio de atualizações frequentes, fazemos o trabalho de integrar conjuntos de dados e tecnologias à plataforma, para que você não precise fazê-lo.

### Segurança e tranquilidade

Proteger seus dados é a principal prioridade do Adobe. O Adobe protege seus dados com processos e controles de segurança desenvolvidos para ajudar a cumprir os padrões, regulamentos e certificações aceitos pelo setor.

A segurança é integrada ao software e aos serviços como parte do ciclo de vida seguro do produto Adobe.
Para saber mais sobre segurança de dados e software de Adobe, conformidade e muito mais, visite a página de segurança em https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] em ação

As previsões e insights fornecem as informações necessárias para fornecer uma experiência altamente personalizada a cada cliente que visita seu site, entra em contato com sua central de atendimento ou participa de outras experiências digitais. Veja como o seu trabalho diário acontece com [!DNL Data Science Workspace].

### Definir o problema

Tudo começa com um problema nos negócios. Por exemplo, uma central de atendimento online precisa de contexto para ajudá-la a tornar positivo um sentimento negativo do cliente.

Há muitos dados sobre o cliente. Eles navegaram pelo site, colocaram itens em seu carrinho e até fizeram pedidos. Eles podem ter recebido emails, usado cupons ou contatado a central de atendimento anteriormente. A fórmula, então, precisa usar os dados disponíveis sobre o cliente e suas atividades para determinar a propensão para comprar e recomendar uma oferta que o cliente provavelmente apreciará e usará.

![](./images/home/example_problem.png)

No momento do contato da central de atendimento, o cliente ainda tinha dois pares de sapatos no carrinho, mas removeu uma camisa. Com essas informações, o serviço inteligente pode recomendar que o agente da central de atendimento ofereça um cupom de 20% de desconto em sapatos durante a chamada. Se o cliente usar o cupom, essas informações serão adicionadas ao conjunto de dados e as previsões se tornarão ainda melhores na próxima vez que o cliente ligar.

### Explorar e preparar os dados

Com base no problema comercial definido, você sabe que a fórmula deve examinar todas as transações do cliente na Web, incluindo visitas ao site, pesquisas, exibições de página, links clicados, ações do carrinho, ofertas recebidas, emails recebidos, interações da central de atendimento e assim por diante.

Um cientista de dados normalmente gasta até 75% do tempo necessário para criar uma fórmula explorando e transformando os dados. Os dados geralmente vêm de vários repositórios e são salvos em esquemas diferentes - eles devem ser combinados e mapeados antes de serem usados para criar uma fórmula.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Se você estiver começando do zero ou configurando uma fórmula existente, inicie sua pesquisa de dados em um catálogo de dados centralizado e padronizado para sua organização, o que simplifica consideravelmente a busca. Você pode até descobrir que outro cientista de dados em sua organização já identificou um conjunto de dados semelhante e optar por ajustar esse conjunto de dados em vez de começar do zero.
Todos os dados no Adobe Experience Platform estão em conformidade com um esquema XDM padronizado, eliminando a necessidade de criar um modelo complexo para unir dados ou obter ajuda de um engenheiro de dados.

Se você não encontrar imediatamente os dados necessários, mas eles existirem fora do Adobe Experience Platform, é uma tarefa relativamente simples assimilar conjuntos de dados adicionais, que também se transformarão no esquema XDM padronizado.\
Você pode usar [!DNL Jupyter Notebook] para simplificar o pré-processamento de dados - possivelmente começando com um modelo de notebook ou um notebook que você usou anteriormente para a propensão à compra.

![](./images/home/notebook_templates-new.png)

### Criar a fórmula

Se você já encontrou uma fórmula que atende a todas as suas necessidades, poderá seguir para a experimentação. Ou você pode modificar um pouco a fórmula ou criar uma do zero - aproveitando o [!DNL Data Science Workspace] tempo de execução de criação no [!DNL Jupyter Notebook]. O uso do tempo de execução da criação garante que você possa usar o [!DNL Data Science Workspace] workflow de treinamento e pontuação e converta a fórmula posteriormente para que ela possa ser armazenada e reutilizada por outros em sua organização.

Você também pode importar uma fórmula no para [!DNL Data Science Workspace] e aproveite os fluxos de trabalho de experimentação ao criar seu serviço inteligente.

### Experimentar com a fórmula

Com uma fórmula que incorpora seus principais algoritmos de aprendizado de máquina, várias instâncias de fórmula podem ser criadas com uma única fórmula. Essas instâncias de receita são chamadas de modelos. Um modelo requer treinamento e avaliação para otimizar sua eficiência e eficácia operacional, um processo que geralmente consiste em tentativa e erro.

![](./images/home/recipe_hiearchy_ui.png)

À medida que você treina seus modelos, são geradas execuções de treinamento e avaliações. [!DNL Data Science Workspace] mantém o controle das métricas de avaliação para cada modelo único e suas execuções de treinamento. As métricas de avaliação geradas pela experimentação permitirão determinar a execução de treinamento com melhor desempenho.

![](./images/home/evaluation_metrics.png)

Visite o [API](./models-recipes/train-evaluate-model-api.md) ou [IU](./models-recipes/train-evaluate-model-ui.md) tutorial sobre como treinar e avaliar modelos no [!DNL Data Science Workspace].

### Operacionalizar o modelo

Ao selecionar a fórmula mais bem treinada para atender às suas necessidades empresariais, você pode criar um serviço inteligente no [!DNL Data Science Workspace] sem ajuda do desenvolvedor. São apenas alguns cliques - não é necessário codificar. Um serviço inteligente publicado pode ser acessado por outros membros da organização sem a necessidade de recriar o modelo.

Um serviço inteligente publicado pode ser configurado para se treinar automaticamente de tempos em tempos usando novos dados à medida que eles se tornam disponíveis. Isso garante que o serviço mantenha a eficiência e a eficácia com o passar do tempo.

## Próximas etapas

[!DNL Data Science Workspace] O ajuda a simplificar o fluxo de trabalho de ciência de dados, desde a coleta de dados até algoritmos e serviços inteligentes para cientistas de dados de todos os níveis de habilidade. Com as ferramentas sofisticadas [!DNL Data Science Workspace] O fornece, você pode reduzir significativamente o tempo dos dados para os insights.

Mais importante ainda, [!DNL Data Science Workspace] O coloca os recursos de ciência de dados e otimização algorítmica da plataforma de marketing líder Adobe nas mãos dos cientistas de dados corporativos. Pela primeira vez, as empresas podem trazer algoritmos proprietários para a plataforma, aproveitando os poderosos recursos de aprendizado de máquina e IA do Adobe para fornecer experiências do cliente altamente personalizadas em escala maciça.

Com o casamento da experiência em marcas e a capacidade de aprendizagem de máquina e IA da Adobe, as empresas têm o poder de impulsionar mais valor comercial e fidelidade à marca, dando aos clientes o que eles querem, antes que eles peçam.

Para obter informações adicionais, como um fluxo de trabalho diário completo, comece lendo o [Apresentação do Espaço de trabalho de ciência de dados](./walkthrough.md) documentação.

## Recursos adicionais

O vídeo a seguir foi projetado para auxiliar na sua compreensão de [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)