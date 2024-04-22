# desafio_impulso_gov


# Desafio Técnico | Impulso Gov

No âmbito do projeto, identificamos a necessidade premente de mitigar o trabalho manual envolvido nos acessos remotos para integração dos bancos de dados. Com base na ordem dos principais problemas previamente solucionados, é imperativo estabelecer um processo eficiente que reduza significativamente o tempo destinado a esses acessos.

## Solução Proposta

A solução apresentada aborda tanto aspectos técnicos quanto de comunicação com o município, visando aumentar a eficiência das instalações e reduzir drasticamente os acessos remotos e trabalho manual associado.

## Processo de Mitigação

O processo proposto envolve as seguintes etapas:

1 - Documentação Detalhada: Será disponibilizada uma documentação abrangente que inclui instruções passo a passo e requisitos técnicos básicos, tais como configuração do computador, conexão de internet e os componentes instalados e configurados.

2 - Identificação de Pessoa-Chave: Será designada uma pessoa-chave na base do município para receber instruções completas sobre o funcionamento do e-SUS APS PEC e do Transmissor, a fim de evitar alterações que possam comprometer a integração dos bancos de dados.

3 - Implantação de Plataforma RMM: A plataforma de Remote Monitoring and Management (RMM) é capaz de monitorar parâmetros específicos pré determinados dos computadores prevenindo interrupções indesejadas. Essa plataforma será responsável por identificar a causa das interrupções, seja por queda de energia ou desligamento manual. A plataforma também será capaz de monitorar o gerenciador de tarefas e garantir que está funcionando. Essa plataforma nos permitirá automatizar soluções reincidentes já conhecidas na base de conhecimento afim de evitar acessos remotos para executar tarefas repetitivas. 

4 - Instalação Remota em Alta Escala: A plataforma RMM possibilitará a instalação da aplicação e-SUS APS PEC de forma remota em segunda plano e em alta escala, de maneira simultânea. Isso elimina a necessidade de acessos remotos individuais, economizando tempo e recursos.

5 - Controle de Incidentes: A plataforma RMM também oferecerá recursos para o controle de incidentes, permitindo que o município abra chamados para resolver problemas ou esclarecer dúvidas sobre o funcionamento do transmissor. Também será possível solicitar mudanças de computador ou alterações no sistema operacional através desta plataforma.

6 - Automatização do monitoramento do agendador de tarefas: Podemos também criar um sistema de monitoramento que periodicamente verifica se o transmissor está devidamente agendado para execução no sistema operacional. Caso seja identificada a remoção do agendamento, o sistema pode enviar alertas automáticos para a equipe responsável, permitindo a rápida intervenção antes que ocorram falhas na transmissão: 

Windows:

Ferramentas utilizadas: PowerShell, Task Scheduler, Send-MailMessage (para enviar e-mails)

Passos:

Criar um script PowerShell para monitorar o agendador de tarefas:
Criar um script PowerShell que verifica periodicamente o status das tarefas agendadas. O script pode procurar por tarefas específicas ou verificar se todas as tarefas estão agendadas corretamente.

powershell

$taskName = "NomeDaTarefa"  # Nome da tarefa a ser monitorada

$task = Get-ScheduledTask -TaskName $taskName

if ($task -eq $null) {
    # A tarefa não está agendada, enviar alerta
    Send-MailMessage -To "equipe@impulso.com" -From "monitor@impulso.com" -Subject "Alerta: Tarefa $taskName não está agendada" -Body "A tarefa $taskName não está agendada no sistema." -SmtpServer "smtp.impulso.com"
}

Linux:

Ferramentas utilizadas: Bash script, cron, mail (ou outro cliente de e-mail)

Passos:

Criar um script Bash que verifica periodicamente o status das tarefas agendadas. O script pode verificar a existência de arquivos de cron ou listar todas as tarefas agendadas.
bash

#!/bin/bash

if crontab -l | grep -q "tarefa_agendada"; then
    echo "Tarefa está agendada."
else
    # A tarefa não está agendada, enviar alerta
    echo "A tarefa não está agendada." | mail -s "Alerta: Tarefa não está agendada" equipe@impulso.com
fi

Agendar a execução do script no cron:
Adicione uma entrada no arquivo cron para executar o script em intervalos regulares.
Abra o arquivo cron digitando crontab -e.
Adicione uma linha para agendar a execução do script em intervalos desejados, por exemplo:
javascript

*/5 * * * * /caminho/para/seu/script.sh

Isso executará o script a cada 5 minutos.


## Base de Conhecimento

 - [Desafios-Processos-Seletivos](https://github.com/ImpulsoGov/desafios-processos-seletivos/blob/main/20240401_ConsultorAnalistaSuporteTI/README.md)

## Apêndice

O que é um software RMM?

O que é um software de monitoramento e gerenciamento remoto (RMM)? Com o software RMM, as equipes de TI gerenciam dispositivos, avaliam a integridade de todos os dispositivos da sua infraestrutura, resolvem problemas em segundo plano sem iniciar uma sessão remota e automatizam tarefas de segurança essenciais. Existem plataformas open source ou com custo acessível no mercado.
