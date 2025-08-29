---
title: Intenção de Bombora
description: Saiba mais sobre a fonte Bombora Intent no Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 8a5fdcfcf503df1b9d5aa338ff530181a2d03b5d
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora] é uma solução de público-alvo abrangente especializada em dados de intenção B2B. O [!DNL Bombora Intent] é uma fonte do Adobe Experience Platform que você pode usar para conectar sua conta do [!DNL Bombora] à Experience Platform e integrar seus dados de intenção de conta.

Com a origem [!DNL Bombora Intent], você pode integrar os dados de intenção de sobretensão da empresa [!DNL Bombora's] para identificar contas que estão pesquisando ativamente seus produtos ou serviços. Use o [!DNL Bombora] para priorizar contas no mercado a fim de criar segmentos precisos e executar campanhas ABM hiperdirecionadas, garantindo que seus esforços de marketing se concentrem nas contas com maior probabilidade de conversão. Além disso, você pode aproveitar estratégias orientadas por intenções para otimizar os gastos com anúncios, aumentar o engajamento e maximizar o ROI.

Leia este documento para obter as informações de pré-requisito sobre a origem [!DNL Bombora].

## Casos de uso {#use-cases}

Leia a seguir os exemplos de caso de uso que você pode aplicar à origem [!DNL Bombora].

### Integração do Demand-Side Platform (DSP)

Como comerciante B2B, você pode criar uma lista de contas no Real-Time CDP, identificar empresas que mostram alta intenção para seus produtos e ativar essa lista no [!DNL Bombora], que se integra diretamente aos DSPs, permitindo que você execute campanhas de anúncios programáticos direcionadas usando dados do [!DNL Bombora's]. Isso garante que seu investimento em anúncios se concentre em empresas com maior probabilidade de conversão.

### Recursos do Account-Based Marketing (ABM)

Como profissional de marketing B2B, você pode criar uma lista de contas com base em sinais de intenção próprios e de terceiros. É possível então ativar essa lista em [!DNL Bombora], onde os recursos de ABM permitem direcionar os funcionários para essas contas especificamente, garantindo que seus anúncios cheguem aos responsáveis pelas decisões em vez de a um público-alvo maior.

### Ativação ABM multicanal

Como profissional de marketing B2B, você pode criar uma lista de contas no Real-Time CDP, identificando empresas com alta intenção e ativá-la em [!DNL Bombora] para executar campanhas direcionadas em vários canais. Nas redes sociais pagas, você pode veicular anúncios personalizados para profissionais em contas de público alvo em plataformas como [!DNL Linkedin] e [!DNL Facebook].

Usando plataformas de anúncios nativas, você pode garantir que o conteúdo chegue aos responsáveis pelas decisões em contextos relevantes. Você também pode estender campanhas para TV avançada, fornecendo anúncios para contas principais. Essa abordagem de vários canais garante mensagens consistentes entre plataformas, maximizando as taxas de engajamento e conversão.

## Pré-requisitos {#prerequisites}

Leia as seções a seguir para obter as etapas de pré-requisito antes de conectar [!DNL Bombora] ao Experience Platform.

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Uma lista de endereços IP deve ser adicionada a uma inclui na lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região ao seu incluo na lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Bombora] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

### Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

* Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
* Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
* Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
* Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
* Caracteres de caminho de URL inválidos não são permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

### Coletar credenciais necessárias

[!DNL Bombora] no Experience Platform está hospedado por [!DNL Google Cloud Storage]. Para autenticar com êxito sua conta do [!DNL Bombora], você deve fornecer os valores apropriados para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| ID da chave de acesso | A ID da chave de acesso [!DNL Bombora]. Esta é uma sequência de 61 caracteres alfanuméricos necessária para autenticar sua conta no Experience Platform. |
| Chave de acesso secreta | A chave de acesso secreta [!DNL Bombora]. Esta é uma sequência de 40 caracteres codificada em base 64 necessária para autenticar sua conta no Experience Platform. |
| Nome do bucket | O bucket [!DNL Bombora] do qual os dados serão extraídos. |

Para obter mais informações sobre essas credenciais, leia o [[!DNL Google Cloud Storage] guia de chaves HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obter etapas sobre como gerar sua própria chave de acesso, leia o [guia de pré-requisito na [!DNL Google Cloud Storage] visão geral da origem](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Esquema [!DNL Bombora] {#schema}

Leia esta seção para obter informações sobre o esquema [!DNL Bombora] e a estrutura de dados.

O esquema [!DNL Bombora] é chamado **Intenção da Conta Bombora B2B**. São as informações de intenção semanal (pesquisa de comprador B2B anônimo e consumo de conteúdo) sobre contas e tópicos especificados. Os dados estão em formato parquet.

* Classe - XDM [!DNL Bombora Account Intent]
* Namespace - B2B [!DNL Bombora Account Intent]
* Identidade principal - `intentID`
* Relacionamentos - Conta B2B

| Nome do campo | Tipo de dados | Descrição |
|------------------------|-----------|----------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJETO | Este campo é usado pelo sistema para auditoria do sistema de origem. |
| `_id` | STRING | Este campo é usado pelo sistema como um identificador exclusivo. |
| `accountDomain` | STRING | Esse campo contém o domínio da conta. |
| `accountID` | STRING | Esse campo contém a ID da conta B2B à qual esse registro de intenção está associado. |
| `bomboraAccountName` | STRING | Esse campo contém a ID da empresa em Bombora. |
| `clusterID` | STRING | Este campo contém a ID do cluster. |
| `clusterName` | STRING | Este campo contém o nome do cluster. |
| `compositeScore` | INTEIRO | Esse campo contém a pontuação composta da intenção. |
| `intentID` | STRING | Este campo contém um valor exclusivo gerado pelo sistema. |
| `partitionDate` | DATA | Este campo contém a data da partição. Isso é feito semanalmente, no final da semana, no formato `mm/dd/yyyy`. |
| `topicID` | STRING | Esse campo contém a ID do tópico de intenção da Bombora. |
| `topicName` | STRING | Este campo contém o nome do tópico de intenção de Bombora. |

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

Sim, você pode assimilar dados de [!DNL Bombora] de forma ad hoc. Você pode criar um novo fluxo de dados para assimilar os dados de intenção mais recentes, desde que haja novos dados de [!DNL Bombora]. No entanto, você só pode ter um fluxo de dados ativo por vez. Portanto, certifique-se de excluir o fluxo de dados existente antes de criar um novo.

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

### Qual campo é usado para corresponder contas de [!DNL Bombora] à Experience Platform?

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

Os dados de intenção podem ser utilizados em [Públicos-alvo da conta](../../../segmentation/types/account-audiences.md) para aprimorar o direcionamento, a segmentação e a personalização. Ao utilizar sinais de intenção, as empresas podem identificar e se envolver com contas que mostram grande interesse em tópicos específicos, otimizando o alcance de marketing e vendas.

+++
