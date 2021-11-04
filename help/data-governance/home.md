---
keywords: Experience Platform, home, tópicos populares, DULE, dule
solution: Experience Platform
title: Visão geral da governança de dados
topic-legacy: overview
description: A Governança de dados do Adobe Experience Platform permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função essencial no Experience Platform em vários níveis, incluindo catálogos, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Visão geral da governança de dados

Um dos principais recursos do Adobe Experience Platform é unir dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, entendam e envolvam clientes. Esses dados podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais. Portanto, é importante garantir que suas operações de dados no [!DNL Platform] são compatíveis com as políticas de uso de dados.

A Governança de dados do Adobe Experience Platform permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.

## Funções de governança de dados

Como conceito, a governança de dados não é automática, nem ocorre no vácuo. O que começou como uma função para um indivíduo, normalmente reconhecido como um administrador de dados, cresceu consideravelmente à medida que o ecossistema de governança de dados se expandia. Atualmente, a governança de dados exige gerenciamento e monitoramento contínuos para ter sucesso e depende de gerentes de dados terem ferramentas com as quais os dados podem ser rotulados corretamente, políticas de uso podem ser criadas e a conformidade com essas políticas pode ser imposta.

Embora a governança de dados deva ser da responsabilidade de cada indivíduo na organização, aqui estão algumas das funções essenciais no ciclo de governança de dados:

![Funções de governança de dados](./images/overview/roles.png)

### Data steward

Os Data Stewards são o coração do controle de dados. Essa função é responsável por interpretar regulamentos, restrições contratuais e políticas, e aplicá-los diretamente aos dados. Informado pela compreensão desses regulamentos, restrições e políticas, a função de um administrador de dados inclui:

* Revisar dados, conjuntos de dados e amostras de dados para aplicar e gerenciar a rotulagem de uso de metadados.
* Criar políticas de dados e aplicá-las a conjuntos de dados e campos.
* Comunicação das políticas de dados à organização.

### Profissional de marketing

Os profissionais de marketing são o ponto final do controle de dados. Eles solicitam dados da infraestrutura de governança de dados criada por gerentes de dados, cientistas e engenheiros. Os profissionais de marketing incluem várias especialidades diferentes sob o guarda-chuva de marketing, incluindo as seguintes:

* Os analistas de marketing solicitam dados para permitir a compreensão dos clientes, como indivíduos e em grupos (também conhecidos como segmentos).
* Especialistas em marketing e designers de experiência usam dados para projetar novas experiências do cliente.


## Estrutura de governança de dados

A estrutura de Governança de dados simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados. Depois que os rótulos de dados tiverem sido aplicados e as políticas de uso de dados estiverem em vigor, as ações de marketing poderão ser avaliadas para garantir o uso correto dos dados.

Há três elementos principais para a estrutura de Governança de dados: Rótulos, políticas e aplicação.

1. **Rótulos:** Classifique dados que refletem considerações relacionadas à privacidade e às condições contratuais para manter a conformidade com as regulamentações e as políticas da organização.
1. **Políticas:** Descreva o(s) tipo(s) de ações de marketing que podem ou não ser realizadas em dados específicos.
1. **Execução:** Usa a estrutura de política para aconselhar e aplicar políticas em diferentes padrões de acesso a dados.

## Rótulos de uso de dados

A Governança de dados permite que os assistentes de dados apliquem rótulos de uso no conjunto de dados e no nível do campo para categorizar dados de acordo com o tipo de políticas aplicáveis.

A estrutura de Governança de dados inclui rótulos de uso de dados predefinidos que podem ser usados para categorizar os dados de três formas:

![Categorias de rótulos de uso de dados](./images/overview/label-categories.png)

* **Rótulos de dados &quot;C&quot; do contrato:** Rotule e categorize os dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados do cliente.
* **Rótulos de dados de identidade &quot;I&quot;:** Rotule e categorize os dados que podem identificar ou entrar em contato com uma pessoa específica.
* **Rótulos de dados &quot;S&quot; sensíveis:** Rotular e categorizar dados relacionados a dados confidenciais, como dados geográficos.

>[!NOTE]
>
>Consulte o guia sobre [rótulos de uso de dados suportados](labels/reference.md) para obter uma lista completa de rótulos disponíveis, bem como as definições para cada tipo de rótulo.

Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que são assimilados em [!DNL Experience Platform]ou assim que os dados forem disponibilizados em [!DNL Platform].

