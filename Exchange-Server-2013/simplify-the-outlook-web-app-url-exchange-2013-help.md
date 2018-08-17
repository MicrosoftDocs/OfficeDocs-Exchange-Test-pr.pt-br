---
title: 'Simplificar a URL do Outlook Web App: Exchange 2013 Help'
TOCTitle: Simplificar a URL do Outlook Web App
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54651969
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Simplificar a URL do Outlook Web App

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-07-16_

**Resumo:**  use os procedimentos deste artigo para simplificar a URL que sua organização usa para acessar o OWA no Exchange 2013.

Você pode simplificar a URL do MicrosoftOutlook Web App que os usuários utilizam para acessar a caixa de correio do Exchange Server 2013.

Para simplificar o acesso ao Outlook Web App para seus usuários, você pode configurar a página da Web do Outlook Web App, que é geralmente o site da Web padrão no IIS, para redirecionar automaticamente usuários para https. O procedimento da seção "Usar o Gerenciador do IIS para simplificar a URL do Outlook Web App e forçar o redirecionamento para SSL" redireciona uma solicitação de http://*server* para https://*server*/owa. Para ajudar a proteger as informações enviadas entre o cliente e o servidor, o site da Web padrão é definido para exigir SSL (Secure Sockets Layer) na instalação.

Ao tentar configurar o redirecionamento a partir de um diretório de nível superior no Windows Server 2008, as configurações são propagadas para diretórios de nível inferior. Por exemplo, quando você configura o redirecionamento do site padrão para o diretório virtual /owa, as configurações definidas também aparecem na página de Redirecionamento HTTP de todos os diretórios virtuais, como /Autodiscover, /Exchange e /Public. Portanto, é necessário remover o redirecionamento de todos os diretórios virtuais, exceto do que desejar redirecionar.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "IIS Manager" na seção Permissões do Outlook Web App do tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Etapa 1: usar o Gerenciador do IIS para simplificar a URL do Outlook Web App e forçar o redirecionamento para SSL

1.  Inicie o Gerenciador do IIS.

2.  Expanda o computador local, expanda **Sites** e depois clique em **Site Padrão**.

3.  Na parte inferior do painel Página Inicial do Site Padrão, clique em **Exibição de Recursos**, caso essa opção ainda não esteja selecionada.

4.  Na seção **IIS**, clique duas vezes em **Redirecionamento HTTP**.

5.  Marque a caixa de seleção **Redirecionar solicitações para este destino**.

6.  Digite o caminho absoluto do diretório virtual /owa. Por exemplo, digite **https://mail.contoso.com/owa**.

7.  Em **Comportamento do Redirecionamento**, marque a caixa de seleção **Somente redirecionar solicitações para conteúdo neste diretório (não subdiretórios)**.

8.  Na lista **Código de status**, clique em **Localizado (302)**.

9.  No painel de Ações, clique em **Aplicar**.

10. Clique em **Site da Web Padrão**.

11. No painel Página Inicial do Site Padrão, clique duas vezes em **Configurações de SSL**.

12. Em **Configurações de SSL**, desmarque **Exigir SSL**.
    

    > [!NOTE]
    > Se você não desmarcar <STRONG>Exigir SSL</STRONG>, os usuários não serão redirecionados quando digitarem uma URL desprotegida. Em vez disso, eles receberão um erro de acesso negado.



## Etapa 2: remover o redirecionamento de diretórios virtuais

Para remover o redirecionamento de um diretório virtual, siga as etapas abaixo:

1.  Abra uma janela de Prompt de Comando.

2.  Navegue até \<*Window directory*\>\\System32\\Inetsrv.

3.  Execute os seguintes comandos:
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  Conclua executando o comando `iisreset/noforce`.

Quando você configura o redirecionamento em um diretório de nível superior, um arquivo web.config pode ser criado em \<*drive*\>\\Arquivos de Programas\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab. Se isso aconteceu e, posteriormente, você removeu o redirecionamento, o Outlook pode congelar quando os usuários clicarem em **Enviar e Receber**. Para evitar que isso aconteça, depois que o redirecionamento for removido, exclua o arquivo web.config de \<*drive*\>\\Arquivos de Programas\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab.

## Como saber se funcionou?

Para verificar se você simplificou com êxito a URL do Outlook Web App e a redirecionou a uma conexão SSL, faça o seguinte:

1.  Abra um navegador da Web e digite a nova URL do Outlook Web App, usando o formato http://\<*URL*\>.

2.  Você deve ser redirecionado à página de entrada do Outlook Web App por uma conexão SSL.

