---
title: Verificando o status do nome de domínio
description: Saiba como determinar se o nome de domínio personalizado foi verificado com êxito pelo Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '384'
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

## Configurações de CDN pré-existentes para nomes de domínio personalizados {#pre-existing-cdn}

Se você tiver uma configuração de CDN preexistente para seus nomes de domínio personalizados, haverá uma mensagem informativa no **Nomes de Domínio Personalizados** e **Ambiente** páginas, incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e configuráveis no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário do . Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte o documento [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obter mais detalhes.
