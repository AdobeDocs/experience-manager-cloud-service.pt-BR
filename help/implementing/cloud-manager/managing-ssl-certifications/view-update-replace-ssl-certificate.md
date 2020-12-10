---
title: 'Exibindo Atualização e Substituição de um Certificado SSL - Gerenciando SSL '
description: Exibindo Atualização e Substituição de um Certificado SSL - Gerenciando Certificados SSL
translation-type: tm+mt
source-git-commit: d1301d4414f87b30f5ab732eacbb61c96f102262
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Exibindo e atualizando e substituindo um certificado SSL {#view-update-replace-ssl-certificate}

## Exibindo e Atualizando um Certificado SSL {#view-update}

Quando usar essas opções na interface do usuário do Cloud Manager:

* Um certificado existente está prestes a expirar. O usuário renovou o certificado com o fornecedor do certificado e deseja substituir o existente que está prestes a expirar. Observação Somente o usuário com as permissões apropriadas pode fazer atualizações.
* Use o menu Visualização e atualização para simplesmente visualização os detalhes do certificado SSL.
* Como alternativa, você pode alterar o nome que foi usado para fazer referência a um certificado nesta tela.
   >[!NOTE]
   >Somente usuários com as permissões apropriadas podem fazer atualizações.


## Atualização de um certificado SSL prestes a expirar {#update-ssl-certificate}


>[!NOTE]
>Quando um certificado expira, quaisquer domínios que estejam em uso com o certificado expirado não funcionarão mais. Para atualizar um certificado expirado, siga as etapas listadas abaixo. Isso garantirá que seu domínio continue a funcionar conforme desejado. A adição de um novo certificado exigirá a atualização do nome de domínio personalizado com o novo Certificado antes que os domínios funcionem conforme desejado. Consulte Visualização e atualização do nome de domínio personalizado para obter mais detalhes

Siga as etapas abaixo para atualizar um certificado SSL:

>[!NOTE]
>Um usuário deve estar na função Proprietário de Negócios ou Gerenciador de Implantação para atualizar um certificado SSL no Cloud Manager.

1. Navegue até a tela Certificados SSL na página **Ambientes**.
1. Você verá uma tabela com uma linha para cada certificado SSL que foi instalado com êxito em seu programa.
1. As opções de menu para cada linha podem ser acessadas selecionando os três botões na extremidade direita extrema da linha de interesse. Aqui, selecione Visualização e atualização. Os detalhes do certificado podem ser exibidos aqui, como ilustrado no exemplo abaixo.
1. Para substituir o certificado, cole o novo conteúdo nos campos de entrada apropriados e salve. Você precisará resolver quaisquer erros que possam surgir. Consulte a seção Erros de certificado para solucionar problemas mais comuns.