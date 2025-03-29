---
title: Intenção do Demandbase
description: Saiba mais sobre a fonte de intenção do Demandbase no Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: 78aae71ff48fc710aaaabf4ef71f6e50d2a8c12e
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] é uma plataforma de marketing baseada em conta que você pode usar para vendas B2B e sucesso de marketing. O [!DNL Demandbase Intent] é uma fonte do Adobe Experience Platform que você pode usar para conectar sua conta do [!DNL Demandbase] à Experience Platform e integrar seus dados de intenção de conta.

Com a origem [!DNL Demandbase], é possível identificar contas de alto interesse com base em compromissos em tempo real. Ao priorizar os sinais de intenção mais fortes, você pode criar segmentos precisos e fornecer campanhas hiperdirecionadas, garantindo que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão. A ativação de estratégias orientadas por intenção permite a otimização de gastos com anúncios, maior engajamento e maior ROI.

Leia este documento para obter as informações de pré-requisito sobre a origem [!DNL Demandbase].

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter as etapas de pré-requisito antes de conectar [!DNL Demandbase] ao Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Uma lista de endereços IP deve ser adicionada a uma inclui na lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região ao seu incluo na lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Demandbase] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

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

Leia esta seção para obter informações sobre o esquema [!DNL Demandbase] e a estrutura de dados.

O esquema [!DNL Demandbase] é chamado de **Intenção Semanal da Empresa**. São as informações de intenção semanal (pesquisa de comprador B2B anônimo e consumo de conteúdo) em uma conta e palavras-chave especificadas. Os dados estão em formato parquet.

| Nome do campo | Tipo de dados | Obrigatório | Chave comercial | Notas |
| --- | --- | --- | --- | --- |
| `company_id` | STRING | TRUE | SIM | A ID canônica da empresa. |
| `domain` | STRING | TRUE | SIM | O domínio identificado da conta que mostra a intenção. |
| `start_date` | DATA | TRUE | SIM | A data inicial de quando a atividade de intenção ocorreu no período de duração. |
| `end_date` | DATA | TRUE | SIM | A data final de quando a atividade de intenção ocorreu no período de duração. |
| `duration_type` | STRING | TRUE | SIM | O tipo de duração. Geralmente, esse valor pode ser diário, semanal ou mensal, dependendo da duração do roll-up escolhida. Para esta amostra de dados, este valor é `week`. |
| `keyword_set_id` | STRING | TRUE | SIM | A ID do conjunto de palavras-chave. É exclusivo para cada cliente. |
| `keyword_set` | STRING | TRUE | SIM | O nome do conjunto de palavras-chave. |
| `is_trending` | STRING | TRUE | | O estado atual de uma determinada tendência. O estado de tendência é medido como uma intermitência na atividade de intenção na última semana em relação às médias das sete semanas anteriores. |
| `intent_strength` | ENUM[CADEIA DE CARACTERES] | TRUE | | Uma medida quantificada da intensidade da intenção. Os valores aceitos incluem: `HIGH`, `MED` e `LOW`. |
| `num_people_researching` | INTEIRO | TRUE | | A contagem de pessoas pertencentes a `company_id` que pesquisaram a palavra-chave nos últimos sete dias. |
| `num_trending_days` | INTEIRO | TRUE | | O número de dias de tendência da palavra-chave em uma determinada duração. |
| `trending_score` | INTEIRO | TRUE | | A pontuação de tendência. |
| `record_id` | STRING | TRUE | | A ID exclusiva do registro principal. |
| `partition_date` | DATA | TRUE | | A data do calendário do instantâneo. Isso é feito semanalmente, no final da semana. |

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
