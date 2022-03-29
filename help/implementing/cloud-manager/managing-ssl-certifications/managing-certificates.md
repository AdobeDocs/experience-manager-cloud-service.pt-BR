---
title: Gerenciar certificados SSL
description: Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.
source-git-commit: 95539851590456b6b5ecbfeb0df8fc7bc7dde74b
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# Gerenciar certificados SSL {#managing-ssl-certificates}

Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.

## Verificar o status dos certificados SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página de certificado SSL.

* **Verde** - Esse status indica que seu certificado é válido por pelo menos 60 dias a partir da data atual.

* **Laranja** - Esse status indica que seu certificado deve expirar em menos de 60 dias.
   * É hora de garantir que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager para evitar possíveis acessos ao site ou interrupções.
   * O Cloud Manager enviará notificações regulares na interface do usuário para alertá-lo sobre uma expiração iminente de certificado.

* **Vermelho** - Esse status indica que o certificado SSL expirou.

## Configurações pré-existentes de CDN {#pre-existing-cdn}

Se você tiver uma configuração CDN preexistente para seu certificado SSL, haverá uma mensagem informativa no **Certificados SSL** , incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e configuráveis no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário do . Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte o documento [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida no **LISTA DE PERMISSÕES IP** e **Ambientes** páginas para ambientes que tenham configurações de CDN pré-existentes para listas de permissões IP ou nomes de domínio personalizados.

## Atualização de um certificado SSL {#update-ssl-certificate}

Quando um certificado expira, qualquer domínio que esteja em uso com o certificado expirado não funcionará mais. Atualizar seus certificados pelas etapas a seguir garante que o domínio continue a funcionar conforme desejado.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Navegar para **Ambientes** da tela **Visão geral** página.
1. Navegue até o **Certificados SSL** da tela **Ambientes** tela.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa. Clique no botão de reticências na extremidade direita da linha do certificado que deseja atualizar e selecione **Exibir e atualizar**.
1. Os detalhes do certificado são exibidos e podem ser atualizados.

>[!NOTE]
>
>Um usuário deve ser membro do **Proprietário da empresa** ou **Gerenciador de implantação** para atualizar um certificado SSL no Cloud Manager.

## Substituição de um certificado SSL {#replace-ssl-certificate}

Um certificado SSL pode ser substituído seguindo as mesmas etapas descritas na seção [Atualização de um certificado SSL.](#update-ssl-certificate)

## Excluir um certificado SSL {#deleting-an-ssl-certificate}

Remover certificados do Cloud Manager é uma ação permanente que não pode ser desfeita. Como prática recomendada, o Adobe recomenda salvar os arquivos SSL localmente antes de excluí-los no Cloud Manager.

O Cloud Manager não permitirá que você exclua um certificado SSL que tenha um ou mais domínios associados a ele. Todos os domínios associados devem ser excluídos antes de excluir o certificado SSL. Consulte o documento [Excluindo um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para saber mais.

Siga estas etapas para excluir um certificado SSL.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Navegar para **Ambientes** da tela **Visão geral** página.
1. Navegue até o **Certificados SSL** da tela **Ambientes** tela.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa. Clique no botão de reticências na extremidade direita da linha do certificado que deseja excluir e selecione **Excluir**.
1. Confirme a exclusão no **Excluir Certificado SSL** caixa de diálogo.

>[!NOTE]
>
>Um usuário deve ser membro do **Proprietário da empresa** ou **Gerenciador de implantação** para excluir um certificado SSL no Cloud Manager.