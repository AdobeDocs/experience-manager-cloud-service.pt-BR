---
title: Notas de versão do Cloud Manager 2024.10.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre as notas de versão do Cloud Manager 2024.10.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 8%

---

# Notas de versão do Cloud Manager 2024.10.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2024.10.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2024.10.0 no AEM as a Cloud Service é 3 de outubro de 2024.

A próxima versão está planejada para sexta-feira, 14 de novembro de 2024.

## Novidades {#what-is-new}

* <!-- BOTH CS & AMS --> A versão do Arquétipo AEM usada no Cloud Manager foi atualizada para a versão 26. Ver [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> Ao adicionar um novo domínio personalizado, o método de verificação anterior envolvia um longo processo de validação de DNS. A Adobe simplificou esse processo para os clientes. Agora, você só precisa fornecer um certificado SSL válido (EV ou OV), que serve como prova de propriedade. Não é mais necessário atualizar registros TXT no DNS.

  >[!NOTE]
  >
  >Esse recurso só se aplica a certificados EV e OV gerenciados pelo cliente. Os certificados DV gerenciados pelo Adobe ainda exigem a presença de um registro CNAME.

  Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

  ![Verificar domínio para um certificado EV/OV gerenciado pelo cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> Ao adicionar ou editar a infraestrutura de rede, os valores nos campos de endereço IP e máscara de rede são validados de acordo com as seguintes regras:

   * O espaço de endereço não deve se sobrepor aos endereços definidos no espaço de endereço de conexão.
   * Os endereços DNS devem pertencer à máscara de rede definida no espaço de endereço de conexão ou ser públicos.

  ![Caixa de diálogo Adicionar infraestrutura de rede](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> As alterações estão sendo feitas no formato de logs de implantação de ambiente para indexação, instalação de conteúdo mutável e transformação de trabalhos.

  >[!NOTE]
  >
  >A implantação dessa alteração está planejada em fases, com data de conclusão prevista para dezembro de 2024.

  ![Implantar no cartão de produção](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  O formato do log mudará de uma simples entrada vista no seguinte:

  ![Arquivo de log mostrando entradas simples](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  Para criar uma entrada JSON vista no seguinte:

  ![Arquivo de log mostrando entradas json](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## Programa de adoção antecipada {#early-adoption}

Faça parte do programa de adoção antecipada da Cloud Manager e tenha a chance de testar os recursos futuros.

### Traga seu próprio Git - agora com suporte para GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

O recurso **Traga seu próprio Git** foi expandido para incluir suporte para repositórios externos, como GitLab e Bitbucket. Esse novo suporte é uma adição ao suporte já existente para repositórios GitHub privados e corporativos. Ao adicionar esses novos repositórios, você também pode vinculá-los diretamente aos seus pipelines. Você pode hospedar esses repositórios em plataformas de nuvem pública ou em sua infraestrutura ou nuvem privada. Essa integração também elimina a necessidade de sincronização constante do código com o repositório Adobe e oferece a capacidade de validar solicitações de pull antes de mesclá-las em uma ramificação principal.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Atualmente, as verificações de qualidade do código de solicitação de pull prontas para uso são exclusivas de repositórios hospedados no GitHub, mas uma atualização para estender essa funcionalidade a outros fornecedores Git está em andamento.

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) com seu endereço de email associado à sua Adobe ID. Certifique-se de incluir qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou corporativo.


<!-- ## Bug fixes




## Known issues {#known-issues} -->
