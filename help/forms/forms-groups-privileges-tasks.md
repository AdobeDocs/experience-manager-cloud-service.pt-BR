---
title: Integrado [!DNL AEM Forms] Grupos as a Cloud Service
description: Lista de grupos de usuários prontos para uso e permissões atribuídas a cada grupo
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: d67e46e2f798e56e322d5c4aad536e718c7aae1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---

# Grupos e permissões {#aem-forms-on-osgi-groups-and-privileges}

Você pode [criar grupos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) e atribuir políticas e [usuários](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) aos grupos. Essas políticas controlam as permissões dos usuários que fazem parte do grupo.

Depois de configurar [!DNL AEM Forms] as a Cloud Service, os grupos listados na tabela abaixo, como [!DNL forms-users] e forms-power-user, estão automaticamente disponíveis para atribuição:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Permissões</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Criar, visualizar, publicar e enviar Forms adaptável</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>Fazer upload de ativos para uma instância AEM</li> 
     <li>Criar temas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Criar, visualizar, publicar e enviar Forms adaptável</li> 
     <!-- <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> -->
     <li>Fazer upload de ativos, incluindo scripts</li> 
     <li>Criar temas</li> 
     <li>Importar pacotes que contêm XDP</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Criar e visualizar Forms adaptável <!-- or interactive communications --> modelos</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>Criar e modificar um modelo de dados de formulário</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>Gerenciar aplicativos de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>
