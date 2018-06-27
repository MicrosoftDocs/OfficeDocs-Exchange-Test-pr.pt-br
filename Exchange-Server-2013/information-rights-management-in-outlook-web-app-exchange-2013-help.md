---
title: 'Gerenciamento de direitos de informação no Outlook Web App: Exchange 2013 Help'
TOCTitle: Gerenciamento de direitos de informação no Outlook Web App
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50485714
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de direitos de informação no Outlook Web App

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Os operadores de informações cada vez mais usam o email para trocar informações confidenciais. Para ajudar a proteger essas informações, as organizações podem usar o Gerenciamento de Direitos de Informação (IRM) para aplicar proteção persistente a conteúdo de mensagens. Antes de Microsoft Exchange Server 2010, o uso efetivo de proteção de IRM foi limitado aos clientes Outlook. No Exchange Server 2007, os usuários do Microsoft Outlook Web Access foram solicitados a baixar o suplemento do Gerenciamento de Direitos para o Microsoft Internet Explorer para que pudessem acessar o conteúdo protegido por IRM.

No Exchange 2013, o IRM no Outlook Web App permite aos usuários acessar a ampla funcionalidade do IRM oferecida pelo Exchange para aplicar proteção por IRM persistente ao conteúdo de mensagens.

A seguinte funcionalidade do IRM está disponível no Outlook Web App:

  - **Enviar mensagens protegidas por IRM**   Como mostrado na figura a seguir, os usuários do Outlook Web App podem usar a lista suspensa de permissões e selecionar um modelo de diretiva de direitos a ser aplicado à mensagem. Isso permite aos usuários enviar mensagens protegidas por IRM pelo Outlook Web App. As mensagens são protegidos por IRM por servidores Acesso para Cliente.
    
    ![Enviando uma mensagem protegida por IRM do OWA](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "Enviando uma mensagem protegida por IRM do OWA")  

  - **Anexos protegidos por IRM**   Quando os usuários enviam uma mensagem protegida por IRM pelo Outlook Web App, quaisquer arquivos anexados à mensagem também recebem a mesma proteção por IRM e são protegidos pelo uso do mesmo modelo de diretiva de direitos da mensagem. No Exchange 2013, a proteção por IRM é aplicada aos arquivos associados ao Microsoft Office Word, Excel e PowerPoint, bem como aos arquivos .xps e às mensagens de email. A proteção por IRM só é aplicada a um anexo se ele ainda não estiver protegido por IRM. Para saber mais sobre os modelos de políticas de direitos dos Serviços de Gerenciamento de Direitos do Active Directory, consulte [Gerenciamento de Direitos de Informação](information-rights-management-exchange-2013-help.md).
    

    > [!TIP]
    > O IRM no Outlook Web App protege somente os anexos de arquivo com suporte mencionados nesta seção. Anexos que usam formatos de arquivo sem suporte não serão protegidos. Quando os usuários do Outlook Web App protegem uma mensagem e anexam um arquivo de um tipo sem suporte, uma notificação é exibida, informando os usuários de que somente os tipos de arquivo suportados são protegidos.

    

    > [!IMPORTANT]
    > A proteção por IRM não pode ser aplicada a uma mensagem já assinada ou criptografada, usando S/MIME. Para aplicar a proteção por IRM, a assinatura e a criptografia S/MIME devem ser removidas da mensagem. O mesmo se aplica às mensagens protegidas por IRM; os usuários não podem assiná-las ou criptografá-las usando S/MIME.



  - **Ler mensagens protegidas por IRM**   As mensagens protegidas pelo remetentes que usam o cluster AD RMS de sua organização são renderizadas no painel de visualização no Outlook Web App. Nenhum suplemento precisa ser instalado, e o computador não precisa estar registrado na implantação do AD RMS. Quando um usuário abre uma mensagem ou a exibe no painel de visualização, a mensagem é descriptografada com a utilização da licença de uso adicionada pelo agente de pré-licenciamento. Depois de descriptografia, a mensagem é exibida no painel de visualização. Se uma pré-licença não estiver disponível, o Outlook Web App solicitará uma ao servidor AD RMS e renderizará a mensagem. Ao ler anexos protegidos por IRM eno Outlook Web App, Exibição de Documento WebReady não fica disponível.
    

    > [!TIP]
    > O IRM no Outlook Web App não pode impedir que os usuários façam capturas de tela usando a funcionalidade Print Screen da forma que o Outlook e outros aplicativos do Office fazem. Isso afeta o direito EXTRACT, que impede a cópia do conteúdo da mensagem, se especificado no modelo da diretiva de direitos do AD&nbsp;RMS.



  - **Vários navegadores, vários plataforma suportar do IRM**   IRM no Outlook Web App oferece vários navegadores, vários plataforma IRM suportar. IRM no Outlook Web App é suportado em todos os navegadores suportados pelo Exchange 2013, incluindo no Apple Macintosh e sistemas operacionais Linux. Para saber mais sobre os sistemas operacionais e navegadores com suporte, consulte [Supported Browsers do Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=129362).

  - **Exibição de Documento WebReady**   No Exchange 2013, os usuários podem exibir anexos protegidos por IRM com suporte utilizando a Exibição de Documento WebReady. Isso permite que os usuários exibam anexos com suporte sem precisar baixar o anexo que usa o aplicativo associado.

Procurando tarefas de gerenciamento relacionadas ao gerenciamento de IRM? Consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## Habilitar IRM no Outlook Web App

Para habilitar o IRM no Outlook Web App, é preciso adicionar a caixa de correio de Federação, uma caixa de correio do sistema criada pela Instalação do Exchange 2013, ao grupo de superusuários no AD RMS. Para mais detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md). Isso permite aos servidores Exchange 2013 acessar mensagens protegidas por IRM.

Você deve também habilitar o IRM no Outlook Web App usando o cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)) no Shell de Gerenciamento do Exchange. Isso habilita o IRM no Outlook Web App para sua organização do Exchange 2013. Você pode desabilitar ou habilitar o IRM no Outlook Web App para um diretório virtual do Outlook Web App. Você também pode controlar o IRM no Outlook Web App nos seguintes níveis de granularidade:

  - **Por diretório virtual do Outlook Web App**   Para habilitar ou desabilitar o IRM no Outlook Web App para um diretório virtual do Outlook Web App, use o cmdlet **Set-OWAVirtualDirectory** e defina o parâmetro *IRMEnabled* para `$false` ou `$true` (padrão). Isso permite que você desabilite o IRM no Outlook Web App para um diretório virtual em um servidor de Acesso para Cliente do Exchange 2013, ao mesmo tempo em que o mantém habilitado em outro diretório virtual em um servidor de Acesso para Cliente diferente.

  - **Por diretiva de caixa de correio do Outlook Web App**   Para habilitar ou desabilitar o IRM no Outlook Web App para uma diretiva de caixa de correio do Outlook Web App, use o cmdlet **Set-OWAMailboxPolicy** e defina o parâmetro *IRMEnabled* para `$false` ou `$true` (padrão). Isso permite que você habilite o IRM no Outlook Web App para um conjunto de usuários e o desabilite para outro conjunto de usuários, atribuindo a eles uma diretiva de caixa de correio do Outlook Web App diferente.

Para mais informações, consulte [Habilitar ou desabilitar o gerenciamento de direitos de informação nos servidores de acesso do cliente](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

