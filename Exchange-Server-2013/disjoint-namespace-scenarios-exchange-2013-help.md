---
title: 'Cenários de namespace separado: Exchange 2013 Help'
TOCTitle: Cenários de namespace separado
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50486170
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cenários de namespace separado

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico fornece informações sobre o conceito de espaços e os cenários com suporte para a implantação do Microsoft Exchange 2013 em um domínio que tenha um namespace separado.

**Sumário**

Nomes de domínio DNS e NetBIOS

Namespaces não contíguos

Namespaces de separado e Exchange 2013

Permitir que os servidores Exchange 2013 acessar os controladores de domínio que estão separados

Exibir DNS e NetBIOS informações relacionadas ao nome de um computador que executa o Windows Server 2008

## Nomes de domínio DNS e NetBIOS

Primeiro, algumas informações básicas. Cada computador que esteja na Internet tem um nome de sistema de nome de domínio (DNS). Isso também é conhecido como o *nome do computador* ou o *nome de host*. Todos os computadores executando o sistema operacional Windows com os recursos de redes também tem um nome NetBIOS.

Um computador que executa o Windows em um domínio Active Directory tem um nome de domínio DNS e de um nome de domínio NetBIOS, da seguinte maneira:

  - **Nome de domínio DNS**   O nome de domínio DNS consiste em um ou mais subdomínios separados por um ponto (**.** ) e é encerrado por um nome de domínio de nível superior. Por exemplo, no nome de domínio DNS corp.contoso.com, os subdomínios são corp e contoso e o nome de domínio de nível superior é com.

  - **Nome de domínio NetBIOS**   Geralmente, o nome de domínio NetBIOS é o subdomínio do nome de domínio DNS. Por exemplo, se o nome de domínio DNS for contoso.com, o nome de domínio NetBIOS é contoso. Se o nome de domínio DNS for corp.contoso.com, o nome de domínio NetBIOS é corp.


> [!TIP]
> Para encontrar informações de DNS e NetBIOS para computadores que executam o Windows Server 2008, consulte DNS de modo de exibição e a informações relacionadas ao nome NetBIOS de um computador que executa o Windows Server 2008.



Um computador em um domínio Active Directory também tem um sufixo DNS primário e pode ter sufixos DNS adicionais. Por padrão, o sufixo DNS primário é igual ao nome de domínio DNS. Para obter instruções detalhadas sobre como alterar o sufixo DNS primário, consulte os procedimentos neste tópico.

