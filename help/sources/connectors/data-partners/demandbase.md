---
title: Intenção do Demandbase
description: Saiba mais sobre a fonte de intenção do Demandbase no Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: e223ea754a250956e65c3f526119a3ebd7bb067c
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] é uma plataforma de marketing baseada em conta que você pode usar para vendas B2B e sucesso de marketing. O [!DNL Demandbase Intent] é uma fonte do Adobe Experience Platform que você pode usar para conectar sua conta do [!DNL Demandbase] à Experience Platform e integrar seus dados de intenção de conta.

Com a origem [!DNL Demandbase], é possível identificar contas de alto interesse com base em compromissos em tempo real. Ao priorizar os sinais de intenção mais fortes, você pode criar segmentos precisos e fornecer campanhas hiperdirecionadas, garantindo que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão. A ativação de estratégias orientadas por intenção permite a otimização de gastos com anúncios, maior engajamento e maior ROI.

Leia este documento para obter as informações de pré-requisito sobre a origem [!DNL Demandbase].

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter as etapas de pré-requisito antes de conectar [!DNL Demandbase] ao Experience Platform.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP

Uma lista de endereços IP deve ser adicionada a um incluo na lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região ao incluo na lista de permissões pode levar a erros ou não desempenho ao usar origens. Consulte a página [incluo na lista de permissões de endereços IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL View Sources]** e **[!UICONTROL Manage Sources]** habilitadas para sua conta para conectar sua conta do [!DNL Demandbase] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

### Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

* Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
* Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
* Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
* Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
* Caracteres de caminho de URL inválidos não são permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

### Coletar credenciais necessárias

[!DNL Demandbase] no Experience Platform está hospedado por [!DNL Google Cloud Storage]. Para autenticar com êxito sua conta do [!DNL Demandbase], você deve fornecer os valores apropriados para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| ID da chave de acesso | A ID da chave de acesso [!DNL Demandbase]. Esta é uma sequência de 61 caracteres alfanuméricos necessária para autenticar sua conta no Experience Platform. |
| Chave de acesso secreta | A chave de acesso secreta [!DNL Demandbase]. Esta é uma sequência de 40 caracteres codificada em base 64 necessária para autenticar sua conta no Experience Platform. |
| Nome do bucket | O bucket [!DNL Demandbase] do qual os dados serão extraídos. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. |

