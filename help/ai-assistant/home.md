---
title: Visão geral do Assistente de IA no Adobe Experience Platform
description: Saiba mais sobre o AI Assistant, suas nuances e casos de uso e como você pode usá-lo para acelerar seu fluxo de trabalho com o Adobe Experience Platform e o Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: b51291e6c3663c6d6e6d416f0d2c37563c852155
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# Assistente de IA no Adobe Experience Platform

Leia este documento para saber mais sobre o Assistente de IA na Adobe Experience Platform.

O Assistente de IA no Adobe Experience Platform é uma experiência de conversação que você pode usar para acelerar seus fluxos de trabalho em aplicativos Adobe. Você pode usar o AI Assistant para entender melhor o conhecimento do produto, solucionar problemas ou pesquisar informações e encontrar insights operacionais. O Assistente de IA é compatível com Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

![A interface do Assistente de IA com a experiência do usuário acionada pela primeira vez.](./images/blank.png)

>[!IMPORTANT]
>
>Você deve concordar com um [contrato do usuário](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) antes de usar o Assistente de IA. O contrato de usuário também contém o contrato público beta. Para que você possa usar os recursos adicionais do Assistente de IA à medida que eles forem implantados na capacidade beta.

+++Selecione para exibir a interface do contrato do usuário

![A primeira página do contrato de usuário.](./images/user-agreement-1.png)

![A última página do contrato de usuário.](./images/user-agreement-2.png)

+++

## Entendendo o assistente de IA {#understanding-ai-assistant}

O Assistente de IA responde às perguntas enviadas consultando um banco de dados e, em seguida, traduzindo os dados do banco de dados em uma resposta legível.

Essa representação interna de dados subjacentes também é conhecida como **[!DNL Knowledge Graph]** - uma ampla rede de conceitos, dados e metadados para uma determinada resposta.

A variável [!DNL Knowledge Graph] consiste em subgráficos que são referenciados sempre que as consultas são enviadas:

* Insights operacionais do cliente.
* Insights operacionais do cliente em várias meta lojas.
* Documentação do Experience League.

Há duas classes de perguntas a serem consideradas antes de consultar o Assistente de IA:

### Conhecimento do produto {#product-knowledge}

O conhecimento do produto refere-se aos conceitos e tópicos baseados na documentação do Experience League. As perguntas sobre o conhecimento do produto podem ser especificadas mais detalhadamente nos seguintes subgrupos:

| Conhecimento do produto | Exemplos |
| --- | --- |
| Aprendizado apontado | <ul><li>Qual é a diferença entre uma identidade e uma chave primária ou estrangeira?</li><li>Como a riqueza do perfil é calculada?</li></ul> |
| Abrir descoberta | <ul><li>Como posso exportar esse conjunto de dados?</li><li>Existem esquemas para clientes de assistência médica?</li></ul> |
| Solução de problemas | <ul><li>Por que não posso ativar um esquema de propriedade do Adobe para perfil?</li><li>Por que não posso excluir um segmento?</li></ul> |

{style="table-layout:auto"}

### Insights operacionais {#operational-insights}

>[!IMPORTANT]
>
>As respostas dos insights operacionais estão na versão beta. Qualquer pessoa que tenha acesso à **Exibir Insights Operacionais** A permissão do terá acesso às respostas dos insights operacionais.

Os insights operacionais se referem às respostas que o AI Assistant gera sobre os objetos de metadados (atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes), incluindo contagens, pesquisas e impacto de linhagem. Ele não analisa dados na sandbox.

* Quantos conjuntos de dados eu tenho?
* Quantos atributos de esquema nunca foram usados?
* Quais públicos-alvo foram ativados?

Você pode fazer perguntas ao Assistente de IA sobre seus insights operacionais nos seguintes domínios:

* Atributos
* Públicos-alvo
* Fluxos de dados
* Conjuntos de dados
* Destinos _(Perguntas sobre contas e algumas perguntas sobre fluxo de dados não podem ser respondidas no momento.)_
* Jornadas
* Esquemas _(Perguntas relacionadas a grupos de campos não podem ser respondidas neste momento.)_
* Origens _(Perguntas relacionadas a contas não podem ser respondidas neste momento.)_

Para perguntas sobre insights operacionais, as respostas podem não refletir o estado atual da interface do usuário. Os dados que sustentam essas perguntas são atualizados uma vez a cada 24 horas. Por exemplo, as alterações que os usuários fazem no Real-Time CDP durante o dia são sincronizadas com os armazenamentos de dados à noite e, em seguida, ficam disponíveis para perguntas do usuário de manhã. Você precisará fazer logon em uma sandbox para consultar sobre dados específicos relacionados a objetos.

### Escopo do recurso {#feature-scope}

Atualmente, o escopo do Assistente de IA é o seguinte:

* [Conhecimento do produto](./home.md#product-knowledge): O Assistente de IA pode responder a perguntas de conhecimento de produto do Experience Platform, Real-time Customer Data Platform e Adobe Journey Optimizer. Você também pode se aprofundar em tópicos de conhecimento sobre produtos para o Customer Journey Analytics, mas somente por meio da interface do usuário do Customer Journey Analytics.
* [Insights operacionais](./home.md#operational-insights): Você pode fazer perguntas ao Assistente de IA sobre insights operacionais nos seguintes objetos de dados: atributos, públicos-alvo, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes.

## Próximas etapas

Agora que você tem uma compreensão geral do Assistente de IA, pode continuar e usar o Assistente de IA durante seus fluxos de trabalho. Consulte a seguinte documentação para obter mais informações:

* [Guia da interface do assistente de IA](./ui-guide.md)
* [Acesso ao recurso](./access.md)
* [Guia de perguntas](./questions.md)
* [Privacidade, segurança e governança no Assistente de IA](./privacy.md)
* [Perguntas frequentes](./faq.md)
