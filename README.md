# Crzgames - Libraries C/C++ - Windows (MSVC)

## Informations sur les types de fichiers des bibliothèques C/C++ sous Windows pour MSVC :
- Bibliothèque statique : `.lib`
- Bibliothèque dynamique/partagée : `.dll`

<br /><br /><br /><br />

## Architecture supportée :
- Windows x64
- Windows arm64

<br /><br /><br /><br />

## 📦 Documentation des dépendances

### OpenSSL :
- Include : `include/openssl/`
- Libs statiques : `lib/libssl-static.lib`, `lib/libcrypto-static.lib`

⚠️ OpenSSL : Il faut lier `libssl-static.lib` **avant** `libcrypto-static.lib`.

---

<br /><br /><br /><br />

### Informations TRES IMPORTANT - Libraries / Executable :

### Localiser dumpbin :
```bash
where dumpbin
```
> Généralement situé dans `C:\Program Files\Microsoft Visual Studio\<version>\VC\Tools\MSVC\<version>\bin\Hostx64\x64\dumpbin.exe`

### Identifier l'architecture et la version Windows utilisé par la librairie static / dynamique
```bash
dumpbin /headers path\to\mylib.lib
```
Cela affiche les headers du fichier, y compris la target machine (ex: `x64`).

### Lister les fonctions exportées par une librairie dynamique :
```bash
dumpbin /exports path\to\mylib.dll
```

### Vérifier les sous dépendances d'une librairie dynamique :
```bash
dumpbin /dependents path\to\myblib.dll
```

---

<br /><br /><br /><br />

## Documentation pour construire les librairies, permet de récupérer les .h / .a / .so des librairies (pour mettre à jour les librairies si il faut) :

### OpenSSL (ex: version 3.5.0 pour Windows, statique, MSVC x64)
1. Cloner le repo officiel :
```bash
git clone -b openssl-3.5.0 https://github.com/openssl/openssl.git
cd openssl
```
2. Ouvrir la `Developer Command Prompt for VS` (x64)
3. Lancer la configuration :
```bash
perl Configure VC-WIN64A no-shared --prefix=%CD%/install
nmake
nmake install
```
4. Les `.lib` et `.h` sont dans `install/lib` et `install/include`.