Você pode definir o nome de domínio DNS e nome NetBIOS do domínio Active Directory quando você configura o primeiro controlador de domínio no domínio. Para obter mais informações sobre como configurar controladores de domínio, consulte [Funções do controlador de domínio](https://go.microsoft.com/fwlink/p/?linkid=268367) and [Active Directory Domain Services Overview](https://go.microsoft.com/fwlink/p/?linkid=268366).

## Namespaces não contíguos

Na maioria das topologias de domínio, o sufixo DNS primário dos computadores no domínio é o mesmo que o nome de domínio DNS.

Em alguns casos, você talvez precise esses namespaces sejam diferentes. Isso é chamado um *namespace separado*. Por exemplo, uma fusão ou aquisição pode causar você tenha uma topologia com um namespace separado. Além disso, se o gerenciamento de DNS em sua empresa é dividido entre os administradores que gerenciam Active Directory e os administradores que gerenciam redes, você pode precisar possui uma topologia com um namespace separado.

Um cenário de namespace separado é a uma na qual o sufixo DNS primário de um computador não corresponde o nome de domínio DNS onde o computador reside. Computador com o sufixo DNS primário que não corresponda é considerado *separado*. Outro cenário de namespace não contíguo ocorre se o nome de domínio NetBIOS de um controlador de domínio não coincidir com o nome de domínio DNS.

## Exchange 2013 e namespaces não contíguo

Exchange 2013 oferece suporte a três cenários a seguir para implantar o Exchange em um domínio que tenha um namespace separado:

  - **Sufixo DNS primário e o nome de domínio DNS são diferentes**   O sufixo DNS primário do controlador de domínio não é igual ao nome de domínio DNS. Computadores que são membros do domínio podem ser separado ou não separado.

  - **Computador membro é não contíguo**   Um computador membro de um domínio Active Directory é não contíguo, mesmo que o controlador de domínio não é não contíguo.

  - **Nome NetBIOS do controlador de domínio difere do subdomínio do seu nome de domínio DNS**   O nome de domínio NetBIOS do controlador de domínio não é igual ao subdomínio do nome de domínio DNS do controlador de domínio.

Esses cenários são detalhados nas seções a seguir.


> [!TIP]
> Há suporte para executar Exchange 2013 nos cenários namespace separado descritos neste tópico. No entanto, se você tiver um cenário de namespace separado que não seja um dos cenários descritos neste tópico, você deve trabalhar com o Microsoft Services para implantar Exchange 2013. Para obter mais informações, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=94845">Microsoft Services</A>.



## Cenário: Sufixo DNS primário e o nome de domínio DNS são diferentes

Neste cenário, o sufixo DNS primário do controlador de domínio não é igual ao nome de domínio DNS. O controlador de domínio é não contíguo neste cenário. Computadores que são membros do domínio, incluindo Exchange servidores e computadores de clientes do Microsoft Outlook, podem ter um sufixo DNS primário que corresponde ao sufixo DNS primário do controlador de domínio ou que corresponde ao nome de domínio DNS.

## Cenário: O computador membro é não contíguo

Neste cenário, o sufixo DNS primário de um computador membro em que Exchange 2013 está instalado não é igual ao nome de domínio DNS, mesmo que o sufixo DNS primário do controlador de domínio é o mesmo que o nome de domínio DNS. Neste cenário, você tem um controlador de domínio que não seja separado e um computador membro que é não contíguo. Computadores de membros que estão executando o Outlook podem ter um sufixo DNS primário que corresponde ao sufixo DNS primário do servidor não contíguo Exchange ou corresponde ao nome de domínio DNS.

## Cenário: Nome NetBIOS do controlador de domínio difere subdomínio do seu nome de domínio DNS

Neste cenário, o nome de domínio NetBIOS do controlador de domínio não é o mesmo que o nome de domínio DNS do mesmo controlador de domínio.

**Nome de domínio NetBIOS não corresponde o nome de domínio DNS**

![O nome de domínio NetBIOS não corresponde ao nome de domínio DNS](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "O nome de domínio NetBIOS não corresponde ao nome de domínio DNS")

## Permitir que os servidores Exchange 2013 acessar os controladores de domínio que estão separados

Para permitir que os servidores Exchange 2013 acessar os controladores de domínio que estão separados, você deve modificar o atributo deActive Directory**msDS-AllowedDNSSuffixes**no contêiner de objeto do domínio. Você deve adicionar ambos os sufixos DNS para o atributo. Para obter instruções detalhadas sobre como modificar o atributo, consulte [sufixo DNS primário do computador não corresponder ao FQDN do domínio em que reside](https://go.microsoft.com/fwlink/p/?linkid=98848).

Além disso, para garantir que a lista de pesquisa de sufixo DNS contém todos os espaços para nome DNS que são implantados dentro da organização, você deve configurar a lista de pesquisa para cada computador no domínio que é não contíguo. A lista dos namespaces deve incluir não apenas o sufixo DNS primário do controlador de domínio e o nome de domínio DNS, mas também quaisquer namespaces adicionais para outros servidores com os quais Exchange podem interoperar (por exemplo, monitoramento de servidores ou para aplicativos de terceiros). Você pode fazer isso, definindo diretiva de grupo para o domínio. Para obter mais informações sobre a diretiva de grupo, consulte os tópicos a seguir:

  - [Perguntas frequentes (FAQ) de diretiva de grupo](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Novas diretivas de grupo para DNS no Windows Server 2003](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=294785)

  - [Diretiva de grupo](https://go.microsoft.com/fwlink/p/?linkid=268043)

Para obter instruções detalhadas sobre como configurar a lista de pesquisa de sufixo DNS da diretiva de grupo, consulte [Configurar a lista de pesquisa de sufixo DNS para um namespace separado](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md).

## Exibir DNS e NetBIOS informações relacionadas ao nome de um computador que executa o Windows Server 2008

1.  Clique em **Iniciar**, clique com o botão direito do mouse em **Computador** e clique em **Propriedades**.

2.  No **sistema**, o nome de host DNS e o sufixo DNS primário são exibidos em **nome do computador, domínio e configurações de grupo de trabalho** ao lado do **nome completo do computador**. O nome de domínio DNS será exibido ao lado de **domínio**.

3.  Clique em **Alterar configurações**.

4.  Nas **Propriedades do sistema**, na guia **Nome do computador**, clique em **Alterar**.

5.  Em **Alterações de nome/domínio do computador**, clique em **mais**. O sufixo DNS primário é exibido em **sufixo DNS primário deste computador**. O nome NetBIOS do computador é exibido em **nome NetBIOS do computador**.
    
    Para alterar o sufixo DNS primário, digite o sufixo DNS primário do novo em **sufixo DNS primário deste computador** e, em seguida, clique em **OK**.

6.  De uma janela de Prompt de comando, digite **set**. A variável USERDNSDOMAIN exibe o nome de domínio DNS. A variável USERDOMAIN exibe o nome de domínio NetBIOS.

