## Demandas comuns - Zabbix

vagrant validate

Criando chaves de monitoramento personalizadas.

Acessar o arquivo /etc/zabbix/zabbix_agentd.confs

Acessar a opção "UserParameter" presente na linha 296 do documento.



### Habilitando telegram no zabbix
Adicionar media type telegram

pip install TeleBot
pip install pyTelegramBotAPI

Script para ser salvo no diretorio

/usr/lib/zabbix/alertscripts

telegram
```bash
#!/usr/bin/env python
import telebot,sys
BOT_TOKEN='***' # numero do hash do bot do telegram
DESTINATION=sys.argv[1]
SUBJECT=sys.argv[2]
MESSAGE=sys.argv[3]
MESSAGE = MESSAGE.replace('/n','\n')
tb = telebot.TeleBot(BOT_TOKEN)
tb.send_message(DESTINATION,SUBJECT + '\n' + MESSAGE,
disable_web_page_preview=True, parse_mode='HTML')
```

### Coletar o id do usuário do telegram
https://api.telegram.org/bot946186932:AAGI9EpwcGqNrG12GRB6gIN6dt8BagWi2ls/getUpdates

Após coletar o id do usuário do telegram, executar o script citado acima com o parametro de id de usuario para testar o funcionamento.
