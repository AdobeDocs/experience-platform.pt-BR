---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Controle de dados de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---


# Visão geral do controle de dados

Um dos principais recursos do Adobe Experience Platform é reunir dados de vários sistemas corporativos para melhor permitir que os profissionais de marketing identifiquem, entendam e engajem os clientes. Esses dados podem estar sujeitos a restrições de uso definidas pela sua organização ou por regulamentos legais. Portanto, é importante garantir que suas operações de dados dentro [!DNL Platform] estejam em conformidade com as políticas de uso de dados.

O controle de dados do Adobe Experience Platform permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo a catalogação, a linhagem de dados, a rotulagem de uso de dados, as políticas de uso de dados e o controle do uso de dados para ações de marketing.

## Funções de controle de dados

Como conceito, o controle de dados não é automático nem ocorre no vácuo. O que começou como uma função para um indivíduo, tipicamente reconhecido como um **administrador** de dados, cresceu consideravelmente à medida que o ecossistema de controle de dados se expandia. Atualmente, o controle de dados exige gerenciamento e monitoramento contínuos para ter sucesso e depende de os administradores de dados terem ferramentas com as quais os dados podem ser rotulados corretamente, políticas de uso podem ser criadas e a conformidade com essas políticas pode ser imposta.

Embora o controle de dados deva ser da responsabilidade de cada indivíduo na organização, aqui estão algumas das funções essenciais dentro do ciclo de gerenciamento de dados:

![Funções de controle de dados](./images/overview/roles.png)

### Gerente de dados

Os gerentes de dados são o coração da governança de dados. Esta função é responsável pela interpretação de regulamentos, restrições contratuais e políticas, e pela sua aplicação direta aos dados. Informado pelo entendimento desses regulamentos, restrições e políticas, a função de um administrador de dados inclui:

* Revisando dados, conjuntos de dados e amostras de dados para aplicar e gerenciar a rotulagem de uso de metadados.
* Criar políticas de dados e aplicá-las a conjuntos de dados e campos.
* Comunicação de políticas de dados à organização.

### Comercializador

Os profissionais de marketing são o ponto final do controle de dados. Eles solicitam dados da infraestrutura de controle de dados criada por gerentes de dados, cientistas e engenheiros. Os profissionais de marketing incluem várias especialidades diferentes sob a sua guarda-chuva de marketing, incluindo as seguintes:

* Os analistas de marketing solicitam dados para permitir a compreensão dos clientes, tanto como indivíduos como em grupos (também conhecidos como segmentos).
* Especialistas em marketing e designers de experiência usam dados para projetar novas experiências do cliente.


## Estrutura DULE

A DULE (Data Usage Labeling and Implementation) é a estrutura principal para o [!DNL Experience Platform] Data Governance. DULE simplifica e simplifica o processo de categorização de dados e criação de políticas de uso de dados. Depois que os rótulos de dados forem aplicados e as políticas de uso de dados estiverem em vigor, as ações de marketing poderão ser avaliadas para garantir o uso correto dos dados.

Há três elementos chave na estrutura DULE: Etiquetas, políticas e aplicação.

1. **Etiquetas:** Classifique os dados que refletem considerações relacionadas à privacidade e condições contratuais para serem compatíveis com regulamentos e políticas da organização.
1. **Políticas:** Descreva que tipo(s) de ações de marketing são permitidas ou não podem ser realizadas em dados específicos.
1. **Execução:** Usa a estrutura de política para aconselhar e aplicar políticas em diferentes padrões de acesso a dados.

## Rótulos de uso de dados

O controle de dados permite que os administradores de dados apliquem rótulos de uso no nível do conjunto de dados e do campo para classificar dados de acordo com o tipo de políticas que se aplicam.

A estrutura DULE inclui rótulos de uso de dados predefinidos que podem ser usados para classificar dados de três formas:

![Categorias de etiquetas de uso de dados](./images/overview/label-categories.png)

* **Rótulos de dados do contrato &quot;C&quot;:** Rotule e categorize os dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados do cliente.
* **Rótulos de dados de identidade &quot;I&quot;:** Rotule e categorize os dados que podem identificar ou entrar em contato com uma pessoa específica.
* **Rótulos de dados &quot;S&quot; sensíveis:** Rótulo e categorizar dados relacionados a dados confidenciais, como dados geográficos.

>[!NOTE]
>
>Consulte o guia nos rótulos [de uso de dados](labels/reference.md) suportados para obter uma lista completa dos rótulos disponíveis, bem como as definições para cada tipo de etiqueta.

As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas encorajam a rotulação de dados assim que eles são ingeridos [!DNL Experience Platform], ou assim que os dados estiverem disponíveis em [!DNL Platform].

Consulte a visão geral sobre rótulos [de uso de](./labels/overview.md) dados para obter mais informações.

## Políticas de uso de dados

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro de [!DNL Experience Platform].

