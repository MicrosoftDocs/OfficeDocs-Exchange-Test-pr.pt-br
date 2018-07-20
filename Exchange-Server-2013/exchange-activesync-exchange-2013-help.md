---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50485724
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Saiba mais sobre o protocolo de cliente do Exchange ActiveSync para o Exchange Server 2013. Você aprenderá sobre os recursos do Exchange ActiveSync, incluindo recursos de segurança, as funções que você pode gerenciar, como torná-lo seguro e como evitar problemas de sincronização com o Windows Phone 7.


> [!TIP]
> Este tópico destina-se a administradores. Deseja configurar o seu dispositivo do Windows Phone, iOS ou Android para acessar sua caixa de correio do Office 365 ou Exchange Server? Confira os tópicos a seguir. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615415">Configurar email no Windows Phone</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615414">Configurar email no iPhone, iPad ou iPod Touch</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/?linkid=615417">Configurar email em um telefone ou tablet Android</A></P></LI></UL>



O Exchange ActiveSync é um protocolo de cliente que permite que você sincronize um dispositivo móvel com sua caixa de correio de Exchange. O Exchange ActiveSync é habilitado por padrão quando você instalar o Microsoft Exchange 2013.

**Sumário**

Visão geral do Exchange ActiveSync

Recursos do Exchange ActiveSync

Gerenciando o Exchange ActiveSync

Sincronização do Windows Phone 7

## Visão geral do Exchange ActiveSync

O Exchange ActiveSync é um protocolo de sincronização do Microsoft Exchange otimizado para funcionar junto com redes de alta latência e baixa largura de banda. O protocolo, baseado em HTTP e XML, permite que celulares acessem as informações de uma organização em um servidor que esteja executando o Microsoft Exchange. O Exchange ActiveSync permite que usuários acessem, via celular, emails, calendários, contatos e tarefas e continuem acessando essas informações enquanto estiverem trabalhando offline.


> [!TIP]
> O Exchange ActiveSync não oferece suporte a caixas de correio compartilhadas ou a acesso de representante.




> [!IMPORTANT]
> Os celulares com Windows Phone 7 suportam apenas um subconjunto de todas as configurações de políticas de caixa de correio do Exchange ActiveSync. Para uma lista completa, consulte Sincronização do Windows Phone 7.



## Recursos do Exchange ActiveSync

O Exchange ActiveSync oferece:

  - Suporte para mensagens HTML

  - Suporte para sinalizadores para acompanhamento

  - Agrupamento de conversa de emails

  - Capacidade para sincronizar ou não sincronizar uma conversa inteira

  - Sincronização de mensagens SMS com uma caixa de correio do Exchange do usuário

  - Suporte para exibição de status de resposta de mensagem

  - Suporte para recuperação rápida de mensagens

  - Informações sobre participantes da reunião

  - Pesquisa avançada do Exchange

  - Redefinição de PIN

  - Segurança de dispositivo avançada por meio de diretivas de senha

  - Descoberta Automática para provisionamento over-the-air

  - Suporte para configuração de respostas automáticas quando os usuários estiverem ausentes, em férias ou não estiverem no escritório

  - Suporte para sincronização de tarefas

  - Direct Push

  - Suporte para informações de disponibilidade para contatos

## Gerenciando o Exchange ActiveSync

Por padrão, o Exchange ActiveSync está habilitado. Todos os usuários que têm uma caixa de correio do Exchange podem sincronizar seus dispositivos móveis com o servidor Microsoft Exchange.

Você pode executar as seguintes tarefas do Exchange ActiveSync:

  - Habilitar e desabilitar o Exchange ActiveSync para usuários

  - Definir diretivas, como tamanho mínimo de senha, bloqueio de dispositivo e máximo de tentativas malsucedidas de senha

  - Iniciar um apagamento remoto para limpar todos os dados de um celular perdido ou roubado

  - Executar vários relatórios para exibição ou exportação para vários formatos

  - Controlar que tipos de dispositivos móveis podem se sincronizar com sua organização através das regras de acesso de dispositivos.

## Segurança no Exchange ActiveSync

Você pode configurar o Exchange ActiveSync para usar criptografia SSL (Secure Sockets Layer) para comunicações entre o servidor Exchange e o dispositivo móvel.

## Gerenciar acesso de dispositivos móveis no Exchange ActiveSync

