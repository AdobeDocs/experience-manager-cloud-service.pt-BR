---
title: Objeto de campo de imagem no Editor de comunicação interativa
description: Objeto de campo de imagem no Editor de comunicação interativa no AEM Forms para permitir que os autores insiram imagens em um layout de comunicação.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Objeto de campo de imagem no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente Campo de imagem no editor de comunicação interativa permite que os autores insiram imagens em um layout de comunicação. É ideal para casos de uso como identificação de foto, verificação de documento ou validação visual, em que a exibição de uma imagem para o usuário final é essencial.

Com suporte para formatos comuns como **JPEG** e **PNG**, este componente oferece opções de configuração flexíveis para definir como a imagem é exibida, armazenada e estilizada. Os autores também podem **atribuir um nome ou rótulo** ao campo de imagem, aprimorando a clareza do layout e a organização.

![Localizar IC Docu](/help/forms/interactive-communication/assets/imagefield.png)

## &#x200B;2. Propriedades

O objeto Image Field inclui várias propriedades configuráveis:

2.1. Campo de base

- **Nome:** Defina um identificador exclusivo para o campo, usado para fazer referência a regras e modelos de dados.

- **Legenda:** exibe o rótulo mostrado aos usuários na interface.

- **Selecionar imagem:** permite que o autor carregue uma imagem usando esta propriedade, geralmente usada para logotipos, IDs ou outros elementos visuais.

- **Reservar Imagem:** Defina o alinhamento da imagem, esquerda, direita, parte superior ou parte inferior ou especifique uma **posição personalizada** usando unidades como milímetros (por exemplo, 20 mm).

2.2. Localização

Controla o posicionamento espacial da imagem no layout.

- Coordenadas X e Y

- Altura e largura (em mm)

2.3. Margem

Defina o espaçamento em torno da caixa de texto:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4. Aspecto

Aparência: define o estilo visual do campo de imagem, escolhe predefinições como bordada, plana ou elevada e personaliza com cor de preenchimento, largura do traçado e estilo de canto (arredondado ou nítido).

2.5. Presença

Determina a visibilidade do objeto de imagem no tempo de execução.

- Visível

- Oculto (mantém espaço)

2.6. Vinculação de dados

Vincule o campo de imagem a uma fonte de dados para recuperar e exibir conteúdo de imagem dinâmico na comunicação.

**Tipo de Associação de Dados:** Define como o campo de imagem se conecta à estrutura ou ao esquema de dados subjacente.

**Nome de Uso:** Associa o campo de imagem usando o nome de campo especificado no modelo de dados ou esquema, permitindo que a imagem seja preenchida dinamicamente em tempo de execução.

**Usar dados globais:** conecta o campo de imagem aos dados globais que são compartilhados em toda a comunicação, garantindo a consistência no conteúdo visual.

**Sem Associação de Dados:** Mantém o campo desconectado de quaisquer dados de back-end, ideal para casos em que uma imagem estática é exibida ou quando a imagem é controlada exclusivamente pelas configurações da interface do usuário.

## &#x200B;3. Utilização

O Campo de imagem é útil em contextos nos quais o envio de conteúdo visual é obrigatório. Casos de uso comuns incluem:

- Carregando comprovante de ID (passaporte, licença)

- Envio de perfil ou fotos pessoais

- Anexação visual de documentos de suporte

Os autores podem colocar o campo em subformulários ou contêineres de layout para alinhamento e usar regras de validação personalizadas para controlar os tipos e tamanhos de arquivo aceitos.

## &#x200B;4. Práticas recomendadas

- Use rótulos ou instruções claras ao solicitar uploads de imagem.

- Limite o tamanho e os formatos de arquivo por meio da validação para fins de desempenho.

- Garanta imagens de fallback (reserva) para acessibilidade.

- Vincular o campo a um caminho de esquema significativo se a integração com o back-end

O objeto Image Field no editor de comunicação interativa é um componente versátil que melhora a interatividade dos formulários, permitindo uploads de conteúdo visual. Quando projetado com estilo, validação e vinculação de dados, ele oferece suporte a uma experiência do usuário contínua e à captura de dados eficiente para envios baseados em imagem.




