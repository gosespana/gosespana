---
title: Backups
tags:
  - grapheneos
---

# 🔐 Cómo hacer una copia de seguridad completa en GrapheneOS (sin depender de Google)

Uno de los retos de usar **GrapheneOS** es la ausencia de una herramienta de backup completa y confiable a nivel de sistema. Aunque _Seedvault_ está integrado como solución de copia de seguridad, su uso está **desaconsejado por la propia comunidad**, ya que no es totalmente fiable ni compatible con todas las apps.

En esta guía te explico **cómo respaldo todo mi ecosistema móvil de forma segura y privada**, usando **software libre, sincronización directa entre dispositivos** y, opcionalmente, **infraestructura autoalojada**.

---

## 🏡 Mi enfoque con servidor propio (opcional)

Tengo un **miniserver con Proxmox** en casa, donde tengo desplegados servicios útiles:

- 📁 **Nextcloud** – archivos, calendario, contactos
    
- 🖼️ **Immich** – fotos y vídeos
    
- 🔐 **Vaultwarden** – gestor de contraseñas
    
- ☁️ **Syncthing** – sincronización de archivos entre dispositivos
    
- 📦 **Obtanium** – backup/restauración de apps desde GitHub, F-Droid, etc.
    

Con este setup, cuando cambio de móvil, simplemente sincronizo con mis servicios y recupero todo.

---

## 🧩 Paso 1 – Sincroniza los datos de cada app con Syncthing

Instala [Syncthing](https://syncthing.net/) en tu PC y móvil para sincronizar datos de forma local, sin nube:

Crea una carpeta tanto en tu PC como en tu móvil para guardar los backups de las apps.

Sincroniza esta carpetas con otro PC, móvil, NAS o servidor local para tener redundancia.

Tutorial para usar Syncthing: https://www.youtube.com/watch?v=GSqHUP_c4Fg

---

## 📦 Paso 2 – Respalda tus apps con Obtanium

[Obtanium](https://github.com/ImranR98/Obtanium) te permite:

- Exportar la lista de apps instaladas como `.json`
    
- Importarla en un nuevo dispositivo
    
- Reinstalar apps automáticamente desde sus fuentes (GitHub, F-Droid…)
    

🔧 **Cómo usarlo:**

1. Abre Obtanium > **Settings > Export Sources**
    
2. Guarda el `.json` en `/backups/obtanium`
    
3. Restaura en el nuevo móvil importando ese archivo
    

---

## 🔁 Paso 3 – Restaurar en el nuevo teléfono

1. Instala Syncthing y Obtanium
    
2. Sincroniza la carpeta `/backups`
    
3. Importa el `.json` en Obtanium para recuperar apps
    
4. Restaura datos manualmente desde cada app
    
5. Vuelve a vincular tus servicios (Nextcloud, Vaultwarden, etc.)
    

---

## 💡 ¿Y si **no tienes** un servidor propio?

No hay problema: puedes aplicar el **mismo enfoque con alternativas locales o portátiles**. Aquí te dejo varias opciones:

### ✅ Alternativas sin servidor:

|Servicio reemplazado|Alternativa sin servidor|
|---|---|
|**Nextcloud**|Aplicaciones locales como Simple File Manager o FolderSync (USB/Wi-Fi)|
|**Immich**|Guarda tus fotos en una carpeta Syncthing (`/DCIM/Camera`) y sincroniza con tu PC|
|**Vaultwarden**|Usa **KeePassDX** con archivos `.kdbx` almacenados localmente o en Syncthing|
|**Syncthing**|Sigue siendo usable **PC ↔ móvil vía LAN**|
|**Obtanium**|Igual, no requiere servidor, solo exporta/importa el JSON|

> 🛜 Incluso puedes sincronizar vía Wi-Fi sin Internet, o llevar tu backup en una microSD/pendrive USB-C.

### Ejemplo de flujo sin servidor:

1. Instalas **Syncthing** en tu PC de escritorio
    
2. En el móvil, creas carpetas para backups por app
    
3. Conectas ambos al mismo Wi-Fi → Syncthing sincroniza en LAN
    
4. Guardas el JSON de Obtanium
    
5. Copias todo a un disco externo por seguridad
    

Con esto, tienes un sistema **de copia de seguridad completo, privado y descentralizado**, sin depender de ningún servidor externo o nube comercial.