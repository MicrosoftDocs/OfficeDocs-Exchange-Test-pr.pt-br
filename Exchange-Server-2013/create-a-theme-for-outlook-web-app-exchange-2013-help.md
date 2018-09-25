---
title: 'Criar um tema para o Outlook Web App: Exchange 2013 Help'
TOCTitle: Criar um tema para o Outlook Web App
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54651975
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um tema para o Outlook Web App

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Um *tema* define a cor de fundo, as fontes, as cores de realce, os ícones e o cabeçalho que serão usados pelo MicrosoftOutlook Web App. Cada tema é um conjunto de arquivos de mídia e arquivos de folhas de estilos em cascata (.css) que são armazenados no servidor MicrosoftExchange no diretório de instalação em \\Client Access\\OWA\\prem\\*version*\\resources\\themes. Cada tema é armazenado em seu próprio subdiretório de \\themes.

O tema padrão pode ser encontrado em \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base. Cada pasta de tema contém todos os arquivos que são necessários para definir um tema. Estes arquivos incluem arquivos CSS, gráficos e um arquivo .xml que define o nome do tema. Temas adicionais são criados copiando-se todos os arquivos de um tema para uma nova pasta e modificando estes arquivos conforme necessário.

Por padrão, vários temas são instalados quando você instala o Exchange Server 2013, conforme a seguir:

  - Os arquivos CSS (.css) definem cores, gradientes e fontes.

  - Os arquivos de imagem (.png) fornecem os ícones e outros elementos gráficos. Se você editar qualquer um dos ícones, não altere seu tamanho. Se alterar o tamanho de qualquer elemento gráfico, teste suas alterações para verificar se os elementos ainda caberão juntos corretamente.

Esses arquivos são armazenados no servidor de Acesso para Cliente no diretório de instalação, em \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes. Cada tema é armazenado em um subdiretório de temas. Você pode criar temas adicionais copiando um tema existente e modificando a cópia.

Após criar um tema, talvez você também queira [Personalizar as páginas de entrada do Outlook Web App, de seleção de idioma e de erro](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md).


> [!TIP]
> A versão light do Outlook Web App não é compatível com temas.




> [!WARNING]
> Se você tiver vários servidores que suportam o Outlook Web App, você deve copiar seu tema personalizado para cada servidor. Você também deve criar uma cópia de backup de seu tema personalizado. Se você reinstalar ou atualizar o Exchange, todos os arquivos nas pastas de temas serão substituídos. Você terá que copiar seu tema de volta para a pasta adequada após fazer a reinstalação ou atualização.<BR>Faça cópias de backup de todos os arquivos que você alterará antes de começar a criar um tema personalizado.



## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 60 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretórios virtuais do Outlook Web App" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Você precisa de acesso de administrador no servidor local para realizar estes procedimentos.

  - Você precisará de um editor de texto para alterar as cores padrão e um editor de elementos gráficos para alterar as imagens. Se você deve coincidir com uma cor específica e você não puder encontrar uma correspondência para ele na [Tabela de cores](https://go.microsoft.com/fwlink/p/?linkid=280679), você pode usar uma ferramenta de edição de imagem de amostra de uma cor e determinar seu valor RGB de HTML.

  - Como prática recomendada, aconselhamos você a usar as seguintes orientações a qualquer hora que você alterar ou criar um tema do Outlook Web App:
    
      - Se você decidir editar um tema existente, faça cópias de backup dos arquivos originais antes de começar a editá-los.
    
      - Não exclua a pasta \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base ou qualquer um dos arquivos contidos nela.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Criar um novo tema do Outlook Web App

Para começar, você irá criar uma pasta para um novo tema e então copiar os arquivos de um tema existente para a nova pasta.

1.  Efetue logon no servidor do Exchange que está hospedando o diretório virtual do Outlook Web App usando uma conta à qual foi delegada a participação no grupo Administradores locais.

2.  Abra o Windows Explorer e, em seguida, encontre o diretório de instalação do servidor do Exchange.

3.  Em \\Client Access\\OWA\\prem\\*version*\\resources\\themes, crie uma nova pasta e coloque um nome, por exemplo, Fourth Coffee.

4.  Copie todos os arquivos de outro tema para a nova pasta.

## Etapa 2: Dar um nome ao novo tema

Para definir o nome para exibição do novo tema, faça o seguinte:

1.  Abra a cópia do themeinfo.xml na pasta do tema personalizado que você acabou de criar.

2.  Encontre o valor do tema do `displayname` e altere o valor para o nome que você quer usar. Por exemplo `displayname = "Fourth Coffee Theme"`.

3.  Salve e feche o themeinfo.xml.

## Etapa 3: Alterar a ordem de classificação de seu novo tema (opcional)

Se desejar, você pode alterar a ordem de classificação do novo tema editando o arquivo themeinfo.xml. A ordem de classificação determina a posição do tema no painel **Alterar tema** no menu Configurações.

Para alterar a ordem de classificação do novo tema usando o arquivo themeinfo.xml, faça o seguinte:

1.  Abra a cópia do themeinfo.xml que está na pasta do tema personalizado.

2.  Encontre o valor do tema `sortorder` e altere o valor para refletir onde você deseja que o novo tema apareça na lista. Os temas serão ordenados pelo valor numérico em ordem crescente. Por padrão, o tema básico é o primeiro e seu valor de `sortorder` é \&quot;0\&quot;. Por exemplo `sortorder="<number>"`.

3.  Salve e feche o themeinfo.xml.

## Etapa 4: Modificar o novo tema

Agora que você copiou os arquivos e deu um nome para o tema, você pode personalizá-lo. Os seguintes elementos podem ser personalizados em um tema do Outlook Web App:

  - Arquivos de imagem, que definem os ícones e a área do cabeçalho.

  - Arquivos CSS, que definem as fontes e cores.

## Arquivos de imagem

As imagens do tema são armazenadas em duas pastas em \\themes*\\\<theme name\>*\\images\\. A pasta \\images\\0 contém imagens que serão usadas nos idiomas da esquerda para a direita (como o inglês) e para idiomas que são lidos da direita para a esquerda usará as imagens na pasta \\images\\rtl.


> [!TIP]
> Algumas das imagens na pasta \images\rtl são as mesmas imagens que as da pasta \images\0 , mas uma é o espelho da outra.



Para personalizar o tema, você pode usar uma ferramenta de edição de imagem para abrir e modificar as seguintes imagens:

  - Headerbgmain.png
    
      - Esta é a imagem do cabeçalho principal. Recomendamos que a imagem não exceda a altura do cabeçalho de 30 pixels. O tema padrão não usa uma imagem de fundo, então esta imagem é transparente. Para um exemplo de um tema que possui uma imagem de fundo personalizada, veja a imagem na pasta do tema **Blueprint**.

  - Headerbgright.png
    
      - Usado como uma imagem de ladrilhamento por trás do cabeçalho. O tema padrão não usa uma imagem de fundo ladrilhada, então esta imagem é transparente. Para um exemplo de um tema que possui uma imagem de fundo ladrilhada, veja a imagem na pasta do tema **Blueprint**.

  - sprite1.mouse.png
    
      - Contém a maioria das imagens usadas em um tema. Você pode alterar a cor das imagens para combinar com seu tema e também alterar o padrão da logo do texto do Outlook Web App.
    
      - Para evitar problemas, não altere o tamanho de qualquer ícone no sprite e certifique-se de que salvou como um arquivo transparente .png.

  - themepreview.png
    
      - Esta imagem será usada para representar o tema no painel **Alterar tema** no menu de Configurações no Outlook Web App.

## Cores e fontes

Os arquivos de folhas de estilo em cascata (.css) definem as cores e fontes usadas em um tema e são armazenadas em várias pastas em \\themes\\*\<theme name\>*. A pasta \\*\<theme name\>*\\0 contém os arquivos .css que serão usados nos idiomas da esquerda para direita (como o inglês) e os idiomas que são lidos da direita para a esquerda usarão os arquivos .css na pasta \\*\<theme name\>*\\rtl. Existem também pastas de idiomas específicos, (por exemplo \\ja, \\ko, \\zhs e \\zht) que contêm os arquivos .css a serem usados com estes idiomas.

Comece modificando a pasta \\*\<theme name\>*\\images\\0. Existem quatro cores usadas em cada tema que podem ser personalizadas.

  - CorMarca: \#0072C6

  - CorPassagemMouseBarNav: \#4C9CD7

  - CorNãoLida: \#2A8DD4

  - CorFoco: \#DFEDFA

Você pode usar um editor de texto como o Bloco de Notas para pesquisar e substituir todas as instâncias destes valores com as cores de seu tema nos dois arquivos a seguir: owa2styles.mouseCSS e owa2styles2.mouseCSS. Isso deve ser feito em todas as pastas do novo tema que contenham esses arquivos .css.

## Etapa 5: Definir o tema padrão do Outlook Web App

Definir um novo tema padrão afetará somente usuários que não tenham alterado seus temas através do menu Configurações no Outlook Web App.

Para fazer com que todos os usuários usem o tema padrão, você deve desabilitar a seleção de tema além de definir um tema padrão.

## Use o Shell para definir o tema padrão do Outlook Web App

Este exemplo define o tema padrão do Outlook Web App no qual o nome do servidor é `fourthcoffee`, o nome do diretório virtual é `owa`, o nome do site é `default web site` e o tema está na pasta chamada `Custom`.

```powershell
set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)).

## Usar o Shell para desabilitar a seleção de temas do Outlook Web App

Este exemplo desabilita a seleção de temas no Outlook Web App no qual o nome do servidor é `fourthcoffee`, o nome do diretório virtual é `owa` e o nome do site é `default web site`.

```powershell
set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 
```

Você também pode concluir os dois comandos ao mesmo tempo como mostra o exemplo a seguir:

```powershell
set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)).

