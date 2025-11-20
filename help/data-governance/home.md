---
keywords: Experience Platform;página inicial;tópicos populares;DULE;dule
solution: Experience Platform
title: Visão geral da governança de dados
description: O Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ela desempenha uma função essencial na Experience Platform em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 9%

---

# Visão geral da governança de dados {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Obrigação de governança de dados"
>abstract="Lembre-se de que é de sua única responsabilidade aderir às políticas de governança de dados da sua organização e atender aos requisitos normativos. A Experience Platform fornece ferramentas de governança de dados para você gerenciar suas obrigações de uso de dados. Aplique os rótulos de uso de dados apropriados antes de consultar ou processar dados. Consulte a documentação para saber mais sobre as ferramentas de governança de dados e as práticas recomendadas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR" text="Visão geral da governança de dados"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=pt-BR" text="Visão geral dos rótulos de governança de dados"

Um dos principais recursos do Adobe Experience Platform é reunir dados de vários sistemas corporativos para permitir que os profissionais de marketing identifiquem, compreendam e envolvam os clientes de maneira mais eficiente. Esses dados podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais. Portanto, é importante garantir que suas operações de dados no [!DNL Experience Platform] estejam em conformidade com as políticas de uso de dados.

Gerencie os dados do cliente e garanta a conformidade com as regulamentações, as restrições e as políticas aplicáveis ao uso de dados com o Adobe Experience Platform Data Governance. A governança de dados desempenha um papel fundamental no Experience Platform em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.

>[!NOTE]
>
>No Experience Platform, a governança de dados só se preocupa com a forma como os dados são usados ou ativados, independentemente do usuário que está executando a ação. Para obter informações sobre como controlar o acesso a campos de dados específicos para determinados usuários do Experience Platform em sua organização, consulte a documentação em [controle de acesso baseado em atributo](../access-control/abac/overview.md).

## Funções de governança de dados {#data-governance-roles}

Como conceito, o controle de dados não é automático nem ocorre no vácuo. O que começou como uma função para um indivíduo, normalmente reconhecido como um administrador de dados, cresceu consideravelmente à medida que o ecossistema de governança de dados se expandiu. Atualmente, o controle de dados requer gerenciamento e monitoramento contínuos para ser bem-sucedido. A governança de dados eficaz depende de administradores de dados que tenham ferramentas com as quais os dados possam ser rotulados corretamente, políticas de uso possam ser criadas e a conformidade com essas políticas possa ser imposta.

Embora a governança de dados deva ser responsabilidade de cada indivíduo na organização, estas são algumas das funções essenciais no ciclo de governança de dados:

![Gráfico para transmitir as quatro funções de governança de dados, com aspas sobre as obrigações de cada função.](./images/overview/roles.png)

### Administrador de dados {#data-steward}

Os administradores de dados são o coração da governança de dados. Essa função é responsável por interpretar regulamentos, restrições contratuais e políticas e aplicá-las diretamente aos dados. Informado por sua compreensão dessas regulamentações, restrições e políticas, o papel de um administrador de dados inclui:

* Revisão de dados, conjuntos de dados e amostras de dados para aplicar e gerenciar a rotulagem de uso de metadados.
* Criação de políticas de dados e sua aplicação a conjuntos de dados e campos.
* Comunicar políticas de dados à organização.

### Profissional de marketing {#marketer}

Os profissionais de marketing são o ponto final da governança de dados. Eles solicitam dados da infraestrutura de governança de dados criada por administradores de dados, cientistas e engenheiros. Os profissionais de marketing englobam várias especialidades diferentes sob a égide do marketing, incluindo as seguintes:

* Os analistas de marketing solicitam dados para permitir a compreensão de clientes, tanto como indivíduos quanto em grupos (também conhecidos como segmentos).
* Os especialistas em marketing e os designers de experiência usam os dados para projetar novas experiências do cliente.

## Estrutura de governança de dados {#data-governance-framework}

A estrutura de governança de dados simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados. Depois que os rótulos de dados forem aplicados e as políticas de uso de dados forem implementadas, as ações de marketing poderão ser avaliadas para garantir o uso correto dos dados.

Há três elementos-chave na estrutura de governança de dados: rótulos, políticas e aplicação.

1. **Rótulos:** classifique os dados que refletem considerações relacionadas à privacidade e às condições contratuais para estar em conformidade com os regulamentos e as políticas da organização.
1. **Políticas:** descreva quais tipos de ações de marketing são permitidas ou não em dados específicos.
1. **Imposição:** usa a estrutura de política para aconselhar e impor políticas em diferentes padrões de acesso a dados.

## Rótulos de uso de dados {#data-usage-labels}

A Governança de dados permite que os administradores de dados apliquem rótulos de uso no nível do campo de esquema para categorizar os dados de acordo com o tipo de políticas aplicáveis.

A estrutura de Governança de dados inclui rótulos de uso de dados predefinidos que podem ser usados para categorizar dados de três maneiras:

![As três categorias de rótulo de uso de dados.](./images/overview/label-categories.png)

* **Rótulos de Dados do Contrato &quot;C&quot;:** Rotule e categorize dados que tenham obrigações contratuais ou estejam relacionados às políticas de governança de dados do cliente.
* **Rótulos de Dados &quot;I&quot; de Identidade:** Rotule e categorize dados que podem identificar ou contatar uma pessoa específica.
* **Rótulos de Dados &quot;S&quot; Confidenciais:** Rotule e categorize dados relacionados a dados confidenciais, como dados geográficos.

