# Crzgames - Libraries C/C++ - Windows - MSVC

## Informations sur les types de fichier des bibliothèques par rapport au system et du compiler :
Compiler : CL

Bibliothèque dynamique/partagée : .dll <br />
Bibliothèque statique : .lib <br />

<br /><br /><br /><br />


## Architecture supportée :
- Windows x64
- Windows arm64


<br /><br /><br /><br />


## Documentation des dépendances pour chacune des librairies :
RCENet : 
  1. dossier include (rcenet) -> à linker
  2. rcenet.lib, ws2_32.lib (Bibliothèque native à Windows), winmm.lib (Bibliothèque native à Windows) <br /><br />

SDL2 : 
  1. dossier include (SDL2) -> à linker
  2. SDL2.lib, SDL2main.lib -> à linker
  3. SDL2.dll -> dossier bin <br /><br />

SDL2_image : 
  1. dossier include (SDL2_image) -> à linker
  2. SDL2_image.lib -> à linker
  3. SDL2_image.dll -> dossier bin <br /><br />

SDL2_ttf : 
  1. dossier include (SDL2_ttf) -> à linker
  2. SDL2_ttf.lib -> à linker
  3. SDL2_ttf.dll -> dossier bin <br /><br />

SDL2_mixer : 
  1. dossier include (SDL2_mixer) -> à linker
  2. SDL2_mixer.lib -> à linker
  3. SDL2_mixer.dll -> dossier bin <br /><br />

OpenSSL : 
  1. dossier include (openssl) -> à linker
  2. libssl_static.lib (doit être link avant libcrypto important), libcrypto_static.lib, Crypt32 (Bibliothèque native à Windows), ws2_32 (Bibliothèque native à Windows) -> à linker
  
<br /><br /><br /><br />


## Documentation pour construire les librairies, pour permettre de récupérer les .h / .lib / .dll des librairies (pour mettre à jour les libraries si il faut) :
### Setup Environment :
1. Download and Install Visual Studio >= 2022 : https://visualstudio.microsoft.com/fr/downloads/
2. Download and Install CMake : https://cmake.org/download/

<br /><br />


### Librairies à récupérer :
#### Informations IMPORTANT - Libraries / Executable :
1. Ajouter 'dumpbin.exe' dans le PATH de Windows :
```bash
# Generalement installer :  "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.34.31933\bin\Hostx64\x64"
# Pour trouver ou es installer le binaire faire la commande :
where dumpbin
```
2. Pour connaître l'architecture ciblée (x64 or x86) d'une library shared/static (.dll/.lib) ou un executable (.exe) : 
```bash
# Exemple for executable !
dumpbin /headers myapp.exe | findstr "machine"
# outputs : 8664 machine (x64) 


# Exemple for librarys shared/static (.dll/.lib) !
dumpbin /headers mylib.dll | findstr "machine"
# outputs : 8664 machine (x64) 
```
3. Pour connaître la version minimale Windows ciblée par un fichier exécutable (.exe) ou une bibliothèque de liens dynamiques (.dll) :
```bash
# Exemple for executable !
dumpbin /headers myapp.exe | findstr /C:"subsystem version"
# outputs : 6.00 subsystem version
# Infos versions Windows : Windows Vista == 6.0, Windows7 == 6.1..etc


# Exemple for librarys shared .dll !
dumpbin /headers mylib.dll | findstr "Subsystem version"
# outputs : 6.00 subsystem version
# Infos versions Windows : Windows Vista == 6.0, Windows7 == 6.1..etc
```
4. Pour connaître la liste des library shared (.dll) dont dépend l'exécutable (.exe) :
```bash
dumpbin /DEPENDENTS myapp.exe
```
5. Pour savoir si une librairie .lib ou .dll est lié à /MD /MDd ou /MT /MTd.. :
```bash
dumpbin /directives mylib.lib | findstr /i "libcmt msvcrt"
dumpbin /imports mylib.dll | findstr /i "libcmt msvcrt"

# Resultat :
# Bibliothèque compilée avec /MD : /DEFAULTLIB:MSVCRT
# Bibliothèque compilée avec /MDd : /DEFAULTLIB:MSVCRTD
# Bibliothèque compilée avec /MT : /DEFAULTLIB:LIBCMT
# Bibliothèque compilée avec /MTd : /DEFAULTLIB:LIBCMTD
```
6. Pour connaître les sous dépendence d'une library dynamique :
```bash
dumpbin /DEPENDENTS path\to\mylib.dll
```
7. Lister les fonctions exportées par une librairie dynamique :
```bash
dumpbin /EXPORTS path\to\mylib.dll
```

<br /><br />

SDL2 : 
1. https://github.com/libsdl-org/SDL/releases
2. Télécharger : SDL2-devel-2.28.5-VC.zip
3. Récupérer les includes/.lib/.dll des version x86/x64 (marchera pour Debug/Release) <br /><br />

