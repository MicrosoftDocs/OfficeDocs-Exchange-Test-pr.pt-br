---
title: 'Sufixo DNS primário estiver faltando: Exchange 2013 Help'
TOCTitle: Sufixo DNS primário estiver faltando
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61203502
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sufixo DNS primário estiver faltando

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2014-01-15_

Microsoft Exchange Server 2013 instalação não pode continuar porque o sufixo de DNS (sistema) do nome de domínio primário para o computador que você estiver instalando o Exchange no ainda não foi configurado.

Para resolver esse problema, adicione um sufixo DNS primário no computador usando as etapas a seguir e execute a instalação novamente.


> [!IMPORTANT]
> Alterando o nome do computador ou o sufixo DNS primário, depois de instalar o Exchange 2013 não é suportado.



1.  Entre no computador em que você deseja instalar a função de Transporte de Borda como um usuário que seja membro do grupo de Administradores Locais.

2.  Abra o **Painel de Controle** e, em seguida, clique duas vezes em **Sistema**.

3.  Na seção **Nome do computador, domínio e configurações do grupo de trabalho**, clique em **Alterar configurações**.

4.  Na janela **Propriedades do Sistema**, certifique-se de que a guia **Nome do Computador** esteja selecionada e clique em **Alterar…**.

5.  Em **Alterações de Nome/Domínio do Computador**, clique em **Mais…**.

6.  Em **Sufixo DNS Primário deste computador**, insira o nome do domínio DNS do servidor de Transporte de Borda. Por exemplo, contoso.com.

7.  Clique em **OK** para fechar cada janela.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

