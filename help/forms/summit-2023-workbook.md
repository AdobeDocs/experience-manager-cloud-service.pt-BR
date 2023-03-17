---
title: Crie Forms envolvente usando componentes principais e headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Crie Forms envolvente usando componentes principais e headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: 26a4450c8b722fd4ca074abb3c260983c1ae0c64
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 3%

---


# Crie Forms envolvente usando componentes principais e headless

## Visão geral do Lab

Neste laboratório prático, você aprende:

Como usar o AEM Forms para criar facilmente formulários adaptáveis usando os componentes principais mais recentes que são consistentes com o AEM Sites, habilitar experiências de captura de dados omnicanais fornecendo os formulários adaptáveis como formulários sem periféricos para Web, dispositivos móveis e bate-papo. Você também aprende as práticas recomendadas de estilo, personalizações e desenvolvimento front-end.

## Capturas de chave

* **Agilidade comercial**: Como usuário empresarial, posso criar facilmente a experiência em Formulário para vários canais.

* **Poder para liderar o desenvolvedor**: Como desenvolvedor principal, posso controlar a experiência do usuário final usando formulários sem periféricos.

* **Velocidade do desenvolvedor**: Como desenvolvedor, posso personalizar de forma fácil e consistente os componentes do Sites e do Forms.

## Pré-requisitos


+++AEM Forms como sandbox de Cloud Service



<table>
        <thead>
            <tr><th>name</th><th>URL da instância do autor</th><th>Publicar URL de instância</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lição 1

### Objetivo

Familiarize-se com o ambiente as a Cloud Service do AEM Forms.

### Contexto da lição

Nesta lição, você se familiariza com o ambiente as a Cloud Service do AEM Forms navegando na interface do usuário.

### Exercício

1. Abra o navegador e insira o URL do ambiente de criação do Cloud Service. Por exemplo:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Faça logon no ambiente do autor do Cloud Service. As credenciais de logon para o ambiente do autor serão compartilhadas com você durante o laboratório.

1. Depois de fazer logon, navegue até a interface do usuário do AEM Forms. Clique em **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Clique em **Forms &amp; Documents**. Ignore quaisquer pop-ups relacionados a preferências ou informações.

   ![](/help/forms/assets/screenshot2028113929.png)

   Todos os formulários disponíveis são exibidos.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lição 2

### Objetivo

Crie um formulário adaptável usando os componentes principais mais recentes, configure e envie o formulário.

### Contexto da lição

Nesta lição, como usuário empresarial, você criará um formulário adaptável para vários canais, como Web, dispositivos móveis e chat, usando a criação de formulários adaptáveis com componentes principais OOTB padronizados para captura de dados.

### Exercício

1. Crie um endpoint de envio para o formulário:

   1. Abrir <https://requestbin.com/> em uma nova guia do navegador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Clique em **Criar um compartimento público** e copie o URL do ponto de extremidade.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Crie um formulário adaptável usando a interface do Assistente:

   1. Na guia do navegador usada na Lição 1, navegue até a interface da Web do AEM Forms como Cloud Service e navegue até Forms e Documents.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Clique em **Criar** e selecione Formulário adaptável.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Selecione o **Em branco com componentes principais** modelo da tela de seleção do modelo, como mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Clique no botão **Estilo** e selecione o **wknd-theme** tema como mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Clique no botão **Submissão** e selecione o **Enviar para o ponto final REST** e especifique o compartimento público na
      **URL para a solicitação de POST** como mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Clique em **Criar**. Especifique um nome e um título para o formulário. Por exemplo, **contato**. Clique em **Criar**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. O editor de formulário adaptável é aberto. Ignore quaisquer pop-ups ou caixas de diálogo para obter preferências ou informações. Clique no navegador de componentes no painel à esquerda e adicione o **Rodapé** na parte inferior do formulário em branco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. O cabeçalho faz parte do modelo de formulário adaptável. Ele permite uma maneira fácil de fornecer um cabeçalho/rodapé consistente em todos os formulários adaptáveis. Como alternativa, você também pode optar por mantê-lo editável no formulário, como visto para o componente Rodapé na próxima etapa.

   1. Adicione um **Título** ao meio do formulário.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Adicione um **Entrada de texto** após o componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Adicione um **Entrada do número** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Adicione um **Botão Enviar** ao formulário.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Clique no botão **Título** para que **menu pop-up** é exibida. Clique no botão **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Enter `Contact Us` como o texto do título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Clique no botão **Entrada de texto** para que o menu pop-up seja exibido. Clique no botão **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Enter **Nome completo** como rótulo de campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Clique no botão **Entrada do número** para que o menu pop-up seja exibido. Clique no botão **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Insira o **Número de telefone** como o rótulo do campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Adicionar validações ao formulário:

   1. Clique no botão **Número de telefone** para que o menu pop-up seja exibido. Clique no botão **Ícone da chave inglesa** no menu para configurar o campo .
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra o **guia validações**, marque o campo **Obrigatório** e clique em **Concluído**. A mensagem de sucesso é exibida.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Clique em **Visualizar** para visualizar o formulário de uma perspectiva do usuário final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Preencha o formulário com dados de teste
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar o formulário
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Na guia bin de solicitações , verifique os dados enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Agora, para o fim do exercício restante, use um formulário de registro pré-criado.

