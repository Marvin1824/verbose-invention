---
title: Zwei-Faktor-Authentifizierung für Dein persönliches Konto deaktivieren
intro: 'Wenn Du die Zwei-Faktor-Authentifizierung (2FA) für Dein persönliches Konto deaktivierst, verlierst Du möglicherweise den Zugriff auf Organisationen, denen Du angehörst.'
redirect_from:
  - /articles/disabling-two-factor-authentication-for-your-personal-account
  - /github/authenticating-to-github/disabling-two-factor-authentication-for-your-personal-account
  - /github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa/disabling-two-factor-authentication-for-your-personal-account
versions:
  fpt: '*'
  ghes: '*'
topics:
  - 2FA
shortTitle: Disable 2FA
---

Wir empfehlen dringend, Dein Konto mit der Zwei-Faktor-Authentifizierung zu schützen. Wenn Du die 2FA deaktivieren musst, empfehlen wir, sie so bald wie möglich wieder zu aktivieren.

{% warning %}

**Warnung:** Wenn Sie ein Mitglied{% ifversion fpt %}, Abrechnungsmanager{% endif %} oder externer Mitarbeiter eines öffentlichen Repositorys einer Organisation sind, die die Zwei-Faktor-Authentifizierung voraussetzt, und Sie die 2FA deaktivieren, werden Sie automatisch aus der Organisation entfernt und verlieren den Zugriff auf deren Repositorys. Um wieder auf die Organisation zugreifen zu können, aktiviere die Zwei-Faktor-Authentifizierung erneut und wende Dich an einen Organisationsinhaber.

{% endwarning %}

Wenn Deine Organisation die Zwei-Faktor-Authentifizierung voraussetzt und Du ein Mitglied, Inhaber oder externer Mitarbeiter bei einem privaten Repository Deiner Organisation bist, musst Du die Organisation zunächst verlassen, bevor Du die Zwei-Faktor-Authentifizierung deaktivieren kannst.

So entfernst Du Dich selbst aus Deiner Organisation:
 - Wenn Du Mitglied oder Inhaber der Organisation bist, findest Du weitere Informationen unter „[Sich selbst aus einer Organisation entfernen](/articles/removing-yourself-from-an-organization/).“
 - Als externer Mitarbeiter bitte einen Organisationsinhaber oder Repository-Administrator, Dich aus den Repositorys der Organisation zu entfernen. Weitere Informationen findest Du unter „[Rollen von Personen in einer Organisation anzeigen](/articles/viewing-people-s-roles-in-an-organization)“ und „[Externen Mitarbeiter von einem Organisationsrepository entfernen](/articles/removing-an-outside-collaborator-from-an-organization-repository/).“

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.security %}
3. Klicke auf **Disable** (Deaktivieren). ![Schaltfläche „Disable two-factor authentication" (Deaktivieren der Zwei-Faktor-Authentifizierung)](/assets/images/help/2fa/disable-two-factor-authentication.png)

## Weiterführende Informationen

- „[Informationen zur Zwei-Faktor-Authentifizierung](/articles/about-two-factor-authentication)“
- „[Zwei-Faktor-Authentifizierung konfigurieren](/articles/configuring-two-factor-authentication)“
- „[Wiederherstellungsmethoden für die Zwei-Faktor-Authentifizierung konfigurieren](/articles/configuring-two-factor-authentication-recovery-methods)“