Para obter mais informações sobre essas credenciais, leia o [[!DNL Google Cloud Storage] guia de chaves HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria chave de acesso, leia o [guia de pré-requisito na [!DNL Google Cloud Storage] visão geral da origem](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Esquema [!DNL Demandbase]

>[!IMPORTANT]
>
>Ao criar um esquema de Intenção de conta B2B do Demandbase na interface do usuário do Experience Platform, ative a Assimilação de perfil para o esquema. Para obter mais informações, leia o manual sobre [criação e edição de esquemas na interface](../../../xdm/ui/resources/schemas.md).

Leia esta seção para obter informações sobre o esquema [!DNL Demandbase] e a estrutura de dados.

O esquema [!DNL Demandbase] é chamado **Intenção da conta do Demandbase B2B**. São as informações de intenção semanal (pesquisa de comprador B2B anônimo e consumo de conteúdo) em uma conta e palavras-chave especificadas. Os dados estão em formato parquet.

* Classe - XDM [!DNL Demandbase Account Intent]
* Namespace - B2B [!DNL Demandbase Account Intent]
* Identidade principal - `intentID`
* Relacionamentos - Conta B2B

| Nome do campo | Tipo de dados | Descrição |
|--------------------------|-----------|-------------------------------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJETO | Este campo contém informações de auditoria do sistema da fonte externa. |
| `_id` | STRING | É o identificador de sistema exclusivo do registro. |
| `accountDomain` | STRING | Esse campo contém o domínio da conta. |
| `accountID` | STRING | É a ID da conta B2B à qual esse registro de intenção está associado. |
| `demandbaseAccountID` | STRING | Esta é a ID da empresa em [!DNL Demandbase]. |
| `durationType` | STRING | Esse campo especifica o tipo de período de validade da intenção, por exemplo, &quot;semana&quot;. |
| `endDate` | DATA | Esta é a data final do período de validade da intenção. |
| `intentID` | STRING | Este é um valor exclusivo gerado pelo sistema para o registro de intenção. |
| `intentStrength` | STRING | Esse campo especifica o tipo de período de validade da intenção, como &quot;DIA&quot;, &quot;SEMANA&quot; ou &quot;MÊS&quot;. |
| `isTrending` | BOOLEANO | Esse campo indica se a palavra-chave está em tendência, com valores possíveis de Baixo, Medium ou Alto. |
| `keyword` | STRING | Este campo contém a palavra-chave ou frase indicando intenção de [!DNL Demandbase]. |
| `keywordSetID` | STRING | Este é o identificador para o conjunto de palavras-chave. |
| `keywordSetName` | STRING | Este é o nome do conjunto de palavras-chave. |
| `numTrendingDays` | INTEIRO | Este campo indica o número de dias de tendência da palavra-chave. |
| `partitionDate` | DATA | Esta é a data de partição do registro. |
| `peopleResearchingCount` | INTEIRO | Este campo indica o número de pessoas pesquisando a palavra-chave. |
| `startDate` | DATA | Esta é a data de início do período de validade da intenção. |
| `trendingScore` | INTEIRO | Esse campo contém a pontuação de tendência da palavra-chave. |

{style="table-layout:auto"}

>[!TIP]
>
>Quaisquer alterações no esquema serão comunicadas à Adobe antecipadamente. Para suportar a evolução contínua do esquema, é essencial manter a compatibilidade com versões anteriores. O Experience Platform aplica uma abordagem de controle de versão aditivo apenas, garantindo que todas as atualizações do esquema não sejam destrutivas. Isso significa que as alterações de quebra são estritamente proibidas e somente as alterações que melhoram ou estendem o esquema existente são permitidas.

## Conectar sua conta do [!DNL Demandbase] à Experience Platform na interface

Após concluir a configuração de pré-requisito, leia o tutorial em [conectando sua conta [!DNL Demandbase] à Experience Platform](../../tutorials/ui/create/data-partners/demandbase.md) para iniciar a integração.

## Perguntas frequentes {#faq}

Leia esta seção para obter respostas a perguntas frequentes sobre a origem [!DNL Demandbase].

### Preciso ter um contrato existente com [!DNL Demandbase] para usar os dados de intenção de conta no Real-Time CDP B2B edition?

+++Resposta

Sim, você deve ter um contrato ativo com [!DNL Demandbase] para acessar e utilizar os dados de intenção no Experience Platform e no Real-Time CDP B2B edition. A integração aproveita seu contrato existente com o [!DNL Demandbase] para assimilar e ativar sinais de intenção de conta na Experience Platform e no Real-Time CDP.

+++

### Há suporte para campos personalizados de [!DNL Demandbase] nesta integração?

+++Resposta

Atualmente, você só pode usar campos [!DNL Demandbase] padrão para assimilação e ativação. Para exibir a lista de campos com suporte, leia o [[!DNL Demandbase] guia de esquema](#schema) para obter detalhes sobre a disponibilidade de campos.

+++

### Posso assimilar dados de [!DNL Demandbase] no Experience Platform de forma ad hoc?

+++Resposta

Sim, você pode assimilar dados de [!DNL Demandbase] de forma ad hoc. Você pode criar um novo fluxo de dados para assimilar os dados de intenção mais recentes, desde que haja novos dados de [!DNL Demandbase]. No entanto, você só pode ter um fluxo de dados ativo por vez. Portanto, certifique-se de excluir o fluxo de dados existente antes de criar um novo.

+++

### Qual é o processo de validação para dados de intenção e como posso verificar quais dados de intenção estão vinculados a uma conta específica?

+++Resposta

Para validar os dados de intenção e determinar quais sinais de intenção estão vinculados a contas específicas, use o [Serviço de consulta do Adobe Experience Platform](../../../query-service/home.md) por AccountID.

+++

### Como posso procurar uma intenção de uma empresa específica?

+++Resposta

Execute uma consulta SQL no [Serviço de consulta](../../../query-service/home.md) para procurar dados de intenção usando o nome da empresa ou AccountID. Para exibir todos os dados de intenção de uma empresa específica, é possível executar uma consulta SQL no Serviço de consulta usando o nome da empresa ou AccountID para buscar todos os sinais de intenção associados.

+++


### Encontrei um problema com o processo de correspondência de contas no Experience Platform, o que devo fazer?

+++Resposta

A resolução depende da questão específica:

* **Domínio de empresa incorreto ou ausente no Experience Platform**: se o problema resultar de um valor de domínio de empresa incorreto nos dados da conta, atualize o campo Domínio de empresa no Experience Platform para garantir uma correspondência precisa.
* **Mapeamento de campo incorreto no fluxo de dados**: se o problema se deve a um caminho de campo de domínio de empresa incorreto no fluxo de dados, atualize a configuração do fluxo de dados para fazer referência ao caminho de campo correto.

+++

### Como excluir dados de intenção no Experience Platform?

+++Resposta

Você deve [excluir o conjunto de dados](../../../catalog/datasets/user-guide.md#delete-a-dataset) para excluir os dados de intenção no Experience Platform.

+++

### Qual campo é usado para corresponder contas de [!DNL Demandbase] à Experience Platform?

+++Resposta

O campo `accountOrganization.domain` é usado para contas correspondentes. Se sua organização usar um campo personalizado diferente para armazenar o nome do site, forneça o caminho de campo correto para mapeamento preciso.

+++

### O que acontece quando um domínio de empresa é atualizado no Experience Platform?

+++Resposta

Quando um domínio de empresa é atualizado, o novo valor de domínio é aplicado na próxima execução do fluxo de dados. Isso garante que:

* A assimilação de dados de intenção futura usa o domínio atualizado para correspondência de conta.
* Todos os sinais de intenção incompatíveis anteriormente agora podem se alinhar corretamente com a conta desejada.
* Nenhuma alteração retroativa é feita em dados assimilados anteriores. Somente dados novos e recebidos refletirão a atualização.

+++

### Qual é o processo de correspondência de domínios?

+++Resposta

A correspondência de domínios no Experience Platform é baseada em uma correspondência exata do valor do campo de domínio depurado. O Experience Platform remove automaticamente os prefixos (por exemplo, https:/<span>/www.) e mantém o domínio de nível superior (por exemplo, adobe.com). A correspondência requer um valor de domínio exato, sem suporte para correspondência difusa ou subdomínios.

+++

### Onde posso usar os dados de intenção?

+++Resposta

Os dados de intenção podem ser utilizados em [Públicos-alvo da conta](../../../segmentation/types/account-audiences.md) para aprimorar o direcionamento, a segmentação e a personalização. Ao utilizar sinais de intenção, as empresas podem identificar e se envolver com contas que mostram grande interesse em tópicos específicos, otimizando o alcance de marketing e vendas

+++