Você pode controlar quais dispositivos móveis podem se sincronizar. Você pode fazer isso monitorando novos dispositivos móveis, conforme eles se conectam à sua organização, ou configurando regras que determinam que tipos de dispositivos móveis têm permissão para se conectar. Independente do método que você escolher para especificar que dispositivos móveis podem se sincronizar, você poderá aprovar ou negar acesso a qualquer dispositivo móvel especifico para um usuário específico, a qualquer momento.

## Recursos de segurança de dispositivo no Exchange ActiveSync

Além do recurso de configurar as opções de segurança para as comunicações entre o servidor Exchange e seus dispositivos móveis, o Exchange ActiveSync oferece os seguintes recursos para melhorar a segurança de dispositivos móveis:

  - **Apagamento Remoto**   Se seu dispositivo móvel for perdido, roubado ou comprometido de alguma forma, você poderá emitir um comando de apagamento remoto do computador do Exchange Server ou de qualquer navegador da Web usando o Outlook Web App. Esse comando apaga todos os dados do dispositivo móvel.

  - **Diretivas de senha de dispositivo **  O Exchange ActiveSync permite configurar várias opções de senhas de dispositivo.
    

    > [!WARNING]
    > O leitor de impressão digital iOS7 não pode ser usado como uma senha do dispositivo. Se escolher usar o leitor de impressão digital iOS7, precisará criar e digitar a senha do dispositivo se a política para a caixa de correio do dispositivo móvel exigir uma senha para o dispositivo.

    
    As opções de senha do dispositivo incluem as seguintes:
    
      - **Tamanho mínimo da senha (caracteres)**   Essa opção especifica o tamanho da senha do dispositivo móvel. O tamanho-padrão é de quatro caracteres, mas a senha pode ter até 18.
    
      - **Número mínimo de conjuntos de caracteres**   Use esta caixa de texto para especificar a complexidade das senhas alfanuméricas e forçar os usuários a usar vários conjuntos diferentes de caracteres, dentre os seguintes: letras minúsculas, letras maiúsculas, símbolos e números.
    
      - **Exigir senha alfanumérica**   Essa opção determina o nível de proteção da senha. Além dos números, você pode impor o uso de caracteres ou símbolos na senha.
    
      - **Tempo de inatividade (segundos)**   Essa opção determina por quanto tempo o dispositivo móvel precisará estar inativo antes que uma senha seja solicitada para desbloqueá-lo.
    
      - **Impor histórico de senha**   Marque essa caixa de seleção para impor que o telefone celular impeça o usuário de reutilizar suas senhas anteriores. O número definido determina o número de senhas anteriores que o usuário não poderá reutilizar.
    
      - **Habilitar recuperação de senha**   Marque essa caixa de seleção para habilitar a recuperação de senha do dispositivo móvel.  Os administradores podem usar o cmdlet **Get-ActiveSyncDeviceStatistics** para pesquisar a senha de recuperação do usuário.
    
      - **Apagar dispositivo após falha (tentativas)**   Essa opção permite especificar se você deseja que a memória do celular seja apagada após várias tentativas malsucedidas de entrada de senha.

  - **Políticas de criptografia de dispositivo**   Existem diversas políticas de criptografia de dispositivos móveis que podem ser impostas a um grupo de usuários. Essas diretivas incluem o seguinte:
    
      - **Exigir criptografia no dispositivo**   Marque essa caixa de seleção para exigir a criptografia no dispositivo móvel. Isso aumenta a segurança, ao criptografar todas as informações sobre o dispositivo móvel.
    
      - **Exigir criptografia nos cartões de armazenamento**   Marque essa caixa de seleção para exigir a criptografia no cartão de armazenamento removível do dispositivo móvel. Isso aumenta a segurança, criptografando todas as informações nos cartões de armazenamento do dispositivo móvel.

## Sincronização do Windows Phone 7

Se sua organização possuir dispositivos móveis com o Windows Phone 7, esses dispositivos terão problemas de sincronização se certas propriedades de política de caixa de correio para Dispositivos Móveis estiverem configuradas. Para permitir que celulares com o Windows Phone 7 se sincronizem com uma caixa de correio do Exchange, defina a propriedade **AllowNonProvisionableDevices** como verdadeira ou apenas configure as seguintes propriedades de política de caixa de correio para Dispositivos Móveis:

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

