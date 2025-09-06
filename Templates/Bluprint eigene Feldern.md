In **Grav CMS** kannst du sogenannte **Blueprints** verwenden, um eigene Felder für Seiten, Module, Plugins oder Themes im Admin-Panel bereitzustellen.
Diese Blueprints sind einfache **YAML-Dateien**, die du im jeweiligen Ordner ablegst.

---

## 1. Seiten-Blueprint erstellen

Wenn du ein Template hast (z. B. `mytemplate.html.twig`), legst du in deinem Theme unter

```
user/themes/dein-theme/blueprints/
```

eine Datei mit gleichem Namen an:

```
mytemplate.yaml
```

### Beispiel `mytemplate.yaml`

```yaml
title: My Custom Page
'@extends':
    type: default
    context: blueprints://pages

form:
  fields:

    tabs:
      type: tabs
      active: 1

      fields:

        content:
          type: tab
          title: Content

        options:
          type: tab
          title: Optionen

          fields:

            header.myfield:
              type: text
              label: Mein eigenes Feld
              help: Trage hier etwas ein

            header.enable_feature:
              type: toggle
              label: Feature aktivieren?
              highlight: 1
              default: 0
              options:
                1: Ja
                0: Nein
              validate:
                type: bool
```

👉 Die Werte landen dann in der **Page-Header-Section** der jeweiligen `.md` Datei, z. B.:

```yaml
---
title: Testseite
myfield: "Hallo Grav"
enable_feature: true
---
```

---

## 2. Plugin-Blueprints

Wenn du ein eigenes Plugin baust, legst du deine Blueprints in:

```
user/plugins/dein-plugin/blueprints.yaml
```

Beispiel:

```yaml
name: Mein Plugin
version: 1.0.0
form:
  validation: strict
  fields:
    enabled:
      type: toggle
      label: Plugin aktivieren
      highlight: 1
      default: 0
      options:
        1: Ja
        0: Nein
      validate:
        type: bool

    custom_text:
      type: text
      label: Benutzerdefinierter Text
      default: "Hallo Welt"
```

Dann erscheint das Feld direkt in der Admin-UI unter den Plugin-Einstellungen.

---

## 3. Feldtypen

Grav unterstützt viele Feldtypen:

* `text`, `textarea`, `toggle`, `select`, `colorpicker`, `datetime`, `file`, `editor`, usw.
  👉 Siehe Doku: [https://learn.getgrav.org/17/forms/blueprints](https://learn.getgrav.org/17/forms/blueprints)