---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Acessar pontuações no AI de atribuição
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# Acessar pontuações no AI de atribuição

>[!IMPORTANT] Entre em contato com attributionai-support@adobe.com para obter mais detalhes sobre downloads de pontuação bruta para a exportação de dados em massa.

O acesso às pontuações para a Atribuição AI é feito por meio do Floco de neve. Atualmente, você precisa enviar um email para o suporte da Adobe em attributionai-support@adobe.com para configurar e receber as credenciais da sua conta de leitor para o Floco de neve.

Depois que o suporte da Adobe tiver processado sua solicitação, você receberá um URL para a conta do leitor para Snowflake e as credenciais correspondentes abaixo:

- URL do floco de neve
- Nome do usuário
- Password

>[!NOTE] A conta do leitor é para consultar os dados usando clientes sql, planilhas e soluções BI que suportam o conector JDBC.

Depois de ter suas credenciais e URL, você poderá query as tabelas modelo, em seu formato bruto, agregadas por data do ponto de contato ou data de conversão.

## Encontrar seu schema em Floco de Neve

Usando as credenciais fornecidas, faça logon no Floco de neve. Clique na guia **Planilhas** na navegação principal superior esquerda e navegue até o diretório do banco de dados no painel esquerdo.

![Planilhas e navegação](./images/download-scores/edited_snowflake_1.png)

Em seguida, clique em **Selecionar Schema** no canto superior direito da tela. Na janela que aparece, confirme se você tem o banco de dados certo selecionado. Em seguida, clique na lista suspensa *Schema* e selecione um dos schemas listados. Você pode query diretamente das tabelas de pontuação listadas abaixo do schema selecionado.

![localizar um schema](./images/download-scores/edited_snowflake_2.png)

## Download de pontuações brutas

Entre em contato com attributionai-support@adobe.com para obter mais detalhes sobre downloads de pontuação bruta.

## Conectando o Power BI ao Floco de neve (opcional)

Suas credenciais do Snowflake podem ser usadas para configurar uma conexão entre os bancos de dados Power BI Desktop e Snowflake.

Primeiro, na caixa *Servidor* , digite o URL do floco de neve. Em seguida, em *Warehouse*, digite &quot;XSMALL&quot;. Em seguida, digite seu nome de usuário e senha.

![exemplo de POWERBI](./images/download-scores/powerbi-snowflake.png)

Depois que a conexão for estabelecida, selecione seu banco de dados Snowflake e selecione o schema apropriado. Agora você pode carregar todas as tabelas.

Depois de selecionar o schema, as tabelas são exibidas contendo as pontuações de atribuição.

| Tabela | Descrição |
| ----- | ----------- |
| APP_{APP_ID} | Pontuação de atribuição bruta. |
| APP_{APP_ID}_BY_CONV_DATE | Pontuação de atribuição bruta agregada no nível da data de conversão. |
| APP_{APP_ID}_BY_TP_DATE | Pontuação de atribuição bruta agregada no nível de data do ponto de contato. |

## Próximas etapas

Este documento descreveu as etapas necessárias para consultar os dados e acessar as pontuações da Atribuição AI. Agora você pode continuar navegando pelos outros serviços [e guias](../home.md) inteligentes oferecidos.