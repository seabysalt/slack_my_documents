# Slack My Documents

Ein simpler Slackbot, der es erlaubt, mit den Daten der eigenen Dokumente zu sprechen.

## Start

### Slack-Konfiguration

Zunächst braucht unser kleiner Bot einen Zugriff auf Slack. Dazu nutzen wir das Bolt-Framework in Python, das von Slack selbst zur Verfügung gestellt wird,
Bitte folge der Anleitung unter https://slack.dev/bolt-python/tutorial/getting-started, um einen SLACK_BOT_TOKEN und einen SLACK_APP_TOKEN zu erhalten. Der SLACK_BOT_TOKEN sollte mit xoxb-... beginnen (Im Reiter OAuth zu finden), der SLACK_APP_TOKEN mit xapp-... . (App-Level Token, nicht Secret oder Verification Token, zu finden über Settings/Basic Information)

Die Slack-App benötigt folgende Einstellungen:

1. Socket Mode enabled
2. Event Subscriptions enabled

- Subscribe to Bot Events:
- `message:channels`
- `message:groups`
- `message:im`
- `message:mpim`
- Je nach Art der Interaktion
- `message:channels`
- `message:groups`
- `message:im`
- `message:mpim`

3. OAuth & Permissions
4. Token (wird bei Integration in Workspace automatisch erstellt)
5. Bot Token Scopes

- `chat:write`

### OpenAI-Key

Bitte lege dir einen OpenAI-Account an und hole dir unter https://platform.openai.com/account/api-keys einen API-Key.

### Installation

In der aktuellen Fassung kann der Bot von überall aus gestartet und genutzt werden, denn er nutzt die WebSocket-API von Slack. Es ist also auch ein Betrieb vom lokalen Netzwerk aus möglich, eine öffentliche API ist nicht erforderlich.

```
git clone https://github.com/mayflower/slack_my_documents
cd slack_my_documents

conda create -n slackbot python=3.10.9
conda activate slackbot
conda install pytorch -c pytorch

pip install -r requirements.txt
```

### Konfiguration

Kopiere die Datei .env.example, um eine eigene Konfiguration anzulegen:

```
cp .env.example .env
```

Tragen jetzt die 3 Werte von oben in die .env ein, und ergänze das Keyword (SLACK_BOT_KEYWORD), auf das der Bot hören soll.

````
# cp .env.example .env
# Edit your .env file with your own values
# DON'T COMMIT OR PUSH .env FILE!

# API CONFIG
OPENAI_API_KEY=
OPENAI_API_MODEL=gpt-3.5-turbo # Options: gpt-4, gpt-4-32k, gpt-3.5-turbo, text-davinci-003, etc.
SLACK_BOT_TOKEN= # Slack Bot token from , "xoxb-..."
SLACK_BOT_KEYWORD= # Slack Bot keyword - when should be answer?
SLACK_APP_TOKEN= # Slack App token from , "xapp-..."```
````

### Daten importieren

Der Bot unterstützt im Moment folgende Formate über unstructured.io:

- Word-Dokumente (.docx, .doc)
- Powerpoint (.pptx, .ppt)
- Mails (.eml, .msg)
- Ebooks (.rtf, .epub)
- HTML-Seiten (.html)
- Acrobat Reader (.pdf)
- MarkDown (.md)
- Text (.txt)
- Text in Grafiken (.png, .jpg)

Bitte kopiere alle benötigten Dateien einfach in den Folder ./data.

Starte danach den Importer:

```
python import.py
```

Bitte nutze dieses Script auch, wenn du deine Daten aktualisieren willst - und startet danach den Bot neu, damit er mit den aktuellen Daten arbeitet.

## Start

Jetzt könnt ihr den Bot starten:

```
python app.py
```