## Etapa 6: Executar iisreset/noforce para salvar as alterações

Se adicionar ou alterar um tema, alterar o nome de um tema ou alterar a ordem de classificação de um tema, você deve interromper e iniciar o IIS para que a alteração tenha efeito. Para fazer isso, abra uma janela de Prompt de Comando no servidor onde você criou o novo tema, e execute o comando **iisresest /nforce**.

## Como saber se essa tarefa funcionou?

1.  Entre no Outlook Web App usando o diretório virtual no servidor onde você criou seu novo tema. Se estiver testando as alterações no site padrão no servidor do Exchange que está hospedando o diretório virtual do Outlook Web App, você poderá testá-las abrindo o Internet Explorer e digitando a URL https://localhost/owa.

2.  Para alterar para seu tema personalizado, selecione o menu Configurações \> **Alterar tema** e escolha seu tema personalizado.

## Se você não visualizar as últimas alterações e executou iisreset/noforce

1.  Na barra de ferramentas do Internet Explorer, selecione o menu Configurações \> **Opções da Internet**.

2.  Na guia **Geral**, em **Histórico de navegação**, escolha **Excluir** e, em seguida, verifique se **Arquivos temporários de Internet e arquivos de site** está marcado. Depois escolha **Excluir** para remover estes arquivos.

3.  Escolha **OK** para fechar as **Opções da Internet**.

4.  Selecione **Atualizar** para ver suas alterações.

Você pode ter que repetir estas etapas para ver suas alterações cada vez que fizer uma alteração nos arquivos de tema. Se você fizer várias alterações, você pode deixar o Outlook Web App aberto e executar novamente **iisreset/noforce** no servidor e limpar os arquivos temporários do Internet Explorer conforme necessário.

