---
title: Componente de imagem no Editor de comunicação interativa
description: Componente de imagem no Editor de comunicação interativa no AEM Forms para permitir que os autores aprimorem os layouts de comunicação inserindo imagens estáticas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 1%

---


# Componente de imagem no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente de Imagem no Editor de comunicação interativa permite que os autores aprimorem os layouts de comunicação inserindo imagens estáticas. Esse componente é essencial para criar layouts visualmente atraentes e incorporar elementos de marca, como logotipos ou ícones visuais. Os autores podem colocá-lo nas Páginas mestras e na Exibição de design para garantir uma aparência consistente em vários formatos de saída, como o PDF.

![Localizar IC Docu](/help/forms/interactive-communication/assets/image.png)

## 2.Properties

O componente de Imagem fornece várias propriedades para ajudar a configurar sua aparência, comportamento e comportamento.

2.1. Descrição da imagem

Nome:
Atua como um identificador exclusivo para o componente de imagem, permitindo uma referência fácil na hierarquia de componentes ou no editor de regras.

Selecionar imagem: permite que o autor faça upload ou referencie uma imagem, como um logotipo, ícone ou qualquer outro visual estático de várias fontes.


2.2. Localização

Descrição: controla o posicionamento espacial da imagem no layout.

Configurações:

Coordenadas X e Y

Altura e largura (em mm)

2.3 Margem

Defina o espaçamento em torno da caixa de texto:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4. Aspecto

Aparência: define o estilo visual do campo de imagem, escolhe predefinições como bordada, plana ou elevada e personaliza com cor de preenchimento, largura do traçado e estilo de canto (arredondado ou nítido).

2.5. Presença

Descrição: determina a visibilidade do componente de imagem no tempo de execução.

- Opções:

   - Visível

   - Oculto (mantém espaço)

## 3.Usage

O componente de Imagem é ideal para:

- Inserir logotipos em cabeçalhos de documento

- Mostrando imagens do produto em faturas ou cotações

- Aumentar o envolvimento visual das comunicações

## 4.Práticas recomendadas

- Use imagens de uma biblioteca compartilhada para facilitar a reutilização e a consistência.

- Mantenha a forma da imagem consistente para evitar o alongamento ou a pixelação.

- Evite usar arquivos de imagem muito grandes para manter o documento rápido e responsivo.

- Defina a imagem para mostrar ou ocultar condicionalmente se nem sempre for necessária.

O componente de Imagem na Comunicação interativa da AEM desempenha um papel vital na criação de comunicações com marca, personalizadas e visualmente eficazes. Com propriedades configuráveis, ele melhora a experiência do usuário enquanto mantém a consistência do design em diferentes formatos.
