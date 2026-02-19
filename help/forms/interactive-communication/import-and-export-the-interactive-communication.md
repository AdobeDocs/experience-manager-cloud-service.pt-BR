---
title: Importar e exportar a comunicação interativa
description: A comunicação interativa de importação e exportação permite que os usuários migrem, reutilizem e gerenciem comunicações facilmente entre ambientes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7e328932-070d-4eb3-8176-500ef31581be
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Importar e exportar a comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

O recurso de importação e exportação na Comunicação interativa (IC) permite que os usuários migrem, reutilizem e gerenciem comunicações facilmente entre ambientes. Ela permite exportar uma IC (Comunicação interativa) juntamente com seus fragmentos e modelos de dados associados de um ambiente e importá-la para outro, garantindo a consistência e reduzindo a duplicação de esforços durante a implantação.

## Principais benefícios

- Simplifica a migração de ICs entre ambientes.
- Preserva fragmentos, modelos de dados e dependências.
- Reduz o esforço de recriação de ICs entre projetos.

## Importar e exportar a comunicação interativa

Crie uma Comunicação interativa (IC) em um ambiente e reutilize-a em outro exportando-a e importando-a seguindo as etapas abaixo:

+++&#x200B;1. Como exportar a comunicação interativa

1.1. Selecione uma IC (Comunicação Interativa) [&#128279;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication)criada.

1.2. Clique na opção **Baixar** para exportá-lo como um arquivo ZIP.
1.3. O arquivo ZIP baixado inclui a IC junto com seu **modelo**, **fragmentos** e **modelo de dados** selecionados.

![Localizar IC Docu](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. Como importar a comunicação interativa

2.1. Vá para o ambiente de destino.
2.2. Navegue até **Forms > Forms e Documentos > Criar > Carregamento de Arquivo**.
2.3. Carregue o arquivo ZIP para **importar** o IC.

![Localizar IC Docu](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. Após o carregamento, o CI aparece juntamente com os fragmentos e o modelo de dados associados.

![Localizar IC Docu](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. Importar e exportar fragmento

3.1. Para exportar, selecione o fragmento necessário em **Forms > Forms e Documentos** e clique em **Baixar** para exportá-lo como um arquivo ZIP.

3.2. Para importar, vá para o ambiente de destino, navegue até Forms > Forms e Documentos > Criar > **Upload de Arquivo** e carregue o arquivo ZIP exportado.

Isso permite a fácil reutilização de fragmentos em diferentes ambientes, garantindo a consistência do design e reduzindo a duplicação de esforços.
+++
