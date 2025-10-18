---
title: Visão geral do Assistente de IA no Adobe Experience Platform
description: Saiba mais sobre o Assistente de IA, suas nuances e casos de uso e como você pode usá-lo para acelerar seu fluxo de trabalho com a Adobe Experience Platform e a Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e90333d09585c8aa0ef176dcfc4717e86364fd54
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 8%

---

# Assistente de IA no Adobe Experience Platform

O vídeo a seguir é destinado a fornecer suporte à sua compreensão do Assistente de IA.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Leia este documento para saber mais sobre o Assistente de IA na Adobe Experience Platform.

O Assistente de IA no Adobe Experience Platform é uma experiência de conversação que você pode usar para acelerar seus fluxos de trabalho em aplicativos do Adobe. Você pode usar o AI Assistant para entender melhor o conhecimento do produto, solucionar problemas ou pesquisar informações e encontrar insights operacionais. O Assistente de IA é compatível com Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

![A interface do Assistente de IA com a primeira experiência de usuário foi acionada.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Você deve concordar com um [contrato de usuário](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) antes de usar o Assistente de IA. O contrato de usuário também contém o contrato público beta. Para que você possa usar os recursos adicionais do Assistente de IA à medida que eles forem implantados na capacidade beta.

+++Selecione para exibir a interface do contrato do usuário

![A primeira página do contrato de usuário.](./images/user-agreement-1.png)

![A última página do contrato de usuário.](./images/user-agreement-2.png)

+++

## Entendendo o assistente de IA {#understanding-ai-assistant}

O Assistente de IA responde às perguntas enviadas consultando um banco de dados e, em seguida, traduzindo os dados do banco de dados em uma resposta legível.

Essa representação interna de dados subjacentes também é conhecida como **[!DNL Knowledge Graph]** - uma Web abrangente de conceitos, dados e metadados para uma determinada resposta.

[!DNL Knowledge Graph] consiste em subgráficos que são referenciados sempre que as consultas são enviadas:

* Insights operacionais do cliente.
* Insights operacionais do cliente em várias meta lojas.
* Documentação do Experience League.

Há duas classes de perguntas a serem consideradas antes de consultar o Assistente de IA:

### Conhecimento do produto {#product-knowledge}

O conhecimento do produto refere-se a conceitos e tópicos fundamentados na documentação do Experience League. As perguntas sobre o conhecimento do produto podem ser especificadas mais detalhadamente nos seguintes subgrupos:

| Conhecimento do produto | Exemplos |
| --- | --- |
| Aprendizado apontado | <ul><li>Qual é a diferença entre uma identidade e uma chave primária ou estrangeira?</li><li>O que são públicos-alvo semelhantes?</li></ul> |
| Abrir descoberta | <ul><li>Como posso exportar esse conjunto de dados?</li><li>Existem esquemas para clientes de assistência médica?</li></ul> |
| Solução de problemas | <ul><li>Por que não posso ativar um esquema de propriedade da Adobe para o perfil?</li><li>Por que não posso excluir um segmento?</li></ul> |

{style="table-layout:auto"}

Assista ao vídeo a seguir para obter informações adicionais sobre o conhecimento do produto do Assistente de IA:

>[!VIDEO](https://video.tv.adobe.com/v/3475935/?captions=por_br&learn=on)

### Insights operacionais {#operational-insights}

Os insights operacionais se referem às respostas que o AI Assistant gera sobre os objetos de metadados (atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes), incluindo contagens, pesquisas e impacto de linhagem. Ele não analisa dados na sandbox.

* Quantos conjuntos de dados eu tenho?
* Quantos atributos de esquema nunca foram usados?
* Quais públicos-alvo foram ativados?

Você pode fazer perguntas ao Assistente de IA sobre seus insights operacionais nos seguintes domínios:

| Domínio | Metadados compatíveis | Metadados incompatíveis |
| --- | --- | --- |
| Atributos | <ul><li>Pesquisa de nome de atributo</li><li>Atributo - relacionamento de esquema</li><li>Relação atributo-conjunto de dados</li><li>Atributo - relacionamento de público</li><li>Relação atributo-destino</li></ul> | <ul><li>Classe de atributo</li><li>Auditoria</li><li>Status de desativação</li><li>Rótulos</li><li>Valor armazenado em atributos</li></ul> |
| Públicos-alvo | <ul><li>Contagem de público-alvo</li><li>Tipo de público-alvo (streaming ou lote)</li><li>Datas de criação/modificação</li><li>Status de ativação</li><li>Contagem de perfis</li><li>Duplicar públicos</li><li>Pesquisa de definição de público</li><li>Público-alvo - relacionamento com o público-alvo</li><li>Público-alvo - relação de atributo</li><li>Público-alvo - relação do conjunto de dados</li><li>Público-alvo - relacionamento de destino</li><li>Pesquisa de nome</li><li>Pesquisa de nome e ID | <ul><li>Sobreposições de público</li><li>Ativação de público-alvo</li><li>Público-alvo - relacionamentos de campanha</li><li>Auditoria</li><li>Criar/modificar</li><li>Rótulos</li><li>Tendências de qualificação de perfil</li></ul> |
| Fluxos de dados | <ul><li>Contagens de fluxo de dados</li><li>Status do fluxo de dados</li><li>Fluxo de dados - relação do conjunto de dados</li><li>Fluxo de dados - relacionamento de origem</li></ul> | <ul><li>Criação/modificação</li><li>Relações fluxo-lote de dados</li><li>Contagem de perfis de assimilação</li></ul> |
| Conjuntos de dados | <ul><li>Contagem do conjunto de dados</li><li>Status de habilitação do perfil</li><li>Data de criação/modificação</li><li>Relação entre conjunto de dados e esquema</li><li>Conjunto de dados - relacionamento de público-alvo</li><li>Conjunto de dados - relação de atributo</li><li>Relação entre conjunto de dados e fluxo de dados</li><li>Pesquisa de nome </li><li>Pesquisa de nome e ID</li></ul> | <ul><li>Auditoria</li><li>Criado por</li><li>Relação entre conjunto de dados e lote</li><li>Criação/modificação do conjunto de dados</li><li>Tamanho do conjunto de dados</li><li>Número de perfis</li><li>Número de linhas</li><li>Pesquisa de valor</li></ul> |
| Destinos | <ul><li>Contagens de destino configuradas</li><li>Relação destino - público</li><li>Relação de atributo de destino</li></ul> | <ul><li>Configuração de conta</li><li>Informações de credencial da conta</li><li>Perfis únicos ativados</li></ul> |
| Jornadas | <ul><li>Contagens</li><li>Pesquisa de nome</li><li>Pesquisa de nome e ID</li><li>Status da jornada</li><li>Status acionado (público-alvo vs. eventos)</li><li>Datas de criação/modificação</li><li>Frequência recorrente</li></ul> | <ul><li>Atributos - Relacionamentos de jornada</li><li>Auditoria</li><li>Criação/modificação</li><li>Criado por</li><li>Eventos</li><li>Jornada - conjunto de dados</li><li>Jornada - esquema</li><li>Ofertas</li><li>Tendências de qualificação de perfil</li><li>Eventos de etapa</li></ul> |
| Esquemas | <ul><li>Contagens de esquema</li><li>Data de criação/modificação</li><li>Esquema - Relação de atributo</li><li>Relação esquema - conjunto de dados</li><li>Esquema - relacionamento de público</li><li>Status de habilitação do perfil</li><li>Pesquisa de nome</li><li>Pesquisa de nome e ID</li></ul> | <ul><li>Auditoria</li><li>Criação/modificação</li><li>Criado por</li><li>Grupos de campos</li><li>Identidades</li><li>Namespaces de identidade</li><li>Rótulos</li><li>Número de perfis</li></ul> |
| Origens | <ul><li>Contagens de conta</li><li>Status da conta</li><li>Fluxos de dados ativos/inativos para cada conta</li><li>Source connector - relação de fluxo de dados</li><li>Relação conta Source - fluxo de dados</li></ul> | <ul><li>Informações de credenciais da conta</li><li>Configuração de conta</li><li>Métricas de assimilação de dados</li><li>Número de perfis</li><li>Source - relacionamentos em lote</li></ul> |

{style="table-layout:auto"}

Para perguntas sobre insights operacionais, as respostas podem não refletir o estado atual da interface do usuário. Os dados que sustentam essas perguntas são atualizados uma vez a cada 24 horas. Por exemplo, as alterações que os usuários fazem no Real-Time CDP durante o dia são sincronizadas com os armazenamentos de dados à noite e, em seguida, ficam disponíveis para perguntas do usuário de manhã. Você precisará fazer logon em uma sandbox para consultar sobre dados específicos relacionados a objetos.

Assista ao vídeo a seguir para obter mais informações sobre os insights operacionais do Assistente de IA:

>[!VIDEO](https://video.tv.adobe.com/v/3444037?learn=on&enablevpops&captions=por_br)

### Escopo do recurso {#feature-scope}

Atualmente, o escopo do Assistente de IA é o seguinte:

* [Conhecimento de produto](./home.md#product-knowledge): o AI Assistant pode responder a perguntas de conhecimento de produto do Experience Platform, Real-Time Customer Data Platform e Adobe Journey Optimizer. Você também pode se aprofundar em tópicos de conhecimento do produto para o Customer Journey Analytics, mas somente por meio da interface do usuário do Customer Journey Analytics.
* [Insights operacionais](./home.md#operational-insights): você pode fazer perguntas ao Assistente de IA sobre insights operacionais nos seguintes objetos de dados: atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes.

## Próximas etapas

Agora que você tem uma compreensão geral do Assistente de IA, pode continuar e usar o Assistente de IA durante seus fluxos de trabalho. Consulte a seguinte documentação para obter mais informações:

* [Guia da interface do assistente de IA](./ui-guide.md)
* [Acesso ao recurso](./access.md)
* [Guia de perguntas](./questions.md)
* [Privacidade, segurança e governança no Assistente de IA](./privacy.md)
* [Perguntas frequentes](./faq.md)
