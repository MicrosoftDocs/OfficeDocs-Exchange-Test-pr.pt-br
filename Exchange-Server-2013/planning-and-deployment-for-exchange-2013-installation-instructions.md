---
title: 'Planejamento e implantação: Exchange 2013 Help'
TOCTitle: Planejamento e implantação
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 50485875
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planejamento e implantação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Você precisa de orientações para realizar uma instalação do Exchange? Este artigo fornece orientações para planejar uma implantação do Microsoft Exchange Server 2013, além de links para artigos que você precisará durante a implantação.

As seções a seguir contêm links para informações sobre como planejar e implantar o Microsoft Exchange Server 2013.


> [!IMPORTANT]
> Não deixe de ler o tópico <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</A> antes de começar a implantação. As notas de versão contêm informações importantes sobre problemas que você pode encontrar durante a após a implantação.



**Sumário**

Planejamento para o Exchange 2013

Implementar uma instalação do Exchange 2013

Noções Básicas Sobre a Configuração do Exchange 2013

Para obter mais informações

## Planejamento para o Exchange 2013

Use os links a seguir para acessar informações que vão ajudá-lo a planejar a implantação do Exchange Server 2013 em sua organização.


> [!IMPORTANT]
> Consulte Estabelecer um ambiente de teste mais adiante neste tópico para saber como instalar o Exchange 2013 em um ambiente de teste.



  - [Servidores de Acesso à Caixa de Correio e do Cliente](mailbox-and-client-access-servers-exchange-2013-help.md)  
    Saiba mais sobre as funções de servidor Caixa de Correio e Acesso para Cliente incluídas no Exchange 2013.

<!-- end list -->

  - [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md)  
    Compreenda os requisitos de sistema que precisam ser atendidos em sua organização para que você possa instalar o Exchange 2013.

<!-- end list -->

  - [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md)  
    Saiba quais recursos do Windows Server 2008 R2 Service Pack 1 (SP1) ou do Windows Server 2012 e quais outros programas devem ser instalados para uma instalação bem-sucedida do Exchange 2013.

<!-- end list -->

  - [Assistente de implantação do Exchange Server](exchange-server-deployment-assistant-exchange-2013-help.md)  
    Use esta ferramenta para gerar uma lista de verificação para planejar, instalar ou atualizar para o Exchange 2013. As orientações estão disponíveis para vários cenários, incluindo implantação local, híbrida ou na nuvem.

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    Leia este tópico para saber como o Exchange 2013 usa o Active Directory e como sua implantação do Active Directory afeta sua implantação do Exchange.

<!-- end list -->

  - [Proteção antimalware](anti-malware-protection-exchange-2013-help.md)  
    Leia este tópico para entender as opções de proteção anti-malware para o Exchange 2013.

