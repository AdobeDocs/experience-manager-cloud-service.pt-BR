---
title: Crie formulários envolventes usando componentes principais e a tecnologia headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Crie formulários envolventes usando componentes principais e a tecnologia headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
exl-id: e1eb0812-c92e-4a18-aabb-5a70b9e6fc7d
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '3359'
ht-degree: 99%

---

# Crie formulários envolventes usando componentes principais e a tecnologia headless

## Visão geral do laboratório

Neste laboratório prático, você aprenderá:

Como usar o AEM Forms para criar adaptive forms de forma fácil, utilizando os componentes principais mais atuais e consistentes com o AEM Sites, e como habilitar experiências de captura de dados omnicanal por meio da entrega de formulários adaptáveis como formulários headless para canais da web, móveis e de bate-papo. Você também aprenderá as práticas recomendadas de estilo, personalização e desenvolvimento do front-end.

## Principais aprendizados

* **Agilidade comercial**: como um usuário empresarial, posso criar uma experiência de formulário para múltiplos canais de forma fácil.

* **Liberdade para o desenvolvedor de front-end**: como um desenvolvedor de front-end, posso controlar a experiência do usuário final utilizando formulários headless.

* **Velocidade do desenvolvedor**: como desenvolvedor, posso personalizar os componentes do Sites e formulários de forma fácil e consistente.

## Pré-requisitos


+++Sandbox do AEM Forms as a Cloud Service



<table>
        <thead>
            <tr><th>ID do laboratório</th><th>URL da instância do autor</th><th>URL da instância de publicação</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lição 1

### Objetivo

Familiarizar-se com o ambiente do AEM Forms as a Cloud Service.

### Contexto da lição

Nesta lição, você poderá se familiarizar com o AEM Forms as a Cloud Service ao navegar pela interface.

### Exercício

1. Abra o navegador e insira a URL do ambiente de autor do Cloud Service.

1. Faça logon no ambiente de autor do Cloud Service. As credenciais de logon do ambiente de criação são compartilhadas com você durante o laboratório.

1. Após fazer o logon, acesse a interface do AEM Forms. Clique em **Formulários**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Clique em **Formulários e documentos**. Ignore quaisquer pop-ups relacionados a preferências ou informações.

   ![](/help/forms/assets/screenshot2028113929.png)

   Todos os formulários disponíveis serão exibidos.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lição 2

### Objetivo

Criar um formulário adaptável utilizando os componentes principais mais recentes, configurá-lo e enviá-lo.

### Contexto da lição

Nesta lição, você atuará como um usuário empresarial e criará um adaptive form para vários canais, como Web, dispositivos móveis e bate-papo, usando componentes principais padronizados e prontos para uso na captura de dados.

### Exercício

1. Crie um ponto de acesso de envio para o formulário:

   1. Abra <https://requestbin.com/> em uma nova guia do navegador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Clique em **Criar um compartimento público** e copie a URL do ponto de acesso.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Crie um formulário adaptável usando a interface do assistente:

   1. Na guia do navegador utilizada na lição 1, acesse a interface web do AEM Forms as a Cloud Service e navegue até Formulários e documentos.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Clique em **Criar** e selecione Formulário adaptável.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Selecione o modelo **Em branco com componentes principais** na tela de seleção de modelos, conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Clique na guia **Estilo** e selecione o tema **wknd-theme**, conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Clique na guia **Envio**, selecione o cartão **Enviar para o ponto de acesso REST** e especifique o compartimento público na
      **URL do campo da solicitação POST**, conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Clique em **Criar**. Especifique um nome e um título para o formulário. Por exemplo, **contato**. Clique em **Criar**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. O editor de formulário adaptável é aberto. Ignore quaisquer pop-ups ou caixas de diálogo de preferências ou informações. Clique no navegador de componentes no painel à esquerda e adicione o componente **Rodapé** na parte inferior do formulário em branco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. O cabeçalho faz parte do modelo de formulário adaptável. Ele facilita o fornecimento de um cabeçalho/rodapé consistente em todos os daptive forms. Alternativamente, você também pode optar por mantê-lo editável no formulário, como pode ser visto no caso do componente Rodapé da próxima etapa.

   1. Adicione um componente de **Título** no meio do formulário.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Adicione um componente de **Entrada de texto** após o componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Adicione um componente de **Entrada de número**.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Adicione um componente de **Botão Enviar** ao formulário.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Clique no componente **Título** para que o **menu pop-up** seja exibido. Clique no **ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Insira `Contact Us` como o texto do título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Clique no componente **Entrada de texto** para que o menu pop-up seja exibido. Clique no **ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Insira o **Nome completo** como o rótulo do campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Clique no componente **Entrada de número** para que o menu pop-up seja exibido. Clique no **ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Insira o **Número de telefone** como o rótulo do campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Adicionar validações ao formulário:

   1. Clique no componente **Número de telefone** para que o menu pop-up seja exibido. Clique no **ícone de ferramenta** no menu para configurar o campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra a **guia de validações**, marque o campo **Obrigatório** e clique em **Concluído**. A mensagem de sucesso é exibida.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Clique em **Visualizar** para visualizar o formulário pela perspectiva do usuário final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Preencha o formulário com dados de teste
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar o formulário
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Na guia Solicitar compartimento, verifique os dados enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Agora, para o fim do exercício restante, use um formulário de registro pré-criado.

