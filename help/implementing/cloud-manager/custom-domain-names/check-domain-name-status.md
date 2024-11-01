---
title: Verificar status do nome de domínio
description: Saiba como verificar se o Cloud Manager confirmou com êxito seu nome de domínio personalizado.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 41a67b0747ed665291631de4faa7fb7bb50aa9b9
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 19%

---


# Verificar status do nome de domínio {#check-status}

Saiba como verificar se o Cloud Manager confirmou com êxito seu nome de domínio personalizado.

## Verificar o status de um nome de domínio personalizado {#how-to}

Antes de verificar o status do nome de domínio no Cloud Manager, verifique se você já adicionou um certificado SSL gerenciado pelo cliente (OV/EV) para o seu domínio personalizado, conforme descrito em [Adicionar um certificado SSL gerenciado pelo cliente](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert).

**Para verificar o status de um nome de domínio personalizado:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no menu do lado esquerdo.

1. Clique no ícone de **Status** do nome do domínio.

Os detalhes do status são mostrados. Seu domínio personalizado está pronto para ser usado quando o status **Domínio verificado e implantado** for exibido. Consulte a [próxima seção](#statuses) para obter detalhes sobre os diferentes status e o seu significado.

>[!NOTE]
>
>Se você estiver usando um *certificado SSL gerenciado por Adobe* com o domínio, o Cloud Manager acionará automaticamente a verificação quando você clicar em **Verificar** na caixa de diálogo Verificar domínio ao [adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
>
>Se você pretende usar um **certificado SSL gerenciado pelo cliente (OV/EV)**, seu domínio será verificado *depois* de você [adicionar o certificado SSL OV/EV](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).


## Status de verificação {#statuses}

A Cloud Manager verifica a propriedade do domínio por meio do certificado SSL gerenciado pelo cliente (OV/EV). Quando concluído, ele exibe uma das seguintes mensagens de status:

| Status | Descrição |
| --- | --- |
| Falha na verificação do domínio | O certificado EV/OV gerenciado pelo Cliente está ausente ou erros foram detectados.<br> Siga as instruções fornecidas na mensagem de status para resolver o problema. Quando estiver pronto, você deverá selecionar o ícone **Verificar novamente** ao lado do status. |
| Verificação de domínio em andamento | Verificação em andamento.<br>Normalmente, esse status é exibido depois de selecionar o ícone **Verificar Novamente** ao lado do status. A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS. |
| Verificado - falha na implantação | A verificação do certificado EV/OV foi bem-sucedida, mas a implantação do CDN falhou.<br>Nesses casos, entre em contato com o representante da Adobe. |
| Domínio verificado e implantado | Esse status indica que o nome de domínio personalizado está pronto para ser usado.<br>Neste ponto, o nome de domínio personalizado está pronto para ser testado e apontado para o nome de domínio do Cloud Manager. Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para saber mais. |
| Excluindo | A exclusão de um nome de domínio personalizado está em andamento. |
| A exclusão falhou | A exclusão de um nome de domínio personalizado falhou e deve ser repetida.<br>Consulte [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais. |


## Erros de nome de domínio {#domain-error}

A seguir estão alguns erros comuns de verificação de nome de domínio e suas resoluções típicas.

### Erro de domínio não instalado {#domain-not-installed}

Esse erro pode ocorrer durante a validação do domínio do certificado EV/OV, mesmo após a verificação de que o certificado foi devidamente atualizado.

#### Causa do erro {#cause}

O Fastly bloqueia um domínio para a conta que o registra primeiro, e outras contas devem solicitar permissão para registrar um subdomínio. Além disso, o Fastly permite atribuir somente um domínio apex e subdomínios associados a um serviço e a uma conta do Fastly. Se você tiver uma conta existente do Fastly que vincula o mesmo ápice e subdomínios usados para seus domínios do AEM Cloud Service, esse erro será exibido.

#### Resolução de erro {#resolution}

O erro é corrigido da seguinte maneira:

* Remova o apex e os subdomínios da conta existente antes de instalar o domínio no Cloud Manager.

* Use essa opção para vincular o domínio apex e todos os subdomínios à conta do Fastly no AEM as a Cloud Service. Consulte [Trabalho com domínios na documentação do Fastly](https://docs.fastly.com/en/guides/working-with-domains) para obter mais detalhes.

* Se o domínio apex tiver vários subdomínios para sites AEM as a Cloud Service e não AEM que precisam ser vinculados a diferentes contas Fastly, tente instalar o domínio no Cloud Manager. Esse processo ajuda a gerenciar conexões de subdomínio em diferentes contas do Fastly. Se a instalação do domínio falhar, crie um tíquete de Suporte ao cliente com o Fastly para que o Adobe possa acompanhar com o Fastly em seu nome.

>[!TIP]
>
>A solução de problemas de delegação de domínio com o Fastly geralmente leva de 1 a 2 dias úteis. Por esse motivo, é recomendável instalar os domínios bem antes de suas datas de ativação.

>[!NOTE]
>
>Não roteie o DNS do site para os IPs do AEM as a Cloud Service se o domínio não tiver sido instalado com sucesso.

## Configurações de CDNs pré-existentes para nomes de domínio personalizados {#pre-existing-cdn}

Se você já tiver uma configuração de CDN para seus nomes de domínio personalizados, uma mensagem informativa será exibida nas páginas **Nomes de Domínio Personalizados** e **Ambiente**. Ele incentiva você a adicionar essas configurações por meio da interface do usuário para que possam ser gerenciadas e visualizadas no Cloud Manager.

A mensagem desaparece depois que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obter mais detalhes.

## Próximas etapas {#next-steps}

Após verificar o status do domínio no Cloud Manager, defina as configurações de DNS adicionando registros DNS, CNAME ou APEX que apontem para o AEM as a Cloud Service. Continue com o documento [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para continuar configurando seu nome de domínio personalizado.
