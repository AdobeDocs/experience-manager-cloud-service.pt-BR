---
title: Gerenciar certificados SSL
description: Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b735c724bd8d68273b3c09a2dc53a13f5f6095ae
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 5%

---


# Gerenciar certificados SSL {#managing-ssl-certificates}

Saiba como usar o Cloud Manager para verificar o status dos certificados SSL e como editá-los, substituí-los, atualizá-los e excluí-los.

## Verificar o status dos certificados SSL {#checking-status-an-ssl-certificate}

O Cloud Manager fornece uma visão geral do status de todos os certificados do seu programa.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.
1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

A página **Certificados SSL** fornece o status dos certificados SSL.

| Status do certificado SSL | Descrição |
| --- | --- |
| Verde | O certificado é válido por pelo menos 14 dias a partir da data atual. |
| Laranja | O certificado vai expirar em menos de 14 dias.<br>· Certifique-se de que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager para evitar possíveis acessos ao site ou interrupções.<br>· O Cloud Manager envia notificações regulares na interface do usuário para alertá-lo sobre a expiração iminente de um certificado. |
| Vermelho | O certificado SSL expirou.<br>Consulte [Atualizar um certificado SSL gerenciado pelo cliente expirado](#update-ssl-certificate) ou [Excluir um certificado SSL](#deleting-an-ssl-certificate). |

## Atualizar um certificado SSL gerenciado pelo cliente expirado {#update-ssl-certificate}

Quando um certificado gerenciado pelo cliente expira, todos os domínios que estão em uso com o certificado expirado deixam de funcionar. Atualizar os certificados garante que o domínio continue a funcionar conforme desejado.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para atualizar um certificado SSL gerenciado pelo cliente expirado:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.
1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.
1. Na linha do certificado gerenciado pelo cliente expirado que você deseja atualizar, clique no botão de reticências na extremidade direita e selecione **Exibir e Atualizar**.

   ![Atualizar uma certificação SSL gerenciada pelo cliente expirada](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. Na caixa de diálogo **Exibir e atualizar certificado SSL**, faça o seguinte:

   * (Opcional) No campo **Nome do certificado**, digite um novo nome.
   * No campo **Certificado**, cole a nova chave de conteúdo do certificado.
   * No campo **Chave privada**, atualize este campo somente se você tiver feito alterações no certificado.
   * No campo **Cadeia de certificados** (ou cadeia de confiança), cole a cadeia de certificados.

1. Clique em **Atualizar** para salvar suas alterações e aplicá-las automaticamente.

>[!NOTE]
>
>Se você tiver dois ou mais certificados SAN que abranjam a mesma entrada de domínio SAN, se esse domínio for coberto por um certificado e o outro for atualizado, o último será instalado para o domínio.
>
>Consulte [Solucionar Problemas de Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert) para obter mais informações.

## Substituir um certificado SSL gerenciado pelo cliente expirado {#replace-ssl-certificate}

Siga as mesmas etapas descritas em [Atualizar um certificado SSL expirado](#update-ssl-certificate) para substituir um certificado SSL gerenciado pelo cliente expirado.

## Renomear um certificado SSL gerenciado por Adobe (#rename-an-ssl-certificate)

Veja a seguir alguns motivos pelos quais você pode querer renomear um certificado SSL:

* **Organização aprimorada**: renomear o certificado pode ajudar a esclarecer sua finalidade, como identificar para qual ambiente (por exemplo, preparo, produção) ou domínio ele se destina.
* **Evitando confusão**: se você estiver gerenciando vários certificados, um nome claro e descritivo pode ajudar a evitar erros, como aplicar o certificado errado ao domínio errado.
* **Conformidade e auditoria**: certificados nomeados corretamente podem ser mais fáceis de rastrear para fins de segurança e auditoria.

**Para renomear um certificado SSL gerenciado por Adobe:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.
1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.
1. Na página **Certificados SSL**, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo certificado *Adobe Managed* você deseja renomear.
1. No menu suspenso, clique em **Renomear**.
1. Na caixa de diálogo **Renomear Certificado DV**, no campo de texto **Nome do certificado**, digite o novo nome do certificado.
1. Clique em **Renomear**.

## Excluir um certificado SSL {#deleting-an-ssl-certificate}

A exclusão de certificados SSL gerenciados por Adobe ou pelo cliente do Cloud Manager é uma ação permanente que não pode ser desfeita. Como prática recomendada, o Adobe recomenda que você salve os arquivos SSL localmente antes de excluí-los no Cloud Manager.

>[!NOTE]
>
>Não é possível excluir um certificado SSL gerenciado por Adobe que tenha um ou mais domínios ativos associados a ele. Todos os domínios ativos associados devem ser excluídos antes de excluir o certificado SSL. Consulte [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para saber mais.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para excluir um certificado SSL:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.
1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.
1. Na página Certificados SSL, na linha da tabela do certificado que você deseja excluir, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)na extremidade direita
1. No menu suspenso, clique em **Excluir**.
Se o botão Excluir tiver um ícone de informações como visto na imagem a seguir, consulte a Observação acima.

   ![Botão Excluir com ícone Informações](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. Na caixa de diálogo **Excluir Certificado SSL**, clique em **Excluir** para confirmar a exclusão.
1. Execute o pipeline para desimplantar o certificado excluído.

## Configurações de CDN pré-existentes {#pre-existing-cdn}

Se você já tiver uma configuração de CDN para seu certificado SSL, a página **Certificados SSL** exibirá uma mensagem informativa. Ele incentiva você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e possam ser gerenciadas no Cloud Manager.

A mensagem desaparece depois que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de um a dois dias úteis para a mensagem desaparecer.

Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas **Lista de permissões de IP** e **Ambientes** para ambientes que tenham configurações de CDN pré-existentes para Listas de permissões de IP ou nomes de domínio personalizados.