Consulte a visão geral em [rótulos de uso de dados](./labels/overview.md) para obter mais informações.

## Políticas de uso de dados

Para que os rótulos de uso de dados sejam compatíveis com a conformidade dos dados, é necessário implementar políticas de uso de dados. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing das quais você tem permissão para ou tem restrição para executar em dados dentro de [!DNL Experience Platform].

Um exemplo de uma ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor informando que tipos específicos de dados, como Informações pessoais identificáveis (PII), não podem ser exportados e um rótulo &quot;I&quot; (Dados de identidade) tiver sido aplicado ao conjunto de dados, você receberá uma resposta do [!DNL Policy Service] informando que uma política de uso de dados foi violada.

Depois que os rótulos de uso de dados forem aplicados, os assistentes de dados poderão criar políticas usando o [!DNL Policy Service] API ou [!DNL Experience Platform] interface do usuário.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, é necessário habilitar manualmente essa política.

Para obter mais informações sobre políticas de uso de dados e ações de marketing, consulte o [visão geral das políticas](./policies/overview.md).

## Próximas etapas

Este documento forneceu uma introdução de alto nível à Governança de dados e à estrutura de Governança de dados. Agora você pode continuar com o [guia do usuário de rótulos de uso de dados](labels/user-guide.md) e comece a adicionar rótulos de uso aos seus dados de experiência.

## Apêndice

A seção a seguir fornece informações adicionais sobre a Governança de dados.

### Terminologia da Governança de dados

A tabela a seguir descreve os principais termos relacionados à Governança de dados e à estrutura de Governança de dados.

| Termo | Definição |
|---|---|
| **Rótulos do contrato** | Os rótulos &quot;C&quot; do contrato são usados para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização. |
| **Dados entre sites** | Dados entre sites é a combinação de dados de vários sites, incluindo uma combinação de dados no site e dados fora do site ou uma combinação de dados de várias fontes fora do site. |
| **Governança de dados** | O controle de dados abrange as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com os regulamentos e as políticas corporativas em relação ao uso de dados. |
| **Data steward** | O administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação efetiva dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de governança de dados sejam salvaguardadas e mantidas para serem compatíveis com os regulamentos governamentais e as políticas de organização. |
| **Rótulos de uso de dados** | Os rótulos de uso de dados oferecem aos usuários a capacidade de categorizar dados que refletem considerações relacionadas à privacidade e às condições contratuais para manter a conformidade com os regulamentos e as políticas corporativas. |
| **Rótulos do conjunto de dados** | Rótulos podem ser adicionados a um conjunto de dados. Todos os campos em um conjunto de dados herdam os rótulos do conjunto de dados. |
| **Rótulos de campos** | Os rótulos de campo são rótulos de governança de dados que são herdados de um conjunto de dados ou aplicados diretamente a um campo.  Os rótulos de governança de dados aplicados a um campo não são herdados de um conjunto de dados. |
| **Geofence** | Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software acione uma resposta quando um dispositivo móvel entra ou sai de uma área específica. |
| **Rótulos de identidade** | Os rótulos de identidade &quot;I&quot; são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica. |
| **Direcionamento baseado em interesses** | O direcionamento baseado em juros, também conhecido como personalização, ocorre se as três condições a seguir forem atendidas: os dados coletados no site são, usados para fazer inferências sobre o interesse dos usuários, são usados em outro contexto, como em outro site ou aplicativo (fora do site) e são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências. |
| **Ação de marketing** | Uma ação de marketing, no contexto da estrutura de governança de dados, é uma ação que [!DNL Experience Platform] dados que o consumidor usa, para os quais é necessário verificar violações das políticas de uso de dados |
| **Política** | Na estrutura de governança de dados, uma política é uma regra que descreve o tipo de ações de marketing que podem ou não ser executadas em dados específicos. |
| **Rótulos sensíveis** | Os rótulos &quot;S&quot; confidenciais são usados para categorizar dados que você e sua organização consideram confidenciais. |

## Recursos adicionais

O vídeo a seguir destina-se a auxiliar na compreensão da estrutura de Governança de dados.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

O vídeo a seguir apresenta uma introdução a vários recursos de Governança de dados no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