SDL2_image : 
1. https://github.com/libsdl-org/SDL_image/releases
2. Télécharger : SDL2_image-devel-version-VC.zip
3. Récupérer les includes/.lib/.dll des version x86/x64 (marchera pour Debug/Release) <br /><br />

SDL2_ttf : 
1. https://github.com/libsdl-org/SDL_ttf/releases
2. Télécharger : SDL2_ttf-devel-version-VC.zip
3. Récupérer les includes/.lib/.dll des version x86/x64 (marchera pour Debug/Release) <br /><br />

SDL2_mixer : 
1. https://github.com/libsdl-org/SDL_mixer/releases
2. Télécharger : SDL2_mixer-devel-version-VC.zip
3. Récupérer les includes/.lib/.dll des version x86/x64 (marchera pour Debug/Release) <br /><br />

RCENet :
1. Télécharger le repository de la dernière release : https://github.com/corentin35000/Crzgames_RCENet/releases (librcenet-windows.zip)
2. Récupérer les fichiers include dans le dossier : ./windows/arch/include/ du dossier télécharger précédemment
3. Récupérer la librairie (rcenet.lib) depuis le dossier : ./windows/arch/lib/ du dossier télécharger précédemment <br /><br />

OpenSSL :
1. Aller sur la page : https://slproweb.com/products/Win32OpenSSL.html
2. Télécharger la dernière version latest (complète et non juste 'light'), via le fichier .msi (le faire pour x64 et x86, ce sont deux .msi diffèrent)
3. Lancer le fichier .msi, faite la procèdure d'installation puis aller récupérer depuis : <br />
   Pour la version x64 : C:\Program Files\OpenSSL-Win64  <br />
   Pour la version x86 : C:\Program Files (x86)\OpenSSL-Win32
4. Récupérer le dossier include de OpenSSL depuis : C:\Program Files\OpenSSL-Win64\include\openssl OU C:\Program Files (x86)\OpenSSL-Win32\include\openssl
5. Récupérer les librairies (.lib) pour x64/x86 ET Debug/Release : <br />
   Debug : C:\Program Files (x86)\OpenSSL-Win32\lib\VC\x86\MDd et C:\Program Files\OpenSSL-Win64\include\openssl\lib\VC\x64\MDd <br />
   Release : C:\Program Files (x86)\OpenSSL-Win32\lib\VC\x86\MD et C:\Program Files\OpenSSL-Win64\include\openssl\lib\VC\x64\MD
6. Récupérer seulement les deux lib static (.lib) : libcrypto_static.lib et libssl_static.lib

<br /><br /><br /><br />


## Signed Executable :
### Documentation Microsoft :
- Il faut lire la documentation : https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-cert-manage
- Après avoir acheter un certificat, il faut ajouté le certificat dans le dashboard des partenanaire de Microsoft si nous déployons une application sur Microsoft Store ou un autre service Microsoft par exemple, sinon ce n'ai pas le cas (tout est expliqué la doc ci-dessus).

<br /><br />

### Pour les anciens certificats avant 2023 (qui permet d'avoir le fichier .pfx / mot de passe du .pfx) :
1. Ajouter SignTool.exe au path de Windows, SignTool.exe ce trouve dans le dossier du SDK Windows installer depuis Visual Studio : <br />
C:\Program Files (x86)\Windows Kits\10\bin\10.0.19041.0\x64
2. Signed the executable with Signtool/Sectigo. <br />
  ```bash
  signtool sign /f "path\to\your\certificate.pfx" /p "pfx_password" /tr http://timestamp.sectigo.com/ /td sha256 /fd sha256 -v MyExecutable.exe
  ```
3. Verify sign binaries.
```bash
signtool verify /pa /v <chemin_vers_le_fichier>
```

<br /><br />

### Pour les nouveaux certificats à partir de 2023 (Azure Key Vault HSM ou Clé USB crypté physique) :
1. Ajouter AzureSignTool.exe en récupérant le binaire ici : https://github.com/vcsjones/AzureSignTool/releases
2. Signer l'executable via AzureSignTool/Azure Key Vault HSM.
  ```bash
  AzureSignTool.exe sign path/to/file.exe --azure-key-vault-url https://xxx.vault.azure.net --azure-key-vault-client-id xxxx --azure-key-vault-client-secret xxxxx --azure-key-vault-tenant-id xxxxx --azure-key-vault-certificate MyNameCertificate --timestamp-rfc3161 http://timestamp.digicert.com --timestamp-digest sha512 --file-digest sha512
  ```
3. Verify sign binaries.
  ```bash
  signtool verify /pa /v <chemin_vers_le_fichier>
  ```

