---
title: Destino de identidade da Merkury Enterprise
description: Saiba como criar uma conexão de destino de identidade corporativa do Merkury usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---


# Destino de identidade da Merkury Enterprise

>[!NOTE]
>
>O conector de destino e a página de documentação são criados e mantidos pelo [!DNL Merkury] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato com o [!DNL Merkury] representante de conta.

## Visão geral

Use o [!DNL Merkury Enterprise Identity] destino para criar perfis de consumidor mais precisos, abrangentes e perspicazes. Com dados de perfil aprimorados, os profissionais de marketing podem utilizar melhores insights, segmentos e modelos, resultando em direcionamento e modelagem preditiva mais precisos.

![Um diagrama mostrando a interconexão entre Merkury e Experience Platform, incluindo assimilação e ativação](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Siga as etapas desta página de documentação para criar uma [!DNL Merkury Identity] conexão de destino e ativação de públicos para identificação e enriquecimento usando a interface do usuário do Adobe Experience Platform.

>[!NOTE]
>
>Se estiver procurando ativar públicos para destinos de mídia com sua [!DNL Merkury Connect] conta, use o [!DNL Merkury Connections] destino em vez disso.

![O cartão de destino Merkury Enterprise Identity é destacado no catálogo de destinos do Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Casos de uso

A variável [!DNL Merkury Enterprise Identity] destino fornece a capacidade de transferir com segurança as PII do consumidor para o [!DNL Merkury] recursos:

* **Qualidade dos dados**: melhore a qualidade dos dados do perfil do consumidor com higiene e padronização de dados. [!DNL Merkury] A inclui a higiene postal dos EUA e a identificação de movimentações para oferecer suporte aos casos de uso de marketing por correspondência direta mais avançados.
* **Resolução de identidade**: crie uma visão única, precisa e abrangente do cliente, informada por [!DNL Merkury] IDs de indivíduo e família. As IDs do Merkury fornecem um nível profundo de vinculação de perfis viabilizada pelo [!DNL Merkury]O gráfico abrangente de identidade do consumidor adulto dos EUA de 268+ milhões de pessoas.
* **Enriquecimento**: promova melhores insights e personalização com o [!DNL Merkury Data]. [!DNL Merkury Data] O inclui mais de 10.000 atributos de dados disponíveis, que variam de dados demográficos, de estilo de vida, financeiros, de eventos de vida e de compra da [!DNL Merkury Data Suite].

>[!NOTE]
>
>Esses casos de uso são executados por meio de uma combinação de conectores de destino e de origem. O cliente começará exportando seus registros de clientes existentes para enriquecimento usando esse conector de destino. [!DNL Merkury]O serviço do pesquisaria o arquivo, recuperaria e enriqueceria com [!DNL Merkury]e gerar um arquivo. Em seguida, o cliente utilizaria o [!DNL Merkury] Placa de origem do conector do Source para assimilar os perfis hidratados do cliente de volta na Adobe Real-Time CDP.

## Pré-requisitos

>[!IMPORTANT]
>
>* Para se conectar ao destino, você precisa da variável **Exibir destinos** e **Gerenciar destinos**, **Ativar destinos**, **Exibir perfis**, e **Exibir segmentos** [[permissões de controle de acesso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Leia o [[visão geral do controle de acesso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **Exibir gráfico de identidade** [[permissão de controle de acesso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identidades suportadas {#supported-identities}

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| ECID | Experience Cloud ID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/features/ecid.md) para obter mais informações. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| extern_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| **Público-alvo** | **Compatível** | **Descrição** | **origem** |
|---|---|---|---|
| Serviço de segmentação | ✓ | Públicos-alvo gerados pelo Experience Platform [[Serviço de segmentação]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Uploads personalizados | x | Públicos-alvo [[importado]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.
|**Público**|**Compatível**|**Origem da descrição**|\
|—|—|—|\
✓ |Serviço de segmentação|µ|Públicos-alvo gerados pelo Experience Platform [[Serviço de segmentação]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).| Uploads personalizados|X|Públicos-alvo [[importado]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) para o Experience Platform de arquivos CSV.

{style="table-layout:auto"}

## Conectar ao destino

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **Exibir destinos** e **Gerenciar e ativar destinos do conjunto de dados** [[permissões de controle de acesso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Leia o [[visão geral do controle de acesso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [[tutorial de configuração de destino]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino

Para autenticar no destino, preencha os campos obrigatórios e selecione **Conectar ao destino**.

Para acessar seu bucket no Experience Platform, você precisa fornecer valores válidos para as seguintes credenciais:

| **Credencial** | **Descrição** |
|---|---|
| Chave de acesso | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da equipe do Merkury. |
| Chave secreta | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da equipe do Merkury. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da equipe do Merkury. |

{style="table-layout:auto"}

![tela de criação de novo destino](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Preencher detalhes do destino

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Uma captura de tela dos detalhes do destino](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nome (obrigatório)** - O nome em que o destino será salvo
* **Descrição** - Breve explicação da finalidade do destino
* **Nome do Período (Obrigatório)** - Nome do bucket do Amazon S3 configurado no S3
* **Caminho da pasta (obrigatório)** - Se os subdiretórios em um bucket forem usados, um caminho deverá ser definido, ou &#39;/&#39; para fazer referência ao caminho raiz.
* **Tipo de arquivo** - Selecione o formato que o Experience Platform deve usar para os arquivos exportados. Consulte sua equipe do Merkury para obter o tipo de arquivo esperado para sua conta.

>[!NOTE]
>
>Ao selecionar a opção CSV, as opções Delimitador, Citação, Caractere de escape, Valor vazio, Valor nulo, Formato de compactação e Incluir arquivo de manifesto serão apresentadas. Consulte sua equipe do Merkury para obter as configurações apropriadas para sua conta.

![imagem da opção csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Conta existente

As contas já definidas usando o destino Merkury Enterprise Identity são exibidas em um pop-up de lista. Quando selecionada, você poderá ver os detalhes da conta no painel direito. Veja o exemplo da interface do usuário ao navegar para **Destinos** > **Contas**;

![Uma captura de tela da conta de destino na página de contas de destino](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Ativar alertas

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Quando terminar de fornecer detalhes da conexão de destino, selecione **Próxima**.

## Ativar públicos-alvo para esse destino

>[!IMPORTANT]
>
>* Para ativar os dados, é necessário **Exibir destinos**, **Ativar destinos**, **Exibir perfis**, e **Exibir segmentos** permissões de controle de acesso. Leia a visão geral do controle de acesso ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar identidades, é necessário **Exibir gráfico de identidade** permissão de controle de acesso.

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Sugestões de mapeamento

O processamento correto dos arquivos no [!DNL Merkury] O lado requer elementos de nome e endereço. Embora nem todos os elementos sejam necessários, fornecer o máximo possível ajudará na correspondência bem-sucedida.

As sugestões de mapeamento são fornecidas na tabela abaixo, listando os atributos no seu lado de destino que são usados pelo [!DNL Merkury] processamento ao qual os clientes podem mapear atributos de perfil. Trate esses elementos como sugestões, pois nem todos os elementos são obrigatórios. Os valores de origem dependerão das necessidades da conta.

| Campo de público alvo | Descrição do Source |
|---|---|
| ID | Campo de identidade a ser usado para mapear [!DNL Merkury] dados para o Experience Platform por meio do [!DNL Merkury Enterprise Identity] Conector do Source |
| Input_First_Name | A variável `person.name.firstName` valor em Experience Platform. |
| Input_Last_Name | A variável `person.name.lastName` valor em Experience Platform. |
| Input_Address_Line_1 | A variável `mailingAddress.street` valor em Experience Platform. |
| Cidade_Entrada | A variável `mailingAddress.city` valor em Experience Platform. |
| Input_State_Province_Code | A variável `mailingAddress.state` valor em Experience Platform. Use se o estado estiver no formato de código de dois caracteres. |
| Input_State_Province_Name | A variável `mailingAddress.state` valor em Experience Platform. Usar se o estado for o nome completo do estado |
| Input_Postal_Code | A variável `mailingAddress.postalCode` valor em Experience Platform. |
| Input_Email_Address | O valor que você deseja mapear como o endereço de email dos perfis. |
| Input_Phone | O valor que você deseja mapear como o número de telefone dos perfis. |

{style="table-layout:auto"}

## Validar exportação de dados

Para verificar se os dados foram exportados com êxito, verifique o bucket do Amazon S3 Storage e se os arquivos exportados contêm as populações de perfis esperadas.

## Uso e governança de dados

Todos os destinos do Adobe Experience Platform estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o Adobe Experience Platform fiscaliza a governança de dados, leia o [Visão geral da governança de dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para exportar dados do perfil do Experience Platform para sua [!DNL Merkury] local do S3 gerenciado. Em seguida, entre em contato com o [!DNL Merkury] representante com o nome da conta, nomes de arquivo e o caminho do bucket para que o processamento possa ser configurado.