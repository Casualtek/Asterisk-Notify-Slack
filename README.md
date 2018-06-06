# Asterisk-Notify-Slack

Simple Python __scripts__ that notify a user in Slack of incoming calls and text messages received via a dongle.

In the scripts, replace ```<WEBHOOK_URL_SLACK>``` with the actual incoming webhook URL of your Slack application.
More on that can be found <a href="https://api.slack.com/incoming-webhooks">here</a>.

Replace ```<USER_SLACK>``` with the identifier of the Slack user to be notified.
Replace ```<BOT_SLACK>``` with the identifier of the channel used by your application to interact with Slack users.

## Usage

The script __notify_slack.agi__ is intented to be executed as an AGI script when there is an incoming text message.
Here is a example for the extensions plan that will thus call the uploader script.

```
[from-trunk-dongle]
exten => sms,1,AGI(notify_slack.agi, ${SMS_BASE64})
exten => sms,n,Hangup()
```

The script __notify_call_slack.agi__ is intented to be executed as an AGI script when there is an incoming phone call.
Here is a example the extensions plan that will thus call the uploader script.

```
exten => PHONE_NUMBER_CALLED,1,Set(__DIRECTION=INBOUND)
exten => PHONE_NUMBER_CALLED,n,ExecIf($[ "${CALLERID(name)}" = "" ] ?Set(CALLERID(name)=${CALLERID(num)}))
exten => PHONE_NUMBER_CALLED,n,AGI(notify_call_slack.agi, ${CALLERID(num)}, ${CALLERID(name)})
```

License
----

MIT
