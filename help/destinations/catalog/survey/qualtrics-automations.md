---
keywords: transmissão, destino Qualtrics
title: Automações do Qualtrics
description: Sincronize a experiência e os dados operacionais do cliente para desbloquear a personalização em escala. Use a agregação de várias fontes de dados operacionais no Adobe Experience Platform como uma entrada no Qualtrics Experience ID para entender melhor seus clientes e permitir que o alcance direcionado feche a lacuna quando se trata de entender a intenção, a emoção e os impulsionadores de experiência.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---

# Automações do Qualtrics

## Visão geral {#overview}

Sincronize a experiência e os dados operacionais do cliente para desbloquear a personalização em escala.

Use a agregação de várias fontes de dados operacionais no Adobe Experience Platform como uma entrada no Qualtrics Experience ID para entender melhor seus clientes e permitir que o alcance direcionado feche a lacuna quando se trata de entender a intenção, a emoção e os impulsionadores de experiência.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe do Qualtrics. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com eles fazendo logon na [Hub de sucesso do cliente](https://support-portal.qualtrics.com/).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o *Automações do Qualtrics* destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1 {#use-case-1}

**Cenário**: uma empresa deseja medir a satisfação do cliente em vários pontos de contato digitais, como seu site e aplicativo móvel. Eles usam o Adobe Experience Platform para acionar pesquisas do Qualtrics com base nas interações do usuário, como concluir uma compra ou visitar uma página da Web específica.

**Resultado**: ao coletar feedback em tempo real, a empresa pode fazer melhorias orientadas por dados na experiência do cliente, resultando em maior satisfação e fidelidade.

### Caso de uso #2 {#use-case-2}

**Cenário**: uma organização tem como objetivo aprimorar o processo de integração de funcionários. Eles utilizam o Adobe Experience Platform para coletar feedback de novas contratações por meio de pesquisas do Qualtrics. As pesquisas são acionadas automaticamente após um período de integração predefinido.

**Resultado**: o feedback contínuo permite que a organização adapte e melhore o processo de integração, resultando em melhor engajamento e produtividade entre os novos funcionários.

## Pré-requisitos

Antes de configurar o destino do Qualtrics no Adobe Experience Platform, verifique se os seguintes pré-requisitos foram atendidos:

* Você tem uma conta do Qualtrics.
* Você obteve o token de API necessário do Qualtrics.

### Obtenção de um token de API

Abaixo estão as etapas necessárias para obter um token de API do Qualtrics.

1. Faça logon na sua conta do Qualtrics.
2. Ir para **Configurações da conta**.
3. Selecionar **IDs do Qualtrics**.
4. Nesta página, procure por **API** seção, contém uma **Token** campo. Este é o token da API e será necessário durante a configuração de destino.

## Identidades suportadas {#supported-identities}

*Automações do Qualtrics* O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email | Endereços de email de texto sem formatação | O Qualtrics oferece suporte somente a endereços de email de texto simples. |
| external_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no *Automações do Qualtrics* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Como parte da autenticação, você precisará fornecer uma **Nome de usuário** e **Senha**. O nome de usuário é seu nome de usuário do Qualtrics e a senha é o token de API da sua conta do Qualtrics. Para recuperar o token da API, siga as instruções do **Pré-requisitos** acima.

![Autenticação](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL URL]**: O URL encontrado no [Evento JSON](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) que aciona o [fluxo de trabalho no Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Consulte a captura de tela abaixo para ver um exemplo.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

Esse destino tem um esquema aberto, portanto, você pode enviar quaisquer propriedades para o Qualtrics.

#### Mapear atributos

Para adicionar um atributo ao mapeamento, basta selecionar **atributos personalizados** ao adicionar um novo mapeamento. Você pode inserir qualquer nome para o seu atributo. O Qualtrics incentiva a *camelCase* convenção de nomenclatura para nomes de atributo (veja abaixo a captura de tela para ver um exemplo).

![Atributo personalizado](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Consulte a captura de tela abaixo para obter um exemplo de possíveis mapeamentos de atributos.

![Exemplo de mapeamentos](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mapear identidades

É obrigatório selecionar um namespace de identidade para este destino. Os dois possíveis mapeamentos de campo de origem para campo de destino são:

| Campo de origem | Campo de destino |
|--------------------|-----------------------|
| IdentityMap: email | Identidade: email |
| IdentityMap: ECID | Identidade: external_id |

Consulte a captura de tela abaixo para ver um exemplo.

![Namespace de identidade](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Como mencionado anteriormente, esse destino usa um esquema aberto, de modo que quaisquer propriedades podem ser enviadas para o Qualtrics. No entanto, os dados enviados para o Qualtrics seguirão a estrutura abaixo:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Para verificar se os dados foram assimilados no Qualtrics, vá para o fluxo de trabalho que contém seus **Evento JSON**, a partir daí, vá para **Executar histórico** onde você deve ver as execuções do seu fluxo de trabalho. Cada workflow tem um status de **Com êxito** ou **Failed**. Selecionar uma execução específica revelará mais informações sobre ela, permitindo que você solucione problemas caso tenha algum problema.

Se não houver execuções visíveis no **Executar histórico** Portanto, significa que o workflow ainda não foi acionado, indicando que pode haver um problema. Verifique se o workflow está ativado e se **URL** no destino no Adobe Experience Platform está correto. As execuções de fluxo de trabalho não são instantâneas, portanto, talvez seja necessário aguardar um pouco antes de concluí-lo.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).
