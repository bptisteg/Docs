!!! warning "Ce site est en cours de construction !"

```
Ce site est actuellement en cours de développement.

Vous pensez pouvoir contribuer ? Cliquez simplement sur l'icône en forme de crayon située à droite de la page !

Vous pouvez également contribuer à n'importe quelle autre page.
```

# Création d'une UI-App

Pour créer une UI-App, vous devez avoir quelques connaissances du framework **AngularJS**. La documentation principale est disponible ici : [documentation AngularJS](https://docs.angularjs.org/guide).

## Structure des fichiers

Une UI-App fonctionnelle nécessite quatre fichiers principaux :

* `app.js` — Contient le code JavaScript principal de l'UI-App. [Documentation JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript)
* `app.html` — Contient le code HTML qui affiche l'application. [Documentation HTML](https://developer.mozilla.org/fr/docs/Web/HTML)
* `app.json` — Contient les informations et la configuration de l'UI-App.
* `app.png` — Image affichée dans le sélecteur d'UI-Apps.

### Style de l'UI-App

Il est recommandé d'utiliser une balise `<style>` directement dans le fichier HTML pour styliser votre application. Un fichier `.css` fonctionne également, mais les modifications ne seront pas visibles en temps réel.

---

## Exemple

Cet exemple provient de **DanielW**. Merci à lui !

### `ui\modules\apps\ExampleApp\app.html`

```html
<div style="width: 100%; height: 100%;" class="bngApp">
    <link type="text/css" rel="stylesheet" href="/ui/modules/apps/ExampleApp/app.css" />

    <div id="exampleAppContainer">
        <span>Rapport : <span>{{ gearName }}</span></span>

        <div layout="row" layout-align="center center">
            <md-input-container flex>
                <label>Message</label>
                <input ng-model="message" ng-keydown="sendMessage($event)">
            </md-input-container>

            <md-button md-no-ink class="md-warn"
                       ng-disabled="!message"
                       ng-click="sendMessage()">Envoyer</md-button>
        </div>

        <span style="display: block">Messages :</span>

        <!-- Zone de défilement -->
        <ul bng-nav-scroll style="margin: 0; padding: 0; overflow-y: auto; width: 100%; height: 100%; background-color: #37373740;">

            <!-- Parcourt les messages et les affiche -->
            <li ng-repeat="message in messages track by $index"
                style="display: flex; align-items: center; height: 35px;">

                <span style="padding: 0 0.2em; width: 100%;">{{ message }}</span>

                <!-- Bouton permettant de supprimer le message.
                     Appelle la fonction deleteMessage() dans app.js -->
                <md-button md-no-ink class="md-icon-button md-warn"
                           ng-click="deleteMessage($index)">
                    <md-icon class="material-icons">delete</md-icon>
                </md-button>
            </li>
        </ul>
    </div>
</div>
```

Ici, vous pouvez voir :

* une balise `<span>` affichant le rapport du véhicule ;
* un champ de saisie permettant d'envoyer un message à la fonction `sendMessage()` du JavaScript ;
* une balise `<li>` répétée grâce à `ng-repeat`, utilisant la variable `messages` définie dans le JavaScript.

---

### `ui\modules\apps\ExampleApp\app.js`

```js
angular.module('beamng.apps')
.directive('exampleApp', [function() {
    return {
        templateUrl: '/ui/modules/apps/ExampleApp/app.html',
        replace: true,
        restrict: 'EA',
        scope: true,

        controller: ['$scope', function($scope) {
            $scope.gearName = '0'
            $scope.message = ''
            $scope.messages = []

            // Configure les flux de données dont nous avons besoin.
            // Ici, nous utilisons uniquement les informations du moteur.
            let streamList = ['engineInfo']
            StreamsManager.add(streamList)

            $scope.$on('destroy', function() {
                StreamsManager.remove(streamList)
            })

            $scope.$on('streamsUpdate', function(event, streams) {
                if (!streams.engineInfo)
                    return

                // lua/vehicle/controller/vehicleController.lua:538
                // (ou utilisez console.log pour effectuer vos propres tests)
                let gear = streams.engineInfo[5]

                // Met à jour le rapport affiché dans le HTML si nécessaire
                if ($scope.gearName !== gear)
                    $scope.gearName = gear
            })

            $scope.sendMessage = function(event) {
                if (event && event.key !== 'Enter')
                    return

                if ($scope.message == '')
                    return

                // Envoie le message à l'extension Lua pour le modifier
                bngApi.engineLua(
                    'extensions.exampleMod.modifyMessage("' +
                    $scope.message +
                    '")'
                )

                $scope.message = ''
            }

            $scope.deleteMessage = function(idx) {
                $scope.messages.splice(idx, 1)
            }

            // La fonction modifyMessage() déclenchera cet événement
            // avec le message modifié.
            $scope.$on('MessageReady', function(_, modifiedMessage) {
                $scope.messages.push(modifiedMessage)
            })
        }]
    }
}])
```

### Le fonctionnement de `$scope`

L'utilisation de **`$scope`** est particulièrement importante.

Vous devez définir vos variables et vos fonctions dans `$scope` afin qu'elles puissent être utilisées depuis le HTML via les directives `ng-*`.

Par exemple :

```js
$scope.message = ''
$scope.messages = []

$scope.sendMessage = function() {
    // ...
}
```

Le HTML peut alors accéder directement à ces éléments :

```html
<input ng-model="message">
```

ou :

```html
<md-button ng-click="sendMessage()">
    Envoyer
</md-button>
```

Dans cet exemple, lorsque `sendMessage()` est exécutée depuis le HTML, elle envoie le message vers une extension Lua située dans le dossier `extensions` du mod afin d'exécuter la fonction `modifyMessage()`.

---

## Communication entre JavaScript et Lua

Voici à quoi peut ressembler la partie Lua :

```lua
local function modifyMessage(message)
    message = message .. " [Modifié !]"
    guihooks.trigger('MessageReady', message)
end
```

Il s'agit ici d'une version simplifiée permettant de comprendre le fonctionnement.

L'élément important est :

```lua
guihooks.trigger('MessageReady', message)
```

`guihooks.trigger()` déclenche un événement AngularJS qui peut être récupéré avec :

```js
$scope.$on('MessageReady', function(_, modifiedMessage) {
    $scope.messages.push(modifiedMessage)
})
```

Le fonctionnement est donc :

```text
HTML
  ↓
sendMessage()
  ↓
bngApi.engineLua()
  ↓
Lua : modifyMessage()
  ↓
guihooks.trigger()
  ↓
JavaScript : $scope.$on()
  ↓
$scope.messages
  ↓
ng-repeat
  ↓
Affichage dans l'UI-App
```

---

# Extension Lua complète

### `lua\ge\extensions\exampleMod.lua`

```lua
local M = {}

--[[
    Point d'entrée de notre extension.
    C'est ce que le jeu charge depuis notre modScript.lua.

    Dans ce fichier, nous pouvons communiquer avec :
      1. Notre extension du véhicule.
      2. Les entrées utilisateur.
]]

-- Hooks de l'extension
--------------------------------------------

local function onExtensionLoaded()
    log('D', "onExtensionLoaded", "Appelée")
end

local function onExtensionUnloaded()
    log('D', "onExtensionUnloaded", "Appelée")
end

-- Fonctions personnalisées
--------------------------------------------

local function onActionKeyDown()
    log('D', "onActionKeyDown", "Touche pressée !")
end

local function onVehicleExtensionLoaded(vehID)
    log('D', "onVehicleExtensionLoaded", "Envoi de données au véhicule")

    local veh = be:getObjectByID(vehID)

    -- Si vous n'avez pas l'ID, vous pouvez également utiliser :
    -- be:getPlayerVehicle(0)

    if not veh then
        return
    end

    local data = {
        ["name"] = "Daniel W"
    }

    veh:queueLuaCommand(
        "extensions.exampleVehicleExtension.onDataReceived('" ..
        jsonEncode(data) ..
        "')"
    )
end

local function modifyMessage(message)
    message = message .. " [Modifié !]"
    guihooks.trigger('MessageReady', message)
end

-- Interface publique
--------------------------------------------

M.onExtensionLoaded = onExtensionLoaded
M.onExtensionUnloaded = onExtensionUnloaded

M.onActionKeyDown = onActionKeyDown
M.onVehicleExtensionLoaded = onVehicleExtensionLoaded
M.modifyMessage = modifyMessage

--[[
    D'autres fonctions peuvent notamment être :

      - onPreRender(dtReal, dtSim, dtRaw)
      - onUpdate(dtReal, dtSim, dtRaw)
      - onClientPreStartMission(levelPath)
      - onClientPostStartMission(levelPath)

    Pour trouver les différents hooks disponibles,
    recherchez "extensions.hook(" dans :

    BeamNG.Drive/lua
]]

return M
```

Il est **très important de retourner la variable `M`** contenant les fonctions nécessaires.

Par exemple, sans :

```lua
M.modifyMessage = modifyMessage
```

l'appel JavaScript :

```js
bngApi.engineLua(
    'extensions.exampleMod.modifyMessage("' + $scope.message + '")'
)
```

ne pourra pas trouver la fonction `modifyMessage()`.

---

# CSS de l'UI-App

### `ui\modules\apps\ExampleApp\app.css`

```css
#exampleAppContainer {
    width: 100%;
    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;
    align-content: center;
}

#exampleAppContainer > * {
    margin: 0;
    padding: 0;
}
```

---

# Configuration de l'UI-App

### `ui\modules\apps\ExampleApp\app.json`

```json
{
    "domElement": "<example-app></example-app>",
    "name": "Example App",
    "types": [
        "ui.apps.categories.debug"
    ],
    "description": "example-app",
    "css": {
        "left": "0px",
        "height": "auto",
        "width": "270px",
        "min-width": "200px",
        "min-height": "90px",
        "top": "0px"
    },
    "author": "Daniel W",
    "version": "0.1",
    "directive": "exampleApp"
}
```

La propriété `directive` doit correspondre exactement à la directive définie dans le fichier JavaScript :

```js
.directive('exampleApp', [function() {
```

Dans cet exemple :

```text
app.json
    ↓
"directive": "exampleApp"
    ↓
app.js
    ↓
.directive('exampleApp', ...)
```

---

# Fonctions JavaScript fournies par BeamNG

Pour exécuter une fonction Lua depuis une UI-App, utilisez :

```js
bngApi.engineLua("chemin.lua.fonction()")
```

Cette fonction est particulièrement utile pour exécuter une fonction Lua avec ou sans arguments.

Par exemple :

```js
bngApi.engineLua(
    'extensions.exampleMod.modifyMessage("Bonjour !")'
)
```

---

# Fonctions Lua fournies par BeamNG pour les UI-Apps

Pour envoyer un événement vers l'interface JavaScript :

```lua
guihooks.trigger("EventName", Payload)
```

Le `Payload` peut être de différents types. Il est cependant recommandé d'utiliser un **tableau**, un **objet** ou une **chaîne de caractères** afin d'éviter les problèmes de transmission des données.

Exemple :

```lua
guihooks.trigger("MessageReady", "Bonjour !")
```

Puis, côté JavaScript :

```js
$scope.$on('MessageReady', function(_, message) {
    console.log(message)
})
```

!!! warning "Attention aux noms d'événements"

````
Il est possible que le nom d'événement que vous utilisez soit déjà utilisé en interne par BeamNG.drive.

Cela peut provoquer des conflits avec d'autres systèmes du jeu.

Par exemple, si votre application s'appelle `Nickel`, il est préférable de préfixer vos événements :

```text
NKEventName
NKMessageReady
NKUpdate
```

plutôt que d'utiliser des noms génériques comme :

```text
EventName
MessageReady
Update
```

Utiliser un préfixe propre à votre application permet de réduire fortement les risques de conflits.
````
