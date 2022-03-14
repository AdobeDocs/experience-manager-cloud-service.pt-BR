---
title: 'Exibição da atualização e substituição de um certificado SSL - Gestão de SSL '
description: Exibição da atualização e substituição de um certificado SSL - Gestão de certificados SSL
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Visualização, atualização e substituição de um certificado SSL  {#view-update-replace-ssl-certificate}

## Exibição e atualização de um certificado SSL {#view-update}

Quando usar essas opções na interface do usuário do Cloud Manager:

* Um certificado existente está prestes a expirar. O usuário renovou o certificado com o fornecedor do certificado e deseja substituir o certificado existente que está prestes a expirar. Observação Somente o usuário com as permissões apropriadas pode fazer atualizações.
* Use o **Exibir e atualizar** para exibir os detalhes do certificado SSL.
* Como alternativa, você pode alterar o nome que foi usado para fazer referência a um certificado nessa tela.
* Somente o usuário com as permissões apropriadas pode fazer atualizações.


## Atualização de um certificado SSL prestes a expirar {#update-ssl-certificate}

Quando um certificado expira, qualquer domínio que esteja em uso com o certificado expirado não funcionará mais. Para atualizar um certificado expirado, siga as etapas listadas abaixo. Isso garantirá que o domínio continue a funcionar conforme desejado. A adição de um novo certificado exigirá a atualização do nome de domínio personalizado com o novo Certificado, antes que os domínios funcionem conforme desejado. Consulte [Visualização e atualização e substituição de um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) para obter mais detalhes.

Siga as etapas abaixo para atualizar um certificado SSL:

>[!NOTE]
>Um usuário deve estar na função Proprietário comercial ou Gerente de implantação para atualizar um certificado SSL no Cloud Manager.

1. Navegue até a tela Certificados SSL no **Ambientes** página.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa.
1. As opções de menu para cada linha podem ser acessadas selecionando os três botões na extremidade direita da linha de interesse.
1. Selecionar **Exibir e atualizar**. Os detalhes do certificado podem ser exibidos aqui.

## Substituição de um certificado SSL {#replace-ssl-certificate}

Siga as etapas abaixo para substituir um certificado SSL:

1. Navegue até a tela Certificados SSL no **Ambientes** página.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa.
1. As opções de menu para cada linha podem ser acessadas selecionando os três botões na extremidade direita da linha de interesse.
1. Selecionar **Exibir e atualizar**.
1. Para substituir o certificado, cole o novo conteúdo nos campos de entrada apropriados e clique em **Salvar**. Você precisará corrigir qualquer erro que possa surgir.

   Consulte [Erros de certificado](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) para solucionar problemas comuns.
