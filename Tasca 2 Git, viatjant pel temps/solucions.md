# Tasca 2: Git, viatjant pel temps

## Objectiu

En aquesta activitat es practica el control de versions amb Git i GitHub: creació de commits, consulta de l'historial, recuperació de canvis del *working directory* i gestió de versions anteriors.


## 1. Preparació del repositori i primers fitxers

A les captures es veu un repositori obert des de PowerShell a VS Code. També s'hi observa un fitxer `README.md` i un fitxer de configuració de xarxa.

La captura 4 mostra la configuració inicial del fitxer `00-installer-config.yaml`:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
```

**Evidències:**

![Configuració inicial del fitxer de xarxa](IMG/4.png/4.png)

La captura 3 mostra l'historial gràfic de Git Graph. En aquest moment es veu un únic commit, amb el fitxer `README.md` i un altre fitxer anomenat `partits.ics`.

![Historial gràfic inicial i contingut del commit](IMG/3.png/3.png)

## 2. Consulta de l'historial

S'han executat les ordres següents:

```bash
git log
git log --oneline
```

La captura 1 mostra la sortida de `git log`, amb el commit `8a94ce408fd356715eccb059c9d9cc4ffe745e36`, l'autor i la data.

![Sortida de git log](IMG/1.pngmg/1.png)

La captura 2 mostra la sortida resumida de `git log --oneline`.

![Sortida de git log --oneline](IMG/2.pngmg/2.png)

També es disposa de la captura de Git Graph, que permet veure el commit i els fitxers associats. La captura 3 inclou, a més, la sortida de terminal amb informació detallada del commit i el diff de `README.md`.

## 3. Inspecció i estat dels fitxers

La captura 5 mostra l'execució de:

```bash
git status
```

El resultat indica que la branca `main` està sincronitzada amb `origin/main`, però hi ha un fitxer no rastrejat anomenat `tatus`. Per tant, en aquell moment el directori de treball no estava completament net.

![Estat del repositori amb un fitxer no rastrejat](IMG/5.pngg/5.png)

La captura 6 mostra el panell *Source Control* de VS Code amb dos canvis detectats: `00-installer-config.yaml` i `tatus`.

![Canvis detectats a Source Control](IMG/6.pngmg/6.png)

## 4. Configuració d'una IP estàtica

La captura 7 mostra una configuració de xarxa amb DHCP desactivat i una adreça IP estàtica per a la interfície `enps03`:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enps03:
      dhcp4: false
      addresses: [192.168.1.100/24]
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [192.168.1.1]
```

![Configuració IP estàtica de la interfície enps03](IMG/7.pngg/7.png)

A la captura 8 es veu una ordre de commit amb el missatge `feat: configura ip estatica a enps03`. La sortida indica que s'ha creat un fitxer anomenat `tatus` amb 184 insercions. Cal revisar el nom del fitxer, ja que no coincideix amb `00-installer-config.yaml`.

![Creació del commit de configuració IP estàtica](IMG/8.pngg/8.png)

La captura 9 mostra l'historial resumit amb dos commits: el commit `eaca969` (`feat: configura ip estatica a enps03`) i el commit anterior `8a94ce4`.

![Historial després del commit de configuració IP](IMG/9.pngg/9.png)

## 5. Intent de crear els commits següents

La captura 11 mostra intents d'executar les ordres per crear els commits següents:

```bash
git commit -m "feat: afegeix segona interfície en DHCP"
git commit -m "feat: actualitza servidor DNS de enps03"
```

La sortida indica `nothing to commit, working tree clean` en aquests intents. Això vol dir que Git no va detectar canvis nous preparats per desar en aquests commits. Per tant, les captures facilitades no acrediten que s'hagin creat aquests dos commits.

![Intents de crear els commits de la segona interfície i del DNS](IMG/11.pngmg/11.png)

La captura 10 mostra el contingut del fitxer amb el servidor DNS `8.8.8.8` configurat a `enps03`:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enps03:
      dhcp4: false
      addresses: [192.168.1.100/24]
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8]
```

![Configuració DNS amb 8.8.8.8](IMG/10.pngg/10.png)

Tot i que es veu el contingut del DNS modificat, no hi ha una evidència que confirmi un commit nou amb aquest canvi.

## 6. Revertir un commit

**Pendent de documentar:** no s'ha facilitat cap captura que mostri l'execució de `git revert` ni el nou commit de reversió a Git Graph.

Per completar aquest apartat caldria mostrar:
- L'ordre `git revert` aplicada al commit correcte.
- L'historial de Git Graph amb el nou commit de reversió.
- La comprovació que el contingut del repositori ha tornat a l'estat esperat.

## 7. Explorar un commit anterior

**Pendent de documentar:** no s'ha facilitat cap captura que mostri el quart commit seleccionat a Git Graph ni la comparació de canvis a VS Code.

Per completar aquest apartat caldria una captura on es vegin les línies afegides i eliminades respecte del commit anterior.

## 8. Eliminar l'últim commit amb `git reset`

**Pendent de documentar:** no s'han facilitat captures de l'estat del repositori abans i després de l'ordre:

```bash
git reset --hard HEAD~1
```

Per completar aquest apartat caldria mostrar:
1. `git log --oneline` abans del reset.
2. El fitxer després del reset.
3. `git status`.
4. `git log --oneline` després del reset.