1. Abra a interface de gerenciamento do AEM Forms, por exemplo, `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`e selecione o formulário de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Clique em **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   A mensagem de sucesso é exibida.

   ![](/help/forms/assets/screenshot2028115729.png)

   O URL de publicação do formulário seria semelhante a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para exibir o formulário publicado, substitua a ID do programa (pXXXX) e a ID do ambiente (eXXXX) no URL acima pelas IDs do seu ambiente.

## Lição 3

### Objetivo

Atualize os estilos usando as práticas recomendadas de desenvolvimento de front-end.

### Contexto da lição

Nesta lição, como desenvolvedor front-end, você aprenderá a atualizar facilmente o estilo do formulário adaptável criado anteriormente.

### Exercício

Configure o repositório local do tema:

1. Abra o Prompt de comando ou shell com direitos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. No Prompt de comando, use o seguinte comando para navegar até **c:\git** pasta

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o código de frontend do tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Use o seguinte comando na ordem listada para navegar até o **aem-forms-theme-canvas** e abra o Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Selecionar **Confiar nos autores de todos os arquivos na pasta pai** e clique em **Sim, eu confio nos autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para renderizar o formulário hospedado no ambiente de publicação do serviço de nuvem, renomeie o `env_template` arquivo.  Para renomear o arquivo, clique com o botão direito do mouse no **env_template** e selecione o **Renomear** opção.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Defina os seguintes valores para as variáveis no arquivo .env e salve o arquivo :

   * **AEM_URL**: Especifique o ambiente de publicação do serviço de nuvem. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: Especifique o caminho do formulário. Por exemplo, se o caminho do formulário for `/content/forms/af/registration`, o valor dessa variável seria `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se receber uma mensagem solicitando a atualização de npm por meio do `npm notice Run npm nstall -g npm@9.6.0`, ignore a mensagem.
   > * Não execute outros comandos npm, a menos que seja instruído na pasta de trabalho.


1. Em seguida, execute o seguinte comando para visualizar o formulário.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Depois que o comando acima for executado, aguarde a `webpack compiled` mensagem. O formulário é exibido em uma guia do navegador.

   >[!NOTE]
   >
   >Se você tiver uma tela em branco no navegador após executar a variável `npm run live` comando por mais de 3 a 4 minutos, alterar `localhost` no URL do navegador para 127.0.0.1 e clique em **Enter**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. No Visual Studio Code, abra o `PROJECT\src\site\_variables.scss` arquivo. Observe que `$error` A cor é uma sombra de VERMELHO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. No navegador, envie o formulário para ver a cor vermelha no **Nome** campo.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Defina as **$error** colorir para **#5736eb** e salve o arquivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Atualize o navegador e envie o formulário. A cor do erro de aviso no campo de nome foi alterada de acordo.

   ![](/help/forms/assets/screenshot2028121129.png)

1. No Prompt de comando, pressione **CTRL+C**, insira **Y** e pressione **Enter** chave para encerrar o processo npm. É importante parar o servidor npm para não entrar em conflito com o próximo conjunto de exercícios.
1. Feche as janelas Código do Visual Studio e Prompt de Comando.

## Lição 4

### Objetivo

Renderize o formulário para Web/dispositivos móveis e outras interfaces como um formulário sem cabeçalho.

### Contexto da lição

Nesta lição, como desenvolvedor principal, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário sem periféricos usando a estrutura de design do espectro de reação.

### Exercício

Configure o repositório local usando o projeto de início de reação:

1. Abra o Prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. No Prompt de comando, use o seguinte comando para navegar até **c:\git** pasta

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o projeto inicial de reação de formulário adaptável:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Use os seguintes comandos na ordem listada para navegar até o **response-starter-kit-aem-headless** e abra o Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   A janela Código do Visual Studio é aberta.

   ![](/help/forms/assets/screenshot2028117429.png)

Para renderizar o formulário hospedado no ambiente de publicação do serviço de nuvem:

1. Renomeie o arquivo env_template para arquivo .env . Para renomear, clique com o botão direito do mouse no botão **env_template** e selecione o **Renomear** opção.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Defina os seguintes valores para as variáveis no arquivo .env . Depois de atualizar as variáveis, salve o arquivo .

   * **AEM_URL**: Especifique o URL do ambiente de publicação do serviço de nuvem. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: Especifique o caminho do formulário adaptável criado na lição anterior. Por exemplo, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra a janela de comando, verifique se você está no diretório response-starter-kit-aem-headless-forms e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   O comando acima inicia um servidor de desenvolvimento local que renderizaria a definição de formulário buscada de AEM de forma headless usando a biblioteca de front-end de espectro de reação.

   >[!NOTE]
   >
   > 
   > Se você tiver uma tela em branco no navegador após executar a variável `npm start` comando por mais de 3 a 4 minutos, alterar `localhost` no URL do navegador para 127.0.0.1 e clique em **Enter**.

   ![](/help/forms/assets/screenshot2028118229.png)

Vamos verificar a execução das regras neste formulário sem periféricos:

1. Selecione o **Marque a caixa para receber 5% de desconto** opção. A opção subsequente para aplicar cartão de crédito está desativada.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desmarcar **Marque a caixa para receber 5% de desconto** para ativar a opção de cartão de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Vamos fazer alterações no formulário no servidor como um usuário empresarial e exibir automaticamente as alterações refletidas no formulário sem periféricos.

1. Abra a interface de gerenciamento do AEM Forms no navegador. Por exemplo, [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Selecione o **registro** formulário e clique em **Editar.** Ele abre o formulário no editor de formulários adaptáveis.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Selecione o **Número de telefone** e clique no botão **Ícone Editar (ícone Lápis)** na barra de ferramentas. Se não conseguir ver a barra de ferramentas pop-up, alterne para o modo Editar clicando em **Editar** botão na parte superior direita, da esquerda para **Visualizar** botão.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Altere o rótulo para Número do celular. Clique em qualquer espaço vazio no formulário e as alterações feitas nele serão salvas.

   ![](/help/forms/assets/screenshot2028119729.png)

Vamos publicar o formulário atualizado para propagar as alterações no ambiente de publicação.

1. Na guia da interface de gerenciamento do AEM Forms, selecione o formulário de registro e clique em **Cancelar publicação**. Se você não vir a variável **Cancelar publicação** pressione para a etapa 3 para publicar as alterações diretamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Clique em **Cancelar publicação**. Clique em **Fechar** na respectiva caixa de diálogo.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Depois que o navegador for atualizado, selecione o formulário de registro e clique em **Publicar**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Clique em **Publicar**. Clique em **Fechar** na respectiva caixa de diálogo.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Atualize a guia do navegador com o formulário sem cabeçalho exibido. Observe que o rótulo Número de telefone foi alterado para Número de celular.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra a janela Prompt de comando usada para iniciar o **response-starter-kit-aem-headless** projeto, pressione **CTRL+C**, em seguida insira **Y** e pressione Enter para encerrar o processo npm. É importante parar o servidor npm para não entrar em conflito com o próximo conjunto de exercícios.

1. Feche as janelas Código do Visual Studio e Prompt de Comando.


## Lição 5

### Objetivo

Renderizar o formulário como um formulário sem cabeçalho usando a interface do usuário do Google Material

### Contexto da lição

Nesta lição, como um desenvolvedor de front-end, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário sem periféricos usando a interface do usuário do Google Material.

### Exercício

Configure o repositório local usando o projeto inicial da interface do usuário de material:

1. Abra o Prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. No Prompt de comando, use o seguinte comando para navegar até **c:\git** pasta:

   ```Shell
   cd c:\git
   ```

1. Execute os seguintes comandos na ordem listada para criar uma pasta chamada mui e navegue até a pasta mui usando os seguintes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Use o seguinte comando para clonar o projeto inicial de reação de formulário adaptável:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Use o seguinte comando na ordem listada para navegar até o **response-starter-kit-aem-headless** e abra o código no Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para renderizar o formulário hospedado no ambiente de publicação do serviço de nuvem:

1. Renomeie o **env_template** para **.env** arquivo. Para renomear, clique com o botão direito do mouse no botão **env_template** e selecione **Renomear**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Defina os seguintes valores para as variáveis no arquivo .env . Depois de atualizar as variáveis, salve o arquivo . Use o **CTRL + S** alterne a combinação para salvar o arquivo.

   * **AEM_URL**: Especifique o URL do ambiente de publicação do serviço de nuvem. Por exemplo, [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Especifique o caminho do formulário adaptável criado na lição anterior. Por exemplo, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Abra a janela de comando e verifique se você está no **response-starter-kit-aem-headless** e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   O comando inicia um servidor de desenvolvimento local e renderiza a definição de formulário buscada de AEM de forma headless usando a biblioteca de front-end da interface do Google Material UI.

   >[!NOTE]
   >
   >Se você tiver uma tela em branco no navegador após executar a variável `npm start` comando por mais de 3 a 4 minutos, alterar `localhost` no URL do navegador para 127.0.0.1 e clique em **Enter**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para avaliar a execução da mesma lógica de negócios nesta representação de formulário:

   Selecionar **Marque a caixa para receber 5% de desconto**. A opção subsequente **Deseja se candidatar ao Formulário de Cartão de Crédito Corporativo We.Finance?** fica desativado.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lição 6

### Objetivo

Criar uma aparência alternativa do formulário sem cabeçalho usando variações de componente da interface do usuário de material

### Contexto da lição

Nesta lição, como desenvolvedor front-end, você aprenderá a criar uma representação alternativa de diferentes componentes usando a interface do usuário de material para o formulário adaptável criado anteriormente pelo usuário empresarial.

### Exercício

Atualize a variação de componentes no projeto sem cabeçalho. Para alterar a variante do componente de entrada de texto da interface de material para `OutlinedInput`:

1. No Visual Code, navegue até o componente de entrada de texto abrindo o `index.tsx` arquivo em `src/components/textinput/index.tsx`.

1. Adicionar `//` no início da linha de código 103. Converte a linha em um comentário.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Adicione o seguinte na linha 104 para usar uma variante diferente do componente e salvar o arquivo. Use o **CTRL + S** alterne a combinação para salvar o arquivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   É essencial usar a capitalização correta para a variante &quot;OutlineInput&quot;; caso contrário, a compilação falharia. A compilação do ambiente de desenvolvimento local começa automaticamente no prompt de comando. Aguarde até visualizar a seguinte mensagem

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Atualize o navegador, se ele não for atualizado automaticamente, para ver se o componente de entrada de texto usa uma variante diferente.

   ![](/help/forms/assets/screenshot2028127729.png)


   Essa alteração ocorre para usuários finais sem qualquer alteração na definição do formulário no AEM Forms Server e é específica para o canal sem periféricos em consideração. Por exemplo, canal da Web neste laboratório.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Feche o Visual Studio Code e o Prompt de Comando do Windows.

