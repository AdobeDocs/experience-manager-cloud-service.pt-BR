---
title: Incorporar um tema Adaptive Forms em um tema AEM Sites
description: Saiba como integrar um tema adaptável do Forms (por exemplo, Tela) a um tema do AEM Sites para que as páginas do Sites e o Adaptive Forms incorporado compartilhem um tema e uma implantação unificados.
keywords: tema de formulários adaptáveis, tema do site, tema do AEM Sites, integração de tema de formulários, pipeline front-end, incorporação de temas
feature: Adaptive Forms, Core Components
role: Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# Incorporar um tema Adaptive Forms em um tema AEM Sites

Você pode incorporar um tema Adaptive Forms (como o [tema do AEM Forms Canvas](https://github.com/adobe/aem-forms-theme-canvas)) ao seu tema do AEM Sites. Dessa forma, um único tema direciona as páginas do seu site e qualquer Forms adaptável inserido nessas páginas, com uma compilação e uma implantação por meio do [Pipeline de front-end do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html).

Este artigo é para desenvolvedores que mantêm ou personalizam o tema padrão (ou personalizado) do AEM Sites e desejam incluir o estilo do Formulário adaptável sem gerenciar uma implantação de tema do Forms separada.

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você tem:

* **AEM as a Cloud Service** com o [Pipeline de Front-End](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html) configurado para o tema do site.
* **Fontes de tema de site** - por exemplo, o [tema de modelo de site padrão](https://github.com/adobe/aem-site-template-standard) (o repositório que contém `theme/` com `src/theme.scss`, `src/components/` e assim por diante).
* **fontes de tema do Forms** - o [tema do AEM Forms Canvas](https://github.com/adobe/aem-forms-theme-canvas) (ou outro tema compatível do Adaptive Forms) clonado ou baixado localmente.
* **Node.js e npm** - para criar o tema do site (consulte o tema README para ver as versões com suporte).
* **Maven** - se você criar o pacote completo de modelo de site (opcional para trabalho somente de tema).

## Etapa 1: criar a pasta de componentes de formulário adaptável {#step-1-create-folder}

No repositório de temas do site, crie a pasta onde o tema do Forms ficará:

```text
theme/src/components/adaptiveform/
```

Todos os ativos de tema do Forms ficarão nesta pasta para que permaneçam separados dos componentes existentes do site.

## Etapa 2: Copiar componentes e imagens do tema do Forms {#step-2-copy-components-and-images}

Usando seus caminhos do **tema do Forms** (por exemplo, `aem-forms-theme-canvas`) e do **tema do site**:

1. **Copiar pastas de componente**\
   A partir do tema do Forms, copie todo o conteúdo de `src/components/` no tema do site como:

   ```text
   theme/src/components/adaptiveform/
   ```

   Assim, você tem caminhos como:

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![adicionar componentes de formulário adaptáveis](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **Copiar imagens**\
   Copie as imagens do tema do Forms no tema do site:

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   Crie `theme/src/components/adaptiveform/resources/images/` se ele não existir, em seguida, copie todos os ativos de imagem (por exemplo, `question.svg`, `Chevron-Left.svg`, `busy-state.gif` e assim por diante).

   ![adicionar imagens](/help/forms/assets/theme-add-images.png)

## Etapa 3: Copiar variáveis e mixins {#step-3-copy-variables-and-mixins}

O tema do Forms usa variáveis e mixins compartilhados em `src/site/`. Copie apenas estes dois arquivos na **raiz** de `adaptiveform/` (não dentro de uma subpasta `site`):

| Source (tema do Forms) | Destino (tema do site) |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

**não** copie o restante da pasta `src/site/` do tema do Forms; somente esses dois arquivos são necessários para os estilos de formulário inseridos.

![adicionar variáveis e mixins](/help/forms/assets/theme-add-mixin-variable.png)

## Etapa 4: corrigir caminhos de imagem no SCSS {#step-4-fix-image-paths}

No tema do Forms, os arquivos SCSS de componentes geralmente fazem referência a imagens com caminhos como `./resources/` ou `url(resources/`. Depois de copiar para o tema do site, esses caminhos devem apontar para `theme/src/components/adaptiveform/resources/images/`.

O **tema de modelo de site padrão** usa Parcel, que resolve `url()` caminhos de `theme/src/`. Portanto, quando as imagens estiverem em `theme/src/components/adaptiveform/resources/images/`, use o caminho **`components/adaptiveform/resources/images/`** (relativo a `theme/src/`).

**Localizar e substituir** a cada `.scss` em `theme/src/components/adaptiveform/`:

| Localizar | Substituir por |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**Exemplo** - antes (tema do Forms):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**Depois** (tema do site, imagens em `adaptiveform/resources/images/`):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![Alterar URL das imagens](/help/forms/assets/theme-change-url.png)

Repita o procedimento para cada arquivo SCSS em `adaptiveform/` que faz referência a imagens (botão, acordeão, assistente, contêiner, rabisco e outros). É recomendável localizar/substituir em todo o projeto no IDE por `theme/src/components/adaptiveform/`.

## Etapa 5: criar o SCSS do ponto de entrada do formulário adaptável {#step-5-create-adaptiveform-scss}

Criar **`theme/src/components/adaptiveform/_adaptiveform.scss`** no tema do site. Esse arquivo deve:

1. Importe as variáveis e mixins compartilhados.
2. Importe o arquivo SCSS principal de cada componente do Formulário adaptável.

Use o seguinte como ponto de entrada completo (corresponde à integração padrão com todos os componentes de formulário baseados em Componentes principais):

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![formulário adaptável scss](/help/forms/assets/theme-adaptive-form-scss.png)

Se o tema do Forms omitir alguns componentes (por exemplo, sem rabisco ou captcha), remova ou comente as linhas `@import` correspondentes para evitar erros de compilação. A lista acima corresponde à estrutura do [Tema da tela](https://github.com/adobe/aem-forms-theme-canvas).

## Etapa 6: importar o tema do formulário adaptável no tema do site {#step-6-import-in-theme-scss}

Em **`theme/src/theme.scss`**, adicione uma única importação no **end** do arquivo (após outras importações de componentes):

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**Exemplo** - fim de `theme.scss`:

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![adicionar formulário adaptável scss](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

Esta é a única alteração necessária na estrutura do tema do site existente; todo o código específico do formulário permanece em `src/components/adaptiveform/`.

## Etapa 7: criar e implantar {#step-7-build-and-deploy}

1. Criar o tema do site a partir da raiz de tema:

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![executar compilação](/help/forms/assets/theme-mpm-run-build.png)

2. Implante através do [Pipeline de front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html) existente. Após a implantação, o mesmo tema CSS será aplicado às páginas do site e ao Forms adaptável incorporado.

## Resolução de problemas {#troubleshooting}

| Problema | O que verificar |
|-------|-------------------------------|
| Falha na criação: &quot;arquivo não encontrado&quot; de uma imagem | Verifique se todas as imagens de formulário estão em `theme/src/components/adaptiveform/resources/images/`. Em cada `.scss` em `adaptiveform/`, use `url(components/adaptiveform/resources/images/...)` para que o caminho seja resolvido a partir de `theme/src/` (necessário para a compilação de tema de site padrão com o Parcel). Não use `../resources/` ou `resources/` sozinho, a menos que seu pacote resolva caminhos por arquivo; em seguida, use o caminho que corresponde à sua pasta de imagens. |
| Falha na compilação: &quot;arquivo não encontrado&quot; para `_variables.scss` ou `_mixin.scss` | Copie ambos os arquivos do tema do Forms `src/site/` para `theme/src/components/adaptiveform/` (a raiz do formulário adaptável), não dentro de uma subpasta `site`. |
| Falha na compilação: &quot;arquivo não encontrado&quot; para um componente (ex.: `_scribble.scss`) | O tema do Forms pode não incluir esse componente. Em `theme/src/components/adaptiveform/_adaptiveform.scss`, remova ou comente a linha `@import` desse componente. |
| O formulário é renderizado, mas não possui estilos | Confirme se a página usa a biblioteca do cliente que inclui o tema CSS e se `theme.scss` contém a linha `@import './components/adaptiveform/_adaptiveform.scss';` e se o tema foi recriado e implantado. |
| Conflito de estilos entre componentes do site e do formulário | As classes de componentes de formulário são namespaces (por exemplo, `cmp-adaptiveform-button`). Se você vir conflitos, inspecione se o CSS do site personalizado substitui essas classes e ajusta a especificidade ou a ordem. |

## Consulte também: {#see-also}

* [Usar temas para estilizar o Forms adaptável com base em Componentes principais](/help/forms/using-themes-in-core-components.md)
* [Desenvolver com pipelines de front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)
