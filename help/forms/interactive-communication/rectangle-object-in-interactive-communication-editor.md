---
title: Objeto Retangle no Editor de comunicação interativa
description: O Retangle Object no Editor de comunicação interativa no AEM Forms permite que os autores adicionem elementos gráficos moldados que servem como divisores de layout, acentos visuais ou contêineres de conteúdo.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Objeto Retangle no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## &#x200B;1. Introdução

O componente Retângulo no editor de IC (Comunicação interativa) permite que os autores adicionem elementos gráficos moldados que servem como divisores de layout, destaques visuais ou contêineres de conteúdo. Os retângulos melhoram a hierarquia visual e orientam a atenção do usuário em layouts de comunicação estruturada.
Esse objeto não está vinculado aos dados, mas é fundamental para melhorar a clareza do design, agrupar campos relacionados e aprimorar a apresentação geral.

![Localizar IC Docu](/help/forms/interactive-communication/assets/rectangle.png)

## &#x200B;2. Propriedades

O objeto Retangle inclui várias propriedades personalizáveis:

2.1. Nome

Nome: um identificador exclusivo do retângulo. Usado principalmente para referência em hierarquias de layout ou aplicação consistente de estilos.

2.2. Localização

- **Descrição:** Determina onde o retângulo aparece no layout do documento.

- **Configurações:**

   - Coordenadas de **X e Y:** defina o posicionamento horizontal e vertical.

   - **Altura e Largura (em mm):** Controle o tamanho do retângulo.

2.3. Margem

Define o espaçamento ao redor do componente de retângulo para separá-lo de outros elementos da interface:

- Superior (Acima)

- Inferior (Abaixo)

- Esquerda

- Direita

2.4. Aspecto

- **Descrição:** Controla o estilo visual do retângulo.

- **Opções de Personalização:**

   - **Preenchimento:** A cor interna do retângulo.

   - **Traço:** a cor de contorno do retângulo.

   - **Largura do Traço:** Espessura da borda do retângulo.

   - **Estilo:** Estilos predefinidos, como plano, bordado ou elevado.

   - **Bordas:** Controla a aparência do canto (por exemplo, bordas arredondadas ou nítidas).

2.5. Presença

- **Descrição:** Especifica se o retângulo é exibido quando a comunicação é renderizada.

- **Opções:**

   - **Visível:** mostra o retângulo no tempo de execução.

   - **Oculto:** Mantém o espaço de layout sem mostrar o retângulo.

## &#x200B;3. Utilização

O objeto Retangle é normalmente usado para fins de layout e estilo em vez de entrada de conteúdo. Casos de uso comuns incluem:

- Criação de separação visual entre seções

- Realce de elementos agrupados

- Melhorando a legibilidade e o equilíbrio visual

- Enquadrar cabeçalhos, rodapés ou seções de chamada

Os retângulos podem ser combinados com outros elementos de layout, como subformulários ou contêineres, para estruturas de design visual complexas.

## &#x200B;4. Práticas recomendadas

- Use um estilo consistente para retângulos no layout para garantir harmonia visual.

- Aplique margens e espaçamento adequados para evitar a aglomeração de campos adjacentes.

- Escolha as cores de preenchimento e traçado alinhadas ao tema da marca ou do documento.

- Use bordas arredondadas sutilmente para melhorar a estética em layouts modernos de interface do usuário.

- Ocultar retângulos se eles forem necessários apenas para fins de design durante a edição, mas não forem necessários na saída final.

O objeto Retangle é uma ferramenta não interativa mas poderosa no Editor IC. Quando estilizado e posicionado de maneira eficaz, ele melhora a precisão do layout, o fluxo visual e a experiência do usuário sem adicionar complexidade à vinculação de dados ou à interatividade.


