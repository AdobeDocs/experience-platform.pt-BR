---
title: Visão geral da extensão do Adobe Experience Cloud Identity Service
description: Saiba mais sobre a extensão de tag do Adobe Experience Cloud Identity Service no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 94%

---

# Visão geral da extensão do Adobe Experience Cloud Identity Service

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Use essa referência para obter informações sobre como configurar a extensão da Adobe Experience Cloud ID e as opções disponíveis ao usar essa extensão para criar uma regra.

Use essa extensão para integrar o Experience Cloud Identity Service às suas propriedades. Com o Experience Cloud Identity Service, você pode criar e armazenar identificadores únicos e persistentes para os visitantes do site.

## Configurar a extensão do Experience Cloud ID

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão do Experience Cloud ID.

Se a extensão Experience Cloud ID ainda não estiver instalada, abra a propriedade e selecione **[!UICONTROL Extensões > Catálogo]**, passe o mouse sobre a extensão Experience Cloud ID e selecione **[!UICONTROL Instalar]**.

Para configurar a extensão, abra a guia Extensões, passe o mouse sobre a extensão e selecione **[!UICONTROL Configurar]**.

![](../../../images/optin.jpg)

As opções de configuração disponíveis são as seguintes:

### ID da organização da Experience Cloud

A ID da organização da Experience Cloud.

Sua ID é uma sequência de 24 caracteres alfanuméricos, seguidos por `@AdobeOrg`. Caso não reconheça essa ID, entre em contato com o Atendimento do cliente.

### Excluir caminhos específicos

A Experience Cloud ID não carrega se o URL corresponder a nenhum dos caminhos especificados.

(Opcional) Ative o Regex se esta for uma expressão regular.

Selecione **[!UICONTROL Adicionar]** para excluir outro caminho.

### Aceitar

Use as opções de Aceitar para determinar se os visitantes devem aceitar em participar dos serviços da Adobe em seu site, incluindo se eles desejam criar cookies que rastreiam as atividades do visitante.

A aceitação é o ponto de referência centralizado para todas as bibliotecas do lado do cliente da solução da plataforma para determinar se os cookies podem ser criados no dispositivo ou no navegador de um usuário quando ele visita o seu site. A opção Aceitar não oferece suporte para coletar ou armazenar preferências de consentimento do usuário.

**Habilitar Aceitar?**

A opção selecionada determina se o site aguardará por consentimento para rastrear as atividades de um visitante em seu site.

Existem três opções:

* **Não:** não aguarda por consentimento para rastrear o visitante. Esse é o comportamento padrão se você não selecionar uma opção.
* **Sim:** aguarda por consentimento para rastrear o visitante.
* **Determinado uso da função no tempo de execução:** determine de maneira programada se o valor é verdadeiro ou falso durante o tempo de execução. Se você selecionar essa opção, o campo Selecionar elemento de dados ficará disponível. Selecione um elemento de dados que pode determinar a espera por consentimento. Esse elemento de dados resolve um valor booliano. Por exemplo, você pode selecionar um elemento de dados que oferece consentimento a depender de onde país do visitante está localizado na UE.

**A opção Aceitar armazenamento está ativada?**

Se ativada, o consentimento é armazenado em um cookie primário em seu domínio. Se não estiver ativado, as configurações de consentimento serão mantidas em seu CMP ou em um cookie que você gerencia.

**Aceitar Domínio de cookie?**

Use essa configuração opcional para especificar o domínio onde o cookie da opção Aceitar é armazenado se o armazenamento estiver ativado. Você pode inserir um domínio ou selecionar um elemento de dados que contenha o domínio.

**Expiração de armazenamento da opção Aceitar?**

Especifique quando o cookie da opção Aceitar expira (valor em segundos) se o armazenamento estiver ativado.

Digite um número e selecione uma unidade de tempo na lista suspensa. Por exemplo, digite 2 e selecione **[!UICONTROL Semanas]**. O padrão é 13 meses.

**Permissões?**

Enviar consentimento anterior para a biblioteca da opção Aceitar. Selecione um elemento de dados que contém o consentimento. O tipo de elemento deve ser um objeto ou uma string JSON. Substitui as aprovações de pré-aceitação.

Exemplo:

`"{"aa":true,"aam":true,"ecid":true}"`

**Aprovações de pré-aceitação?**

Defina quais categorias são aprovadas ou negadas quando nenhuma preferência foi definida pelo visitante. O consentimento é presumido pelas soluções selecionadas a partir do momento em que a página é carregada. O tipo de elemento deve ser um objeto ou uma string JSON (exemplo: `{aam: true}`).

### Variáveis

Defina pares nome-valor como propriedades da instância do Experience Cloud ID. Use o menu suspenso para selecionar uma variável e, em seguida, digite ou selecione um valor. Para obter informações sobre cada variável, consulte a [documentação do Experience Cloud Identity Service](https://experiencecloud.adobe.com/resources/help/pt_BR/mcvid/mcvid-overview.html).

## Tipos de ação de extensão do Experience Cloud ID

Esta seção descreve os tipos de ação disponíveis na extensão do Experience Cloud ID.

### Tipos de ação

#### Definição das IDs de cliente

Defina uma ou mais IDs do cliente.

1. Insira o código de integração.

   O código de integração deve conter o valor configurado como fonte de dados no Audience Manager ou em Atributos do cliente.

1. Selecione um valor.

   O valor deve ser uma ID de usuário. Os elementos de dados são mais adequados para valores dinâmicos, como IDs de um sistema interno específico do cliente.

1. Selecione um estado de autenticação.

   As opções disponíveis são:

   * Desconhecido
   * Autenticado
   * Logout realizado

1. (Opcional) Selecione **[!UICONTROL Adicionar]** para definir mais IDs de cliente.
1. Selecione **[!UICONTROL Manter alterações]**.
