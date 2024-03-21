---
title: Anúncios do Amazon
description: O Amazon Ads oferece uma variedade de opções para ajudá-lo a atingir suas metas de publicidade para vendedores registrados, fornecedores, fornecedores de livros, autores de KDP (Kindle Direct Publishing), desenvolvedores de aplicativos e/ou agências. A integração do Amazon Ads com o Adobe Experience Platform fornece integração pronta para uso com produtos Amazon Ads, incluindo o Amazon DSP (ADSP). Usando o destino do Amazon Ads no Adobe Experience Platform, os usuários podem definir públicos-alvo do anunciante para direcionamento e ativação no Amazon DSP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: ba768b3148d57e9df12a34f0324c086a17a6d45a
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# (Beta) Conexão com o Amazon Ads {#amazon-ads}

## Visão geral {#overview}

[!DNL Amazon Ads] O oferece uma variedade de opções para ajudar você a atingir suas metas de publicidade para vendedores registrados, fornecedores, fornecedores de livros, autores de Kindle Direct Publishing (KDP), desenvolvedores de aplicativos e/ou agências.

A variável [!DNL Amazon Ads] integração com o Adobe Experience Platform fornece integração pronta para uso para [!DNL Amazon Ads] incluindo o Amazon DSP (ADSP) e o Amazon Marketing Cloud (AMC).

Usar o [!DNL Amazon Ads] destino no Adobe Experience Platform, os usuários podem definir públicos-alvo do anunciante para direcionamento e ativação no Amazon DSP.  Além disso, os usuários podem fazer upload de seus dados no [!DNL Amazon Marketing Cloud] para entender o desempenho por público-alvo, dimensões fornecidas pelo anunciante, associação a segmentos do Amazon ou outros sinais disponíveis na AMC. Depois de fazer upload dos públicos-alvo do anunciante para a AMC, os usuários podem usar [!DNL Amazon Marketing Cloud] para modificar, aprimorar ou anexar a membros do público usando sinais do Amazon de dentro do [!DNL Amazon Marketing Cloud].

