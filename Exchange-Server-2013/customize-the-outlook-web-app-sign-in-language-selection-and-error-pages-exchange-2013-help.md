---
title: 'Personalizar páginas de entrada do Outlook Web App, seleção de idioma e erro'
TOCTitle: Personalizar as páginas de entrada do Outlook Web App, de seleção de idioma e de erro
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54651988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizar as páginas de entrada do Outlook Web App, de seleção de idioma e de erro

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico explica como personalizar a cor e as imagens das páginas de entrada, de seleção de idioma e de erro do Outlook Web App.

O Outlook Web App entrar, seleção de idioma e páginas de erro são criadas com base nos arquivos. CSS e elementos gráficos na pasta de recursos de temas. Outlook Web App usa apenas um conjunto de entrar, seleção de idioma e as páginas de erro para todos os temas. Quaisquer modificações para essas páginas serão vistas por todos os usuários. Você pode localizar a pasta de recursos de tema no diretório de instalação Exchange em V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources. Você precisará de um editor de texto para alterar as cores padrão e um editor de elementos gráficos para alterar as imagens. Se você deve coincidir com uma cor específica e você não puder encontrar uma correspondência para ele na [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679), você pode usar uma ferramenta de edição de imagem de amostra de uma cor e determinar seu valor RGB de HTML.

Se você tiver vários servidores que suportam o Outlook Web App e quiser que todos eles usem o mesmo logon, idioma e páginas de erro, você deve copiar os arquivos modificados para cada servidor. Você também deve criar uma cópia de backup dos seus arquivos personalizados. Se você reinstalar ou atualizar o Exchange, todos os arquivos na pasta de temas serão substituídos. Você terá que copiar seus arquivos personalizados de volta para a pasta de tema adequada, após fazer a reinstalação ou atualização.


> [!IMPORTANT]
> As cópias de backup de todos os arquivos que você alterará antes de começar a criar suas páginas de logon e logoff personalizadas.



Para saber mais sobre a criação de um tema personalizado, confira [Criar um tema para o Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão desta tarefa: 45 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Editor de elementos gráficos" em "Permissões do Outlook Web App" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Personalizar a cor da página de logon:

1.  Faça logon no servidor Exchange e use o Windows Explorer para ir até o diretório de instalação do servidor Exchange e localizar \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Use um editor de texto, como o Bloco de Notas, para abrir logon.css.

3.  Procure o valor \#0072 de cor padrão c 6 e substituí-lo com o valor RGB de HTML para a cor que você deseja usar. Você pode encontrar HTML RGB valores aqui: [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salve e feche o arquivo.

## Personalizar a cor da página de erro

1.  Faça logon no servidor Exchange e use o Windows Explorer para ir até o diretório de instalação do servidor Exchange e localizar \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Use um editor de texto, como o Bloco de Notas, para abrir errorFE.css.

3.  Procure o valor \#0072 de cor padrão c 6 e substituí-lo com o valor RGB de HTML para a cor que você deseja usar. Você pode encontrar HTML RGB valores aqui: [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salve e feche o arquivo.

## Personalizar a cor da página de seleção de idioma

1.  Faça logon no servidor do Exchange e use o Windows Explorer para ir para o diretório de instalação do servidor Exchange e encontrar \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles.

2.  Use um editor de texto, como o Bloco de Notas, para abrir LanguageSelection.css.

3.  Procure o valor \#0072 de cor padrão c 6 e substituí-lo com o valor RGB de HTML para a cor que você deseja usar. Você pode encontrar HTML RGB valores aqui: [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salve e feche o arquivo.

## Personalizar as imagens das páginas de logon e de erro

Use uma ferramenta de edição de imagem para abrir e editar as imagens usadas para compilar as páginas de logon e de erro.

1.  Faça logon no servidor Exchange e use o Windows Explorer para ir até o diretório de instalação do servidor Exchange e localizar \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Use um editor de gráficos para abrir e modificar os seguintes arquivos:
    
      - owa\_text\_blue.png, para alterar o logotipo de texto "Outlook Web App".
    
      - olk\_logo\_white.png, para alterar o logotipo de aplicativo na barra da esquerda.
    
      - olk\_logo\_white\_cropped.png, para alterar a imagem no painel esquerdo da página de erro.
    
      - sign\_in\_arrow.png, para alterar o ícone à esquerda do botão "Entrar".
    
      - olk\_exchange\_text\_blue.png, para alterar o logotipo \&quot;Outlook Mobile\&quot; no layout tnarrow.
    
      - olk\_logo\_white\_small.png é usado no tnarrow.
    
      - olk\_exchange\_text\_stacked\_white\_small.png é usado no tnarrow.

3.  Procure o valor \#0072 de cor padrão c 6 e substituí-lo com o valor RGB de HTML para a cor que você deseja usar. Você pode encontrar HTML RGB valores aqui: [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Salve e feche o arquivo.

## Como saber se funcionou?

Abra a página de entrada do Outlook Web App no Internet Explorer. Se estiver testando as alterações no site padrão no servidor que hospeda o diretório virtual do Outlook Web App, você poderá testá-las abrindo o Internet Explorer e digitando a URL https://localhost/owa.

Se você não vir as alterações, faça o seguinte:

1.  Na barra de ferramentas, selecione **Configurações** \> **Opções da Internet** \> **Geral**.

2.  Em **Histórico de Navegação**, selecione **Excluir**.

3.  Selecione **Arquivos de Internet Temporários e arquivos de site** e, em seguida, selecione **Excluir**.

4.  Quando o Internet Explorer terminar a exclusão, selecione **OK** para fechar **Opções da Internet**.

5.  Atualizar a janela do navegador.


> [!TIP]
> Para ver os efeitos de suas alterações, você pode manter aberto o arquivo .css que está editando e atualizar a janela do navegador depois de salvar todas as alterações.


