---
title: Acxiom Real ID Audience Connection
description: Use o  [!DNL Acxiom Real ID Audience Connection] destino para aprimorar públicos-alvo com a  [!DNL Acxiom's Real ID] tecnologia e ativar públicos-alvo para várias plataformas, como  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e muito mais.
badge: label="Beta" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: fda542e62c448788099d63951277278a146fdfc8
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 3%

---

# [!DNL Acxiom Real ID Audience Connection] destino

>[!NOTE]
>
>O destino [!DNL Acxiom Real ID Audience Connection] está na versão beta. Esse conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Acxiom]. Para fazer consultas ou solicitações de atualização, entre em contato diretamente com a Acxiom [aqui](mailto:acxiom-adobe-help@acxiom.com).

Use o destino [!DNL Acxiom Real ID Audience Connection] para aprimorar públicos com a tecnologia [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) e ativar públicos para várias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e muito mais.

Este tutorial fornece instruções para criar um conector de destino [!DNL Acxiom Real ID Audience Connection] usando a interface do usuário [!DNL Adobe Experience Platform]. Esse conector é usado para criar e distribuir públicos-alvo para destinos selecionados.

## Casos de uso {#use-cases}

Esse conector é compatível com clientes que têm o Acxiom Real Identity carregado na Real-Time CDP como um identificador. Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Acxiom Real ID Audience Connection], este é um exemplo de caso de uso que os clientes [!DNL Adobe Experience Platform] podem resolver usando este conector.

### Enviar públicos-alvo do Experience Platform para a sua conta da Acxiom {#send-audiences}

Use este conector de destino se você for um profissional de marketing que deseja enviar públicos-alvo de [!DNL Experience Platform] para sua conta do [!DNL Acxiom], para aquisição entre canais.

Por exemplo, o departamento de Operações de marketing de uma marca global de serviços financeiros está interessado na aquisição de clientes entre canais por meio de várias plataformas de publicidade. Eles podem usar o conector de destino [!DNL Acxiom Real ID Audience Connection] para enviar públicos de [!DNL Experience Platform] para [!DNL Acxiom], aprimorar os públicos com a tecnologia [!DNL Acxiom's Real ID] e ativar os públicos para várias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e muito mais.


## Pré-requisitos {#prerequisites}

* **Confirmar Termos de Uso:** Antes de configurar um novo destino do [!DNL Acxiom Real ID Audience Connection], você deve ler e assinar o Contrato de Termos de Uso do [!DNL Acxiom's]. Você receberá o link para o contrato assim que a ordem de venda executada for concluída. Até que você assine o contrato, você não verá o cartão de destino [!DNL Acxiom Real ID Audience Connection] no catálogo de destino do Experience Platform. Depois que você aceitar e assinar o contrato, o [!DNL Adobe] concluirá o processo de integração e você verá o cartão de destino [!DNL Acxiom Real ID Audience Connection].
* **Conhece sua ID da organização da Adobe:** Sua ID da organização [!DNL Adobe] é necessária para concluir seus Termos de Contrato do Usuário. Consulte o tópico [!DNL Adobe's] *Organizações na Experience Cloud* para obter detalhes sobre como [exibir a ID da sua organização](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Obter licença para o produto [!DNL Acxiom's Real ID]:** depois que a licença for obtida, disponibilize a Real ID da Acxiom no Real-Time CDP. Consulte [Acxiom Data Enhancement](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement) para obter mais informações.


## Identidades suportadas {#supported-identities}

O destino [!DNL Acxiom's Real ID Audience Connection] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces).

| Identidade de destino | Descrição | Considerações |
|---------------|----------------|----------------|
| ID real | [!DNL Acxiom Real ID] | Selecione essa identidade de destino quando a identidade de origem for um namespace da Acxiom Real ID. |
| extern_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------------|----------------|----------------|
| Serviço de segmentação | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](https://experienceleague.adobe.com/pt-br/docs/experience-platform/segmentation/home) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal#import-audience) para o Experience Platform de arquivos CSV. |


## Destinos compatíveis {#supported-destinations}

Atualmente, o destino [!DNL Acxiom's Real ID Audience Connection] oferece suporte à ativação de público-alvo para as seguintes plataformas.

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Conectar ao destino {#connect}

A autenticação para o destino [!DNL Acxiom's Real ID Audience Connection] é tratada automaticamente em segundo plano para sua conveniência.

## Configurações específicas de destino {#destination-settings}

Alguns destinos do [!DNL Acxiom Real ID Audience Connection] exigem informações adicionais. As seções abaixo fornecem orientação detalhada sobre como configurar essas opções.

### [!DNL LG Ads] {#lg-ads}

Para configurar detalhes para o destino, preencha os campos abaixo.

* **Categoria do segmento**: a categoria ou vertical de destino na qual seu segmento se enquadra. Exemplo: serviços financeiros, automotivo, saúde, etc.

![Detalhes de destino do LG Ads](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}



Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) para obter instruções sobre como ativar públicos-alvo para esse destino.

>[!NOTE]
>
>O destino [!DNL Acxiom Real ID Audience Connection] dá suporte apenas a exportações completas de arquivos.


### Mapear atributos e identidades {#map}

Para que o destino [!DNL Acxiom Real ID Audience Connection] receba corretamente os dados de público-alvo, você deve mapear o campo de origem do Experience Platform para o campo de destino [!DNL Acxiom Real ID Audience Connection] correto.

[!DNL Acxiom Real ID Audience Connection] permite mapeamento somente para o seguinte campo de destino.

| Nome do campo | Descrição | Obrigatório |
|--------------------|------------|--------| 
| ID real | Uma ID real é um identificador alfanumérico (ID) exclusivo de 36 bytes do gráfico de resolução de identidade proprietário da Acxiom, semelhante a uma chave primária para um banco de dados relacional. É um identificador que representa uma pessoa, residência ou endereço. | Sim |



Na coluna **[!UICONTROL Source Field]**, digite o nome do atributo de origem que você deseja mapear para o campo de destino correspondente ou selecione o ícone de seta para abrir a tela **[!UICONTROL  Select source field]**. Em seguida, selecione **[!UICONTROL Next]**.
![Tela de mapeamento](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


Se você não estiver usando o esquema padrão [!DNL Adobe's], consulte a documentação do [Guia da Interface do Usuário do Serviço de Consulta](../../../query-service/ui/overview.md) para obter informações sobre como usar o serviço de consulta para preencher o esquema padrão [!DNL Adobe] com seus nomes de campo.


### Revisar {#review}

Depois de concluir todas as etapas acima, você terá a oportunidade de revisar o status da conexão de destino e os detalhes do público-alvo antes de ativá-lo (distribuí-lo). Os públicos selecionados aparecerão na parte inferior de uma lista. Cada público será uma chamada separada para a API [!DNL Acxiom Real ID Audience Connection].

Se você estiver satisfeito com os resultados, selecione **[!UICONTROL Finish]** para ativar seu destino.

![Revise seu público-alvo](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Solução de problemas {#troubleshooting}

Se o representante de destino não puder localizar o público-alvo, contate o representante do [!DNL Adobe] para obter assistência.

Será necessário fornecer as seguintes informações ao representante do [!DNL Adobe]:

* Nome do público-alvo
* Nome do destino
* Data de ativação do público
* Nome do arquivo exportado

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você ativou com êxito um público-alvo para a plataforma de destino selecionada. Em seguida, entre em contato com o representante da plataforma de destino para começar a configurar o Campaign.
