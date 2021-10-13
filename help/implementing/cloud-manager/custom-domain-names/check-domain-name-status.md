---
title: Verificando o status do nome de domínio
description: Verificando o status do nome de domínio
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Verificando o status do nome de domínio {#check-status}

Você pode determinar se o nome de domínio foi verificado com êxito clicando no ícone Status do nome de domínio da tabela em Ambientes na página Configurações do domínio .

>[!NOTE]
>O Cloud Manager acionará automaticamente uma verificação TXT ao selecionar Salvar na etapa de verificação do assistente Adicionar domínio personalizado . Para verificações subsequentes, você deve selecionar ativamente o ícone **verify novamente** ao lado do status.

O Cloud Manager verificará a propriedade do domínio por meio do valor TXT e exibirá uma das seguintes mensagens de status:

* **O valor**
FailedTXT da Verificação de Domínio está ausente ou é detectado com erros. Siga as instruções e tente novamente. Quando estiver pronto, você deverá selecionar a variável 
*verifique novamente* ícone ao lado do status .

* **Verificação de Domínio em**
AndamentoVerificação em andamento. Normalmente, esse status é visualizado depois que você seleciona a variável 
*verifique novamente* ícone ao lado do status .

* **Verificado se a verificação**
FailedTXT da implantação foi bem-sucedida. No entanto, a implantação da CDN falhou. Entre em contato com o representante do Adobe.

* **Domínio verificado e**
implantado Este status indica que seu nome de domínio personalizado está pronto para ser usado.
   >[!NOTE]
   >Neste ponto, o nome de domínio personalizado está pronto para teste e deve ser apontado para o nome de domínio do Cloud Manager. Consulte [Configuração de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.

* ****
A exclusão do nome de domínio personalizado está em processo.

* **Falha na exclusão**
FailedDeletion do nome de domínio personalizado. Você deve tentar novamente. Consulte [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para saber mais.


## Configurações de CDN pré-existentes para nomes de domínio personalizados {#pre-existing-cdn}

Os clientes com ambientes que incluem configurações de CDN pré-existentes para Listas de permissões de IP, certificados SSL ou nomes de domínio personalizados verão a seguinte mensagem na página de detalhes **Lista de permissões de IP** e **Ambiente**. A mensagem exibida na interface do usuário desaparecerá assim que o cliente migrar totalmente todas as configurações de ambiente pré-existentes por meio da interface do usuário e talvez demore de 1 a 2 dias úteis para a mensagem desaparecer.

>[!NOTE]
>Para visualizar e gerenciar as configurações pré-existentes, elas devem ser adicionadas por meio da interface do usuário. Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obter mais detalhes.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