Um exemplo de uma ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor dizendo que tipos específicos de dados, como Informações pessoais identificáveis (PII), não podem ser exportados e um rótulo &quot;I&quot; (Dados de identidade) tiver sido aplicado ao conjunto de dados, você receberá uma resposta do Serviço de política informando que uma política de uso de dados foi violada.

Depois que os rótulos de uso de dados forem aplicados, os administradores de dados poderão criar políticas usando a API do serviço de política DULE ou a interface do [!DNL Experience Platform] usuário.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as principais políticas fornecidas pela Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente.

Para obter mais informações sobre políticas de uso de dados e ações de marketing, consulte a visão geral [das](./policies/overview.md)políticas.

## Versões futuras

Atualmente, o Data Governance oferece suporte à rotulagem DULE em dois níveis (conjunto de dados e campo). O Data Governance também suporta a criação e o gerenciamento de políticas de uso de dados e ações de marketing por meio da DULE Policy Service API.

As versões subsequentes fornecerão os seguintes recursos:

* Rótulos de uso de dados personalizados: Crie novos rótulos e definições com base nas necessidades de sua organização.
* Aplicação da política: Use a estrutura de política para aconselhar e aplicar políticas em diferentes padrões de acesso a dados.
* Auditoria: Monitore atividades de acesso aos dados e identifique e reporte problemas de conformidade.

## Próximas etapas

Este documento forneceu uma introdução de alto nível ao Data Governance e à estrutura DULE. Agora, você pode continuar com o guia [do usuário dos rótulos de uso de](labels/user-guide.md) dados e adicionar os rótulos de uso aos dados da experiência.

## Apêndice

A seção a seguir fornece informações adicionais sobre o Data Governance.

### Terminologia do Data Governance

A tabela a seguir descreve os termos principais relacionados à Data Governance e à estrutura DULE.

| Termo | Definição |
|---|---|
| **Rótulos do contrato** | As etiquetas &quot;C&quot; do contrato são usadas para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados de sua organização. |
| **Dados entre sites** | Os dados entre sites são a combinação de dados de vários sites, incluindo uma combinação de dados no site e fora dele ou uma combinação de dados de várias fontes fora do site. |
| **Governação de dados** | O controle de dados engloba as estratégias e tecnologias usadas para garantir que os dados estejam em conformidade com os regulamentos e as políticas corporativas em relação ao uso de dados. |
| **Gerente de dados** | O administrador de dados é a pessoa responsável pelo gerenciamento, supervisão e aplicação efetiva dos ativos de dados de uma organização. Um administrador de dados também garante que as políticas de controle de dados sejam salvaguardadas e mantidas para serem compatíveis com os regulamentos governamentais e as políticas de organização. |
| **Rótulos de uso de dados** | As etiquetas de uso de dados fornecem aos usuários a capacidade de categorizar dados que refletem considerações relacionadas à privacidade e condições contratuais para serem compatíveis com regulamentos e políticas corporativas. |
| **Rótulos de conjuntos de dados** | Rótulos podem ser adicionados a um conjunto de dados. Todos os campos em um conjunto de dados herdam os rótulos do conjunto de dados. |
| **MÓDULO** | DULE é um acrônimo para &quot;Rotulação e aplicação do uso de dados&quot;. Parte essencial do gerenciamento de dados, DULE é uma coleção de recursos que permite a rotulagem do uso de dados e a aplicação de políticas de acesso a dados para as necessidades de governança em uma organização. |
| **Rótulos de campos** | Rótulos de campo são rótulos de controle de dados herdados de um conjunto de dados ou aplicados diretamente a um campo.  Os rótulos de controle de dados aplicados a um campo não são herdados até um conjunto de dados. |
| **Geofence** | Uma geofence é um limite geográfico virtual, definido pela tecnologia GPS ou RFID, que permite que o software dispare uma resposta quando um dispositivo móvel entra ou sai de uma área específica. |
| **Rótulos de identidade** | Os rótulos &quot;I&quot; de identidade são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica. |
| **Direcionamento baseado em interesse** | A definição de metas baseada em juros, também conhecida como personalização, ocorre se as três condições a seguir forem atendidas: os dados coletados no site são, usados para fazer inferências sobre o interesse de um usuário, são usados em outro contexto, como em outro site ou aplicativo (fora do site) e são usados para selecionar qual conteúdo ou anúncios são fornecidos com base nessas inferências. |
| **Ação de marketing** | Uma ação de marketing, no contexto da estrutura de controle de dados, é uma ação que um consumidor de [!DNL Experience Platform] dados toma, para a qual há necessidade de verificar violações das políticas de uso de dados |
| **Política** | Na estrutura de gerenciamento de dados, uma política é uma regra que descreve que tipo de ações de marketing são permitidas ou não para serem tomadas em dados específicos. |
| **Rótulos sensíveis** | As etiquetas &quot;S&quot; sensíveis são usadas para categorizar dados que você e sua organização consideram confidenciais. |

## Recursos adicionais

O vídeo a seguir tem como objetivo dar suporte à compreensão sobre o controle de dados e descreve os principais aspectos da estrutura DULE (Data Usage Labeling and Implementation).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
