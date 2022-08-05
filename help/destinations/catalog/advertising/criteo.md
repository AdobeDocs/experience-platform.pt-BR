---
keywords: publicidade; critérios;
title: Conexão de critério
description: O Criteo capacita a publicidade confiável e impactante para trazer experiências mais avançadas para todos os consumidores através da Internet aberta. Com o maior conjunto de dados de comércio do mundo e a melhor IA do setor, o Criteo garante que cada ponto de contato na jornada de compras seja personalizado para alcançar os clientes com o anúncio certo, na hora certa.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 8211ca28462548e1c17675e504e6de6f5cc55e73
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# (Beta) Conexão de critério

## Visão geral {#overview}

>[!IMPORTANT]
>
>Esta página de documentação foi criada por Criteo. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para quaisquer consultas ou pedidos de atualização, contacte diretamente o Criteo [here](mailto:criteoTechnicalPartnerships@criteo.com).

O Criteo capacita a publicidade confiável e impactante para trazer experiências mais avançadas para todos os consumidores através da Internet aberta. Com o maior conjunto de dados de comércio do mundo e a melhor IA do setor, o Criteo garante que cada ponto de contato na jornada de compras seja personalizado para alcançar os clientes com o anúncio certo, na hora certa.

## Pré-requisitos {#prerequisites}

* Você precisa ter uma conta de usuário de administrador em [Centro de gerenciamento de critérios](https://marketing.criteo.com).
* Você precisará da ID do anunciante do Criteo (entre em contato com o Criteo se não tiver essa ID).
* Você precisará fornecer [!DNL GUM caller ID], caso queira usar [!DNL GUM ID] como identificador.

## Limitações {#limitations}

* Apenas aceita o critério [!DNL SHA-256]Emails com hash e texto sem formatação (a ser transformado em [!DNL SHA-256] antes de enviar). Não envie PII (Informações pessoais identificáveis, como nomes ou números de telefone).
* O critério precisa de pelo menos um identificador para ser fornecido pelo cliente. Ele prioriza [!DNL GUM ID] como identificador por email com hash, pois contribui para uma melhor taxa de correspondência.

![Pré-requisitos](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identidades suportadas {#supported-identities}

O critério suporta a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade do Target | Descrição | Considerações |
| --- | --- | --- |
| `email_sha256` | Endereços de email com hash com o algoritmo SHA-256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA-256. Quando o campo de origem contém atributos com hash, verifique a [!UICONTROL Aplicar transformação] , para que a Platform faça o hash automático dos dados na ativação. |
| `gum_id` | Critério [!DNL GUM] identificador de cookie | [!DNL GUM IDs] permitir que os clientes mantenham uma correspondência entre o seu sistema de identificação de utilizador e a identificação de utilizador de Criteo ([!DNL UID]). Se o tipo de identificador for `gum_id`, um parâmetro adicional, a variável [!DNL GUM Caller ID], deve também ser incluído. Entre em contato com a equipe de conta do Criteo para obter as informações apropriadas [!DNL GUM Caller ID] ou para obter mais informações sobre isso [!DNL GUM ID] sincronizar, se necessário. |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportação | Exportar segmento | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na [!DNL Criteo] destino. |
| Frequência de exportação | Streaming | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](../../destination-types.md#streaming-destinations). |

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como usar a variável [!DNL Criteo] destino, aqui estão algumas metas que os clientes da Adobe Experience Platform podem alcançar com [!DNL Criteo]:

### Caso de uso 1 : Obter tráfego

Mostre sua empresa com ofertas de produtos relevantes e criações flexíveis. Com recomendações inteligentes de produtos, seus anúncios exibirão automaticamente os produtos com maior probabilidade de acionar visitas e envolvimento. O direcionamento flexível permite criar públicos-alvo a partir do conjunto de dados de comércio do Criteo ou de suas próprias listas de prospecto e segmentos de CDP do Adobe.

### Caso de uso 2 : Aumentar conversões do site

Quando os visitantes saírem do seu site, lembre-os do que estão faltando com o redirecionamento de anúncios que aumenta as conversões mostrando ofertas especiais e ofertas hiper-relevantes, onde quer que sejam. Conecte seu segmento de CDP do Adobe para engajar novamente clientes existentes ou direcionar consumidores semelhantes aos seus compradores mais leais.

## Conectar-se ao Critério {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Autenticar para o critério

As etapas para conexão são as seguintes:

1. Faça logon no Adobe Experience Platform e se conecte ao destino Criteo.

   ![Fazer logon](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Você será redirecionado para Criteo para autorizar a conexão. Talvez seja necessário fazer logon primeiro com suas credenciais de Critério:

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Logon de critério](../../assets/catalog/advertising/criteo/log-in-3.png)


### Parâmetros de conexão {#connection-parameters}

Depois de autenticar para o destino, preencha os seguintes parâmetros de conexão.

![Parâmetros de conexão](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Campo | Descrição | Obrigatório |
| --- | --- | --- |
| Nome | Um nome para ajudá-lo a reconhecer esse destino no futuro. O nome escolhido aqui será o [!DNL Audience] no Centro de Gestão de Projetos e não pode ser modificado numa fase posterior. | Sim |
| Descrição | Uma descrição para ajudar a identificar esse destino no futuro. | Não |
| ID do anunciante | ID de anunciante de critério da sua organização. Entre em contato com o gerente de conta do Criteo para obter essas informações. | Sim |
| Critério [!DNL GUM caller ID] | [!DNL GUM Caller ID] da sua organização. Entre em contato com a equipe de conta do Criteo para obter as informações apropriadas [!DNL GUM Caller ID] ou para obter mais informações sobre isso [!DNL GUM] sincronizar, se necessário. | Sim, sempre [!DNL GUM ID] é fornecido como um identificador |

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate-segments}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Você pode ver os segmentos exportados na variável [Centro de gestão de critérios](https://marketing.criteo.com/audience-manager/dashboard).

O corpo da solicitação de adicionar um perfil de usuário recebido pela [!DNL Criteo] a conexão é semelhante a esta:

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

O corpo da solicitação de remoção do perfil do usuário recebido pela [!DNL Criteo] a conexão é semelhante a esta:

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

Todos os destinos do Adobe Experience Platform são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como o Adobe Experience Platform aplica o controle de dados, leia a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Recursos adicionais

* [Central de ajuda de critérios](https://help.criteo.com/kb/en)
* [Portal do desenvolvedor de critérios](https://developers.criteo.com)
