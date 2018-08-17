---
title: 'Contêiner de objetos de sistema do Exchange duplicado no Active Directory'
TOCTitle: Contêiner de objetos de sistema do Microsoft Exchange duplicado existe no Active Directory
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50486654
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contêiner de objetos de sistema do Microsoft Exchange duplicado existe no Active Directory

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2013-02-18_

Microsoft Exchange Server 2013 instalação não pode continuar porque ele encontrado um contêiner de objetos do sistema do Microsoft Exchange duplicado no contexto de nomeação do domínio Active Directory. Quando a instalação encontrar um contêiner de objetos do sistema do Microsoft Exchange duplicado, você deve excluir o contêiner duplicado para continuar a instalação. Quando não existe um contêiner de objetos do sistema do Microsoft Exchange duplicado, você não pode resolver o problema executando **DomainPrep** novamente. Você deve identificar e exclua o contêiner de objetos do sistema do Microsoft Exchange duplicado.

Para resolver esse problema, faça o seguinte:

1.  Faça logon no controlador de domínio com credenciais administrativas.

2.  Nas **Ferramentas administrativas**, clique em **e computadores do Active Directory Users**.

3.  No painel de console Gerenciamento de **usuários do Active Directory e computadores**, clique em **Exibir**, no menu da barra de ferramentas e, em seguida, selecione **Recursos avançados**.

4.  Localize o contêiner de objetos do sistema do Microsoft Exchange duplicado.

5.  Verifique se que o contêiner de objetos do sistema do Microsoft Exchange duplicado não contém objetos do Active Directory válidos.

6.  Clique com o botão duplicado contêiner objetos do sistema do Microsoft Exchange e clique em **Excluir**.

7.  Confirme a exclusão, clicando em **Sim** na caixa de diálogo do Active Directory.


> [!NOTE]
> Se desejar que a alteração seja replicada imediatamente, você deve iniciar manualmente a replicação entre os controladores de domínio.



Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

