---
title: 'Configurar anexos modernos com o OneDrive for Business e o Exchange 2016 local: Exchange 2013 Help'
TOCTitle: Configurar anexos modernos com o OneDrive for Business e o Exchange 2016 local
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70318023
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar anexos modernos com o OneDrive for Business e o Exchange 2016 local

 

_<strong>Aplica-se a:</strong>Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

**Resumo:** Como permitir que os usuários do Exchange Server 2016 no local aproveitem o uso da colaboração em documentos com o OneDrive for Business e o SharePoint Online enquanto estiverem em uma configuração híbrida.

Recentemente uma nova opção de anexo foi disponibilizada no Office 365. No Exchange 2016, essa opção, conhecida como *colaboração em documentos*, permite que os usuários locais integrem anexos armazenados no OneDrive for Business diretamente no cliente Outlook na Web.


> [!TIP]
> Começando com a versão do Exchange Server 2016, o Outlook Web App agora é conhecido como Outlook na Web.



Tradicionalmente, um usuário poderia enviar um arquivo para outras pessoas anexando-o a uma mensagem. Dessa forma, quando um ou mais destinatários fizessem alterações nas suas cópias desse arquivo, seria necessário que, no fim, todas elas fossem mescladas em algum momento. Além disso, esses arquivos anexados ocupam espaço de armazenamento na caixa de correio de cada usuário. Com a colaboração de documentos, em vez disso, os usuários inserem um link para um arquivo armazenado em uma conta do OneDrive for Business, permitindo que o arquivo a ser editado por várias pessoas permaneça no mesmo local de origem, sem a necessidade de armazenamento extra.

Antes de o ambiente do Exchange 2016 ser configurado de forma adequada para a colaboração em documentos, a caixa de diálogo de anexos padrão de um usuário do Outlook na Web será parecida com esta:

![diálogo de anexo tradicional](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "diálogo de anexo tradicional")

Depois de configurar o ambiente com as instruções abaixo, as caixas de diálogo de anexos do Outlook na Web serão parecidas com esta:

![caixa de diálogo de anexo com anexos modernos habilitados](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "caixa de diálogo de anexo com anexos modernos habilitados")

Os usuários em sua organização com caixas de correio locais e que tenham uma conta do OneDrive for Business no Office 365 estão qualificados a usar o método moderno de anexo, que permite que eles compartilhem um documento armazenado no OneDrive for Business com vários destinatários. A localização dos destinatários (online ou local) não faz diferença.

Para saber mais sobre implantações híbridas, confira [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Revise [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) e certifique-se de que entendeu as áreas que serão afetadas pela configuração de uma implantação híbrida.

  - Reveja e conclua todos os requisitos de implantação híbrido descritos em [Pré-requisitos de implantação híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](https://technet.microsoft.com/pt-br/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Configurar o Exchange 2016 para habilitar a colaboração de documentos em um ambiente híbrido

Verifique se as seguintes etapas de pré-requisito foram concluídas e, depois, utilize o procedimento a seguir para habilitar a colaboração de documentos.

**Pré-requisitos**

  - Configure o ambiente híbrido do Exchange usando o [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md) (HCW).

  - O Exchange 2016 deve ser instalado em sua organização local. O Exchange 2016 pode coexistir com versões anteriores dele, mas a colaboração em documentos funcionará apenas para as caixas de correio em um servidor Exchange 2016.

  - O servidor de autenticação deve ser instalado com todos os usuários sincronizados. É possível usar o cmdlet [Get-AuthServer](https://technet.microsoft.com/pt-br/library/jj218613\(v=exchg.150\)) para localizar seu servidor de autenticação. Recomendamos usar o HCW de um servidor Exchange 2016 para realizar as configurações do OAuth necessárias.
    

    > [!IMPORTANT]
    > É necessário configurar corretamente o OAuth entre o Exchange 2016 e o Office 365. Para saber mais, confira <A href="https://technet.microsoft.com/pt-br/library/dn594521(v=exchg.150)">Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online</A>.



  - Os usuários devem ter as licenças adequadas. Os usuários com uma conta do OneDrive for Business precisam ter licença para o OneDrive for Business ou para o SharePoint Online. É possível verificar a licença de um usuário selecionando-o no portal do Office 365 e escolhendo o botão **Editar**.
    

    > [!TIP]
    > Veja <A href="http://go.microsoft.com/fwlink/p/?linkid=627455">Configurar o OneDrive for Business no Office 365</A> para mais informações.



Execute as etapas a seguir:

1.  Configure a política da caixa de correio padrão do Outlook na Web para que ela ajuste a URL do host do OneDrive for Business.
    

    > [!TIP]
    > Vá ao Administrador de Locatário do SharePoint Online do Office 365 para recuperar a URL do host do OneDrive for Business. Por exemplo, https://contoso-my.sharepoint.com é a URL do host do Meu Site no locatário do O365 de Contoso.<BR>Mesmo que a política de caixa de correio do Outlook na Web que vem com o Exchange 2016 seja chamada "Padrão", ela não é aplicada automaticamente a qualquer caixa de correio, a menos que você a torne a política padrão ou atribua-a diretamente a uma caixa de correio.

    
    Seguindo o exemplo a seguir como base, use o Shell de Gerenciamento do Exchange para configurar a URL interna e externa do Meu Site na política de caixa de correio Padrão do Outlook na Web:
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  Em seguida, defina a política que você acabou de configurar como a política padrão para que ela seja aplicada a todas as caixas de correio ou atribua-a a usuários individuais.
    
    Para torná-la a política padrão de caixas de correio do Outlook na Web, digite o seguinte comando no Shell de Gerenciamento do Exchange:
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    Para atribuir a política à caixa de correio de uma pessoa, digite o seguinte comando no Shell de Gerenciamento do Exchange:
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (Opcional) Em cada servidor Exchange 2016, reinicie o **Pool de Aplicativos do OWA**, que fará com que a configuração funcione imediatamente. Se você não executar este comando, irá demorar alguns minutos até que seus servidores Exchange 2016 apliquem a política de caixa de correio atualizada. No Shell de Gerenciamento do Exchange execute:
    
        Restart-WebAppPool MSExchangeOWAAppPool

Uma vez configurados, os usuários do Outlook na Web poderão escolher o tipo de anexo que eles gostariam de aplicar às suas mensagens: tradicional ou moderno.

![caixa de diálogo de opções de anexo, Compartilhar com o OneDrive ou Enviar como anexo](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "caixa de diálogo de opções de anexo, Compartilhar com o OneDrive ou Enviar como anexo")

