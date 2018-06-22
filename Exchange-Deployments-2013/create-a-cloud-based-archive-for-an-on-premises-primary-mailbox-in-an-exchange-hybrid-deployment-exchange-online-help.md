---
title: 'Criar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local em uma implantação híbrida do Exchange: Exchange 2013 Help'
TOCTitle: Criar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local em uma implantação híbrida
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253379
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local em uma implantação híbrida do Exchange

 

_<strong>Aplica-se a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2017-01-20_

Em uma implantação híbrida do Exchange, você pode configurar uma caixa de correio principal com uma caixa de correio de arquivo morto baseado na nuvem no Exchange Online.

Etapa 1: Habilitar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local

Etapa 2: Verificar se a caixa de correio de arquivo morto baseado na nuvem foi criada

(Opcional) Executar sincronização de diretório

## Antes de começar

  - O usuário com a caixa de correio principal no local deve ter uma conta de usuário na sua organização do Office 365.

  - A conta de usuário do Office 365 deve receber um Arquivamento do Exchange Online para uma licença do Exchange Server. As etapas para atribuição de uma licença estão incluídas nos procedimentos na Etapa 1.

  - Após a habilitação da caixa de correio de arquivo morto baseada em nuvem, na Etapa 1, pode levar até 30 minutos para que ela seja provisionada. Isso ocorre porque a caixa de correio de arquivo morto baseada em nuvem é criada pelo processo de sincronização de diretórios, em que seu Active Directory local é sincronizado com oAzure Active Directory (AD do Azure) no Office 365. Por padrão, a sincronização de diretório ocorre uma vez a cada 30 minutos.

## Etapa 1: Habilitar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local

Use um dos seguintes procedimentos para habilitar uma caixa de correio de arquivo morto baseado na nuvem para uma caixa de correio principal no local. Siga estas etapas no Centro de administração do Exchange na sua organização do Exchange no local e no Centro de administração do Office 365.

Criar uma caixa de correio de arquivo morto baseado na nuvem para um novo usuário

Criar uma caixa de correio de arquivo morto baseado na nuvem para um usuário existente

## Criar uma caixa de correio de arquivo morto baseado na nuvem para um novo usuário

1.  No EAC em sua organização no local, vá até **Destinatários**  \> **Caixas de Correio**.

