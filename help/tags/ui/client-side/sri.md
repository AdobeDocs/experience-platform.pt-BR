---
title: Compatibilidade de Integridade de sub-recursos (SRI)
description: Saiba como a integridade de sub-recursos (SRI) é compatível com o Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 78%

---

# Compatibilidade de Integridade de sub-recursos (SRI)

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Este documento aborda como a SRI (Integridade de sub-recursos) é compatível com o Adobe Experience Platform.

Sites modernos são criados referenciando imagens, conteúdo e scripts de vários locais na Web. A SRI permite que um navegador verifique se o conteúdo de um arquivo solicitado não foi modificado inesperadamente.

Embora seus casos de uso se complementem, a SRI é diferente de uma Política de segurança de conteúdo (CSP), o que garante que somente arquivos de origens confiáveis sejam permitidos em seu site. A SRI vai um passo além, garantindo que o conteúdo desses arquivos corresponda às suas expectativas.

>[!NOTE]
>
>Para obter informações mais detalhadas sobre a SRI, consulte os [documentos da Web do MDN](https://developer.mozilla.org/pt-BR/docs/Web/Security/Subresource_Integrity).

O processo de validação da SRI pode ser resumido da seguinte forma:

1. Você gera um hash criptográfico do ativo que deseja validar.
1. Em seu site, o hash é colocado no atributo `integrity` do elemento HTML que carrega o arquivo.
1. Quando o navegador vê o atributo `integrity`, o navegador solicita o recurso e gera independentemente sua própria versão do hash criptográfico.
1. O navegador compara o hash do `integrity` com o que ele gerou. Se houver correspondência, o ativo será permitido. Se não corresponderem, o ativo será bloqueado.

## Limitações nos sistemas de gerenciamento de tags

Como um sistema de gerenciamento de tags (TMS), as tags no Adobe Experience Platform fornecem uma build de biblioteca JavaScript que você carrega em suas páginas com um único elemento `<script>` (código incorporado). A funcionalidade dinâmica oferecida pelo TMS é alcançada pela troca dinâmica do conteúdo desse script sem a necessidade de alterar mais nada.

No entanto, quando o conteúdo do script é alterado, o mesmo acontece com o hash criptográfico desse conteúdo. Portanto, a única maneira de fazer a SRI funcionar com um TMS é atualizar seu código integrado ao mesmo tempo em que você publica uma nova build. Para muitos, isso elimina o objetivo principal de usar um TMS em primeiro lugar.

A próxima melhor opção de segurança para tags é implementar uma Política de segurança de conteúdo. Para obter mais informações, consulte o guia sobre [CSPs e tags](./content-security-policy.md).

## Integração da SRI na implantação de build

Se você ainda quiser usar a SRI para seus builds de biblioteca, é necessário usar a hospedagem própria. Se você estiver usando a hospedagem gerenciada pela Adobe, não há como usar a SRI sem ter algum tempo em que o novo conteúdo da build não corresponda ao atributo `integrity` do código integrado.

A automatização do processo de atualização do código integrado varia em complexidade, dependendo da estrutura do site, mas as etapas gerais podem ser resumidas da seguinte maneira:

1. Recupere a build da biblioteca de produção, por meio do delivery SFTP ou baixe o arquivo da interface do usuário.
1. Gere o hash criptográfico da build principal.
1. Verifique se o atributo `integrity` do código integrado foi atualizado para o novo hash e se a build referenciada foi atualizada como parte da mesma implantação.

>[!IMPORTANT]
>
>Essa abordagem só abrange a build principal. Ela não inclui nenhum dos arquivos menores que possam existir.

## Próximas etapas

Este documento cobriu as limitações do uso da SRI com tags e as etapas necessárias para integrá-la às implantações de build da biblioteca, apesar dessas limitações. Caso ainda não o tenha feito, é altamente recomendável que você leia o guia em [CSPs e tags](./content-security-policy.md) para obter uma opção alternativa de segurança.
