---

copyright:
  years: 2015, 2016
  
---

# Berechtigung mit Touch ID schützen
{: #before-you-begin}

Touch ID ist eine Fingerabdruckerkennungsfunktion für iOS-Geräte. Sie können Touch ID verwenden, um Berechtigungsinformationen für eine zukünftige Verwendung automatisch zu schützen. Zur Konfiguration des Sicherheitsgrads legen Sie eine der folgenden Persistenzrichtlinien mit der Methode `IMFAuthorizationManager.setAuthorizationPersistencePolicy()` fest.

* **IMFAuthorizationPersistencePolicyNever** (höchste Sicherheit): Berechtigungsinformationen nie auf dem Gerät speichern. Ein Berechtigungsheader ist nur während einer Anwendungssitzung gültig. Die Berechtigungsinformationen werden in der iOS-Schlüsselkette (Keychain) gespeichert.

* **IMFAuthorizationPersistencePolicyAlways** (geringste Sicherheit): Berechtigungsinformationen immer auf dem Gerät speichern, unabhängig davon, ob Touch ID vorhanden ist, unterstützt wird oder aktiviert ist. Touch ID und die Gerätekenncodeauthentifizierung sind niemals erforderlich.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: Verwenden Sie Touch ID, um die Berechtigungsinformationen aus der iOS-Schlüsselkette (Keychain) abzurufen. Diese Option bietet einen Kompromiss zwischen Sicherheit und Bedienungskomfort. Die Berechtigungsinformationen werden nur gespeichert, wenn Touch ID vorhanden ist, aktiviert ist und unterstützt wird. Touch ID oder die Gerätekenncodeauthentifizierung ist erforderlich, um auf die gespeicherten Berechtigungsinformationen einmal pro Anwendungssitzung zuzugreifen. Wenn diese Richtlinie festgelegt wurde, jedoch kein Zugriff auf Touch ID vorhanden ist, weil zum Beispiel die erforderliche Hardware nicht vorhanden ist oder inaktiviert wurde, wird auf die Richtlinie **IMFAuthorizationPersistancePolicyNever** zurückgegriffen.