1. Abra a interface de gerenciamento do AEM Forms (por exemplo, `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`) e selecione o formulário de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Clique em **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   A mensagem de sucesso é exibida.

   ![](/help/forms/assets/screenshot2028115729.png)

   A URL de publicação do formulário seria semelhante a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para exibir o formulário publicado, substitua a ID do programa (pXXXXXX) e a ID do ambiente (eXXXXXX) na URL acima pelas IDs do seu 
ambiente.

## Lição 3

### Objetivo

Atualizar os estilos usando práticas recomendadas de desenvolvimento de front-end.

### Contexto da lição

Nesta lição, como um desenvolvedor de front-end, você aprenderá a atualizar facilmente o estilo do formulário adaptável criado anteriormente.

### Exercício

Configure o repositório local do tema:

1. Abra o prompt de comando ou o shell com direitos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. No prompt de comando, use o seguinte comando para navegar até a pasta **c:\git**

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o código de front-end do tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Use o seguinte comando na ordem listada para navegar até o diretório **aem-forms-theme-canvas** e abra o Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Selecione **Confiar nos autores de todos os arquivos da pasta pai** e clique em **Sim, eu confio nos autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service, renomeie o arquivo `env_template`.  Para renomear o arquivo, clique com o botão direito no arquivo **env_template** e selecione a opção **Renomear**.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Defina os seguintes valores para as variáveis no arquivo .env e salve o arquivo:

   * **AEM_URL**: especifica o ambiente de publicação do Cloud Service. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: especifica o caminho do formulário. Por exemplo, se o caminho do formulário for `/content/forms/af/registration`, o valor dessa variável será `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Na janela do prompt de comando, execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se receber uma mensagem solicitando a atualização do npm por meio do comando `npm notice Run npm nstall -g npm@9.6.0`, ignore a mensagem.
   > * Não execute outros comandos de npm, a menos que seja instruído na pasta de trabalho.

1. Em seguida, execute o seguinte comando para visualizar o formulário.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Depois que o comando acima for executado, aguarde a mensagem `webpack compiled`. O formulário é exibido em uma guia do navegador.

   >[!NOTE]
   >
   >Se uma tela em branco for exibida no navegador após executar o comando `npm run live` por mais de 3 a 4 minutos, altere o `localhost` na URL do navegador para 127.0.0.1 e pressione **Enter**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. No Visual Studio Code, abra o arquivo `PROJECT\src\site\_variables.scss`. Observe que a cor do `$error` é um tom de VERMELHO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. No navegador, envie o formulário para ver a cor vermelha no campo **Nome**.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Defina a cor do **$error** para **#5736eb** e salve o arquivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Atualize o navegador e envie o formulário. Observe que a cor do erro no campo de nome foi alterada de acordo.

   ![](/help/forms/assets/screenshot2028121129.png)

1. No prompt de comando, pressione **CTRL+C**, insira **Y** e pressione **Enter** para encerrar o processo do npm. É importante parar o servidor do npm para evitar conflitos nos próximos exercícios.
1. Feche as janelas do Visual Studio Code e do prompt de comando.

## Lição 4

### Objetivo

Renderizar o formulário para web/dispositivos móveis e outras interfaces como um formulário headless.

### Contexto da lição

Nesta lição, como um desenvolvedor de front-end, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário headless usando a estrutura de design do React Spectrum.

### Exercício

Configure o repositório local usando o projeto inicial do React:

1. Abra o prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. No prompt de comando, use o seguinte comando para navegar até a pasta **c:\git**

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o projeto inicial de formulário adaptável do React:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Use os seguintes comandos na ordem listada para navegar até o diretório **react-starter-kit-aem-headless-forms** e abra o Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   A janela do Visual Studio Code é aberta.

   ![](/help/forms/assets/screenshot2028117429.png)

Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service:

1. Renomeie o arquivo env_template para .env. Para renomear, clique com o botão direito no arquivo **env_template** e selecione a opção **Renomear**.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Defina os seguintes valores para as variáveis no arquivo .env. Depois de atualizar as variáveis, salve o arquivo.

   * **AEM_URL**: especifica a URL do ambiente de publicação do Cloud Service. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: especifica o caminho do formulário adaptável criado na lição anterior. Por exemplo, `/content/forms/af/registration/`

     ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra a janela de comando, verifique se você está no diretório react-starter-kit-aem-headless-forms e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Na janela do prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   O comando acima inicia um servidor de desenvolvimento local que renderiza a definição de formulário obtida do AEM através do método headless usando a biblioteca de front-end do React Spectrum.

   >[!NOTE]
   >
   > 
   > Se uma tela em branco for exibida no navegador após executar o comando `npm start` por mais de 3 a 4 minutos, altere o `localhost` na URL do navegador para 127.0.0.1 e pressione **Enter**.

   ![](/help/forms/assets/screenshot2028118229.png)

Vamos verificar a execução das regras neste formulário headless:

1. Selecione a opção **Marque a caixa para receber 5% de desconto**. A opção subsequente para utilizar o cartão de crédito será desativada.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desmarque a opção **Marque a caixa para receber 5% de desconto** para ativar a opção do cartão de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Vamos fazer alterações no formulário no servidor como um usuário empresarial e vejamos como elas são aplicadas automaticamente no formulário headless.

1. Abra a interface de gerenciamento do AEM Forms no navegador.
\
1. Selecione o formulário de **registro** e clique em **Editar.** Isso abre o formulário no editor de adaptive forms.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Selecione o campo **Número de telefone** e clique no **ícone Editar (ícone de Lápis)** na barra de ferramentas. Se não conseguir visualizar o pop-up da barra de ferramentas, alterne para o modo de edição clicando no botão **Editar** na parte superior direita, à esquerda do botão **Visualizar**.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Altere o rótulo para Número do celular. Clique em qualquer espaço vazio no formulário e as alterações serão salvas.

   ![](/help/forms/assets/screenshot2028119729.png)

Vamos publicar o formulário atualizado para propagar as alterações no ambiente de publicação.

1. Na guia da interface de gerenciamento do AEM Forms, selecione o formulário de registro e clique em **Desfazer a publicação**. Se não estiver vendo o botão **Desfazer a publicação**, pule para a etapa 3 para publicar as alterações diretamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Clique em **Desfazer a publicação**. Clique em **Fechar** na caixa de diálogo correspondente.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Depois que o navegador for atualizado, selecione o formulário de registro e clique em **Publicar**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Clique em **Publicar**. Clique em **Fechar** na caixa de diálogo correspondente.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Atualize a guia do navegador que contém o formulário headless exibido. Observe que o rótulo Número de telefone foi alterado para Número de celular.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra a janela do prompt de comando usada para iniciar o projeto **response-starter-kit-aem-headless**, pressione **CTRL+C**,
digite **Y** e pressione Enter para encerrar o processo do npm. É importante parar o servidor do npm para evitar conflitos nos próximos exercícios.

1. Feche as janelas do Visual Studio Code e do prompt de comando.


## Lição 5

### Objetivo

Renderizar o formulário como um formulário headless usando a interface do Google Material

### Contexto da lição

Nesta lição, como um desenvolvedor de front-end, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário headless usando a interface do Google Material.

### Exercício

Configure o repositório local usando o projeto inicial da interface do Material:

1. Abra o prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. No prompt de comando, use o seguinte comando para navegar até a pasta **c:\git**:

   ```Shell
   cd c:\git
   ```

1. Execute os seguintes comandos na ordem listada para criar uma pasta chamada mui e navegue até ela usando os seguintes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Use o seguinte comando para clonar o projeto inicial de formulário adaptável do React:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Use o seguinte comando na ordem listada para navegar até a pasta **react-starter-kit-aem-headless-forms** e abra o código no Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service:

1. Renomeie o arquivo **env_template** para **.env**. Para renomear, clique com o botão direito no arquivo **env_template** e selecione **Renomear**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Defina os seguintes valores para as variáveis no arquivo .env. Depois de atualizar as variáveis, salve o arquivo. Use as teclas **CTRL+S** para salvar o arquivo.

   * **AEM_URL**: especifica a URL do ambiente de publicação do Cloud Service.

   * **AEM_FORM_PATH**: especifica o caminho do formulário adaptável criado na lição anterior. Por exemplo, /content/forms/af/registration/

     ![](/help/forms/assets/screenshot2028126929.png)

1. Abra a janela de comando, verifique se você está no diretório **react-starter-kit-aem-headless-forms** e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Na janela do prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   O comando inicia um servidor de desenvolvimento local e renderiza a definição de formulário obtida do AEM através do método headless usando a biblioteca 
de front-end da interface do Google Material.

   >[!NOTE]
   >
   >Se uma tela em branco for exibida no navegador após executar o comando `npm start` por mais de 3 a 4 minutos, altere o `localhost` na URL do navegador para 127.0.0.1 e pressione **Enter**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para avaliar a execução da mesma lógica de negócios nesta representação de formulário:

   Selecione **Marque a caixa para receber 5% de desconto**. A opção subsequente **Deseja preencher um Formulário de cartão de crédito corporativo da We.Finance?** será desativada.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lição 6

### Objetivo

Criar uma aparência alternativa para o formulário headless usando variações de componente da interface do Material

### Contexto da lição

Nesta lição, como um desenvolvedor de front-end, você aprenderá a criar uma representação alternativa de diferentes componentes usando a interface do Material para o formulário adaptável criado anteriormente pelo usuário empresarial.

### Exercício

Atualize a variação de componentes no projeto headless. Para alterar a variante do componente de entrada de texto da interface do Material para `OutlinedInput`:

1. No Visual Code, navegue até o componente de entrada de texto abrindo o arquivo `index.tsx` em `src/components/textinput/index.tsx`.

1. Adicione `//` no início da linha de código 103. Isso converte a linha em um comentário.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Adicione a seguinte informação na linha 104 para usar uma variante diferente do componente e salve o arquivo. Use as teclas **CTRL+S** para salvar o arquivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   É essencial organizar corretamente as letras maiúsculas na variante “OutlinedInput”, caso contrário a compilação falhará. A compilação do ambiente de desenvolvimento local é iniciada automaticamente no prompt de comando. Aguarde até ver a seguinte mensagem

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Atualize o navegador; se ele não for atualizado automaticamente, utilize uma variante diferente para ver o componente de entrada de texto.

   ![](/help/forms/assets/screenshot2028127729.png)


   Essa alteração ocorre para usuários finais sem qualquer alteração na definição do formulário no servidor do AEM Forms, e é específica para o 
