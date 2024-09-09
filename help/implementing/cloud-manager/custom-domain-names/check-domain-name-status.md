---
title: Verificação de status do nome de domínio
description: Saiba como determinar se o nome de domínio personalizado foi verificado com sucesso pelo Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 63%

---


# Verificação de status do nome de domínio {#check-status}

Saiba como determinar se o nome de domínio personalizado foi verificado com sucesso pelo Cloud Manager.

## Requisitos {#requirements}

Você deve atender a esses requisitos antes de verificar o status do nome de domínio no Cloud Manager.

* Primeiro, adicione um registro TXT para o domínio personalizado conforme descrito no documento [Adicionando um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

## Como verificar o status do seu nome de domínio personalizado {#how-to}

Você pode determinar o status do seu nome de domínio personalizado no Cloud Manager.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no painel de navegação esquerdo.

1. Clique no ícone de **Status** do nome do domínio.

Os detalhes do status são mostrados. Seu domínio personalizado está pronto para ser usado quando o status **Domínio verificado e implantado** for exibido. Consulte a [próxima seção](#statuses) para obter detalhes sobre os diferentes status e o seu significado.

>[!NOTE]
>
>O Cloud Manager disparará automaticamente a verificação quando você selecionar **Criar** na etapa de verificação do assistente **Adicionar Domínio Personalizado** ao [adicionar um novo nome de domínio personalizado ao Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Para as verificações subsequentes, você deverá selecionar ativamente o ícone Verificar novamente ao lado do status.

## Noções básicas sobre status de verificação {#statuses}

O Cloud Manager verificará a propriedade do domínio por meio do [valor TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) e exibirá uma das mensagens de status a seguir.

* **Falha ao verificar o domínio** - O valor TXT está ausente ou erros foram detectados.

   * Siga as instruções fornecidas na mensagem de status para resolver o problema.
   * Quando estiver pronto, você deverá selecionar o ícone **Verificar novamente** ao lado do status.

* **Verificação de domínio em andamento** - A verificação está em andamento.

   * Normalmente, esse status é exibido depois de selecionar o ícone **Verificar novamente** ao lado do status.
   * A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.

* **Verificado, Falha na implantação** - A verificação TXT foi bem-sucedida, mas a implantação do CDN falhou.

   * Nesses casos, entre em contato com o representante da Adobe.

* **Domínio verificado e implantado** - Esse status indica que o nome de domínio personalizado está pronto para ser usado.

   * Nesse ponto, o nome de domínio personalizado está pronto para ser testado e deve ser apontado para o nome de domínio do Cloud Manager.
   * Consulte [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.

* **Em exclusão** - A exclusão de um nome de domínio personalizado está em andamento.

* **Falha ao excluir** - A exclusão do nome de domínio personalizado falhou e deve ser repetida.

   * Consulte [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais.

## Erros de nome de domínio {#domain-error}

A seguir estão alguns erros comuns de verificação de nome de domínio e suas resoluções típicas.

### Erro de domínio não Instalado {#domain-not-installed}

Esse erro pode ocorrer durante a validação do domínio do registro TXT, mesmo após confirmar que o registro foi atualizado adequadamente.

#### Causa do erro {#cause}

O Fastly bloqueia um domínio para a conta inicial que o registrou e nenhuma outra conta pode registrar um subdomínio sem solicitar permissão. Além disso, o Fastly permite atribuir somente um domínio apex e subdomínios associados a um serviço e a uma conta do Fastly. Se você tiver uma conta existente do Fastly que vincula o mesmo ápice e subdomínios usados para seus domínios do AEM Cloud Service, esse erro será exibido.

#### Resolução de erro {#resolution}

O erro é corrigido da seguinte maneira:

* Remova o apex e os subdomínios da conta existente antes de instalar o domínio no Cloud Manager.

* Use essa opção para vincular o domínio apex e todos os subdomínios à conta do Fastly no AEM as a Cloud Service. Consulte [Trabalho com domínios na documentação do Fastly](https://docs.fastly.com/en/guides/working-with-domains) para obter mais detalhes.

* Se o seu domínio apex tiver vários subdomínios para os sites do AEM as a Cloud Service e os sites diferentes do AEM as a Cloud Service que você deseja vincular a diferentes contas Fastly, tente instalar o domínio no Cloud Manager. Se a instalação do domínio falhar, crie um tíquete de Suporte ao cliente com o Fastly para que a Adobe possa dar seguimento com o Fastly em seu nome.

>[!TIP]
>
>A solução de problemas de delegação de domínio com o Fastly geralmente leva de 1 a 2 dias úteis. Por esse motivo, é altamente recomendável instalar os domínios bem antes das respectivas datas de ativação.

>[!NOTE]
>
>Não roteie o DNS do site para os IPs do AEM as a Cloud Service se o domínio não tiver sido instalado com sucesso.

## Configurações de CDNs pré-existentes para nomes de domínio personalizados {#pre-existing-cdn}

Se você tiver uma configuração de CDN pré-existente para seus nomes de domínio personalizados, há uma mensagem informativa nas páginas **Nomes de domínio personalizados** e **Ambiente** incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e possam ser definidas no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obter mais detalhes.

## Próximas etapas {#next-steps}

Depois de verificar o status do domínio no Cloud Manager, será necessário definir as configurações de DNS adicionando registros CNAME ou APEX de DNS que apontem para o AEM as a Cloud Service. Prossiga para o documento [Definindo as Configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para continuar configurando seu nome de domínio personalizado.
