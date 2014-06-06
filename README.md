# API Hörsuppe
URL: http://hoersuppe.de/api/
Original Doku: http://hoersuppe.de/feature/api.txt

Der Aufruf erfolgt über den URL und angehangene Parameter.
Wichtigster Parameter ist die action, die bestimmt, was gefragt und zurückgegeben wird.
Die zurückgegebenen Daten enthalten immer einen Status, eine Meldung und bei Erfolg die zurückgegebenen Daten.
Folgende Aktionen sind möglich:

## getPodcasts
* action: `getPodcasts`
* Parameter: -
* Beschreibung: gibt eine Liste aller Podcasts in der Hörsuppe zurück
* Beispiel: http://hoersuppe.de/api/?action=getPodcasts

```javascript
{
  "status":1,
  "msg":"ok",
  "data":[
    {
      "title":"\/dev\/radio",
      "slug":"devradio"
    },
    {
      "title":"1337kultur",
      "slug":"1337kultur"
    },
    {
      "title":"Alternativlos",
      "slug":"alternativlos"
    }
    // ...
  ]
}
```

## getPodcastData
* Action: `getPodcastData`
* Parameter:
	* `podcast`: Podcast-Slug (erforderlich)
* Beschreibung: gibt die in der Hörsuppe vorhandenen Metadaten zu einem Podcast aus. Der Slug ist unveränderlich, aber nicht immer direkt zu erraten.
* Beispiel: http://hoersuppe.de/api/?action=getPodcastData&podcast=wrint

```json
{
  "status":1,
  "msg":"ok",
  "data":
    {
      "ID":2598,
      "title":"Wrint",
      "description":"Wer redet ist nich tot",
      "url":"http:\/\/www.wrint.de","
      feedurl":"http:\/\/feeds.feedburner.com\/wrint\/",
      "imageurl":"http:\/\/www.wrint.de\/wp-content\/uploads\/powerpress\/wrint_basis_weiss_1400.jpg",
      "slug":"wrint",
      "recension":"",
      "cluster":"Berlin",
      "rec_pos":"Interessante Interviews mit fern und nah lebenden Menschen, spannende Biografien und eine Talksendung mit H\u00f6rerfragen gibt's hier im Paket mit professioneller Arbeit.",
      "rec_neg":"Wie soll ich das nun formulieren? Es soll Menschen geben, die mit Holgers \"Meinungsst\u00e4rke\" nicht zurechtkommen. Zart besaitete Freunde der Hom\u00f6opathie sollten nicht reinh\u00f6ren.",
      "chat_server":"irc.freenode.net",
      "chat_channel":"kleitung\n",
      "chat_url":"http:\/\/webchat.freenode.net\/?channels=kleitung\n",
      "obsolete":"",
      "freeze":"",
      "rundfunk":"",
      "stream":"http:\/\/xsn.io\/wrint.mp3",
      "otitle":"WRINT",
      "contact":
        {
          "twitter":"wrint_de",
          "adn":"holgi",
          "email":"mail@wrint.de"
        },
      "feature":"0"
    }
}
```

## getPodcastLive
* Action: `getPodcastLive`
* Parameter
	* `podcast`: Podcast-Slug (erforderlich)
	* `count`: Limitiert die Ausgabe auf die nächsten `count` Livetermine (optional)
* Beschreibung: gibt die nächsten Livetermine eines Podcasts aus. Vorhergeganene Termine sind nicht zugänglich
* Beispiel: http://hoersuppe.de/api/?action=getPodcastLive&podcast=wrint&count=5

```json
{
   "status":1,
   "msg":"ok",
   "data":[
     {
       "id":"2948",
       "podcast":"wrint",
       "state":"1",
       "type":"0",
       "synced":"1",
       "title":"Wrint - Wrintheit",
       "url":"http:\/\/www.wrint.de\/",
       "streamurl":"http:\/\/streams.xenim.de\/wrint.mp3",
       "livedate":"2012-12-02 13:00:00",
       "duration":"90",
       "twittered":"0"
     },
     {
       "id":"2426",
       "podcast":"wrint",
       "state":"1",
       "type":"0",
       "synced":"1",
       "title":"Wrint - Realit\u00e4tsabgleich",
       "url":"http:\/\/www.wrint.de\/",
       "streamurl":"http:\/\/streams.xenim.de\/wrint.mp3",
       "livedate":"2012-12-05 11:30:00",
       "duration":"90",
       "twittered":"0"
     }
   ]
 }
 ```
	
