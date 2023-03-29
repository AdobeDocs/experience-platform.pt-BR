---
title: Anúncios do Amazon
description: O Amazon Ads oferece uma variedade de opções para ajudá-lo a atingir suas metas de publicidade para vendedores registrados, vendedores, vendedores de livros, autores Kindle Direct Publishing (KDP), desenvolvedores de aplicativos e/ou agências. A integração do Amazon Ads com o Adobe Experience Platform fornece integração chave para os produtos Amazon Ads, incluindo o Amazon DSP (ADSP). Usando o destino Anúncios do Amazon no Adobe Experience Platform, os usuários podem definir públicos do anunciante para direcionamento e ativação no Amazon DSP.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (Beta) Conexão de anúncios do Amazon {#amazon-ads}

## Visão geral {#overview}

O Amazon Ads oferece uma variedade de opções para ajudá-lo a atingir suas metas de publicidade para vendedores registrados, vendedores, vendedores de livros, autores Kindle Direct Publishing (KDP), desenvolvedores de aplicativos e/ou agências.

A integração do Amazon Ads com o Adobe Experience Platform fornece integração chave para os produtos Amazon Ads, incluindo o Amazon DSP (ADSP). Usando o destino Anúncios do Amazon no Adobe Experience Platform, os usuários podem definir públicos do anunciante para direcionamento e ativação no Amazon DSP.

Essa conexão é compatível com a criação de público-alvo nos seguintes Amazon Marketplaces: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela *Anúncios do Amazon* equipe. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável *Anúncios do Amazon* destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Ativação e direcionamento {#activation-and-targeting}

Essa integração com o Amazon DSP permite que os anunciantes do Amazon Ads passem segmentos de CDP do anunciante do Adobe Experience Platform para o Amazon, criando DSP públicos anunciantes para direcionamento de anúncios. Os públicos-alvo podem ser selecionados na DSP do Amazon para direcionamento positivo, bem como para direcionamento negativo (supressão). Além disso, usando sinais gerados por meio do Amazon Marketing Cloud, os anunciantes podem otimizar os públicos-alvo do anunciante, o que sincronizará as alterações do público-alvo com o Amazon DSP.

## Pré-requisitos {#prerequisites}

Para usar a conexão do Amazon Ads com o Adobe Experience Platform, os usuários devem primeiro ter acesso a uma conta de anunciante do Amazon DSP.  Para provisionar essas instâncias, visite a seguinte página no site do Amazon Ads:

* [Introdução ao Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identidades suportadas {#supported-identities}

O *Anúncios do Amazon* A conexão oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md). Para obter mais detalhes sobre as identidades suportadas pelo Amazon Ads, visite o [Centro de suporte ao Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na *Anúncios do Amazon* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

Você será levado à interface de conexão do Amazon Ads, onde primeiro selecionará as contas de anunciante que deseja se conectar.  Após a conexão, você será redirecionado de volta ao Adobe Experience Platform com uma nova conexão, fornecida com a ID da conta do anunciante selecionada. Selecione a Conta de anunciante apropriada na tela de configuração de destino para continuar.

* **[!UICONTROL Token de portador]**: Preencha o token portador para autenticar para o destino.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante do Amazon Ads]**: Selecione a ID da conta de destino do Amazon Ads usada para o destino.

Observação: ao selecionar essa ID de anunciante do Amazon Ads, será necessário criar um novo destino para alterar isso. Se você autenticar novamente as credenciais do OAuth e selecionar uma nova ID de anunciante, as alterações não serão aplicadas.

![Configurar novo destino](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Mapear atributos e identidades {#map}

A conexão Amazon Ads oferece suporte a endereço de email com hash e números de telefone com hash para fins de correspondência de identidade.  A captura de tela abaixo fornece um exemplo compatível com a conexão do Amazon Ads:

![Adobe para o mapeamento de anúncios do Amazon](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para mapear endereços de email com hash, selecione a variável `Email_LC_SHA256` namespace de identidade como um campo de origem.
* Para mapear números de telefone com hash, selecione o `Phone_SHA256` namespace de identidade como um campo de origem.
* Para mapear endereços de email ou números de telefone sem hash, selecione os namespaces de identidade correspondentes como campos de origem e verifique o `Apply Transformation` para que a Platform coloque hash nas identidades na ativação.

É altamente recomendável mapear quantos campos estiverem disponíveis. Se apenas um atributo de origem estiver disponível, você poderá mapear um único campo.  O destino Amazon Ads utilizará todos os campos mapeados para fins de mapeamento, produzindo taxas de correspondência mais altas se mais campos forem fornecidos. Para obter mais informações sobre os identificadores aceitos, visite o [Página de ajuda do público-alvo com hash do Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que o público-alvo for carregado, você poderá validar se o público-alvo foi criado e carregado corretamente usando as seguintes etapas:

**Para Amazon DSP**

Navegue até a ID do anunciante → Públicos-alvo → Públicos-alvo do anunciante. Se o seu público-alvo tiver sido criado com sucesso e atender ao número mínimo de membros do público-alvo, você verá um Status de `Active`.  Detalhes adicionais sobre o tamanho e o alcance do seu público podem ser encontrados no painel Alcance previsto no lado direito da interface do usuário do Amazon DSP.

![Validação da criação de público-alvo do Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter a documentação de ajuda adicional, visite os seguintes recursos de ajuda do Amazon Ads:

* [Central de ajuda do Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
