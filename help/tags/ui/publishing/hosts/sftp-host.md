---
title: Hosts SFTP
description: Saiba como configurar tags no Adobe Experience Platform para fornecer builds de biblioteca a um servidor SFTP seguro e auto-hospedado.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 44%

---

# Hosts SFTP

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Se você não quiser que suas bibliotecas hospedadas sejam gerenciadas pela Adobe, a outra opção é fazer o Adobe Experience Platform entregar builds para um servidor SFTP seguro que você hospeda.

O Platform se conecta com seu site SFTP usando uma chave criptografada. Há algumas etapas para configurar isso corretamente:

1. Você deve ter um par de chaves pública/privada instalado no servidor SFTP. Você pode gerar essas chaves em seu servidor ou gerá-las em outro lugar e instalá-las em seu servidor. Consulte a documentação do GitHub sobre [como gerar chaves SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) para obter mais informações.
1. A chave privada é usada para criptografar a chave GPG pública. Será necessário fornecer sua chave privada durante o processo de criação do host SFTP. Consulte a seção [Criptografar valores](https://developer.adobelaunch.com/api/guides/encrypting_values/) na documentação da API do reator para obter instruções sobre como criptografar chaves GPG públicas. Use a chave GPG do ambiente de produção, a menos que você saiba que precisa de uma específica. Por fim, você pode criptografar sua chave privada de qualquer computador e não precisa instalar o GPG no servidor para concluir essa etapa.
1. Talvez seja necessário aprovar os endereços IP usados com o firewall da empresa para permitir que a Platform alcance seu servidor SFTP e se conecte a ele. Esses endereços IP são:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>A estrutura das builds de tags mudou com o tempo. Eles usam links simbólicos (symlinks) internamente para manter a compatibilidade com versões anteriores, para que os códigos incorporados anteriores continuem a funcionar com a estrutura de build mais recente. Seu servidor SFTP deve oferecer suporte ao uso de symlinks para servir como destino válido para builds de tags.

Para obter informações mais detalhadas, consulte o seguinte artigo Médio sobre [como configurar servidores SFTP para fornecer uma build](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Criar um host SFTP

1. Abra a guia [!UICONTROL Hosts].
1. Crie o novo host.
1. Dê um nome ao host.
1. Selecione **[!UICONTROL SFTP]** como o tipo de host.
1. Insira o host, o caminho, a porta, o nome de usuário e a chave privada criptografada.

   A porta deve ser uma das seguintes:

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Como prática recomendada de segurança, a Adobe limita o número de portas que podem ser usadas para tráfego de saída. As portas selecionadas geralmente são permitidas por meio de firewalls corporativos, além de incluírem alguns intervalos para oferecer flexibilidade.

1. Selecione **[!UICONTROL Salvar]**.

Ao selecionar **[!UICONTROL Save]**, a conexão e a capacidade de entregar os arquivos ao servidor SFTP são testadas. A Platform cria uma pasta, grava um arquivo nessa pasta, verifica se o arquivo está lá e depois faz a limpeza. Se a conta de usuário no servidor SFTP (aquele anexado ao certificado seguro fornecido para a Platform) não tiver as permissões necessárias para executar essa ação, o host entrará em um status &quot;Falha&quot;.
