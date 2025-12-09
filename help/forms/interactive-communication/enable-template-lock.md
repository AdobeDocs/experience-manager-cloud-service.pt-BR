---
title: Bloqueio de modelo no Editor de comunicações interativas
description: O Bloqueio de modelo no Editor de comunicação interativa fornece aos autores de modelo a capacidade de bloquear o layout ou o conteúdo para os autores do documento.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Bloqueio de modelo no Editor de comunicações interativas

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O recurso Bloqueio de modelo no Editor de IC (comunicação interativa) permite que os autores de modelo restrinjam modificações a elementos específicos de um modelo de comunicação. Isso garante a consistência do design, protege o conteúdo essencial e fiscaliza o controle em equipes que reutilizam modelos para criar comunicações personalizadas.

Quando aplicados, os componentes bloqueados aparecem visualmente distintos e não podem ser modificados por autores downstream ou colaboradores, dependendo do tipo de bloqueio definido. Esse recurso ajuda a manter os padrões da marca, a integridade dos dados e a uniformidade do layout em todas as comunicações derivadas.

![Localizar IC Doc](/help/forms/interactive-communication/assets/template-lock.png)

## &#x200B;2. Tipos de bloqueio

Os autores de modelos podem aplicar Bloqueios de conteúdo e layout, individualmente ou em conjunto, para controlar alterações de conteúdo e layout nos modelos de Comunicação interativa:

### 2.1 Bloqueio de conteúdo

Um Bloqueio de conteúdo restringe qualquer modificação no conteúdo ou nas propriedades do elemento selecionado. Esse tipo de bloqueio garante que dados essenciais, texto ou propriedades de design permaneçam inalterados, mesmo quando reutilizados em várias comunicações.

Quando aplicados, os autores não podem modificar:

- Conteúdo de texto ou legendas

- Configurações de aparência (fonte, cor, plano de fundo, bordas, etc.)

- Configurações de vinculação de dados

- Elementos constituintes em um componente de contêiner (como subformulários)

### 2.2 Bloqueio de layout

Um Bloqueio de layout restringe as alterações relacionadas à posição e ao tamanho de um elemento. Isso garante que o alinhamento visual e a hierarquia de design permaneçam consistentes com os padrões de marca ou documento.

Quando aplicados, os autores não podem:

- Mover o elemento para uma nova posição na página

- Redimensionar a largura ou a altura do elemento

## &#x200B;3. Como usar o bloqueio de modelo no Editor de comunicação interativa

Siga as etapas abaixo para aplicar os Bloqueios de conteúdo ou layout no modelo de IC (Comunicação interativa):

1. Abra o seu modelo
Abra ou crie um Modelo, siga o guia [Criar um Modelo de Comunicação Interativa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/overview/create-interactive-communication-template)

1. Selecione o componente
Clique no componente (caixa de texto, imagem ou subformulário) que deseja restringir.

1. Opções de Bloqueio de Acesso
No painel Propriedades, vá para a seção Bloqueio.

1. Aplicar Bloqueios

   1. Bloqueio de conteúdo: impede edições de texto, estilo e dados.

   1. Bloqueio de layout: restringe a movimentação e o redimensionamento.

   1. Você pode ativar ambos para proteção total.

1. Salvar e verificar
Salve o template e crie uma nova IC baseada nele para confirmar que os elementos bloqueados não podem ser modificados.

## &#x200B;4. Práticas recomendadas

- **Bloqueie os Componentes críticos com antecedência:** Aplique bloqueios aos cabeçalhos, rodapés, avisos legais e logotipos para preservar a conformidade e a identidade da marca.

- **Usar bloqueios de conteúdo para precisão:** Proteger campos associados a modelos de dados principais ou texto regulamentar.

- **Usar bloqueios de layout para fins de consistência:** Evite desalinhamento ou distorção visual em modelos reutilizados com frequência.

- **Uso do bloqueio de comunicação:** verifique se os usuários downstream estão cientes de quais seções estão intencionalmente restritas para evitar confusão.
