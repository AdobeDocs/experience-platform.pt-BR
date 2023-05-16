---
description: Saiba como configurar seu destino para as configurações de mapeamento de identidade e atributo suportadas.
title: Configurações de mapeamento suportadas
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Configurações de mapeamento suportadas

Os destinos criados com o Destination SDK suportam configurações específicas de namespace de identidade e mapeamento de atributos, com base no tipo de destino.

Este artigo descreve todas as configurações de mapeamento compatíveis que podem ser usadas ao configurar seu destino.

>[!WARNING]
>
>Qualquer configuração de mapeamento não descrita neste artigo não é suportada pelo Destination SDK.

Ao criar seu destino, configure seu esquema e namespaces de identidade de acordo com uma das configurações de mapeamento descritas nesta página.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Mapeamentos compatíveis para destinos de streaming {#streaming-mappings}

Os destinos em tempo real (streaming) criados com o Destination SDK suportam as configurações de mapeamento descritas na tabela abaixo.

| Campo de origem | Campo de destino |
| --- | --- |
| Atributo XDM | Atributo personalizado |
| Namespace de identidade | Namespace de identidade |

O exemplo de configuração abaixo permite que os clientes usem ambos os mapeamentos na tabela acima.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Mapear atributos XDM para atributos personalizados {#streaming-xdm-to-custom}

Os usuários podem mapear atributos do perfil XDM de origem para atributos personalizados no lado do destino.

Os usuários devem inserir manualmente o nome do atributo personalizado de destino ao selecionar o mapeamento do campo de destino.

![Captura de tela da interface do usuário da plataforma que mostra a seleção personalizada do atributo.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do atributo XDM para atributos personalizados para destinos de transmissão.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Mapear namespaces de identidade para namespaces de identidade do parceiro {#streaming-identity-to-identity}

Os usuários podem mapear namespaces de identidade personalizados ou globais da Plataforma para namespaces de identidade definidos por você.

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Captura de tela da interface do usuário da plataforma que mostra o mapeamento de identidade para destinos de transmissão.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Mapeamentos suportados para destinos baseados em arquivo {#batch-mappings}

Os destinos com base em arquivo criados com o Destination SDK suportam as configurações de mapeamento descritas na tabela abaixo. Consulte as próximas seções para obter exemplos detalhados de mapeamento.

| Campo de origem | Campo de destino |
| --- | --- |
| Atributo XDM | Atributo / Atributo personalizado |
| Namespace de identidade | Atributo / Atributo personalizado |
| Namespace de identidade | Namespace de identidade |

O exemplo de configuração abaixo permite que os clientes usem todos os mapeamentos da tabela acima.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Mapear atributos XDM para atributos personalizados {#batch-xdm-to-custom}

Os usuários podem mapear atributos do perfil XDM de origem para atributos personalizados no lado do destino.

Para destinos com base em arquivos, o campo de destino é preenchido automaticamente com um atributo padrão com o mesmo nome do campo de origem.

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Captura de tela da interface do usuário da plataforma que mostra o mapeamento XDM para atributos personalizados para destinos com base em arquivo.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Os usuários podem deixar o nome padrão no lugar ou inserir um nome de atributo personalizado na tela de seleção de campo de destino.

![Captura de tela da interface do usuário da plataforma que mostra a seleção de atributo de destino personalizado para destinos com base em arquivo.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Mapear namespaces de identidade para atributos personalizados {#batch-identity-to-custom}

Os usuários podem mapear namespaces de identidade personalizados ou globais da Platform para atributos personalizados no lado do destino.

Ao selecionar um namespace de identidade como um campo de origem, o campo de destino é automaticamente preenchido com um namespace de identidade equivalente. Para substituir o campo de destino por um atributo personalizado, os usuários devem inserir um nome de atributo personalizado na tela de seleção do campo de destino.

![Captura de tela da interface do usuário da plataforma que mostra a seleção de atributo de destino personalizado para destinos com base em arquivo.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Captura de tela da interface do usuário da plataforma que mostra o mapeamento de identidade para atributos personalizados para destinos com base em arquivo.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Mapear namespaces de identidade para namespaces de identidade do parceiro {#batch-identity-to-identity}

Os usuários podem mapear namespaces de identidade personalizados ou globais da Platform para namespaces de identidade equivalentes.

Ao selecionar um namespace de identidade como um campo de origem, o campo de destino é automaticamente preenchido com um namespace de identidade equivalente.

A experiência resultante da interface do usuário é mostrada na imagem abaixo.

![Captura de tela da interface do usuário da plataforma que mostra o mapeamento de identidade para destinos com base em arquivo.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão do que os mapeamentos são suportados por destinos criados com o Destination SDK.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)