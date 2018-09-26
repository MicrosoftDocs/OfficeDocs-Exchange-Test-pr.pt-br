---
title: 'Instalar um pacote de idiomas para UM: Exchange 2013 Help'
TOCTitle: Instalar um pacote de idiomas para UM
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50486952
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalar um pacote de idiomas para UM

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Para disponibilizar um idioma na lista de idiomas de Unificação de mensagens disponíveis em um plano de discagem ou atendedor automático, você deve instalar primeiro o pacote de idiomas de Unificação de MENSAGENS apropriado. Você pode instalar o pacote de idiomas em um servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange, usando o arquivo executável autoextraível de idioma específico ou o comando **setup.exe /AddUmLanguagePack** . Antes de instalar um pacote de idiomas de Unificação de MENSAGENS, você deve primeiro baixá-lo para uma pasta local no servidor de caixa de correio. Você pode baixar os pacotes de idiomas de Unificação de MENSAGENS do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542). Há um arquivo executável separado para cada idioma.

Após instalar o pacote de idiomas de Unificação de MENSAGENS apropriado, você pode exibir a lista de pacotes de idiomas de Unificação de MENSAGENS instaladas, exibindo a lista suspensa na página **configurações** de um plano de discagem ou lista suspensa **idioma da interface de voz automatizados** na página **Geral** de um atendedor automático. Você também pode configurar o idioma padrão para ser um idioma diferente do inglês (en-US) em planos de discagem de Unificação de MENSAGENS e atendedores automáticos.


> [!CAUTION]
> Os pacotes de idiomas de Unificação de MENSAGENS para o Microsoft Exchange Server 2007 ou Exchange 2007 Service Pack 1 (SP1), SP2, ou SP3 ou Exchange 2010 Service Pack 1 SP1, SP2 ou SP3 não podem ser usados em um servidor de caixa de correio Exchange 2013.



Para tarefas adicionais relacionadas aos idiomas da UM, consulte [Procedimentos de idiomas, saudações e prompts de Unificação de mensagens](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Servidor de caixa de correio (serviço de Unificação de MENSAGENS)" no [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verificar que o servidor de caixa de correio é instalado em um computador diferente do servidor de acesso para cliente ou os servidores de acesso para cliente e caixa de correio estão no mesmo hardware.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o arquivo de instalação de pacote de idioma UM (.exe) para instalar um pacote de idiomas de Unificação de MENSAGENS

1.  Do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542), baixe o arquivo de pacote (.exe) de idioma de Unificação de MENSAGENS específicas do idioma em uma pasta local no servidor de caixa de correio.

2.  Clique duas vezes a UMLanguagePack. arquivo *\<CultureCode\>.exe* . Por exemplo, para o pacote de idioma alemão UM, você pode baixar o arquivo denominado UMLanguagePack.de-DE.exe.

3.  No Assistente de instalação Exchange 2013, na página **Contrato de licença**, leia os termos do contrato, selecione **eu aceito os termos do contrato de licença** e clique em **Avançar**.

4.  Na página **Pacote de Idiomas para Unificação de Mensagens**, verifique se o idioma correto está listado na janela **O(s) seguinte(s) Pacote(s) de Idiomas para Unificação de Mensagens será(ão) instalados** e clique em **Instalar**.

5.  Clique em **Concluir** para concluir a instalação do pacote de idiomas para UM.

## Use setup.exe para instalar um pacote de idiomas de Unificação de MENSAGENS

Este exemplo instala o japonês (ja-JP) UM pacote de idiomas que tenha sido baixado até a pasta D:\\Exchange\\UMLanguagePacks em um servidor de caixa de correio.

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

Este exemplo instala o espanhol do México (es-MX) e alemão (de-DE) UM pacotes de idiomas que foram baixados para a pasta D:\\Exchange\\UMLanguagePacks em um servidor de caixa de correio.

```powershell
setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

> [!WARNING]
> Se você não usar o parâmetro /IAcceptExchangeServerLicenseTerms, você verá o seguinte erro: Bem-vindo à instalação autônoma do Microsoft Exchange Server 2013. Você precisa aceitar os termos de licença para instalar o Microsoft Exchange Server 2013. Para ler o contrato de licença, visite http://go.microsoft.com/fwlink/p/?LinkId=150127. Para aceitar o contrato de licença, adicione o parâmetro /IAcceptExchangeServerLicenseTerms ao comando que você está executando. Para obter mais informações, execute a instalação /?.



Para obter mais informações sobre os idiomas de Unificação de MENSAGENS disponíveis e os códigos de cultura, consulte [Saudações e prompts de idiomas de Unificação de MENSAGENS](um-languages-prompts-and-greetings-exchange-2013-help.md).

