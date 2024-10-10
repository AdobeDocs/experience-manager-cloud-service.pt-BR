---
title: Adicionar um repositório GitHub privado no Cloud Manager
description: Saiba como configurar o Cloud Manager para trabalhar com os seus repositórios privados do GitHub.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2fa4abca9823bbc62900023d637429f3fbfd894d
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 34%

---

# Adicionar um repositório GitHub privado no Cloud Manager {#private-repositories}

Ao configurar o Cloud Manager para integrar com seus repositórios GitHub privados, você pode validar seu código diretamente no GitHub usando o Cloud Manager. Essa configuração remove o requisito de sincronizar o código regularmente com o repositório Adobe.

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager. -->

>[!NOTE]
>
>Esse recurso é exclusivo do GitHub público. A compatibilidade com o GitHub auto-hospedado não está disponível.

## Configuração {#configuration}

A configuração de um repositório GitHub privado no Cloud Manager consiste em duas etapas:

1. [Adicionar um repositório GitHub privado](#add-repo) a um programa selecionado.
1. Em seguida, [valide a propriedade do repositório GitHub privado](#validate-ownership).

### Adicionar um repositório GitHub privado a um programa {#add-repo}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa ao qual deseja vincular um repositório Git privado.

1. No menu lateral, em **Serviços**, selecione ![Ícone de pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Repositórios**.

   ![A página Repositórios](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Próximo ao canto superior direito da página **Repositórios**, clique em **Adicionar Repositório**.

1. Na caixa de diálogo **Adicionar repositório**, selecione **Repositório privado** como o tipo de repositório.

   ![Adicionar repositório próprio](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Em cada campo respectivo, forneça os seguintes detalhes sobre o repositório:

   | Texto | Descrição |
   | --- | --- |
   | Nome do repositório | Um nome expressivo para o novo repositório. |
   | URL do repositório | A URL do repositório privado, que deve terminar em `.git`.<br>Por exemplo, *`https://github.com/org-name/repo-name.git`* (o caminho da URL é apenas para fins ilustrativos). |
   | Descrição (opcional) | Uma descrição detalhada do repositório. |

1. Selecione **Salvar**.
Agora você pode [validar a propriedade do repositório privado](#validate-ownership).

>[!TIP]
>
>Para obter detalhes sobre como gerenciar repositórios no Cloud Manager, consulte [Repositórios do Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).



### Validar a propriedade de um repositório GitHub privado {#validate-ownership}

O Cloud Manager agora reconhece seu repositório GitHub, mas ainda precisa de acesso. Para conceder acesso, é necessário instalar o aplicativo GitHub da Adobe e confirmar que você é proprietário(a) do repositório especificado.

**Para validar a propriedade de um repositório GitHub privado:**

1. Depois de adicionar seu próprio repositório, siga as etapas restantes na caixa de diálogo **Validação da Propriedade do Repositório Privado**.

   ![Validação de propriedade de repositório privado](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | Descrição |
   | --- | --- |
   | **Etapa 1: aplicativo GitHub** | O Cloud Manager usa um aplicativo GitHub para interagir com seu repositório privado de forma segura.<br>· Um proprietário de sua organização do GitHub deve instalar o aplicativo localizado em `https://github.com/apps/cloud-manager-for-aem` e conceder acesso ao repositório.<br>· Para obter detalhes sobre como instalar e conceder acesso, consulte a documentação do GitHub. |
   | **Etapa 2: Arquivo Secreto** | Para melhorar a segurança, você deve criar um arquivo secreto na ramificação padrão do seu repositório.<br>· Clique em **Gerar** e em **Confirmar**. O Cloud Manager gera o conteúdo do arquivo particular no campo de texto **Conteúdo do arquivo secreto**.<br>· Clique em ![Ícone Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar o conteúdo desse campo. O conteúdo do arquivo secreto será mostrado apenas uma vez. Se você não copiar o conteúdo antes de fechar esta caixa de diálogo, gere novamente o segredo. |

1. Crie um novo arquivo na ramificação padrão do repositório GitHub chamada:

   `.well-known/adobe/cloud-manager-challenge`

1. Cole o conteúdo do arquivo secreto no novo arquivo que acabou de criar e salve.

   Depois que o aplicativo estiver instalado e o arquivo secreto existir no repositório, continue a etapa.

1. Na caixa de diálogo **Validação de Propriedade de Repositório Privado**, clique em **Validar**.

O aplicativo pode ser instalado e um arquivo secreto pode ser criado em qualquer ordem. No entanto, ambas as etapas devem ser concluídas para que você possa validar.

Até a validação, o repositório será listado com um ícone vermelho, indicando que ainda não foi validado e não pode ser usado.

![Repositório não validado](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

A coluna **Tipo** na tabela na página **Repositórios** identifica repositórios fornecidos por Adobe (**Adobe**) e seus próprios repositórios privados (**GitHub**).

Se precisar retornar ao repositório mais tarde para concluir a validação, na página **Repositórios**, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na linha que representa o repositório GitHub que você acabou de adicionar. Na lista suspensa, selecione **Validação de Propriedade**.



## Usar repositórios GitHub privados com o Cloud Manager {#using}

Depois que o repositório GitHub for validado no Cloud Manager, a integração será concluída. Você pode usar o repositório com o Cloud Manager.

**Para usar repositórios privados com o Cloud Manager:**

1. Ao criar uma solicitação de pull, começa uma verificação do GitHub automaticamente.

   ![Verificações do GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Para cada solicitação de pull, é criado um [pipeline de qualidade de código de pilha completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) automaticamente. Esse pipeline é iniciado a cada atualização de solicitação de pull.

1. A verificação do GitHub permanece em estado de execução até que a verificação de qualidade do código seja concluída. Os resultados de qualidade do código são então propagados para a verificação do GitHub.

   ![Verificações de qualidade do código do GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Quando a solicitação de pull é mesclada ou fechada, o pipeline de qualidade do código de pilha completa criado é excluído automaticamente.

>[!TIP]
>
>Consulte [Anotações de verificação do GitHub](github-annotations.md) para obter detalhes sobre as informações fornecidas por meio do GitHub quando as verificações de solicitação de pull são executadas.

>[!TIP]
>
>Você pode controlar os pipelines criados automaticamente para validar cada solicitação de pull para um repositório privado. Consulte [Configuração de verificação do GitHub para repositórios privados](github-check-config.md) para obter mais informações.



## Associação de repositórios privados a pipelines {#pipelines}

Repositórios privados validados podem ser associados a [pipelines de pilha completa e front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).



## Limitações {#limitations}

Certas limitações se aplicam ao uso de repositórios privados com o Cloud Manager.

* Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados.
* Nenhuma tag do Git será criada e enviada ao usar repositórios privados em pipelines de pilha completa de produção.
* Se o aplicativo GitHub do Adobe for removido da organização GitHub, o recurso de validação de solicitações de pull será removido de todos os repositórios.
* Os pipelines que usam repositórios privados e o acionador de build ao confirmar não são iniciados automaticamente quando uma nova confirmação é enviada para a ramificação selecionada.
* A [Funcionalidade de reutilização de artefato](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) não se aplica a repositórios privados.
* Não é possível pausar a validação da solicitação de pull usando a verificação do GitHub da Cloud Manager.
Se o repositório GitHub for validado no Cloud Manager, o Cloud Manager sempre tentará validar as solicitações de pull criadas para esse repositório.
