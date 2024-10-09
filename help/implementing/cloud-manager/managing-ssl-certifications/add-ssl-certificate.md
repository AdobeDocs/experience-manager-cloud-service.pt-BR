---
title: Adicionar um certificado SSL
description: Saiba como adicionar seu próprio certificado SSL ou e um certificado DV (Validação de domínio) gerenciado por Adobe usando as ferramentas de autoatendimento da Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 4%

---


# Adicionar um certificado SSL {#add-ssl-cert}

Saiba como adicionar seu próprio certificado SSL ou e certificado DV (Validação de domínio) gerenciado por Adobe usando a nuvem

>[!TIP]
>
>Um certificado pode levar alguns dias para ser provisionado. Dessa forma, a Adobe recomenda que, se você estiver fornecendo seu próprio certificado, ele seja provisionado com bastante antecedência em relação a qualquer prazo ou data de ativação.

## Pré-requisitos {#prerequisites}

* O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para adicionar um certificado.
* Se você estiver instalando seu próprio certificado, consulte **Requisitos de certificado** em [Introdução ao Gerenciamento de Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).

## Adicionar um certificado SSL {#add-certificate}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu lateral.
1. No cabeçalho **Serviços**, clique em ![Ícone Bloquear fechado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Adicionando um certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Próximo ao canto superior direito da página Certificados SSL, clique em **Adicionar certificado SSL**.

1. Na caixa de diálogo **Adicionar certificado SSL**, com base em [seu caso de uso específico](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), execute um dos procedimentos a seguir:

   | | Caso de uso | Etapas |
   | --- | --- | --- |
   | 1 | **Adicionar um certificado DV (gerenciado por Adobe)** | **Para adicionar um certificado DV (Adobe managed):**<br> a. Na caixa de diálogo **Adicionar Certificado SSL**, selecione o tipo de certificado **DV (Adobe managed)**.<br>![Adicionar um certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. No campo **Nome do certificado**, digite um nome que você deseja associar ao certificado.<br>c Na lista suspensa **Selecionar domínios**, selecione um ou mais domínios que deseja associar ao certificado DV.<br>Nenhum domínio para selecionar? Em caso afirmativo, significa que você deve adicionar um domínio personalizado. Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Quando terminar de adicionar um nome de domínio personalizado, retorne a este tópico e comece na etapa 1 novamente.<br>d Continue com a etapa 7. |
   | 2 | **Adicionar um certificado gerenciado pelo cliente (OV/EV)** | **Para adicionar um certificado gerenciado pelo cliente (OV/EV):**<br> a. Na caixa de diálogo **Adicionar Certificado SSL**, selecione o tipo de certificado **Gerenciado pelo cliente (OV/EV)**.<br>b. No campo **Nome do certificado**, digite um nome para o certificado. Este campo é apenas para fins informativos e pode ser qualquer nome que o ajude a identificar o certificado com facilidade.<br>c Nos campos **Certificado**, **Chave privada** e **Cadeia de certificados**, cole os valores necessários nos respectivos campos.<br>![Caixa de diálogo Adicionar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Todos os erros detectados nos valores são exibidos. Antes de salvar o certificado, é necessário corrigir todos os erros. Consulte [Erros de Certificado](#certificate-errors) para saber mais sobre como solucionar erros comuns.<br>d Continue com a etapa 7. |

1. No canto inferior direito da caixa de diálogo, clique em **Salvar**.

Depois que o certificado for emitido com êxito, ele será exibido com uma marca de seleção verde na tabela **Certificados SSL**.

Agora você adicionou um certificado SSL de trabalho ao projeto. Essa etapa geralmente é a primeira a configurar um nome de domínio personalizado.

* Para configurar um nome de domínio personalizado, consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Para saber mais sobre como atualizar e gerenciar certificados SSL no Cloud Manager, consulte [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

>[!TIP]
>
>Se tiver problemas ao adicionar ou gerenciar certificados, consulte [Solucionar erros de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).
