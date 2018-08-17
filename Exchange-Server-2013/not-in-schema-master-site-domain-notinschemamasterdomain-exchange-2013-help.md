---
title: 'Não no site/domain_NotInSchemaMasterDomain mestre-esquema: Exchange 2013 Help'
TOCTitle: Não no site/domain_NotInSchemaMasterDomain mestre de esquema
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50485702
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não no site/domain\_NotInSchemaMasterDomain mestre de esquema

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque o computador que está executando a instalação não está no mesmo site do serviço de diretório Active Directory® ou domínio do servidor que é atribuída a domínio esquema função de mestre, também conhecido como flexíveis operações de mestres único ou FSMO.

A instalação do Exchange 2007 exige o controlador de domínio que serve como o mestre de esquema do domínio que estar no mesmo domínio e site do computador local que está executando a instalação do Exchange.

O mestre de esquema do domínio controla todas as atualizações e modificações no esquema do Active Directory.

Para resolver esse problema, execute a instalação do Exchange Server 2007 usando os switches **/prepareschema** e **/prepareAD** do mesmo domínio e site como o mestre de esquema do domínio.

Para obter mais informações sobre as opções de instalação **/prepareschema** e **/prepareAD**, consulte o tópico de documentação do produto Exchange 2007 "Como para preparar e domínios do Active Directory" (<https://go.microsoft.com/fwlink/?linkid=78453>)

Você pode usar a ferramenta de mestre de esquema para identificar a função. No entanto, a DLL Schmmgmt deve ser registrada para disponibilizar a ferramenta esquema como um snap-in do MMC.

Para exibir o mestre de esquema atual

1.  Em um prompt de comando, digite **regsvr32 schmmgmt. dll**
    

    > [!NOTE]
    > <STRONG>RegSvr32</STRONG> foi registrado com êxito ao seguinte caixa de diálogo é exibida:<BR>DllRegisterServer em schmmgmt teve êxito.



2.  Para abrir um novo console de gerenciamento, clique em **Iniciar**, clique em **Executar** e digite **mmc**.

3.  No menu do Console, clique em **Adicionar/Remover Snap-in**.

4.  Clique em **Adicionar** para abrir a caixa de diálogo **Adicionar Snap-in autônomo**.

5.  Selecione o **Esquema do Active Directory** e, em seguida, clique em **Adicionar**.

6.  "Esquema do active Directory" é exibido no Adicionar/remover snap-in, clique em **Fechar** e, em seguida, clique em **OK** para voltar para o console.

7.  Selecione o **Esquema do Active Directory** para que as seções de **Classes** e **atributos** são exibidas no lado direito.

8.  Com o botão direito o **Esquema do Active Directory** e clique em **Mestre de operações**.

9.  O mestre de esquema atual é exibido

Depois de identificar o mestre de esquema atual, determine qual sub-rede mestre de esquema está localizado em. Em seguida, use um dos métodos a seguir para instalar o Exchange:

  - Modifica a sub-rede no servidor do Exchange para movê-lo para o site no qual o mestre de esquema está localizado. Em seguida, instale o Exchange.

  - Forçar temporariamente uma alteração de associação do site no Exchange server e, em seguida, instalar o Exchange. Após a instalação do Exchange, retorne o servidor do Exchange ao seu site original.

Para forçar a associação do site

1.  No servidor no qual você deseja instalar o Exchange, inicie o Editor do registro. Para fazer isso, clique em **Iniciar**, clique em **Executar**, digite **regedit**e clique em **OK**.

2.  Localize a seguinte subchave do registro:
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  Crie o novo valor de **cadeia de caracteres** a seguir:
    
    Nome do valor: **SiteName**
    
    Tipo de valor: **REG\_SZ**
    
    Dados do valor: **\< site\_that\_contains\_the\_schema\_master \>**

4.  Saia do Editor do registro e reinicie o serviço logon de rede. Essa ação forçará o servidor do Exchange para participar do site que você especificou.

5.  Instale o Exchange.

6.  Remova a entrada do registro que você adicionou na etapa 3.

7.  Reinicie o serviço logon de rede. Essa ação retorna Exchange para o site original.