>[!NOTE]
>
>Consulte o guia em [rótulos de uso de dados com suporte](labels/reference.md) para obter uma lista completa de rótulos disponíveis e definições para cada tipo de rótulo.

Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. A prática recomendada incentiva a rotulagem de dados quando eles são assimilados na Experience Platform ou assim que os dados são disponibilizados em [!DNL Experience Platform].

Consulte a visão geral em [rótulos de uso de dados](./labels/overview.md) para obter mais informações sobre como os rótulos de uso de dados são usados para ajudar a impor a conformidade com a governança de dados.

## Políticas de uso de dados {#data-usage-policies}

Para que os rótulos de uso de dados estejam de acordo com a conformidade de dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados dentro do Experience Platform.

Um exemplo de ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor declarando que as Informações de identificação pessoal (PII) não podem ser exportadas e um rótulo &quot;I&quot; (dados de identidade) foi aplicado ao nível do campo de seu esquema. O Serviço de política impede qualquer ação que exporte esse conjunto de dados para um destino de terceiros. Se uma dessas tentativas ocorrer, o Serviço de política envia uma mensagem informando que uma política de uso de dados foi violada.


Há dois tipos de políticas disponíveis:

* **[!UICONTROL Data governance policy]**: Restrinja a ativação de dados com base na ação de marketing que está sendo executada e nos rótulos de uso de dados transportados pelos dados em questão.
* **[!UICONTROL Consent policy]**: filtre os perfis que podem ser ativados para [destinos](../destinations/home.md) com base no consentimento ou nas preferências dos clientes.

Depois que os rótulos de uso de dados forem aplicados, os administradores de dados poderão criar políticas usando a API de serviço de política ou a interface do usuário do Experience Platform. Para obter mais informações sobre políticas de uso de dados e ações de marketing, consulte a [visão geral das políticas](./policies/overview.md).

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, você deve ativar manualmente essa política.

## Próximas etapas

Este documento forneceu uma introdução de alto nível à Governança de dados e à estrutura de Governança de dados. Agora você pode continuar com o [guia do usuário de rótulos de uso de dados](labels/user-guide.md) e começar a adicionar rótulos de uso aos seus dados de experiência.

## Apêndice

A seção a seguir fornece informações adicionais sobre a governança de dados.

### Terminologia de governança de dados {#data-governance-terminology}

A tabela a seguir descreve os termos principais relacionados à Governança de dados e à Estrutura de governança de dados.

| Termo | Definição |
|---|---|
| **Rótulos de contrato** | Os rótulos de contrato (C) são usados para categorizar dados que contêm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização. |
| **Dados entre sites** | Os dados entre sites são a combinação de dados de vários sites. Os dados entre sites incluem dados locais e externos ou uma combinação de dados de várias fontes externas. |
| **Governança de dados** | A governança de dados abrange as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com as regulamentações e as políticas corporativas em relação ao uso de dados. |
| **Administrador de dados** | O administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de governança de dados sejam protegidas e mantidas para estar em conformidade com as regulamentações governamentais e as políticas da organização. |
| **Rótulos de uso de dados** | Os rótulos de uso de dados oferecem aos usuários a capacidade de categorizar dados que refletem considerações relacionadas à privacidade e às condições contratuais para estar em conformidade com os regulamentos e as políticas corporativas. |
| **Rótulos do conjunto de dados** | Rótulos podem ser adicionados a um esquema. Todos os campos em um conjunto de dados herdam os rótulos do esquema. |
| **Rótulos de campos** | Os rótulos de campo são rótulos de governança de dados herdados de um esquema ou aplicados diretamente a um campo. Os rótulos de governança de dados aplicados a um campo não são herdados até o nível do esquema. |
| **Geofence** | Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software acione uma resposta quando um dispositivo móvel entra ou sai de uma área específica. |
| **Rótulos de identidade** | Os rótulos “I” de identidade são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica. |
| **Direcionamento baseado em interesses** | O direcionamento baseado em interesses, também conhecido como personalização, ocorrerá se as três condições a seguir forem atendidas:<br>Os dados coletados no site são,<br><ul><li>Usado para deduzir sobre o interesse de um usuário,</li><li>Usado em outro contexto, como em outro site ou aplicativo (fora do site)</li><li>Usado para selecionar qual conteúdo ou quais anúncios são veiculados com base nessas inferências.</li></ul> |
| **Ação de marketing** | Uma ação de marketing, no contexto da estrutura de governança de dados, é uma ação que um consumidor de dados do Experience Platform toma, para a qual é necessário verificar violações das políticas de uso de dados |
| **Política** | Na estrutura de governança de dados, uma política é uma regra que descreve quais tipos de ações de marketing são permitidas ou não em dados específicos. |
| **Rótulos de esquema** | Gerencie os rótulos para governança de dados, consentimento e controle de acesso no nível do esquema. Isso propaga os rótulos para cada conjunto de dados que usa esse esquema. |
| **Rótulos sensíveis** | Os rótulos de sensibilidade (S) são usados para categorizar dados que você e sua organização consideram sensíveis. |

## Recursos adicionais

O vídeo a seguir é destinado a apoiar a sua compreensão da estrutura de governança de dados.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

O vídeo a seguir fornece orientação sobre como aplicar rótulos de uso de dados aos seus esquemas ou à totalidade de um conjunto de dados na Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
