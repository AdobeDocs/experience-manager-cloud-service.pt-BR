---
title: 'Exibindo Atualização e Substituição de um Certificado SSL - Gerenciando SSL '
description: Exibindo Atualização e Substituição de um Certificado SSL - Gerenciando Certificados SSL
translation-type: tm+mt
source-git-commit: d5a119921a06ea06cbf2b95353083aa987869629
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Exibindo e atualizando e substituindo um certificado SSL {#view-update-replace-ssl-certificate}

## Exibindo e Atualizando um Certificado SSL {#view-update}

Quando usar essas opções na interface do usuário do Cloud Manager:

* Um certificado existente está prestes a expirar. O usuário renovou o certificado com o fornecedor do certificado e deseja substituir o existente que está prestes a expirar. Observação Somente o usuário com as permissões apropriadas pode fazer atualizações.
* Use o menu **Visualização e atualização** para simplesmente visualização os detalhes do certificado SSL.
* Como alternativa, você pode alterar o nome que foi usado para fazer referência a um certificado nesta tela.
* Somente usuários com as permissões apropriadas podem fazer atualizações.


## Atualização de um certificado SSL prestes a expirar {#update-ssl-certificate}

Quando um certificado expira, quaisquer domínios que estejam em uso com o certificado expirado não funcionarão mais. Para atualizar um certificado expirado, siga as etapas listadas abaixo. Isso garantirá que seu domínio continue a funcionar conforme desejado. A adição de um novo certificado exigirá a atualização do nome de domínio personalizado com o novo Certificado antes que os domínios funcionem conforme desejado. Consulte [Visualizar e atualizar e substituir um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)para obter mais detalhes

Siga as etapas abaixo para atualizar um certificado SSL:

>[!NOTE]
>Um usuário deve estar na função Proprietário de Negócios ou Gerenciador de Implantação para atualizar um certificado SSL no Cloud Manager.

1. Navegue até a tela Certificados SSL na página **Ambientes**.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa.
1. As opções de menu para cada linha podem ser acessadas selecionando os três botões na extremidade direita extrema da linha de interesse.
1. Selecione **Visualização e atualização**. Os detalhes do certificado podem ser exibidos aqui.

## Substituição de um certificado SSL {#replace-ssl-certificate}

Siga as etapas abaixo para substituir um certificado SSL:

1. Navegue até a tela Certificados SSL na página **Ambientes**.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa.
1. As opções de menu para cada linha podem ser acessadas selecionando os três botões na extremidade direita extrema da linha de interesse.
1. Selecione **Visualização e atualização**.
1. Para substituir o certificado, cole o novo conteúdo nos campos de entrada apropriados e clique em **Salvar**. Você precisará resolver quaisquer erros que possam surgir.

   Consulte [Erros de Certificado](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) para solucionar problemas mais comuns.