<!-- end list -->

  - [Implantações Híbridas do Exchange Server](https://technet.microsoft.com/pt-br/library/jj200581\(v=exchg.150\))  
    Leia este tópico para obter ajuda com o planejamento de uma implantação híbrida com o Microsoft Office 365 em sua organização do Exchange 2013 no local.

<!-- end list -->

  - [Planejamento de alta disponibilidade e de resiliência do site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    Leia este tópico para obter ajuda com o planejamento e alcançar requisitos de alta disponibilidade e continuidade dos negócios.

<!-- end list -->

  - [Integração com o SharePoint e o Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    Leia este tópico para saber como integrar o Exchange 2013, o Microsoft SharePoint 2013 e o Microsoft Lync 2013, habilitando o arquivamento, a retenção e a Descoberta Eletrônica entre produtos; as caixas de correio de site; a autenticação; a presença do Lync; e muito mais.

<!-- end list -->

  - [Planejamento para o Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)  
    Leia este tópico para saber mais sobre como planejar para a Unificação de Mensagens do Exchange 2013.

<!-- end list -->

  - [Opções de configuração de armazenamento do Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    Leia este tópico para conhecer as arquiteturas de armazenamento, os tipos de discos e as configurações de armazenamento suportadas pela função de servidor Caixa de Correio do Exchange 2013.

<!-- end list -->

  - [Virtualização do Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md)  
    Leia este tópico para saber mais sobre como implantar o Exchange 2013 em um ambiente virtualizado.

<!-- end list -->

  - [A multilocação no Exchange 2013](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    Leia este tópico para saber mais sobre como você pode configurar o Exchange 2013 para hospedar várias e diferentes organizações ou unidades de negócio que normalmente não compartilham email, dados, usuários, listas de endereço global (GALs) ou outros objetos comumente usados no Exchange.

<!-- end list -->

  - [Tecnologias de desenvolvimento do Exchange](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    Este tópico contém informações importantes sobre as Interfaces de Programação de Aplicativo (APIs) disponíveis para aplicativos que usam o Exchange 2013.

## Estabelecer um ambiente de teste

Antes de instalar o Exchange 2013 pela primeira vez, recomendamos instalá-lo em um ambiente de teste isolado. Essa abordagem reduz o risco de tempo de inatividade do usuário final e ramificações negativas para o ambiente de produção.

O ambiente de teste atuará como sua "prova de conceito" para o novo design do Exchange 2013 e permitirá avançar ou retroceder quaisquer implementações antes da implantação final nos ambientes de produção. Ter um ambiente de teste exclusivo para validação e realização de testes permite efetuar verificações de pré-instalação para os ambientes de produção futuros. Realizando a instalação em um ambiente de teste primeiro, acreditamos que sua organização terá uma probabilidade de êxito muito maior em uma implementação de produção completa.

Para muitas organizações, os custos de construção de um laboratório de teste podem ser altos devido à necessidade de duplicar o ambiente de produção. Para reduzir os custos de hardware associados ao laboratório de protótipo, recomendamos o uso da virtualização, com a utilização das tecnologias Windows Server 2008 R2 ou Windows Server 2012 Hyper-V. O Hyper-V oferece a virtualização de servidor, permitindo que vários sistemas operacionais virtuais sejam executados em uma única máquina física.

Para informações mais detalhadas sobre o Hyper-V, consulte [Virtualização de servidores](https://go.microsoft.com/fwlink/p/?linkid=117704). Para informações sobre o suporte da Microsoft do Exchange 2013 em produção no software de virtualização de hardware, consulte "Virtualização de Hardware" em [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

## Implementar uma instalação do Exchange 2013

A fase de implantação é o período durante o qual você instala o Exchange 2013 em sua organização. Antes de começar a fase de implantação, você deve planejar sua organização do Exchange. Para obter mais informações, consulte a seção Planejamento para o Exchange 2013 anteriormente neste tópico.

Utilize os links a seguir para acessar as informações de que você precisa para a implantação do Exchange 2013.

  - [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md)  
    Conheça as instruções para preparar sua floresta do Active Directory para o Exchange 2013 e as mudanças que o Exchange realiza em sua floresta.

<!-- end list -->

  - [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    Siga as instruções deste tópico para usar o assistente de instalação do Exchange 2013 para instalar o Exchange 2013 em uma nova organização do Exchange.

<!-- end list -->

  - [Instalar o Exchange 2013 usando o modo autônomo](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    Siga as instruções deste tópico para usar a instalação autônoma do Exchange 2013 para instalar o Exchange 2013 em uma nova organização do Exchange.

<!-- end list -->

  - [Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    Siga as etapas deste tópico para usar o assistente de Instalação do Exchange 2013 para instalar a função de Transporte de Borda do Exchange 2013 em uma rede de perímetro.

<!-- end list -->

  - [Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    Siga as etapas neste tópico para aplicar a atualização cumulativa ou o service pack mais recente em servidores do Exchange 2013 em sua organização.

<!-- end list -->

  - [Atualizar do Exchange 2010 para o Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    Siga as etapas neste tópico para instalar o Exchange 2013 em uma organização existente do Exchange 2010.

<!-- end list -->

  - [Atualização do Exchange 2007 para o Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    Siga as etapas neste tópico para instalar o Exchange 2013 em uma organização existente do Exchange 2007.

<!-- end list -->

  - [Implantar várias topologias de floresta do Exchange 2013](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    Leia este tópico para informações que ajudarão você a implantar o Exchange 2013 em uma organização que contém mais de uma floresta do Active Directory.

<!-- end list -->

  - [Implantando a caixa postal e Unificação de MENSAGENS](deploying-voice-mail-and-um-exchange-2013-help.md)  
    Leia este tópico para obter informações que o ajudarão a compreender a implantação da Unificação de Mensagens do Exchange 2013, seja ela uma nova implantação ou uma atualização.

<!-- end list -->

  - [Procedimentos de Implantação Híbrida](https://technet.microsoft.com/pt-br/library/jj200788\(v=exchg.150\))  
    Leia este tópico para obter informações que vão ajudá-lo a implantar o Exchange 2013 em uma implantação híbrida existente.

<!-- end list -->

  - [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    Saiba mais sobre as tarefas pós-instalação para completar sua instalação do Exchange 2013.

## Noções Básicas Sobre a Configuração do Exchange 2013

Diferentes tipos e modos de instalação do Exchange 2013 podem ser usados para instalar e manter as várias edições e versões do Exchange 2013.

## Edições e versões do Exchange

está disponível em duas edições de servidor: Standard Edition e Enterprise Edition. Essas são edições de licenciamento definidas por uma chave de produto. Para obter mais informações, consulte [Licenciamento do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=237292).

## Tipos de instalação do Exchange

As seguintes opções de instalação do Exchange 2013 estão disponíveis:

  - **UI de Instalação do Exchange**   A execução de Setup.exe sem opções de linha de comando oferece uma experiência interativa em que você é conduzido pelo assistente de Instalação do Exchange 2013.

  - **Instalação Autônoma do Exchange**   A execução de Setup.exe sem opções de linha de comando permite que você instale o Exchange a partir de uma linha de comando interativa ou de um script.

Setup.exe está disponível no DVD do Exchange 2013 ou nos arquivos de origem baixados.

## Modos de instalação do Exchange

A instalação do Exchange 2013 inclui vários modos de instalação:

  - **Instalar**   Use esse modo ao instalar uma nova função de servidor ou adicionar uma função de servidor a uma instalação existente (modo de manutenção). Você pode usar este modo na instalação autônoma e no Assistente de instalação do Exchange.

  - **Desinstalar**   Use este modo quando estiver removendo a instalação do Exchange de um computador. Você pode usar este modo na instalação autônoma e no Assistente de instalação do Exchange.

  - **Atualizar**   Selecione este modo se você já tiver uma instalação existente do Exchange e estiver instalando uma atualização cumulativa ou um service pack. Você pode usar este modo na instalação autônoma e no Assistente de instalação do Exchange.
    

    > [!NOTE]
    > O Exchange 2013 não oferece suporte para atualizações in-loco de versões anteriores do Exchange. Este modo é usado apenas para instalar atualizações cumulativas ou service packs.



  - **RecoverServer**   Use este modo quando houve uma falha catastrófica de um servidor, e você precisa recuperar os dados. Você deve instalar um servidor com o mesmo FQDN (nome de domínio totalmente qualificado) utilizado pelo servidor que falhou, e em seguida executar o Programa de Instalação com a opção **/m:RecoverServer**. Não especifique as funções a serem restauradas. A Instalação detecta o objeto do Exchange Server no Active Directory e instala automaticamente a configuração e os arquivos correspondentes. Após recuperar o servidor, você pode restaurar bancos de dados e reconfigurar quaisquer definições adicionais. Para executar no modo **RecoverServer**, o Exchange não pode estar instalado no servidor. O objeto do servidor do Exchange deve existir no Active Directory. Você pode usar este modo apenas durante uma instalação autônoma.


> [!NOTE]
> É necessário concluir um modo de instalação antes de poder usar outro modo.



## Para obter mais informações

[Suporte a IPv6 no Exchange 2013](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Centro de administração do Exchange no Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Suporte de idioma do Exchange 2013](exchange-2013-language-support-exchange-2013-help.md)

[Verificações de preparação do Exchange 2013](exchange-2013-readiness-checks-exchange-2013-help.md)

