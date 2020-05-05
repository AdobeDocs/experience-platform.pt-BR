---
title: start rápido com o Launch
seo-title: start rápido do SDK da Web do Adobe Experience Platform com Launch
description: Guia de start rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
seo-description: Guia de start rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
translation-type: tm+mt
source-git-commit: e23b0ce9c20d5d2d770d1c1261fe08de5743325a

---


# Pré-requisitos (Beta)

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atualmente, o SDK da Web da plataforma Adobe Experience só oferece suporte ao envio de dados para a plataforma Adobe Experience usando o XDM. Você deve atender aos seguintes pré-requisitos.

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para o Analytics, use esse.
- Esteja qualificado para a Adobe Experience Platform
- Usar a versão mais recente do serviço de ID de Visitante

## Preparar plataforma

Para poder enviar dados para a Adobe Experience Platform, você deve criar um schema XDM e um conjunto de dados que use esse schema.

- [Crie um schema](../../xdm/tutorials/create-schema-ui.md) com as seguintes combinações:
   - Detalhes da implementação do ExperienceEvent
   - Detalhes do Ambiente ExperienceEvent
   - Detalhes da Web do ExperienceEvent
- Adicionar a combinação do SDK da Web da plataforma Adobe Experience ao schema criado
- [Crie um conjunto de dados](https://platform.adobe.com/dataset/overview) com seu schema onde você gostaria que os dados fossem aterrados

## Criar uma ID de configuração

Você pode criar uma ID de configuração usando a ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda na inicialização.

>Observação: Sua organização deve estar na lista de permissões do recurso. Entre em contato com o seu CSM para ser colocado na lista para uma eventual lista de permissões.

## Instalar o SDK no Launch

Efetue login em Iniciar e instale a `AEP Web SDK` extensão. Como parte da instalação do SDK, você será solicitado a configurar a extensão. Insira a ID de configuração solicitada acima. A extensão preenche automaticamente a ID da empresa.

Para obter mais detalhes sobre diferentes opções de configuração, consulte [Configuração do SDK](../fundamentals/configuring-the-sdk.md).

## Enviar um evento

Depois que a extensão é instalada, o start envia eventos adicionando uma ação &quot;Send Beacon&quot; da extensão AEP Web SDK. É recomendável enviar pelo menos um evento sempre que uma página for carregada com a opção &quot;Ocorre no start de uma visualização&quot; marcada.

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de Eventos](../fundamentals/tracking-events.md).

## Enviar dados

Você pode enviar dados que correspondem ao schema criado anteriormente junto com seus eventos. Por exemplo, se você possuir um site de comércio e adicionar a mistura de comércio ao seu schema, você enviará a seguinte estrutura quando alguém visualização um produto.

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
