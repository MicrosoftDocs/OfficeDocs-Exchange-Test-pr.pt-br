---
title: 'Portabilidade de tom de discagem: Exchange 2013 Help'
TOCTitle: Portabilidade de tom de discagem
ms:assetid: ea62fae0-5e0a-460c-beb6-52532c8c8dbc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876950(v=EXCHG.150)
ms:contentKeyID: 51407929
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Portabilidade de tom de discagem

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-01-28_

Portabilidade de tom de discagem é um recurso do Microsoft Exchange Server 2013 que fornece uma solução de continuidade de negócios limitados para falhas que afetam um banco de dados de caixa de correio, um servidor ou um site inteiro. Portabilidade de tom de discagem permite que os usuários têm uma caixa de correio temporária para envio e recebimento de email enquanto suas caixas de correio original está sendo restaurado ou reparado. A caixa de correio temporária pode ser no mesmo servidor de caixa de correio Exchange 2013 ou em qualquer outro servidor de caixa de correio Exchange 2013 na sua organização que possui bancos de dados com a mesma versão do esquema de banco de dados. Isso permite que um servidor alternativo hospedar as caixas de correio de usuários que estavam anteriormente em um servidor que não está mais disponível. Clientes que suportam a descoberta automática serão automaticamente redirecionados para o novo servidor sem precisar atualizar manualmente o perfil do usuário da área de trabalho. Depois que os dados do usuário original da caixa de correio foi restaurados, um administrador pode mesclar a caixa de correio recuperada do usuário e a caixa de correio de tom de discagem do usuário em uma caixa de correio única e atualizada.

O processo para usar a portabilidade de tom de discagem é chamado de uma *recuperação de sinal*. Uma recuperação de sinal envolve a criação de um banco de dados vazio em um servidor de caixa de correio para substituir um banco de dados com falha. Este banco de dados vazio, conhecido como um *banco de dados de tom de discagem*, permite que os usuários enviem e recebam mensagens de email enquanto o banco de dados com falha é recuperado.

Existem três opções para realizar uma recuperação de tom de discagem:

  - **Recuperação de sinal no servidor com o banco de dados com falha**   Se o servidor que hospeda o banco de dados com falha ainda está funcionando, que recomendamos que você executar uma recuperação de sinal nesse servidor. Isso significa menos tempo de inatividade porque você não precisa mover arquivos de banco de dados entre servidores. Além disso, você não será necessário reconfigurar os perfis de mensagens para clientes que não oferecem suporte a descoberta automática.

  - **Recuperação de sinal usando um servidor alternativo para o banco de dados de tom de discagem**   Se um servidor falha e precisa ser recriados, da maneira mais eficiente para dar aos usuários a funcionalidade básica de email é criar um banco de dados de tom de discagem em outro servidor e usar a portabilidade do banco de dados para mover a configuração de caixa de correio dos usuários para esse novo servidor. Como esse processo envolve a mover o banco de dados de tom de discagem de volta ao servidor original (recuperado), essa opção adiciona mais tempo para o processo geral de recuperação. Além disso, esse processo é mais complexo do que a execução de uma recuperação de sinal no servidor original. Ao executar esse processo, o servidor que hospeda o banco de dados de tom de discagem deve ter recursos suficientes para suportar a carga adicional dos usuários adicionais. Além disso, se o cliente dos usuários não oferece suporte a descoberta automática, o seu perfil de mensagens precisará ser reconfigurados para apontar para o servidor de tom de discagem.

  - **Recuperação de sinal usando e manter-se em um servidor alternativo para o banco de dados de tom de discagem**   Este é semelhante à opção anterior, exceto que você não reverter para o servidor original. É recomendável essa opção para as situações em que não é possível ou viável para recuperar o servidor com falha. Neste cenário, os usuários será normalmente permanecem em um servidor alternativo após a operação de recuperação foi concluída. Ao executar esse processo, o servidor que hospeda o banco de dados de tom de discagem deve ter recursos suficientes para suportar a carga adicional dos usuários adicionais. Além disso, se o cliente dos usuários não oferece suporte a descoberta automática, o seu perfil de mensagens precisará ser reconfigurados para apontar para o servidor de tom de discagem.

Todas as três opções siga as mesmas etapas básicas:

1.  **Crie um banco de dados vazio tom de discagem para substituir o banco de dados com falha.**
    
    Este novo banco de dados permitirá que os usuários que tinham caixas de correio no banco de dados com falha para enviar e receber mensagens novas. Portabilidade de tom de discagem permite que você aponte a um usuário para outro banco de dados sem mover a caixa de correio. Se você criou o banco de dados de tom de discagem em um servidor diferente do servidor que hospedados o banco de dados com falha, você precisa mover a configuração de caixa de correio para esse novo servidor.

2.  **Restaure o banco de dados antigo.**
    
    Use o software de backup e recuperação que normalmente é usado para restaurar o banco de dados com falha. Se não houver nenhum backup do banco de dados com falha, recupere o banco de dados com falha usando outros meios se possível. Se você estiver usando o mesmo servidor para recuperação de tom de discagem, você precisará restaurar o banco de dados para um banco de dados de recuperação (RDB).

3.  **Troque o banco de dados de tom de discagem com o banco de dados restaurado.**
    
    Depois que o banco de dados com falha é restaurado, troque-lo com o banco de dados de tom de discagem. Assim, os usuários a capacidade de enviar e receber emails e acessar todos os dados no banco de dados restaurado. Se os usuários foram movidos para um banco de dados de tom de discagem em outro servidor, você precisa mover a configuração de caixa de correio de volta ao servidor original.

4.  **Mescle os bancos de dados.**
    
    Para obter os dados do banco de dados de tom de discagem para o banco de dados restaurado, mesclar os dados usando o cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) .

Para obter instruções detalhadas sobre como executar uma recuperação de tom de discagem, consulte [Executar uma recuperação de sinal de linha](perform-a-dial-tone-recovery-exchange-2013-help.md).

