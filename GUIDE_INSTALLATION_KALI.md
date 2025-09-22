### **Titre : Guide d'installation de .NET 9 sur Kali Linux avec les pilotes NVIDIA**

**Date :** 22 septembre 2025
**Auteur :** kd (avec l'aide de Gemini)
**Environnement :**
*   **Distribution :** Kali Linux (kali-rolling)
*   **Version de .NET :** 9.0.305
*   **Pilotes NVIDIA :** (Pilotes propriétaires installés)

**Introduction :**
Ce guide a pour but de documenter l'installation du SDK .NET 9 sur une distribution Kali Linux où les pilotes propriétaires NVIDIA sont également installés. Il détaille les étapes pour surmonter les conflits de paquets potentiels entre les paquets système et les dépendances NVIDIA.

**Étapes de l'installation :**

1.  **Prérequis :**
    *   Assurez-vous que votre système est à jour :
        ```bash
        sudo apt update && sudo apt upgrade -y
        ```

2.  **Résolution des conflits avec les pilotes NVIDIA :**
    *   Lors de l'installation de nouvelles dépendances, une erreur peut survenir avec le paquet `nvidia-installer-cleanup`. Voici la solution pour forcer sa suppression et réparer les paquets cassés :
        ```bash
        sudo dpkg --remove --force-remove-reinstreq nvidia-installer-cleanup
        sudo apt --fix-broken install
        sudo apt autoremove
        ```
    *   *Note : Cette étape est cruciale car le script de post-installation du paquet `nvidia-installer-cleanup` peut entrer en conflit avec les mises à jour du système, bloquant ainsi d'autres installations.*

3.  **Installation du SDK .NET 9 :**
    *   Ajoutez le dépôt de paquets Microsoft pour Debian 12 (Bookworm), qui est compatible avec la base de Kali Linux :
        ```bash
        wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        rm packages-microsoft-prod.deb
        sudo apt update
        ```
    *   Installez le SDK .NET 9 (la version `9.0` installera la dernière version disponible) :
        ```bash
        sudo apt install -y dotnet-sdk-9.0
        ```

4.  **Vérification de l'installation :**
    *   Vérifiez que la bonne version du SDK .NET est active :
        ```bash
        dotnet --version
        ```
    *   *Sortie attendue :*
        ```
        9.0.305
        ```

**Conclusion :**
L'installation de .NET sur des configurations spécifiques comme Kali Linux avec des pilotes NVIDIA est tout à fait réalisable. La clé est d'identifier et de résoudre les conflits de paquets de manière méthodique. Ce guide sert de référence pour toute personne rencontrant des problèmes similaires.
