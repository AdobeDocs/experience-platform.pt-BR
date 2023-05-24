---
title: Anúncios do Amazon
description: O Amazon Ads oferece uma variedade de opções para ajudá-lo a atingir suas metas de publicidade para vendedores registrados, fornecedores, fornecedores de livros, autores de KDP (Kindle Direct Publishing), desenvolvedores de aplicativos e/ou agências. A integração do Amazon Ads com o Adobe Experience Platform fornece integração pronta para uso com produtos Amazon Ads, incluindo o Amazon DSP (ADSP). Usando o destino do Amazon Ads no Adobe Experience Platform, os usuários podem definir públicos-alvo do anunciante para direcionamento e ativação no Amazon DSP.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---

# (Beta) Conexão com o Amazon Ads {#amazon-ads}

## Visão geral {#overview}

O Amazon Ads oferece uma variedade de opções para ajudá-lo a atingir suas metas de publicidade para vendedores registrados, fornecedores, fornecedores de livros, autores de KDP (Kindle Direct Publishing), desenvolvedores de aplicativos e/ou agências.

A integração do Amazon Ads com o Adobe Experience Platform fornece integração pronta para uso com produtos Amazon Ads, incluindo o Amazon DSP (ADSP). Usando o destino do Amazon Ads no Adobe Experience Platform, os usuários podem definir públicos-alvo do anunciante para direcionamento e ativação no Amazon DSP.

Essa conexão oferece suporte à criação de públicos-alvo nos seguintes Amazon Marketplaces: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pelo *Anúncios do Amazon* equipe. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o *Anúncios do Amazon* destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Ativação e direcionamento {#activation-and-targeting}

Essa integração com o Amazon DSP permite que os anunciantes do Amazon Ads transmitam segmentos de CDP do anunciante do Adobe Experience Platform para o Amazon DSP a fim de criar públicos-alvo de anunciantes para direcionamento de anúncios. Os públicos podem ser selecionados no DSP do Amazon para direcionamento positivo, bem como direcionamento negativo (supressão). Além disso, usando sinais gerados pelo Amazon Marketing Cloud, os anunciantes podem otimizar os públicos-alvo do anunciante, o que sincronizará as alterações de público com o Amazon DSP.

## Pré-requisitos {#prerequisites}

Para usar a conexão do Amazon Ads com o Adobe Experience Platform, os usuários devem primeiro ter acesso a uma conta do anunciante do Amazon DSP.  Para provisionar essas instâncias, visite a seguinte página no site do Amazon Ads:

* [Introdução ao Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identidades suportadas {#supported-identities}

A variável *Anúncios do Amazon* A conexão suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md). Para obter mais detalhes sobre as identidades compatíveis com o Amazon Ads, visite o [Centro de suporte ao Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no *Anúncios do Amazon* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

Você será direcionado para a interface de conexão do Amazon Ads, onde primeiro selecionará as contas de anunciante às quais deseja se conectar.  Após a conexão, você será redirecionado de volta para a Adobe Experience Platform com uma nova conexão, fornecida com a ID da conta do anunciante selecionada. Selecione a Conta do anunciante apropriada na tela de configuração de destino para continuar.

* **[!UICONTROL Token de portador]**: Preencha o token do portador para autenticar no destino.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante do Amazon Ads]**: selecione a ID da conta do Amazon Ads de destino usada para o destino.

Observação: após selecionar esta ID do anunciante do Amazon Ads, será necessário criar um novo destino para alterá-la. Se você autenticar novamente as credenciais do OAuth e selecionar uma nova ID do anunciante, suas alterações não serão aplicadas.

![Configurar novo destino](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

A conexão do Amazon Ads é compatível com endereços de email com hash e números de telefone com hash para fins de correspondência de identidade.  A captura de tela abaixo fornece um exemplo de correspondência compatível com a conexão do Amazon Ads:

![Mapeamento de Adobe para anúncios do Amazon](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para mapear endereços de email com hash, selecione a `Email_LC_SHA256` namespace de identidade como um campo de origem.
* Para mapear números de telefone com hash, selecione o `Phone_SHA256` namespace de identidade como um campo de origem.
* Para mapear endereços de email com hash ou números de telefone, selecione os namespaces de identidade correspondentes como campos de origem e verifique a `Apply Transformation` opção para que o Platform coloque as identidades em hash na ativação.

É altamente recomendável mapear quantos campos estiverem disponíveis. Se apenas um atributo de origem estiver disponível, você poderá mapear um único campo.  O destino do Amazon Ads utilizará todos os campos mapeados para fins de mapeamento, produzindo taxas de correspondência mais altas se mais campos forem fornecidos. Para obter mais informações sobre os identificadores aceitos, visite o [Página de ajuda do público-alvo com hash do Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que o público-alvo for carregado, você poderá validar se o público-alvo foi criado e carregado corretamente usando estas etapas:

**Para o Amazon DSP**

Navegue até a ID do anunciante → Públicos → Públicos do anunciante. Se o público-alvo for criado com sucesso e atender ao número mínimo de membros do público-alvo, você verá um Status de `Active`.  Detalhes adicionais sobre o tamanho e o alcance do seu público-alvo podem ser encontrados no painel Alcance previsto no lado direito da interface do usuário do Amazon DSP.

![Validação da criação de público do Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter a documentação de ajuda adicional, visite os seguintes recursos de ajuda do Amazon Ads:

* [Centro de ajuda do Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
