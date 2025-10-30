---
title: Suporte à edição de XDP no Editor de comunicação interativa
description: A Edição de XDP compatível com o Editor de comunicações interativas permite que os xdps existentes sejam editados dentro do Editor de comunicações interativas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 0cfbf6d61bc2d557b0a096db5b3cb26ae4570748
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# Suporte à edição de XDP no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## Introdução

O Editor de IC (Comunicação Interativa) agora oferece **suporte simples para editar arquivos XDP (Pacote de Dados XML)** no ambiente de criação. Esse aprimoramento permite que os autores gerenciem, modifiquem e mantenham modelos XDP sem esforço, sem depender de ferramentas externas. Com esse recurso, os usuários podem fazer upload, visualizar e editar arquivos XDP diretamente no Editor IC, permitindo um fluxo de trabalho unificado e eficiente do projeto até a entrega.

## Principais recursos

- **Carregar e Gerenciar Arquivos XDP:**
Carregar modelos XDP por meio do **Forms Manager**. Depois de carregados, eles ficam disponíveis para edição direta no Editor de comunicação interativa.

- **Editar Usando o Editor IC:**
Abra e edite XDPs usando o Editor IC com acesso total aos recursos de edição existentes, incluindo ajustes de layout, vinculação de dados, estilo e configuração de componentes.

- **Salvar novamente no Source:**
Quaisquer modificações feitas através do Editor IC são salvas diretamente no arquivo XDP original, mantendo a integridade da versão e simplificando o fluxo de trabalho de design.

## Suporte a fragmento

- **Referências de fragmento:**
Se um XDP fizer referência a um fragmento, esse fragmento deverá existir no **AEM no mesmo caminho relativo** definido no arquivo XDP.
Se um fragmento estiver ausente, o editor exibirá uma **mensagem de aviso** indicando que o fragmento necessário não está presente.

- **Reutilização de Fragmento no Editor:**
Todos os fragmentos XDP existentes aparecem no **Painel de Fragmentos** do Editor IC.
Os autores podem **arrastar e soltar** esses fragmentos diretamente na tela. As referências são preservadas, garantindo que as atualizações dos fragmentos se propaguem em todos os XDPs que as utilizam.

## Exemplo de uso

1. Navegue até **Forms > Forms e Documentos**.

1. Carregue seu arquivo .xdp usando a opção **Criar > Carregar Arquivo**.

1. Abra o XDP no **Editor de Comunicação Interativa**.

1. Faça as alterações necessárias de **design ou associação de dados**.

1. Salve as alterações e as atualizações serão refletidas automaticamente no arquivo XDP de origem.

## Benefícios

- Elimina a dependência de ferramentas externas para modificação do XDP.

- Preserva as associações de dados existentes e os relacionamentos de fragmento.

- Permite design consistente e ciclos de iteração mais rápidos.

## Práticas recomendadas

- Verifique se todos os fragmentos referenciados existem no caminho relativo correto antes de editar.

- Use o controle de versão para gerenciar atualizações entre dependências de XDP e fragmento.

- Valide as associações de dados após a edição para confirmar a renderização correta.

