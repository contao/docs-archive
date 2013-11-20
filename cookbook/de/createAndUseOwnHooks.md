# Hooks in Contao

## Was sind Hooks

Durch Hooks können eigene Funktionen registriert werden, die von Contao beim
Eintreten eines bestimmten Ereignisses ausgeführt werden.

## Eigenene Hooks erstellen

Um einen eigenen Hook anzubieten wird überprüft ob in ```$GLOBALS['TL_HOOKS']
``` entsprechende Elemente verfügbar sind. Falls dies der Fall ist werden die
entsprechende Klassen importiert und  die entsprechenden Methoden der Klasse
ausgeführt. Dies geschieht in der Reihenfolge in der die Elemente hinzugefügt
wurden. Registrieren mehrere Erweiterungen Aktionen auf den Hook so ist dies
die Reihenfolge in der die Module geladen wurden.

``` {.php}
// Beispiel aus /system/modules/comments/classes/Comments.php
// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['addComment']) && is_array($GLOBALS['TL_HOOKS']['addComment']))
{
	foreach ($GLOBALS['TL_HOOKS']['addComment'] as $callback)
	{
		$this->import($callback[0]);
		$this->$callback[0]->$callback[1]($objComment->id, $arrSet, $this);
	}
}
```

Bei der Ausführung werden der Methode Parameter übergeben. Die Signatur der
Methode muss dann bei der Benutzung des Hooks mit dieser Definition
übereinstimmen.
``` {.php}
$this->$callback[0]->$callback[1]($objComment->id, $arrSet, $this);
```

``` {.php}
class MyEmailCommentClass
{

	/**
	 * @param $intCommentId   Id des Kommentars der hinzugefügt wurde
	 * @param $arrSet         Array mit Daten des Kommentars
	 * @param $objComments    Das Comments Objekt
	 *
	 * @return void           Es wird kein return-Wert erwartet
	 */
	public function sendEmailWithComment($intCommentId, $arrSet, $objComments)
	{
		// Hier können wir nun unsere E-Mail verschicken
	}

}

```

## Den Hook verwenden

Wir wollen eine Aktion ausführe, die beim hinzufügen eines Kommentars eine
E-Mail verschickt.
Hierzu fügen wir in der config.php unseres Moduls unsere Methode zu hinzu
um Contao mitzuteilen dass wir diese dann ausführen möchten.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyEmailCommentClass', 'sendEmailWithComment');

```

Nun weiß Contao dass wir bei hinzufügen eines Kommentars die Methode
```sendEmailWithComment``` unserer Klasse ```MyEmailCommentClass``` ausführen
wollen. Die Klasse muss über Autoloader geladen werden können bzw. anderweitig
eingebunden sein.

Diese Funktionen werden dann beim Eintreten des Ereignisses in der Reihenfolge
ausgeführt in der sie registriert wurden.