## getPodcastEpisodes:
* Action: `getPodcastEpisodes`
* Parameter:
	* `podcast`: Podcast-Slug (erforderlich)
	* `count`: Limitiert die Ausgabe auf die letzten `count` Episoden (optional, default: `10`)
* Beschreibung: gibt die letzten (count) Episoden eines Podcasts aus.
* Beispiel: http://hoersuppe.de/api/?action=getPodcastEpisodes&podcast=wrint&count=1

```json
{
  "status":1,
  "msg":"ok",
  "data":[
    {
      "ID":43803,
      "post_date":"2012-11-28 12:20:19",
      "post_date_gmt":"2012-11-28 11:20:19",
      "post_title":"WR127 Realit\u00e4tsabgleich: Arbeit schade",
      "post_name":"wr127-realitatsabgleich-arbeit-schade",
      "post_modified":"2012-11-28 12:20:19",
      "post_modified_gmt":"2012-11-28 11:20:19",
      "post_link":"http:\/\/www.wrint.de\/2012\/11\/28\/wr127-realitatsabgleich-arbeit-schade\/",
      "post_commentlink":"http:\/\/www.wrint.de\/2012\/11\/28\/wr127-realitatsabgleich-arbeit-schade\/#comments",
      "post_mediaurl":"http:\/\/wrint.de\/download\/WR127_Realitaetsabgleich_Arbeit_schade.mp3",
      "post_duration":"2630"
    }
  ]
}
```

## getDeleted
* Action: `getDeleted`
* Parameter: keine
* Beschreibung: gibt eine Liste aller gelöschten Events mit Löschdatum zurück.
* Beispiel: http://hoersuppe.de/api/?action=getDeleted

```json
{
   "status":1,
   "msg":"ok",
   "data":[
      {
         "event_ID":"7712",
         "deldate":"2014-04-07 15:23:00"
      },
      {
         "event_ID":"7719",
         "deldate":"2014-04-07 22:11:38"
      }
   ]
}
```

## getLive
* Action: `getLive`
* Parameter:
	* `count`: Limitiert die Ausgabe auf die nächsten `count` Livetermine (optional)
	* `dateStart`: erstes abzufragendes Datum (optional, `YY-mm-dd`)
	* `dateEnd`: letztes abzufragendes Datum (optional, `YY-mm-dd`)
* Beschreibung: gibt die in den Datumsgrenzen im Kalender aufgeführten Livetermine zurück. Count begrenzt dies auf die ersten (count) Termine. Wird kein Startdatum angegeben, gilt das aktuelle Datum als Start.
* Beispiel: http://hoersuppe.de/api/?action=getLive&count=2&dateStart=2012-12-07

```json
{
  "status":1,
  "msg":"ok",
  "data":[
    {
      "id":"1494",
      "podcast":"fanb0ys",
      "state":"1",
      "type":"0",
      "synced":"1",
      "title":"fanb0ys",
      "url":"http:\/\/fanboys.fm",
      "streamurl":"http:\/\/streams.xenim.de\/fanboys.mp3",
      "livedate":"2012-12-07 16:00:00",
      "duration":"90",
      "twittered":"0"
    },
    {
      "id":"2912",
      "podcast":"knorkpod",
      "state":"1",
      "type":"0",
      "synced":"1",
      "title":"KNORKPod",
      "url":"http:\/\/knorkpod.moepmoep.com\/",
      "streamurl":"http:\/\/moep1.moepmoep.com",
      "livedate":"2012-12-07 18:30:00",
      "duration":"90",
      "twittered":"0"
    }
  ]
}
```

## getLiveByID
* action: `getLiveByID`
* Parameter:
	* `ID`: die ID eines Liveevents
* Beschreibung: gibt die Daten eines Liveevents aus, der über die ID identifiziert wird
* Beispiel: http://hoersuppe.de/api/?action=getLiveByID&ID=3019

```json
{
	"status":1,
	"msg":"ok",
	"data":[
		{
			"id":"3019",
			"podcast":"binaergewitter",
			"state":"1",
			"type":"0",
			"synced":"1",
			"title":"Bin\u00e4rgewitter-Talk",
			"url":"http:\/\/blog.binaergewitter.de\/",
			"streamurl":"http:\/\/streams.xenim.de\/binaergewitter.mp3.m3u",
			"livedate":"2013-05-23 19:30:00",
			"duration":"180",
			"twittered":"0"
		}
	]
}
```

