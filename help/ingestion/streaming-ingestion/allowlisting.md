---
title: INCLUIR NA LISTA DE PERMISSÕES de endereço IP relacionado à API de assimilação de streaming
description: Saiba como proteger o acesso à API de assimilação de streaming permitindo somente endereços IP especificados por meio do incluir na lista de permissões de. Este guia explica como configurar, habilitar e gerenciar restrições baseadas em endereço IP para segurança de API.
hide: true
hidefromtoc: true
badge: beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# API de assimilação de streaming do incluir na lista de permissões de endereço IP

>[!AVAILABILITY]
>
>Incluir na lista de permissões A compatibilidade com o endereço IP A API de assimilação de streaming está na versão beta e sua organização pode não ter acesso a ela ainda. A funcionalidade e a documentação estão sujeitas a alterações.

Agora é possível incluir na lista de permissões endereços IP para a API de assimilação de streaming. Use esse recurso para proteger seus pontos de extremidade de assimilação, restringindo o acesso somente aos endereços IP especificados.

## Como funciona o incluir na lista de permissões de endereço IP

O recurso de incluir na lista de permissões IP funciona da seguinte maneira:

1. **Enviar endereços IP:** você fornece uma lista de endereços IP confiáveis, mapeados para suas sandboxes.
2. **Configuração:** o Adobe configura o incluo na lista de permissões no nível da organização e da sandbox para sua organização.
3. **Imposição:** as solicitações de entrada são avaliadas em relação ao incluo na lista de permissões fornecido:
   * Se o endereço IP corresponder ao seu incluo na lista de permissões, a solicitação será processada normalmente.
   * Se o endereço IP não estiver no incluo na lista de permissões, a solicitação será bloqueada e um erro HTTP 403 será recebido sem nenhum corpo de resposta.

## Principais considerações

* O recurso de incluir na lista de permissões de endereço IP aplica-se somente à [API de assimilação de streaming](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) e **não** se aplica a `server.adobedc.net` ou `edge.adobedc.net`.
* Novas sandboxes são abertas por padrão até que o incluir na lista de permissões esteja ativado.
* Remover uma sandbox do incluo na lista de permissões a reabrirá na Internet.
* Você deve manter a lista completa de mapeamentos de sandbox para endereço IP do seu lado e sempre enviar a lista completa no formulário de incluir na lista de permissões de endereço IP. Não há suporte para atualizações incrementais.

## Ativar o incluir na lista de permissões de endereço IP

Siga as etapas abaixo para ativar o incluir na lista de permissões de endereço IP para sua organização:

1. Baixe e conclua o [formulário de incluir na lista de permissões de endereço IP](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Abra um tíquete de suporte e arquive o assunto como **Assimilação de AEP DCS e Streaming - Solicitação de Incluir na lista de permissões IP**. Anexe o formulário preenchido a este tíquete.
3. Depois de enviar o tíquete, o Atendimento ao cliente da Adobe encaminhará sua solicitação para a equipe de engenharia.
4. Os engenheiros permitem o incluir na lista de permissões e confirmam a configuração.
5. Em seguida, você valida o acesso e confirma usando o tíquete de suporte.

| Organização | Nome da sandbox | Endereços IP permitidos |
| --- | --- | --- |
| ACME | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| ACME | Desenvolvedor | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Perguntas frequentes

Leia o seguinte para obter respostas a perguntas frequentes sobre o incluir na lista de permissões de endereço IP relacionado à API de assimilação de streaming.

### Quais APIs são cobertas?

Somente os pontos de extremidade da API de assimilação de streaming `dcs.adobedc.net`.

## O que acontece se minha solicitação vem de um endereço IP não listado?

Ele está bloqueado com um erro HTTP 403.

### As novas sandboxes são protegidas automaticamente?

Não. Elas permanecerão abertas até que você forneça mapeamentos de endereço IP por meio do formulário de incluir na lista de permissões.

### É possível enviar somente endereços IP atualizados quando meu incluo na lista de permissões é alterado?

Não. Você sempre deve enviar a lista completa de mapeamentos de sandbox e endereço IP. Atualizações parciais (incrementais) não são aceitas.