# Cambios de la rama `update-2026`

> Esta rama es el mismo curso —el Bootcamp de Unity (seis juegos)—, preparada para abrirse con **Unity 6**. La rama
> principal sigue exactamente como en el vídeo.
> Revisado contra el código fuente de Unity 6, pero todavía no se ha abierto en el editor: es un salto grande (de Unity 5.6 a Unity 6). Si algo no abre o no compila, cuéntalo en la comunidad del curso.

## Cómo usarla

1. Instala **Unity 6** (la versión LTS que te ofrezca Unity Hub).
2. Descarga solo esta rama: `git clone --depth 1 -b update-2026 https://github.com/joanby/cursos-unity-2017` (o, en GitHub, cambia a la
   rama `update-2026` y *Code → Download ZIP*). Sin el `--depth 1`, git se trae también el historial
   de la rama principal, con la caché antigua dentro.
3. En Unity Hub, **Add → Add project from disk** y elige la carpeta de un proyecto (`UB - P1 - Twin Stick Shooter`, `UB - P2 - FirstPersonShooter`, `UB - P3 - Tappy Plane`, `UB - P4 - Shooting Ducks`, `UB - P5 - Clicker`, `UB - P6 - Capsule Kong`),
   no la raíz del repositorio.
4. Unity te avisará de que el proyecto es de una versión anterior: acepta la actualización.

## Qué ha cambiado y por qué

### La caché de Unity ya no está en el repositorio

La rama principal guarda en git la caché de Unity (`Library/`, `Logs/`, `obj/`…): **5684 de los 6884 ficheros**. Unity la regenera al abrir el proyecto y con Unity 6 se reconstruye
entera, así que solo hacía la descarga enorme. En esta rama no está, y el `.gitignore` evita que vuelva.
**No cambia nada de lo que ves en el vídeo:** escenas, scripts, modelos, materiales y ajustes siguen ahí.

### Scripts de utilidad que no compilan en Unity 6 y nadie usaba

Usan APIs que Unity ha eliminado (`GUIText`, `GUITexture`…). Ninguna escena, prefab ni script
del curso los usa, así que se han quitado para que el proyecto compile:

- `UB - P2 - FirstPersonShooter`: `ForcedReset.cs`, `SimpleActivatorMenu.cs`

### Shooting Ducks: un parche en iTween, no en el código del curso

iTween es una librería de terceros (`Assets/Plugins/Pixelplacement/iTween`) que tenía partes para
`GUIText` y `GUITexture`, que Unity eliminó: en Unity 6 el proyecto no compilaba. Esas partes —las de
cambiar el color de un texto o una textura de la UI antigua, y el fundido de cámara— quedan ahora
dentro de `#if !UNITY_2019_3_OR_NEWER`, así que en la versión del vídeo todo compila igual que antes y
en Unity 6 simplemente no existen. El juego solo usa `iTween.MoveBy`, `iTween.ValueTo` e `iTween.Hash`,
que no pasan por ahí.

### El código del curso no se ha tocado

Los scripts que escribimos en el vídeo están igual. Lo que puedes ver en la consola de Unity 6:

- `UB - P2 - FirstPersonShooter`: .drag (hoy linearDamping; lo cambia el API Updater); .velocity (en Rigidbody, hoy linearVelocity; lo cambia el API Updater); FindObjectOfType (obsoleto: aviso amarillo); propiedades antiguas de ParticleSystem (obsoletas)
- `UB - P3 - Tappy Plane`: .velocity (en Rigidbody, hoy linearVelocity; lo cambia el API Updater); atajos de Unity 4 (rigidbody., renderer.…): los reescribe el API Updater
- `UB - P4 - Shooting Ducks`: atajos de Unity 4 (rigidbody., renderer.…): los reescribe el API Updater
- `UB - P6 - Capsule Kong`: .velocity (en Rigidbody, hoy linearVelocity; lo cambia el API Updater); atajos de Unity 4 (rigidbody., renderer.…): los reescribe el API Updater

Son avisos (amarillos) o cambios que Unity hace solo al abrir el proyecto: el juego funciona igual.

## Lo que se ve distinto al vídeo

La interfaz del editor: Unity 6 ha movido y rediseñado paneles y menús. Lo que aprendes en el
curso (componentes, físicas, scripts, escenas) es exactamente lo mismo.