A AMC reúne sinais únicos de todas as propriedades próprias e operadas da Amazon, abrangendo mídia, incluindo exibição, vídeo, transmissão de TV, áudio e anúncios patrocinados. Os usuários podem enviar facilmente segmentos com curadoria do Adobe Experience Platform para a AMC a fim de aprimorar o aprendizado, como grupos dentro do mercado, coortes de estilo de vida e padrões de engajamento da marca. Segmentos aumentados podem ser usados para otimizar ativações de mídia no Amazon DSP.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo *[!DNL Amazon Ads]* equipe. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o *[!DNL Amazon Ads]* destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Ativação e direcionamento {#activation-and-targeting}

Essa integração com o Amazon DSP permite [!DNL Amazon Ads] anunciantes passem públicos-alvo de CDP do anunciante do Adobe Experience Platform para o DSP da Amazon para criar públicos-alvo de anunciantes com direcionamento de publicidade. Os públicos podem ser selecionados no DSP do Amazon para direcionamento positivo, bem como direcionamento negativo (supressão).

### Analytics e Measurement {#analytics-and-measurement}

Essa integração com [!DNL Amazon Marketing Cloud] (AMC) permite [!DNL Amazon Ads] anunciantes passarem segmentos de CDP do formulário do Adobe Experience Platform para a AMC. Os anunciantes podem então se associar às entradas de CDP com [!DNL Amazon Ads] O sinaliza e faz análises personalizadas em tópicos como impacto de mídia, segmentos de público-alvo e jornadas do cliente em formato compatível com a privacidade. Por exemplo, um anunciante pode fazer upload de uma lista de seus clientes existentes para entender o desempenho agregado da campanha de publicidade ou estatísticas agregadas de eventos de conversão no Amazon, como visualizar uma página de detalhes do produto, adicionar um produto a um carrinho de compras ou comprar um produto.

### Otimização de publicidade:

Essa integração com [!DNL Amazon Marketing Cloud] (AMC) permite que os anunciantes façam upload de suas próprias listas de clientes e usem [!DNL Amazon Marketing Cloud] SQL, executar análise de sobreposição, supressões, adições ou otimizações para públicos-alvo de forma recorrente antes de criar um público pronto para ativação no Amazon DSP para direcionamento.

## Pré-requisitos {#prerequisites}

Para usar o [!DNL Amazon Ads] com o Adobe Experience Platform, os usuários devem primeiro ter acesso a uma conta de anunciante do Amazon DSP ou a uma [!DNL Amazon Marketing Cloud] instância. Para provisionar essas instâncias, visite a seguinte página no [!DNL Amazon Ads] site:

* [Introdução ao Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Introdução ao Amazon Marketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identidades suportadas {#supported-identities}

A variável *[!DNL Amazon Ads]* A conexão suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service//features/namespaces.md). Para obter mais detalhes sobre as identidades compatíveis com o [!DNL Amazon Ads], visite o [Centro de suporte ao Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no *[!DNL Amazon Ads]* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

Você é levado para o [!DNL Amazon Ads] interface de conexão na qual você seleciona primeiro as contas de anunciante às quais deseja se conectar. Após a conexão, você será redirecionado de volta ao Adobe Experience Platform com uma nova conexão, fornecida com a ID da conta do anunciante selecionada. Selecione a Conta do anunciante apropriada na tela de configuração de destino para continuar.

* **[!UICONTROL Token de portador]**: Preencha o token do portador para autenticar no destino.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Conexão do Amazon Ads]**: selecione a ID do público alvo [!DNL Amazon Ads] conta usada para o destino.

>[!NOTE]
>
>Depois de salvar a configuração de destino, você não poderá alterar a variável [!DNL Amazon Ads] ID do anunciante, mesmo se você reautenticar por meio da sua conta da Amazon. Para usar um [!DNL Amazon Ads] ID do anunciante, você deve criar uma nova conexão de destino.

* **[!UICONTROL Região do anunciante]**: selecione a região apropriada na qual seu Anunciante está hospedado. Para obter mais informações sobre os mercados apoiados por cada região, visite o [Documentação do Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configurar novo destino](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos e identidades {#map}

A variável [!DNL Amazon Ads] A conexão aceita endereços de email com hash e números de telefone com hash para fins de correspondência de identidade. A captura de tela abaixo fornece um exemplo de correspondência compatível com o [!DNL Amazon Ads] conexão:

![Mapeamento de Adobe para anúncios do Amazon](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para mapear endereços de email com hash, selecione a `Email_LC_SHA256` namespace de identidade como um campo de origem.
* Para mapear números de telefone com hash, selecione o `Phone_SHA256` namespace de identidade como um campo de origem.
* Para mapear endereços de email com hash ou números de telefone, selecione os namespaces de identidade correspondentes como campos de origem e verifique a `Apply Transformation` opção para que o Platform coloque as identidades em hash na ativação.

Você só seleciona um determinado campo de destino uma vez em uma configuração de destino do [!DNL Amazon Ads] conector.  Por exemplo, se você enviar um email comercial, não poderá mapear o email pessoal na mesma configuração de destino.

É altamente recomendável mapear quantos campos estiverem disponíveis. Se apenas um atributo de origem estiver disponível, você poderá mapear um único campo. A variável [!DNL Amazon Ads] o destino utiliza todos os campos mapeados para fins de mapeamento, produzindo taxas de correspondência mais altas se mais campos forem fornecidos. Para obter mais informações sobre os identificadores aceitos, visite o [Página de ajuda do público-alvo com hash do Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que o público-alvo for carregado, você poderá validar se o público-alvo foi criado e carregado corretamente usando estas etapas:

**Para o Amazon DSP**

Navegue até o **[!UICONTROL ID do anunciante]** > **[!UICONTROL Públicos-alvo]** > **[!UICONTROL Públicos-alvo do anunciante]**. Se o público-alvo for criado com sucesso e atender ao número mínimo de membros do público-alvo, você verá um Status de `Active`. Detalhes adicionais sobre o tamanho e o alcance do seu público-alvo podem ser encontrados no painel Alcance previsto no lado direito da interface do usuário do Amazon DSP.

![Validação da criação de público do Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Para[!DNL Amazon Marketing Cloud]**

No navegador de esquema esquerdo, encontre seu público-alvo em **[!UICONTROL Anunciante carregado]** > **[!UICONTROL aep_audiences]**. Você pode então consultar seu público no editor AMC SQL com a seguinte cláusula:

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Validação da criação de público-alvo do Amazon Marketing Cloud](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter a documentação de ajuda adicional, visite o seguinte [!DNL Amazon Ads] recursos de ajuda:

* [Centro de ajuda do Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Esta seção captura a funcionalidade e as atualizações de documentação significativas feitas neste conector de destino.

+++ Exibir changelog

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Março de 2024 | Atualização de funcionalidade e documentação | Adicionada a opção de exportar públicos-alvo para serem usados no [!DNL Amazon Marketing Cloud] AMC). |
| Maio de 2023 | Atualização de funcionalidade e documentação | <ul><li>Adição de suporte para a seleção da Região do anunciante no [fluxo de trabalho da conexão de destino](#destination-details).</li><li>Atualização da documentação para refletir a adição da seleção da Região do anunciante. Para obter mais informações sobre como selecionar a Região do anunciante correta, consulte [Documentação do Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Março de 2023 | Versão inicial | Versão inicial de destino e documentação publicada. |

{style="table-layout:auto"}

+++
