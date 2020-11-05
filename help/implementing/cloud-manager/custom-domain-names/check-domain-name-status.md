---
title: Verificando o status do nome do domínio
description: Verificando o status do nome do domínio
translation-type: tm+mt
source-git-commit: 5cd22d8af20bb947e4cdab448cf8f20c6596bb2e
workflow-type: tm+mt
source-wordcount: '810'
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

### Registro APEX {#apex-record}

Um domínio de ápice é um domínio personalizado que não contém um subdomínio, como example.com. Um domínio de ápice está configurado com um `A` , `ALIAS` ou `ANAME` registro por meio do seu provedor DNS. Os domínios Apex devem apontar para endereços IP específicos.

Adicione todos os seguintes registros A às configurações de DNS do Domínio por meio do provedor de domínio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Verificando o status do registro DNS {#check-status-dns-record}

Você pode determinar se seu nome de domínio está resolvendo corretamente para seu AEM como um site de Cloud Service, clicando no ícone Status do registro DNS na tabela da página Configurações de domínio. O Cloud Manager realiza uma pesquisa DNS para seu nome de domínio e exibe uma das seguintes mensagens de status:

>[!NOTE]
>O Cloud Manager acionará automaticamente uma pesquisa DNS quando seu Nome de domínio personalizado for verificado e implantado pela primeira vez com êxito. Para tentativas subsequentes, você deve selecionar ativamente o ícone **resolver novamente** ao lado do status. INSERIR IMAGEM

* **O status de DNS não detectado** O status de DNS não será detectado até que seu nome de domínio personalizado tenha sido verificado e implantado com êxito. Esse status também é observado quando seu nome de Domínio personalizado está em processo de exclusão.

* **Resoluções de DNS incorretas** Isso indica que a configuração de registros de DNS ainda não foi resolvida/apontou para cima ou está incorreta. Um representante Adobe será notificado automaticamente.

   >[!NOTE]
   >Você deve configurar um `CNAME` ou `A-record` seguindo as instruções correspondentes. Vá até Configuração de DNS INSERIR LINK para saber mais sobre o tópico. Quando estiver pronto, você deve selecionar o ícone &quot;resolver novamente&quot; ao lado do status.

* **Resolução DNS em andamento** Resolução em andamento. Normalmente, esse status é visto depois que você seleciona o ícone &quot;resolver novamente&quot; ao lado do status.

* **Resolve o DNS corretamente** As suas definições de DNS estão corretamente configuradas. Seu site está servindo visitantes.
