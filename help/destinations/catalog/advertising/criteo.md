---
keywords: publicidade, critério,
title: Conexão de critério
description: O Criteo capacita a publicidade confiável e impactante para trazer experiências mais ricas para cada consumidor através da internet aberta. Com o maior conjunto de dados de comércio do mundo e a melhor IA do setor, o Criteo garante que cada ponto de contato na jornada de compras seja personalizado para alcançar os clientes com o anúncio certo, na hora certa.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# (Beta) Conexão de critério

## Visão geral {#overview}

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela Criteo. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para qualquer consulta ou solicitação de atualização, contate o Critério diretamente [aqui](mailto:criteoTechnicalPartnerships@criteo.com).

O Criteo capacita a publicidade confiável e impactante para trazer experiências mais ricas para cada consumidor através da internet aberta. Com o maior conjunto de dados de comércio do mundo e a melhor IA do setor, o Criteo garante que cada ponto de contato na jornada de compras seja personalizado para alcançar os clientes com o anúncio certo, na hora certa.

## Pré-requisitos {#prerequisites}

* Você precisa ter uma conta de usuário administrador no [Centro de Gerenciamento de Critérios](https://marketing.criteo.com).
* Você precisará da sua ID de anunciante da Criteo (pergunte ao contato da Criteo se não tiver essa ID).
* Você precisará fornecer [!DNL GUM caller ID], caso queira usar [!DNL GUM ID] como identificador.

## Limitações {#limitations}

* O critério aceita apenas emails com hash [!DNL SHA-256] e de texto sem formatação (a serem transformados em [!DNL SHA-256] antes do envio). Não envie informações de identificação pessoal (como nomes ou números de telefone).
* O critério precisa de pelo menos um identificador a ser fornecido pelo cliente. Ele prioriza [!DNL GUM ID] como identificador em vez de email com hash, pois contribui para uma melhor taxa de correspondência.

![Pré-requisitos](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identidades suportadas {#supported-identities}

O critério é compatível com a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidade de destino | Descrição | Considerações |
| --- | --- | --- |
| `email_sha256` | Endereços de email com hash com o algoritmo SHA-256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA-256. Quando o campo de origem contiver atributos sem hash, marque a opção [!UICONTROL Aplicar transformação] para que o Platform coloque os dados em hash automaticamente durante a ativação. |
| `gum_id` | Identificador de cookie do critério [!DNL GUM] | [!DNL GUM IDs] permite que os clientes mantenham uma correspondência entre seu sistema de identificação de usuário e a identificação de usuário do Critério ([!DNL UID]). Se o tipo de identificador for `gum_id`, um parâmetro adicional, o [!DNL GUM Caller ID], também deverá ser incluído. Entre em contato com a equipe de conta da Criteo para o [!DNL GUM Caller ID] apropriado ou para obter mais informações sobre esta sincronização [!DNL GUM ID], se necessário. |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportação | Exportação de público | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino [!DNL Criteo]. |
| Frequência de exportação | Transmissão | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](../../destination-types.md#streaming-destinations). |

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como usar o destino [!DNL Criteo], veja a seguir algumas metas que os clientes da Adobe Experience Platform podem alcançar com o [!DNL Criteo]:

### Caso de uso 1: obter tráfego

Mostre sua empresa com ofertas de produtos relevantes e criações flexíveis. Com recomendações de produtos inteligentes, seus anúncios apresentarão automaticamente os produtos com maior probabilidade de acionar visitas e engajamento. O direcionamento flexível permite criar públicos-alvo a partir do conjunto de dados de comércio da Criteo ou de suas próprias listas de clientes potenciais e segmentos da CDP Adobe.

### Caso de uso 2: aumentar as conversões de site

Quando os visitantes saírem do site, lembre-os do que estão perdendo com anúncios de redirecionamento que aumentam as conversões ao mostrar ofertas especiais e ofertas hiper-relevantes, onde quer que estejam. Conecte seu público-alvo da CDP do Adobe para reengajar clientes existentes ou direcionar consumidores semelhantes aos seus compradores mais fiéis.

## Conectar-se ao critério {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Autenticar para o critério

As etapas para se conectar são as seguintes:

1. Faça logon no Adobe Experience Platform e conecte-se ao destino do Critério.

   ![Fazer logon](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Você será redirecionado para Critério para autorizar a conexão. Talvez seja necessário primeiro fazer logon com suas credenciais de Critério:

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-3.png)


### Parâmetros de conexão {#connection-parameters}

Após a autenticação no destino, preencha os seguintes parâmetros de conexão.

![Parâmetros de conexão](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Campo | Descrição | Obrigatório |
| --- | --- | --- |
| Nome | Um nome para ajudá-lo a reconhecer este destino no futuro. O nome escolhido aqui será o nome [!DNL Audience] no Centro de Gerenciamento de Critérios e não poderá ser modificado posteriormente. | Sim |
| Descrição | Uma descrição para ajudar a identificar este destino no futuro. | Não |
| ID de anunciante | ID de anunciante de critérios de sua organização. Entre em contato com o gerente de conta da Criteo para obter essas informações. | Sim |
| Critério [!DNL GUM caller ID] | [!DNL GUM Caller ID] de sua organização. Entre em contato com a equipe de conta da Criteo para o [!DNL GUM Caller ID] apropriado ou para obter mais informações sobre esta sincronização [!DNL GUM], se necessário. | Sim, sempre que [!DNL GUM ID] for fornecido como um identificador |

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate-segments}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados {#exported-data}

Você pode ver os públicos exportados no [Centro de gerenciamento de critérios](https://marketing.criteo.com/audience-manager/dashboard).

O corpo da solicitação de adição de um perfil de usuário recebido pela conexão [!DNL Criteo] é semelhante a:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

O corpo da solicitação de remoção do perfil de usuário recebido pela conexão [!DNL Criteo] é semelhante a:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Uso e governança de dados {#data-usage}

Todos os destinos do Adobe Experience Platform estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como a Adobe Experience Platform fiscaliza a governança de dados, leia a [visão geral da Governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais

* [Central de ajuda do Criteo](https://help.criteo.com/kb/en)
* [Portal do Desenvolvedor de Critérios](https://developers.criteo.com)