2.  Clique em **Nova**![Ícone Adicionar](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") \> **Caixa de correio de usuário**.

3.  Na página **Nova caixa de correio de usuário**, crie uma caixa de correio para um usuário novo ou existente. Para mais detalhes sobre como criar uma caixa de correio de usuário, confira [Criar caixas de correio do usuário](https://technet.microsoft.com/pt-br/library/jj991919\(v=exchg.150\)).

4.  Clique em **Mais opções** para habilitar uma caixa de correio de arquivo morto baseado na nuvem.

5.  Em **Arquivo Morto**, clique na caixa de seleção **Criar um arquivo morto no local para este usuário** e clique em **Arquivo morto baseado na nuvem**. O nome do domínio no qual a caixa de correio de arquivo morto será provisionada é exibido.
    
    ![Em Arquivo morto, clique na caixa de seleção e em Arquivo morto baseado em nuvem](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "Em Arquivo morto, clique na caixa de seleção e em Arquivo morto baseado em nuvem")  

6.  Clique em **Salvar** para criar a caixa de correio e o arquivo morto baseado na nuvem.
    
    Na página **Caixas de Correio**, o valor **Usuário (Arquivo Morto)** é exibido na coluna **Tipo de caixa de correio** da caixa de correio selecionada.

7.  Espere até 30 minutos para a sincronização do diretório para criar uma conta de usuário correspondente no Office 365.
    

    > [!TIP]
    > No Centro de administração do Office 365, vá para <STRONG>Integridade</STRONG> &gt; <STRONG>Status de sincronização de diretório</STRONG> para ver a última vez em que a sincronização do diretório ocorreu.



8.  Após verificar se a sincronização do diretório ocorreu depois que você criou a nova caixa de correio no local, no Centro de administração do Office 365, vá até **Usuários** \> **Usuários ativos** e selecione a nova conta de usuário do Office 365 que foi criada para a nova caixa de correio no local.

9.  Na página de propriedades do usuário que é exibida, clique em **Editar** na seção **Licenças de Produto**.
    
    ![Clique em Editar, no painel de detalhes, para atribuir uma licença ao usuário selecionado](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Clique em Editar, no painel de detalhes, para atribuir uma licença ao usuário selecionado")  

10. No menu suspenso **Localização**, selecione um local para o usuário.

11. Expanda a lista de licenças do Office 365 Enterprise e atribua a licença **Arquivamento do Exchange Online para o Exchange Server**. Salve as alterações.
    
    Na coluna **Status** na lista de usuários, observe que agora uma licença foi atribuída ao usuário.

12. Novamente, espere até 30 minutos para que a sincronização do diretório provisione a caixa de correio de arquivo morto baseado na nuvem. Vá para a Etapa 2 para ver como verificar se a caixa de correio de arquivo morto baseado na nuvem foi criada. Depois que a caixa de correio de arquivo morto for criada, o usuário poderá acessá-la usando o Outlook ou o Outlook na Web.

Voltar ao início

## Criar uma caixa de correio de arquivo morto baseado na nuvem para um usuário existente

1.  No Centro de administração do Office 365, vá para **Usuários** \> **Usuários ativos** e selecione a conta de usuário para a qual você deseja criar uma caixa de correio de arquivo morto baseado na nuvem.

2.  Na página de propriedades do usuário que é exibida, clique em **Editar** na seção **Licenças de Produto**.
    
    ![Clique em Editar, no painel de detalhes, para atribuir uma licença ao usuário selecionado](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Clique em Editar, no painel de detalhes, para atribuir uma licença ao usuário selecionado")  

3.  No menu suspenso **Localização**, selecione um local para o usuário.

4.  Expanda a lista de licenças do Office 365 Enterprise e atribua a licença **Arquivamento do Exchange Online para o Exchange Server**. Salve as alterações.
    
    Na coluna **Status** na lista de usuários, observe que agora uma licença foi atribuída ao usuário.

5.  No EAC em sua organização no local, vá até **Destinatários**  \> **Caixas de Correio**.

6.  Na lista de caixas de correio, selecione o usuário ao qual você acabou de atribuir a licença.

7.  No painel de detalhes, em **Arquivamento no Local**, clique em **Habilitar**.
    
    ![Clique em Habilitar, no painel de detalhes, para habilitar a caixa de correio de arquivo morto do usuário selecionado](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "Clique em Habilitar, no painel de detalhes, para habilitar a caixa de correio de arquivo morto do usuário selecionado")  

8.  Na página **Criar arquivo morto no local**, clique em **Arquivo morto baseado na nuvem** e, em seguida, clique em **Ok**. O nome do domínio no qual a caixa de correio de arquivo morto será provisionada é exibido.
    
    ![Na página Criar arquivo morto no local, clique em Arquivo morto baseado em nuvem](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "Na página Criar arquivo morto no local, clique em Arquivo morto baseado em nuvem")  
    
    Na página **Caixas de Correio**, o valor **Usuário (Arquivo Morto)** é exibido na coluna **Tipo de caixa de correio** da caixa de correio selecionada.

9.  Aguarde até 30 minutos para que a sincronização do diretório crie a caixa de correio de arquivo morto baseado na nuvem. Vá para a Etapa 2 para ver como verificar se a caixa de correio de arquivo morto baseado na nuvem foi criada. Depois que a caixa de correio de arquivo morto for criada, o usuário poderá acessá-la usando o Outlook ou o Outlook na Web.
    

    > [!TIP]
    > No Centro de administração do Office 365, vá para <STRONG>Integridade</STRONG> &gt; <STRONG>Status de sincronização de diretório</STRONG> para ver a última vez em que a sincronização do diretório ocorreu.



Voltar ao início

## Etapa 2: Verificar se a caixa de correio de arquivo morto baseada na nuvem foi criada

Conforme foi explicado anteriormente, pode haver um atraso entre o momento em que você habilita uma caixa de correio de arquivo morto baseado na nuvem e o momento em que ela é criada de fato. Isso ocorre porque a sincronização do diretório precisa ser executada para criar a caixa de correio de arquivo morto baseado na nuvem. Estas são algumas maneiras de verificar se a caixa de correio de arquivo morto baseado em nuvem foi criada.

Em sua organização Exchange Online, execute o seguinte comando do PowerShell para exibir as propriedades relacionadas ao correio de arquivo morto do usuário. Para conectar ao Exchange Online usando o PowerShell remoto, consulte [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554).

    Get-MailUser <cloud mail user> | FL *archive*

As capturas de tela a seguir mostram as propriedades que serão retornadas quando o provisionamento da caixa de correio de arquivo morto baseado em nuvem estiver pendente e depois que a caixa de correio de arquivo morto for criada.

**Propriedades de usuário de email antes de a caixa de correio de arquivo morto baseado em nuvem ser provisionada pela sincronização de diretório**

![Propriedades de usuário de email baseado na nuvem antes que o arquivo-morto baseado na nuvem seja provisionado](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "Propriedades de usuário de email baseado na nuvem antes que o arquivo-morto baseado na nuvem seja provisionado")

Antes de a sincronização de diretório provisionar o arquivo morto baseado em nuvem, a propriedade *ArchiveStatus* é definida como `None`. Observe, também, que as propriedades *ArchiveGuid* e *ArchiveName* estão vazias.

**Propriedades de usuário de email após a caixa de correio de arquivo morto baseado em nuvem ser provisionada pela sincronização de diretório**

![Propriedades de usuário de email baseado na nuvem depois que o arquivo-morto baseado na nuvem é provisionado](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "Propriedades de usuário de email baseado na nuvem depois que o arquivo-morto baseado na nuvem é provisionado")

Após a sincronização de diretório provisionar o arquivo morto baseado em nuvem, a propriedade *ArchiveStatus* será definida como `Active` e as propriedades *ArchiveGuid* e *ArchiveName* serão populadas. Nesse ponto, o usuário poderá acessar a própria caixa de correio de arquivo morto baseado em nuvem no Outlook ou no Outlook na Web.

![O usuário pode acessar as caixas de correio de arquivo morto baseadas em nuvem no Outlook ou no Outlook na Web](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "O usuário pode acessar as caixas de correio de arquivo morto baseadas em nuvem no Outlook ou no Outlook na Web")

Na sua organização do Exchange no local, também é possível executar o seguinte comando do PowerShell para exibir as propriedades relacionadas à caixa de correio de arquivo morto baseado em nuvem de um usuário.

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**Propriedades da caixa de correio no local antes de a caixa de correio de arquivo morto baseado em nuvem ser provisionada pela sincronização de diretório**

![Propriedades da caixa de correio antes do provisionamento do arquivo morto baseado em nuvem](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "Propriedades da caixa de correio antes do provisionamento do arquivo morto baseado em nuvem")

Antes de a sincronização de diretório provisionar o arquivo morto baseado em nuvem, a propriedade *ArchiveStatus* é definida como `None` e a propriedade *ArchiveState* é definida como `HostedPending`.

**Propriedades da caixa de correio no local após a caixa de correio de arquivo morto baseado em nuvem ser provisionada pela sincronização de diretório**

![Propriedades da caixa de correio após o provisionamento do arquivo morto baseado em nuvem](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "Propriedades da caixa de correio após o provisionamento do arquivo morto baseado em nuvem")

Após a sincronização de diretório provisionar o arquivo morto baseado na nuvem, a propriedade *ArchiveStatus* é definida como `Active` e a propriedade *ArchiveState* é definida como `HostedProvisioned`. Nesse ponto, o usuário poderá acessar a própria caixa de correio de arquivo morto baseado em nuvem no Outlook ou no Outlook na Web.

Voltar ao início

## (Opcional) Executar sincronização de diretório

Como explicado anteriormente, a caixa de correio de arquivo morto baseada em nuvem é criada pelo processo de sincronização de diretório. Por padrão, seu Active Directory local é sincronizado com o AD do Azure no Office 365 uma vez a cada 30 minutos. É possível ver quando ocorreu a última sincronização de diretório acessando **Integridade** \> **Status de Sincronização de Diretório** no Centro de administração do Office 365.

Em alguns casos, talvez você queira iniciar a sincronização de diretório para provisionar a caixa de correio de arquivo morto baseada em nuvem antes da próxima sincronização agendada. É possível fazer isso executando o seguinte comando do PowerShell no servidor onde o AD do Azure Connect está instalado.

    Start-ADSyncSyncCycle -PolicyType Delta

Para obter mais informações, confira [Sincronização do Azure AD Connect: Agendador](https://go.microsoft.com/fwlink/p/?linkid=836813).

Voltar ao início

