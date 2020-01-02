# Web-Rezepte

| Recipe |
| :--- |
| [Webseiten-Elemente ein- oder ausblenden auf Basis von Ereignissen](recipes.md#elemente-ein-oder-ausblenden-auf-basis-von-ereignissen-oder-informationen-z-b-ueber-den-login-status) |
| [Unterschied zwischen `textContent` und `innerHTML`](recipes.md#unterschied-zwischen-textcontent-und-innerhtml)\`\` |

## Elemente ein- oder ausblenden auf Basis von Ereignissen oder Informationen z.B. über den Login-Status

Oft wollen wir auf Basis der Information, ob ein Benutzer eingeloggt ist oder nicht, Elemente auf unserer Webseite ein- oder ausblenden. Das gilt zum Beispiel für einen Logout-Button. Dieser ergibt nur Sinn, wenn auch ein Benutzer eingeloggt ist; ansonsten sollte der Button nicht sichtbar sein.

Mit Javascript und den Firebase-Tools können wir das wie folgt umsetzen:

```javascript
firebasetools.onLoginChanged(loginChanged);

function loginChanged(user) {

    // Get a reference to the logout button
    btnLogout = document.querySelector('btnLogout');
    
    if(user) {
        // Remove the hidden attribute if a user is present
        btnLogout.removeAttribute('hidden');
    }
    else {
        // Add the hidden attribute if no user is present
        btnLogout.setAttribute('hidden', '');    
    }
}
```

Der Ansatz ist auf andere Elemente oder Aktionen übertragbar. Das Vorgehen ist immer gleich:

1. Ereignis bestimmen, dass dazu führen soll, etwas ein- oder auszublenden \(z.B. User hat sich eingeloggt\).
2. Herausfinden, wie wir dieses Ereignis _mitbekommen_ \(im Code, z.B. über `onLoginChanged()`\).
3. Mit entsprechender WENN-DANN Logik die Funktionalität umsetzen. Wenn es um ein- oder ausblenden geht eignet sich das Attribute `hidden` sehr gut. Dieses können wir mit den beiden Funktionen `setAttribute()` bzw. `removeAttribute()` hinzufügen oder entfernen.

## Unterschied zwischen `textContent` und `innerHTML`