canal headless que está sendo considerado. Por exemplo, o canal da Web neste laboratório.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Feche as janelas do Visual Studio Code e do prompt de comando.

## Perguntas frequentes

+++ O Assistente de formulário adaptável está disponível publicamente?

Sim, ele está disponível com o AEM Forms as a Cloud Service.

+++


+++ Os componentes principais estão disponíveis publicamente?

Sim, os componentes principais dos formulários adaptáveis estão disponíveis com o AEM Forms as a Cloud Service.

+++

+++ Os formulários headless estão disponíveis publicamente?

Sim, os formulários headless estão disponíveis com o AEM Forms as a Cloud Service.

+++

+++ Os formulários headless exigem uma licença separada?

Não, os formulários headless usam a mesma métrica de valor de licenciamento: o número de envios de formulários.

+++

+++ Os componentes principais e formulários headless estão disponíveis com o AEM Forms 6.5?

Sim, os componentes principais dos adaptive forms e os formulários headless estão disponíveis para o Pacote de serviços 16 do AEM Forms 6.5 e versões posteriores.

+++


## Próximas etapas

Agora que aprendeu a criar adaptive forms e entregá-los a vários canais usando formulários headless, você deve tentar colocar suas novas habilidades em ação. Divirta-se e prossiga com a criação e a entrega de experiências excepcionais de captura de dados em escala para seus usuários finais, onde quer que eles estejam.

## Recursos

* [Introdução aos componentes principais de formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br)

* [Criar um formulário adaptável usando componentes principais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=pt-BR)

* [Atualizar estilo do formulário adaptável baseado em componentes principais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=pt-br)

* [Headless adaptive forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-br)

* [Uso do kit inicial headless do React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=pt-br)
