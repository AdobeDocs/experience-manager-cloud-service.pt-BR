---
title: Práticas recomendadas para criação de Forms de alto desempenho
description: Conheça as práticas recomendadas essenciais para criar formulários amigáveis, acessíveis e de alto desempenho usando o AEM Forms. Melhore a qualidade dos dados, a experiência do usuário e as taxas de sucesso de envio.
feature: Edge Delivery Services
role: Admin, Developer
hide: true
hidefromtoc: true
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Práticas recomendadas para a criação do Forms

## Visão geral

A criação de formulários eficazes vai além da implementação técnica — requer o entendimento da psicologia do usuário, dos padrões de acessibilidade e da otimização do desempenho. Este guia abrangente fornece práticas recomendadas e comprovadas para criar formulários que os usuários realmente desejam preencher.

### O que você vai aprender

No final deste documento, você entenderá como:

- Crie formulários amigáveis e acessíveis que funcionem para todos
- Otimizar o desempenho dos formulários e os tempos de carregamento
- Lidar com os dados do usuário de forma responsável e transparente
- Implementar a manipulação e a validação adequadas de erros
- Criar formulários com altas taxas de conclusão

### Público-alvo

Este guia foi projetado para:

- **Designers de formulários** que desejam criar melhores experiências de usuário
- **Desenvolvedores** implementando a funcionalidade do formulário
- **Profissionais de UX** otimizando fluxos de trabalho de formulário
- **Partes interessadas comerciais** que buscam melhorar as taxas de conversão de formulários

### Princípios principais

As melhores formas seguem estes princípios fundamentais:

1. **Design centralizado no usuário** - Concentre-se no que os usuários precisam realizar
2. **Acessibilidade primeiro** - Verifique se todos podem usar seus formulários
3. **Otimização do desempenho** - Os formulários rápidos são concluídos com mais frequência
4. **Responsabilidade de dados** - Respeite a privacidade do usuário e minimize a coleta de dados
5. **Comunicações claras** - Orientar os usuários durante o processo sem problemas

Construir grandes formas vai além apenas da tecnologia. Veja como garantir que seus formulários sejam fáceis de usar e atinjam suas metas:

## Criação de Forms amigáveis e acessíveis

- **Usar rótulos claros e visíveis:** todo campo de formulário precisa de um `<label>`. Não se baseie apenas no texto de espaço reservado (texto dentro do campo de entrada), pois ele desaparece quando os usuários digitam e é ruim para acessibilidade.

   - *Bom:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   - *Ruim:* `<input type="email" placeholder="Email Address">`

- **Manter Simples:** Use os tipos de entrada padrão do HTML (`<input type="date">`, `<input type="tel">`) quando possível. Geralmente, eles têm melhor suporte móvel e acessibilidade do que widgets personalizados complexos.
- **Ordem lógica e agrupamento:** organize os campos de forma a fazer sentido para o usuário. Agrupar campos relacionados usando `<fieldset>` e `<legend>`.
- **Forneça Instruções Claras:** Para todos os campos que possam ser confusos, forneça textos de ajuda concisos ou dicas de ferramentas.
- **Navegação do Teclado:** verifique se os usuários podem navegar por todo o formulário usando apenas o teclado (Tab, Shift+Tab, Enter, Barra de Espaços).
- **Tratamento de Erros:** Torne os erros óbvios e fáceis de corrigir. Exiba mensagens de erro ao lado do campo relevante e explique o que precisa ser corrigido.
- **Garantindo Que Seu Forms Seja Carregado Rapidamente e Esteja Visível**
- **Coloque o Forms em destaque:** Se um formulário for importante, certifique-se de que os usuários possam vê-lo facilmente sem muito deslocamento (&quot;acima da dobra&quot; se possível). A pesquisa da Adobe mostra que muitas formas têm baixa interação porque estão ocultas.
- **Otimizar o Assets:** mantenha qualquer JavaScript ou CSS personalizado para seus formulários o menor possível para garantir tempos de carregamento rápidos. O Edge Delivery Services ajuda no carregamento da página base, mas scripts de formulário pesados ainda podem retardar as coisas.
- **Manipulando os Dados do Usuário com Responsabilidade**
- **Pergunte somente o que você precisa:** Quanto menos informações pessoais identificáveis (PII) você solicitar, melhor. Cada campo é um motivo potencial para um usuário abandonar o formulário.
- **Seja transparente**: explique claramente *por que* você precisa de determinadas informações e *como elas serão usadas*. Link para a política de privacidade. Isso cria confiança.
- **Aprimorando a Experiência do Usuário: Alternativas do Captcha**
- **Repense os Captchas Visíveis:** Esses testes &quot;digite o texto ondulado&quot; ou &quot;clique em todos os semáforos&quot; podem ser muito frustrantes para os usuários, especialmente os portadores de deficiências, e geralmente geram altas taxas de devolução.
- **Considerar alternativas:**
   - **Campos Honeypot:** adicione um campo oculto que somente bots preencheriam. Se tiver dados, o envio provavelmente é spam.
   - **Verificações com Base no Tempo:** Meça a rapidez com que um formulário é enviado. Envios muito rápidos são geralmente bots.
   - **reCAPTCHA invisível (v3):** este serviço do Google analisa o comportamento do usuário em segundo plano e somente apresenta um desafio se o usuário parecer suspeito. Geralmente, essa é uma experiência do usuário muito melhor.

## O que fazer e o que não fazer no design do formulário

| ✅ Permitir - Para Um Forms Melhor | ❌ Não permitir - Evitar estes |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Usar marcas `<label>` visíveis para todos os campos | Usar somente texto de espaço reservado em vez de rótulos adequados |
| Preferir tipos de entrada padrão do HTML (por exemplo, `<input type="email">`) | Usar widgets personalizados muito complexos |
| Garantir a navegação completa do teclado | Fornecer mensagens de erro vagas ou ausentes |
| Mostrar mensagens de erro claras e acionáveis | Solicitar dados pessoais em excesso sem justificativa |
| Solicitar apenas as informações necessárias | Usar CAPTCHAs visíveis difíceis de resolver |
| Explicar como os dados são usados (informações ou links de privacidade) | Ocultar o formulário no fundo da página |
| Usar técnicas de CAPTCHA invisíveis ou comportamentais |                                                                  |
| Facilitar a localização do formulário na página (posição de destaque) |                                                                  |


## Próximas etapas

Este guia fornece uma visão geral do uso de formulários com o AEM Edge Delivery Services. Para obter instruções passo a passo mais detalhadas sobre configurações específicas, consulte a documentação oficial do Adobe Experience Manager:

- [Criação baseada em documento com o Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
- [Editor universal com o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Criação de Documentos (DA) e Incorporação de Conteúdo](https://www.aem.live/developer/da-tutorial)
- [Serviço de Envio do AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
