---
title: Verificando o status do nome de domínio
description: Saiba como determinar se o nome de domínio personalizado foi verificado com êxito pelo Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Verificando o status do nome de domínio {#check-status}

Você pode determinar o status do seu nome de domínio personalizado no Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** da tela **Visão geral** página.

1. Clique em **Configurações de domínio** no painel de navegação esquerdo.

1. Clique no botão **Status** ícone para o nome do domínio.

O Cloud Manager verificará a propriedade do domínio por meio do valor TXT e exibirá uma das seguintes mensagens de status.

* **Falha na Verificação de Domínio** - O valor TXT está ausente ou é detectado com erros.

   * Siga as instruções fornecidas para resolver o problema.
   * Quando estiver pronto, você deverá selecionar a variável **Verificar novamente** ícone ao lado do status.

* **Verificação de Domínio em Andamento** - A verificação está em curso.

   * Normalmente, esse status é visualizado depois que você seleciona a variável **Verificar novamente** ícone ao lado do status.

* **Verificado, Falha na Implantação** - A verificação TXT foi bem-sucedida, mas a implantação da CDN falhou.

   * Nesses casos, entre em contato com o representante do Adobe.

* **Domínio verificado e implantado** - Esse status indica que o nome de domínio personalizado está pronto para ser usado.

   * Neste ponto, o nome de domínio personalizado está pronto para teste e deve ser apontado para o nome de domínio do Cloud Manager.
   * Consulte o documento [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.

* **Exclusão** - A exclusão de um nome de domínio personalizado está em andamento.

* **Falha na Exclusão** - A exclusão do nome de domínio personalizado falhou e deve ser repetida.

   * Consulte o documento [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais.

O Cloud Manager acionará automaticamente uma verificação TXT ao selecionar **Salvar** sobre a etapa de verificação do **Adicionar domínio personalizado** assistente. Para verificações subsequentes, você deve selecionar ativamente o ícone de verificação novamente ao lado do status.

## Erros de nome de domínio {#domain-error}

Esta seção explica os erros que você pode ver e como resolvê-los.

**Domínio não instalado** - Você recebe esse erro durante a validação do domínio do registro TXT mesmo depois de verificar que o registro foi atualizado adequadamente.

**Explicação de erro** - Bloqueia com frequência um domínio para a conta inicial que o registrou e nenhuma outra conta pode registrar um subdomínio sem solicitar permissão. Além disso, o Fastly permite atribuir somente um domínio de ápice e subdomínios associados a um serviço e uma conta do Fastly. Se você tiver uma conta Fastly existente que vincula o mesmo apex e subdomínios usados para os domínios da AEM Cloud Service, verá esse erro.

**Resolução de Erro** - O erro é corrigido da seguinte maneira:

* Remova o apex e os subdomínios da conta existente antes de instalar o domínio no Cloud Manager. Use essa opção para vincular o domínio apex e todos os subdomínios à conta as a Cloud Service Fastly AEM. Consulte [Trabalhar com domínios na documentação do Fastly](https://docs.fastly.com/en/guides/working-with-domains) para obter mais detalhes.

* Se o domínio apex tiver vários subdomínios para AEM sites as a Cloud Service e não AEM que você deseja vincular a contas Fastly diferentes, tente instalar o domínio no Cloud Manager e, se a instalação do domínio falhar, crie um tíquete de Suporte ao Cliente com Fastly para podermos dar seguimento com Fastly em seu nome.

>[!NOTE]
>
>OBSERVAÇÃO: Não roteie o DNS do site para AEM IPs as a Cloud Service se o domínio não tiver sido instalado com êxito.

## Configurações de CDN pré-existentes para nomes de domínio personalizados {#pre-existing-cdn}

Se você tiver uma configuração de CDN preexistente para seus nomes de domínio personalizados, haverá uma mensagem informativa no **Nomes de Domínio Personalizados** e **Ambiente** páginas, incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e configuráveis no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário do . Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte o documento [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obter mais detalhes.