## Perguntas frequentes

+++ O Assistente para formulário adaptável está disponível publicamente?

Sim, ele está disponível com o AEM Forms as Cloud Service.

+++


+++ Os componentes principais estão disponíveis publicamente?

Sim, os componentes principais do Adaptive Forms estão disponíveis com o AEM Forms como Cloud Service.

+++

+++ Os formulários headless estão disponíveis publicamente?

Sim, os formulários headless estão disponíveis com o AEM Forms como Cloud Service.

+++

+++ Os formulários headless exigem uma licença separada?

Não, os formulários headless usam a mesma métrica de valor de licenciamento, o mesmo número de envios de formulários.

+++

+++ Os componentes principais e formulários headless estão disponíveis com o AEM 6.5 Forms?

Sim, os componentes principais dos formulários adaptáveis e os formulários sem periféricos estão disponíveis com o AEM Forms 6.5 Service Pack 16 e seguintes.

+++


## Próximas etapas

Agora que você aprendeu a criar formulários adaptáveis e entregá-los a vários canais usando formulários sem periféricos, você deve tentar colocar suas novas habilidades em ação. Divirta-se e prossiga com a criação e o fornecimento de experiências excepcionais de captura de dados para seus usuários finais, onde estiverem, em escala!

## Recursos

* [Introdução dos componentes principais do formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Criar formulário adaptável usando componentes principais](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Atualizar estilo de AF baseado em componentes principais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Formulários adaptáveis sem periféricos](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Uso do kit inicial do React Sem Cabeça](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


