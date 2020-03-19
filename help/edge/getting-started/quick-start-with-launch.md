---
title: Início rápido com o Launch
seo-title: Início rápido do SDK da Web do Adobe Experience Platform com o Launch
description: Guia de início rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
seo-description: Guia de início rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# Pré-requisitos (Beta)

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atualmente, o SDK da Web da plataforma Adobe Experience só oferece suporte ao envio de dados para a plataforma Adobe Experience usando o XDM. Você deve atender aos seguintes pré-requisitos.

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para o Analytics, use esse.
- Esteja qualificado para a Adobe Experience Platform
- Usar a versão mais recente do serviço de ID de visitante

## Preparar plataforma

Para poder enviar dados à Adobe Experience Platform, você deve criar um esquema XDM e um conjunto de dados que use esse esquema.

- [Crie um esquema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) com as seguintes combinações:
   - Detalhes da implementação do ExperienceEvent
   - Detalhes do ambiente ExperienceEvent
   - Detalhes da Web do ExperienceEvent
- Adicione a combinação do SDK da Web do Adobe Experience Platform ao esquema criado
- [Crie um conjunto de dados](https://platform.adobe.com/dataset/overview) com seu esquema no qual você gostaria que os dados chegassem

## Solicitação de uma ID de configuração

É necessário ter uma ID de configuração para usar o SDK. A ID de configuração garante que seus dados sejam roteados para o local certo. Você pode obter uma ID de configuração do seu consultor ou por meio do Client Care. Eles precisarão das seguintes informações:

- **ID da organização:** Você pode encontrar isso usando as instruções [aqui](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **ID do conjunto de dados:** Isso está disponível na interface do usuário do conjunto de dados quando você clica em um conjunto de dados
- **ID do esquema:** Isso está disponível no URL da tela de criação do esquema
- **Nome amigável:** Este é o nome amigável que será usado em interfaces futuras para esta configuração

## Instalar o SDK no Launch

Efetue login em Iniciar e instale a `AEP Web SDK` extensão. Como parte da instalação do SDK, você será solicitado a configurar a extensão. Insira a ID de configuração solicitada acima. A extensão preenche automaticamente a ID da empresa.

Para obter mais detalhes sobre diferentes opções de configuração, consulte [Configuração do SDK](../fundamentals/configuring-the-sdk.md).

## Enviar um evento

Depois que a extensão for instalada, comece a enviar eventos adicionando uma ação &quot;Send Beacon&quot; da extensão AEP Web SDK. É recomendável enviar pelo menos um evento sempre que uma página for carregada com a opção &quot;Ocorre no início de uma exibição&quot; marcada.

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de eventos](../fundamentals/tracking-events.md).

## Enviar dados

Você pode enviar dados que correspondam ao esquema criado anteriormente junto com seus eventos. Por exemplo, se você possuir um site de comércio e adicionar a combinação de comércio ao seu esquema, você enviará a seguinte estrutura quando alguém exibir um produto.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
