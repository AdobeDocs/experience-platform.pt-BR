---
title: Intenção bombora
description: Conheça a fonte de intenção bombora no Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 9ab2c4725d2188f772bde1f7a89db2bb47c7a46b
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora] é uma solução de público-alvo abrangente especializada em dados de intenções B2B. O [!DNL Bombora Intent] é uma fonte do Adobe Experience Platform que você pode usar para conectar sua conta do [!DNL Bombora] à Experience Platform e integrar seus dados de intenção de conta.

Com a origem [!DNL Bombora Intent], você pode integrar os dados de intenção de sobretensão da empresa [!DNL Bombora's] para identificar contas que estão pesquisando ativamente seus produtos ou serviços. Use o [!DNL Bombora] para priorizar contas no mercado a fim de criar segmentos precisos e executar campanhas ABM hiperdirecionadas, garantindo que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão. Além disso, você pode aproveitar estratégias orientadas por intenções para otimizar os gastos com anúncios, aumentar o engajamento e maximizar o ROI.

Leia este documento para obter as informações de pré-requisito sobre a origem [!DNL Bombora].

## Casos de uso {#use-cases}

Leia a seguir os exemplos de caso de uso que você pode aplicar à origem [!DNL Bombora].

### Integração de Platform do Lado da demanda (DSP)

Como B2B profissional de marketing, você pode criar uma conta lista no CDP em tempo real, identificar empresas que demonstram grande intenção para seus produtos e, em seguida, ativá-la lista em [!DNL Bombora], que se integra diretamente a DSPs, permitindo que você execute campanhas de publicidade programática direcionadas usando [!DNL Bombora's] dados. Isso garante que seus publicidade gastos se concentrem nas empresas mais propensas a converter.

### Recursos de marketing baseado em conta (ABM)

Como profissional de marketing B2B, você pode criar uma lista de contas com base em sinais de intenção próprios e de terceiros. É possível então ativar essa lista em [!DNL Bombora], onde os recursos de ABM permitem direcionar os funcionários para essas contas especificamente, garantindo que seus anúncios cheguem aos responsáveis pelas decisões em vez de a um público-alvo maior.

### Ativação ABM multicanal

Como profissional de marketing B2B, você pode criar uma lista de contas no Real-Time CDP, identificando empresas com alta intenção e ativá-la em [!DNL Bombora] para executar campanhas direcionadas em vários canais. Nas redes sociais pagas, você pode veicular anúncios personalizados para profissionais em contas de público alvo em plataformas como [!DNL Linkedin] e [!DNL Facebook].

Usando plataformas de anúncios nativas, você pode garantir que o conteúdo chegue aos responsáveis pelas decisões em contextos relevantes. Você também pode estender campanhas para TV avançada, fornecendo anúncios para contas principais. Essa abordagem de vários canais garante mensagens consistentes entre plataformas, maximizando as taxas de engajamento e conversão.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter as etapas de pré-requisito antes de conectar [!DNL Bombora] ao Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Uma lista de endereços IP deve ser adicionada a uma inclui na lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região ao seu incluo na lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Bombora] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o guia[&#128279;](../../../access-control/abac/ui/permissions.md) de interface de controle de acesso.

### Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

* Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
* Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
* Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
* Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
* Caracteres de caminho URL ilegais não são permitidos. Code pontos curtir `\uE000`, embora válidos em nomes de arquivo NTFS, são caracteres Unicode inválidos. Além disso, alguns caracteres ASCII ou Unicode, curtir caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem as cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras](https://www.ietf.org/rfc/rfc2616.txt) básicas e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, ponto character (.), e dois caracteres de ponto (..).

### Reunir as credenciais necessárias

[!DNL Bombora] no Experience Platform é hospedado por [!DNL Google Cloud Storage]. No solicitar para autenticar seu [!DNL Bombora] conta com êxito, você deve fornecer os valores apropriados para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| ID da chave de acesso | A ID da chave de acesso [!DNL Bombora]. Essa é uma sequência de 61 caracteres alfanuméricos necessários para autenticar os conta para Experience Platform. |
| Chave de acesso secreta | A chave de acesso secreta [!DNL Bombora]. Esta é uma sequência de 40 caracteres codificada em base 64 necessária para autenticar sua conta no Experience Platform. |
| Nome do bucket | O bucket [!DNL Bombora] do qual os dados serão extraídos. |

Para obter mais informações sobre essas credenciais, leia o [[!DNL Google Cloud Storage] guia de chaves HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria chave de acesso, leia o [guia de pré-requisito na visão geral](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account) da [!DNL Google Cloud Storage] fonte.

## [!DNL Bombora] esquema {#schema}

Leia esta seção para obter informações sobre o [!DNL Bombora] schema e a estrutura de dados.

A [!DNL Bombora] schema é chamada de **Semana da Intenção** da Conta. São as informações de intenção semanais (anônimos B2B comprador pesquisa e consumo conteúdo) em contas e tópicos especificados. Os dados estão no formato parquet.

| Nome do campo | Tipo de dados | Obrigatório | chave Empresas | Notas |
| --- | --- | --- | --- | --- |
| `Account_Name` | STRING | TRUE | SIM | O nome canônico da empresa. |
| `Domain` | STRING | TRUE | SIM | O domínio da conta identificada que está mostrando a intenção. |
| `Topic_Id` | STRING | TRUE | SIM | A [!DNL Bombora] ID do tópico. |
| `Topic_Name` | CORDA | VERDADEIRO | | O nome do [!DNL Bombora] tópico. |
| `Cluster_Name` | CORDA | VERDADEIRO | | O nome do cluster em [!DNL Bombora] para um determinado tópico. |
| `Cluster_Id` | STRING | TRUE | | A ID do cluster associada a um determinado tópico. |
| `Composite_Score` | INTEIRO | TRUE | | A pontuação composta representa o padrão de consumo de um domínio para um determinado tópico durante um período especificado. A pontuação composta é medida entre 0 e 100, onde 100 representa a maior pontuação possível e 0 representa a menor pontuação possível. Uma pontuação composta acima de 60 representa um aumento no interesse em um tópico específico por um domínio. Isso também é conhecido como &quot;aumento de tropas&quot;. |
| `Partition_Date` | DATA | TRUE | | A data do calendário de um instantâneo. Isso é feito semanalmente, no formato de fim de semana `mm/dd/yyyy` . |

{style="table-layout:auto"}

>[!TIP]
>
>Quaisquer alterações no esquema serão comunicadas à Adobe antecipadamente. Para suportar a evolução contínua do esquema, é essencial manter a compatibilidade com versões anteriores. O Experience Platform aplica uma abordagem de controle de versão aditivo apenas, garantindo que todas as atualizações do esquema não sejam destrutivas. Isso significa que as alterações de quebra são estritamente proibidas e somente as alterações que melhoram ou estendem o esquema existente são permitidas.

## Conectar sua conta do [!DNL Bombora] à Experience Platform na interface

Após concluir a configuração de pré-requisito, leia o tutorial em [conectando sua conta [!DNL Bombora] à Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) para iniciar a integração.

## Perguntas frequentes {#faq}

Leia esta seção para obter respostas a perguntas frequentes sobre a origem [!DNL Bombora].

### Preciso ter um contrato existente com [!DNL Bombora] para usar os dados de intenção de conta no Real-Time CDP B2B edition?

+++Resposta

Sim, você deve ter um contrato ativo com [!DNL Bombora] para acessar e utilizar os dados de intenção no Experience Platform e no Real-Time CDP B2B edition. A integração aproveita seu contrato existente com o [!DNL Bombora] para assimilar e ativar sinais de intenção de conta na Experience Platform e no Real-Time CDP.

+++

### Há suporte para campos personalizados de [!DNL Bombora] nesta integração?

+++Resposta

Atualmente, você só pode usar campos [!DNL Bombora] padrão para assimilação e ativação. Para exibir a lista de campos com suporte, leia o [[!DNL Bombora] guia de esquema](#schema) para obter detalhes sobre a disponibilidade de campos.

+++

### Posso assimilar dados de [!DNL Bombora] no Experience Platform de forma ad hoc?

+++Resposta

Sim, você pode assimilar dados de [!DNL Bombora] uma base publicidade hoc. Você pode criar um novo fluxo de dados para assimilar os dados de intenção mais recentes, desde que haja novos dados de [!DNL Bombora]. No entanto, você só pode ter um fluxo de dados ativo por vez. Portanto, certifique-se de excluir o fluxo de dados existente antes de criar um novo.

+++

### Qual é o processo de validação para dados de intenção e como posso verificar quais dados de intenção estão vinculados a uma conta específica?

+++Resposta

Para validar os dados de intenção e determinar quais sinais de intenção estão vinculados a contas específicas, use o [Serviço de consulta do Adobe Experience Platform](../../../query-service/home.md) por AccountID.

+++

### Como posso procurar uma intenção de uma empresa específica?

+++Resposta

Execute uma query SQL no [Serviço](../../../query-service/home.md) de consulta para pesquisa para dados de intenção usando o nome da empresa ou AccountID. Para visualização todos os dados de intenção de um empresa específico, você pode executar um query SQL no Serviço de consulta usando o nome empresa ou AccountID para buscar todos os sinais de intenção associados.

+++


### Encontrei um problema com o conta processo de correspondência no Experience Platform, o que devo fazer?

+++Resposta

A resolução depende do problema específico:

* **Domínio de empresa incorreto ou ausente no Experience Platform**: se o problema decorre de um valor de domínio empresa incorreto nos dados de conta, atualize o campo de domínio empresa em Experience Platform para garantir uma correspondência precisa.
* **Mapeamento de campo incorreto no fluxo de** dados: se o problema for devido a um caminho incorreto empresa campo de domínio no fluxo de dados, atualize a configuração do dataflow para fazer referência ao caminho de campo correto.

+++

### Como excluo os dados de intenção no Experience Platform?

+++Resposta

Você deve [excluir o conjunto de dados](../../../catalog/datasets/user-guide.md#delete-a-dataset) para excluir os dados de intenção no Experience Platform.

+++

### Qual campo é usado para corresponder contas de [!DNL Bombora] à Experience Platform?

+++Resposta

O campo `accountOrganization.domain` é usado para contas correspondentes. Se sua organização usar um campo personalizado diferente para armazenar o nome do site, forneça o caminho de campo correto para mapeamento preciso.

+++

### O que acontece quando um domínio do empresa é atualizado no Experience Platform?

+++Resposta

Quando um domínio de empresa é atualizado, o novo valor de domínio é aplicado na próxima execução do fluxo de dados. Isso garante que:

* A assimilação de dados de intenção futura usa o domínio atualizado para correspondência de conta.
* Todos os sinais de intenção incompatíveis anteriormente agora podem se alinhar corretamente com a conta desejada.
* Nenhuma alteração retroativa é feita em dados assimilados anteriores. Somente dados novos e recebidos refletirão a atualização.

+++

### Qual é o processo de correspondência de domínio?

+++Resposta

A correspondência de domínio em Experience Platform baseia-se em uma correspondência exata do valor do campo de domínio limpo. O Experience Platform remove automaticamente os prefixos (por exemplo, https:/<span>/www.) e mantém o domínio de nível superior (por exemplo, adobe.com). A correspondência requer um valor de domínio exato, sem suporte para correspondência difusa ou subdomínios.

+++

### Onde posso usar os dados de intenção?

+++Resposta

Os dados de intenção podem ser utilizados em [Públicos-alvo da conta](../../../segmentation/types/account-audiences.md) para aprimorar o direcionamento, a segmentação e a personalização. Ao utilizar sinais de intenção, as empresas podem identificar e se envolver com contas que mostram grande interesse em tópicos específicos, otimizando o alcance de marketing e vendas.

+++
