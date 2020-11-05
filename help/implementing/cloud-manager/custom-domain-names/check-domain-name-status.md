---
title: Verificando o status do nome do domínio
description: Verificando o status do nome do domínio
translation-type: tm+mt
source-git-commit: 91b06bcd96fe8a37c3fb20ef90e1684f6d19183f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Verificando o status do nome do domínio {#check-status}

Você pode determinar se seu nome de domínio foi verificado com êxito clicando no ícone Status do nome de domínio na tabela em Ambientes da página Configurações de domínio.

>[!NOTE]
>O Cloud Manager acionará automaticamente uma verificação TXT quando você selecionar Salvar na etapa de verificação do assistente para Adicionar domínio personalizado. Para verificações subsequentes, você deve selecionar ativamente o ícone &quot;verificar novamente&quot; ao lado do status. INSERIR IMAGEM

O Cloud Manager verificará a propriedade do domínio por meio do valor TXT e exibirá uma das seguintes mensagens de status:

* **O valor** TXT com falha na verificação do domínio está ausente ou é detectado com erros. Siga as instruções e tente novamente. Quando estiver pronto, você deve selecionar o ícone &quot;verificar novamente&quot; ao lado do status.

* **Verificação de domínio em andamento** Verificação em andamento. Normalmente, esse status é visto depois que você seleciona o ícone &quot;verificar novamente&quot; ao lado do status.

* **Verificado se a verificação** TXT de Implantação falhou com êxito. No entanto, a implantação do CDN falhou. Um representante Adobe será notificado automaticamente.

* **Domínio verificado e implantado** Este status indica que seu nome de domínio personalizado está pronto para ser usado. Observação: Nesse ponto, seu nome de domínio personalizado está pronto para teste e deve ser apontado para o nome de domínio do Cloud Manager. Vá até Configuração de DNS INSERIR LINK para saber como fazer isso.

* **A exclusão** da exclusão do nome de domínio personalizado está em andamento.

* **Falha na exclusão** da exclusão do nome de domínio personalizado. Você deve tentar novamente. Vá até Excluir nome de domínio personalizado para saber mais sobre o tópico.


## Configuração de configurações DNS {#configure-dns}

Depois que seu nome de domínio personalizado for verificado e implantado com êxito, você estará pronto para atualizar os registros de DNS para seu nome de domínio personalizado com seu provedor DNS. Isso permite que seu site sirva visitantes. Esta atividade é, portanto, tipicamente feita antes do Go-live.

>[!NOTE]
>Você ou o indivíduo apropriado em sua organização deve poder fazer logon ou entrar em contato com seu provedor DNS (a empresa da qual você adquiriu o domínio) e fazer atualizações nas configurações de DNS.

Para fazer isso, é necessário determinar se as configurações de DNS devem ser definidas para um registro `CNAME` ou Apex que aponte seu nome de domínio personalizado para o nome de domínio do Cloud Manager. Um registro `CNAME` ou A, uma vez provisionado, roteará todo o tráfego da Internet para o domínio para onde ele estiver apontando. Se esse local não for provisionado para servir o tráfego, haverá uma interrupção. Se não tiver sido testado, pode haver erros no conteúdo. É por isso que essa etapa é sempre realizada depois que o teste é concluído e o cliente está pronto para o Go-live.

### Registro CNAME {#cname-record}

As seções a seguir ajudarão você a determinar que tipo de registro é apropriado para sua configuração de DNS.

Um registro ou nome canônico é um tipo de registro DNS que mapeia um nome de alias para um nome de domínio verdadeiro ou canônico. `CNAME` Os registros CNAME são normalmente usados para mapear um subdomínio, como `www.example.com` o domínio que hospeda o conteúdo desse subdomínio.

Faça logon no Registrador de domínio e crie um registro CNAME para apontar seu nome de domínio personalizado para o público alvo, como mostrado abaixo:

| CNAME | Ponto de nome de domínio personalizado para Público alvo |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |
