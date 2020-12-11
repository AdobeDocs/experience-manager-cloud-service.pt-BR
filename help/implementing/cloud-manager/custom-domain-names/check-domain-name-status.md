---
title: Verificando o status do nome do domínio
description: Verificando o status do nome do domínio
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Verificando o status do nome do domínio {#check-status}

Você pode determinar se seu nome de domínio foi verificado com êxito clicando no ícone Status do nome de domínio na tabela em Ambientes da página Configurações de domínio.

>[!NOTE]
>O Cloud Manager acionará automaticamente uma verificação TXT quando você selecionar Salvar na etapa de verificação do assistente para Adicionar domínio personalizado. Para verificações subsequentes, você deve selecionar ativamente o ícone **verificar novamente** ao lado do status.

O Cloud Manager verificará a propriedade do domínio por meio do valor TXT e exibirá uma das seguintes mensagens de status:

* **O valor**
FailedTXT de verificação de domínio está ausente ou é detectado com erros. Siga as instruções e tente novamente. Quando estiver pronto, você deve selecionar a variável 
*verifique* novamente ao lado do status.

* **Verificação de domínio em**
andamentoVerificação em andamento. Esse status geralmente é visto depois que você seleciona a variável 
*verifique* novamente ao lado do status.

* **Verificado se a verificação**
FailedTXT da implantação foi bem-sucedida. No entanto, a implantação do CDN falhou. Um representante Adobe será notificado automaticamente.

* **Domínio verificado e**
implantadoEste status indica que seu nome de domínio personalizado está pronto para ser usado.
   >[!NOTE]
   >Nesse ponto, seu nome de domínio personalizado está pronto para teste e deve ser apontado para o nome de domínio do Cloud Manager. Consulte [Configuração de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.

* **A**
exclusão do nome de domínio personalizado está em andamento.

* **Falha na exclusão de**
FailedExclution do nome do domínio personalizado. Você deve tentar novamente. Consulte [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para saber mais.

