---
title: Gerenciar certificados SSL
description: Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 73%

---


# Gerenciar certificados SSL {#managing-ssl-certificates}

Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.

## Verificação do status dos certificados SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página de certificados SSL.

* **Verde** - Esse status indica que o certificado é válido por pelo menos 14 dias a partir da data atual.

* **Laranja** - Esse status indica que o certificado vai expirar em menos de 14 dias.
   * É hora de garantir que você tenha um plano para renovar seu certificado e substituí-lo por meio da interface do Cloud Manager para evitar possíveis acessos ou interrupções no site.
   * O Cloud Manager enviará notificações regulares na interface do usuário para alertá-lo sobre a expiração iminente de um certificado.

* **Vermelho** - Esse status indica que o certificado SSL expirou.

## Atualização de um certificado SSL {#update-ssl-certificate}

Quando um certificado expira, todos os domínios que usem o certificado expirado deixam de funcionar. Atualizar os certificados de acordo com as etapas a seguir garante que o domínio continue a funcionar conforme desejado.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada
1. No **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)** selecione o programa.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Navegue até a tela **Certificados SSL** da tela **Ambientes**.
1. Você pode ver uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa. Clique no botão de reticências na extremidade direita da linha do certificado que deseja atualizar e selecione **Exibir e atualizar**.
1. Os detalhes do certificado são exibidos e podem ser atualizados.
1. Execute o pipeline para implantar o certificado atualizado.

>[!NOTE]
>
>É necessário ser um membro com a função **Proprietário da empresa** ou **Gerente de implantação** para atualizar um certificado SSL no Cloud Manager.

## Substituição de um certificado SSL {#replace-ssl-certificate}

Um certificado SSL pode ser substituído seguindo as mesmas etapas descritas na seção [Atualização de um certificado SSL.](#update-ssl-certificate)

## Exclusão de um certificado SSL {#deleting-an-ssl-certificate}

A remoção de certificados do Cloud Manager é uma ação permanente que não pode ser desfeita. Como prática recomendada, a Adobe recomenda salvar os arquivos SSL localmente antes de excluí-los no Cloud Manager.

O Cloud Manager não permitirá a exclusão de um certificado SSL que tenha um ou mais domínios associados a ele. Todos os domínios associados devem ser excluídos antes de excluir o certificado SSL. Consulte [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais.

Siga estas etapas para excluir um certificado SSL.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Navegue até a tela **Certificados SSL** da tela **Ambientes**.
1. Você pode ver uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa. Clique nas reticências na extremidade direita da linha do certificado que deseja excluir e selecione **Excluir**.
1. Confirme a exclusão na caixa de diálogo **Excluir certificado SSL**.
1. Execute o pipeline para desimplantar o certificado excluído.

>[!NOTE]
>
>É necessário ser um membro com a função **Proprietário da empresa** ou **Gerente de implantação** para excluir um certificado SSL no Cloud Manager.

## Configurações pré-existentes de CDN {#pre-existing-cdn}

Se você tiver uma configuração de CDN pré-existente para seu certificado SSL, haverá uma mensagem informativa no **Certificados SSL** incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e possam ser definidas no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adição de um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas **Lista de permissões de IP** e **Ambientes** para ambientes que tenham configurações pré-existentes de CDN para listas de permissões de IP ou nomes de domínio personalizados.
