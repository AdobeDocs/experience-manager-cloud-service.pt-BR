---
title: Gerenciar certificados SSL
description: Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 14%

---


# Gerenciar certificados SSL {#managing-ssl-certificates}

Saiba como usar o Cloud Manager para verificar o status dos certificados SSL gerenciados pelo Adobe e pelo cliente e como excluí-los. Para certificados gerenciados pelo cliente, você também pode editá-los e atualizá-los (substituí-los).

## Verificar o status dos certificados SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página **Certificados SSL**.

| Status do certificado SSL | Descrição |
| --- | --- |
| Verde | O certificado é válido por pelo menos 14 dias a partir da data atual. |
| Laranja | O certificado vai expirar em menos de 14 dias.<br>· Certifique-se de que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager para evitar possíveis acessos ao site ou interrupções.<br>· O Cloud Manager envia notificações regulares na interface do usuário para alertá-lo sobre a expiração iminente de um certificado. |
| Vermelho | O certificado SSL expirou.<br>Consulte [Atualizar um certificado SSL gerenciado pelo cliente expirado](#update-ssl-certificate) ou [Excluir um certificado SSL](#deleting-an-ssl-certificate). |

## Atualizar um certificado SSL gerenciado pelo cliente expirado {#update-ssl-certificate}

Quando um certificado gerenciado pelo cliente expira, todos os domínios que estão em uso com o certificado expirado deixam de funcionar. Atualizar os certificados garante que o domínio continue a funcionar conforme desejado.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para atualizar um certificado SSL gerenciado pelo cliente expirado:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Na página **Visão geral**, navegue até a tela **Ambientes**.
1. Na tela **Ambientes**, navegue até a tela **Certificados SSL**.
1. Na linha do certificado gerenciado pelo cliente expirado que você deseja atualizar, clique no botão de reticências na extremidade direita e selecione **Exibir e Atualizar**.

   ![Atualize uma certificação SSL expirada e gerenciada pelo cliente](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. Na caixa de diálogo **Exibir e atualizar certificado SSL**, faça o seguinte:

   * (Opcional) No campo **Nome do certificado**, digite um novo nome.
   * No campo **Certificado**, cole a nova chave de conteúdo do certificado.
   * No campo **Chave privada**, atualize este campo somente se você tiver feito alterações no certificado.
   * No campo **Cadeia de certificados** (ou cadeia de confiança), cole a cadeia de certificados.

1. Clique em **Atualizar** para salvar suas alterações e aplicá-las automaticamente.

## Substituir um certificado SSL gerenciado pelo cliente expirado {#replace-ssl-certificate}

Siga as mesmas etapas descritas em [Atualizar um Certificado SSL expirado](#update-ssl-certificate) para substituir um certificado SSL gerenciado pelo cliente expirado.

## Excluir um certificado SSL {#deleting-an-ssl-certificate}

A exclusão de certificados SSL gerenciados por Adobe ou pelo cliente do Cloud Manager é uma ação permanente que não pode ser desfeita. Como prática recomendada, o Adobe recomenda que você salve os arquivos SSL localmente antes de excluí-los no Cloud Manager.

>[!NOTE]
>
>Não é possível excluir um certificado SSL gerenciado por Adobe que tenha um ou mais domínios ativos associados a ele. Todos os domínios ativos associados devem ser excluídos antes de excluir o certificado SSL. Consulte [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para excluir um certificado SSL:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Na página **Visão geral**, navegue até a tela **Ambientes**.
1. Na tela **Ambientes**, navegue até a tela **Certificados SSL**.
1. Na linha do certificado que você deseja excluir, clique no botão de reticências na extremidade direita e selecione **Excluir**.
Se o botão Excluir tiver um ícone de informações como visto na imagem a seguir, consulte a Observação acima.

   ![Botão Excluir com ícone Informações](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. Na caixa de diálogo **Excluir Certificado SSL**, clique em **Excluir** para confirmar a exclusão.
1. Execute o pipeline para desimplantar o certificado excluído.

## Configurações de CDN pré-existentes {#pre-existing-cdn}

Se você já tiver uma configuração de CDN para seu certificado SSL, a página **Certificados SSL** exibirá uma mensagem informativa. Ele incentiva você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e possam ser gerenciadas no Cloud Manager.

A mensagem desaparece depois que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas **Lista de permissões de IP** e **Ambientes** para ambientes que tenham configurações pré-existentes de CDN para listas de permissões de IP ou nomes de domínio personalizados.
