---
title: Notas de versão para Tags
description: As notas de versão mais recentes de tags na Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 58%

---

# Notas de versão para tags no Adobe Experience Platform

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 15 de novembro de 2021

**Aceitar o código ES6 em Tags** - As extensões e o código personalizado contendo o código ES6 agora podem ser usados em Tags. No catálogo de extensões, você verá um rótulo ES6+ dentro do cartão de cada extensão que contém o código ES6. IE10 e IE11 não oferecem suporte ao código ES6. Antes de usar o código ES6 nas bibliotecas de tags, faça a análise necessária.

**Uso do Terser como compressor JavaScript** - Uglifier foi substituído por Terser. A partir desta versão, todas as bibliotecas de Tags serão minificadas pelo Terser.

## 21 de outubro de 2021

**Enviar dados para endpoints autenticados no encaminhamento de eventos** - Usando segredos, você pode enviar dados para endpoints que exigem os seguintes protocolos de autenticação:

* **[!UICONTROL Token]**: Uma única string de caracteres que representa um valor de token de autenticação.
* **[!UICONTROL HTTP simples]**: Contém dois atributos de string para um nome de usuário e senha.
* **[!UICONTROL OAuth2]**: Contém vários atributos para suportar a variável [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) especificações.

Para obter mais informações, consulte os guias em [gerenciamento de segredos na interface do usuário da coleção de dados](../ui/event-forwarding/secrets.md) ou [gerenciamento de segredos na API do reator](../api/guides/secrets.md).

## 19 de julho de 2021

**Ajustes para o direito &quot;Gerenciar propriedades&quot;** - O direito Gerenciar propriedades encontrou um problema em que um usuário tinha permissão para criar uma nova propriedade, mas não podia vê-la depois de ter sido criada (como descrito no encadeamento da comunidade [here](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). Uma correção agora está ativa com permissões sendo aplicadas, conforme descrito no artigo.

>[!NOTE]
>
>Se você atribuir o novo direito &quot;Editar propriedade&quot; a um grupo de usuários, a interface do usuário não será atualizada para ativar os campos na tela de configuração da propriedade. Uma correção para esse problema será implementada em uma versão futura.

## 17 de maio de 2021

**Melhor tratamento das alterações não salvas** — sempre que você saía de uma exibição de configurações (extensões, elementos de dados e componentes de regras), recebia um aviso sobre se queria descartar as alterações. Porém, a lógica para determinar isso não era boa. Então, na maioria das vezes, você era solicitado a salvar mudanças, mesmo que não houvesse nenhuma. Isso foi corrigido. A partir de agora, você só deverá ver esse aviso quando tiver feito realmente alterações.

## 10 de maio de 2021

**Publicação simplificada** — a criação no ambiente de preparo não é mais necessária. Se você tiver os direitos apropriados, ignore totalmente o estado Enviado e publique diretamente do Desenvolvimento, desde que tenha tido uma criação bem-sucedida e não haja outras bibliotecas upstream

## 22 de abril de 2021

**Coleção de dados da Adobe Experience Platform** — o envio de dados à Adobe não se resume à implantação de tags no site ou à configuração no aplicativo.  O uso dos SDKs do Experience Platform e da Edge Network requer acesso a outros recursos da plataforma. Isso costumava exigir o logon em algumas ferramentas diferentes, mas agora elas estão reunidas em um único lugar.

A Coleção de dados da Platform consiste em seis recursos, e sua navegação recentemente simplificada conterá apenas os itens aos quais sua empresa e conta de usuário têm acesso.  Alguns dos recursos também foram atualizados para corresponder aos padrões de nomenclatura do Experience Platform.

* Cliente (acessado anteriormente como lado do cliente)
* Datastreams (acessados anteriormente como configurações de borda)
* Servidor (acessado anteriormente como lado do servidor)
* Configurações do aplicativo
* Esquemas
* Identidades

Aguarde mais atualizações à medida que o Experience Platform e a Coleção de dados continuarem a evoluir.

## 18 de fevereiro de 2021

* Atualização da interface da Coleção de dados para o react-spectrum v3
* Placas de extensão atualizadas para os padrões mais recentes do Spectrum
* Aumento do tamanho dos campos de nome em todo o aplicativo

## 13 de janeiro de 2021

**Disponibilidade geral: encaminhamento de eventos** Envie dados de nível de evento à Adobe Experience Platform Edge Network e, em seguida, use o encaminhamento de eventos para transformar, enriquecer e enviar esses dados a um endpoint que não seja da Adobe usando servidores da Adobe, não o cliente, com baixa latência.

Consulte a [visão geral do encaminhamento de eventos](../ui/event-forwarding/overview.md) e [guia de introdução](../ui/event-forwarding/getting-started.md) para obter mais informações.
