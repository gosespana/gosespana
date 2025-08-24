---
title: Usuarios
tags:
  - grapheneos
---
# 🔐 Perfiles en GrapheneOS: Cómo funciona el aislamiento entre usuarios

Una de las características más potentes —y menos comentadas— de **GrapheneOS** (y de AOSP en general) es la posibilidad de crear **múltiples perfiles de usuario**, completamente separados entre sí. Esto permite crear compartimentos seguros dentro del mismo dispositivo: uno para tus apps personales, otro para trabajo, uno para apps con Google Play… incluso uno secreto y oculto.

Pero ¿cómo de separados están realmente estos perfiles? ¿Puede el usuario "principal" acceder a los datos de los demás? ¿Qué diferencia hay entre un **usuario secundario** y el nuevo **Espacio Privado** de GrapheneOS?

Vamos a explicarlo.

---

## 👤 Tipos de usuarios en Android / GrapheneOS

- **Usuario “owner” (sistema)**
    
    - Es el primer perfil. Tiene privilegios exclusivos: ajustes de sistema (Wi‑Fi, desarrollador), desbloqueo tras reinicio, ACLs, instalación/desinstalación de apps para otros usuarios [developer.android.com+15discuss.grapheneos.org+15discuss.grapheneos.org+15](https://discuss.grapheneos.org/d/11715-multiple-user-setup?utm_source=chatgpt.com)[source.android.com+3source.android.com+3discuss.grapheneos.org+3](https://source.android.com/docs/devices/admin/multi-user?utm_source=chatgpt.com).
        
- **Usuarios secundarios (secondary users)**
    
    - Perfiles independientes con apps y datos separados; no pueden acceder a datos o almacenamiento de otros usuarios y se pueden eliminar reorganizar [arsenb.wordpress.com+8source.android.com+8developer.android.com+8](https://source.android.com/docs/devices/admin/multi-user?utm_source=chatgpt.com).
        
    - No pueden modificar sistemas críticos ni eliminar el dispositivo.
        
    - En GrapheneOS pueden desactivarse permisos de fondo para evitar registros en segundo plano [developer.android.com](https://developer.android.com/work/dpc/dedicated-devices/multiple-users?utm_source=chatgpt.com).
        

- **Invitado (Guest)**  
    Un perfil temporal pensado para prestar el teléfono de forma segura. Se borra automáticamente al cerrar sesión.

## 🔒 Diferencias con el “espacio privado” (Private Space)

- Es un tipo especial de perfil creado solo para el owner.

- Puede bloquearse por separado y oculta apps y datos cuando está cerrado.
    
- Mantiene el mismo nivel de aislamiento que un perfil secundario, pero no añade un perfil completo, sólo una partición protegida [source.android.com](https://source.android.com/docs/devices/admin/multi-user?utm_source=chatgpt.com).

---

## 🔐 ¿Hasta qué punto son independientes?

1. **Datos y apps**
    
    - Apps instaladas por el **owner** pueden distribuirse a perfiles secundarios. Sin embargo, los datos se mantienen aislados por perfil [discuss.privacyguides.net+8discuss.grapheneos.org+8discuss.grapheneos.org+8](https://discuss.grapheneos.org/d/11715-multiple-user-setup?utm_source=chatgpt.com).
        
2. **Ejecutables compartidos, datos separados**
    
    - El código de la app es común, pero cada perfil guarda sus propios datos en carpetas distintas (`/data/user/<userid>/...`) [discuss.grapheneos.org+4arsenb.wordpress.com+4source.android.com+4](https://arsenb.wordpress.com/2014/09/30/android-multiuser-model-architecture-and-related-security-threats/?utm_source=chatgpt.com).
        
3. **Sandbox efectivamente reforzado**
    
    - Los perfiles secundarios ofrecen mayor aislamiento que un simple workspace: cada uno tiene su propia encriptación y llaves; se puede “finalizar sesión” (cerrar el perfil) y apagar sus apps completamente [discuss.grapheneos.org](https://discuss.grapheneos.org/d/115-work-profile-vs-user-profile?utm_source=chatgpt.com).
        
4. **Sin comunicación interperfil**
    
    - Apps en distintos perfiles **no interactúan entre sí**. No comparten almacenamiento, contactos, red y sólo pueden comunicarse mediante red (si están activos) .
        
5. **Limitaciones técnicas**
    
    - Al reiniciar, primero deben iniciar sesión en el perfil owner, **no se puede iniciar directamente en un perfil secundario** [discuss.grapheneos.org+1discuss.grapheneos.org+1](https://discuss.grapheneos.org/d/4867-secondary-user-profile-as-a-main-one-advantages-and-disadvantages?utm_source=chatgpt.com).
        
    - Solo **2 perfiles secundarios pueden estar activos simultáneamente** junto al owner; el sistema cierra otros si hay limitación de recursos [discuss.grapheneos.org](https://discuss.grapheneos.org/d/9802-multi-users-notifications-issues?utm_source=chatgpt.com).
        
    - Algunas funciones (SMS, datos móviles, VPN global) solo se gestionan desde el owner .
        

---


## 🧠 ¿Qué tan separados están los perfiles?

### ✅ Aislamiento real

Cada perfil de usuario tiene su propia **clave de cifrado**. Esto significa que sus datos están cifrados y protegidos incluso frente al propietario del teléfono.

- El **Owner no puede acceder** al almacenamiento de un perfil secundario si no se ha desbloqueado ese perfil.
    
- Al **cerrar la sesión** de un usuario secundario, su volumen de datos se desmonta completamente.
    
- Las apps en cada perfil no pueden comunicarse entre sí, ni compartir archivos, ni siquiera notificaciones.
    

> 🔐 **Incluso con acceso root, el Owner no puede leer los datos cifrados de otros perfiles.** Las claves sólo se derivan tras introducir la contraseña de ese usuario.



# 🔄 Compartir archivos entre perfiles en GrapheneOS

En **GrapheneOS (AOSP)**, cada perfil de usuario está completamente aislado: no comparten datos, almacenamiento ni notificaciones. Esto es genial para la privacidad, pero también supone un reto cuando quieres **transferir archivos** entre perfiles. Aquí tienes un método probado y efectivo.

## 📁 Syncthing entre perfiles

Un enfoque popular consiste en instalar **Syncthing** en los perfiles que quieres conectar. No requiere servidor externo, funciona enteramente dentro del teléfono:

Tutorial para configurar Syncthing: https://www.youtube.com/watch?v=GSqHUP_c4Fg

**Guía básica :**

1. Instala Syncthing en el perfil _Owner_ y en un perfil secundario 🔁 
    
2. Configura ambos para que usen puertos diferentes (evitas conflictos): edita `127.0.0.1:22000`, etc.
    
3. Intercambia Device IDs (copiando o escaneando código QR entre perfiles)
    
4. Crea una carpeta sincronizada en ambos perfiles, elige qué datos quieras compartir (por ejemplo, `/DCIM/Camera`) 
    
5. Acepta la petición de sincronización en ambos perfiles y habilita la carpeta
    
6. Syncthing sincronizará los archivos localmente, sin Internet ni servidor externo [
    

**Ventajas**: cifrado, independiente de la nube, automática tras la configuración inicial.  
_💬 "Syncthing. My setup is a synced folder between the profiles and my PC... The PC could be a NAS, server, phone…"_ [discuss.grapheneos.org+4discuss.grapheneos.org+4discuss.grapheneos.org+4](https://discuss.grapheneos.org/d/4324-sharing-files-between-user-profiles?utm_source=chatgpt.com)


## 🔧 Cómo cambiar los puertos en Syncthing en Android (GrapheneOS)

Cuando usas **Syncthing en varios perfiles de usuario** en el mismo dispositivo (por ejemplo, _Owner_ y un perfil secundario), es necesario que **cada instancia use puertos distintos**, ya que comparten el mismo sistema y podrían entrar en conflicto si usan los mismos por defecto.

### 🎯 Objetivo

- Cambiar:
    
    - El puerto de **sincronización de datos** (por defecto `22000`)
        
    - El puerto de la **interfaz web (GUI)** (por defecto `8384`)
        

---

## 📱 Guía paso a paso desde la app Syncthing en Android

### 🔹 Paso 1 – Abre la app Syncthing y accede a la interfaz web integrada

1. Abre **Syncthing** en el perfil donde lo tienes instalado.
    
2. Toca el **menú de tres líneas horizontales** (☰) en la esquina superior izquierda.
    
3. Selecciona **"Interfaz gráfica web"**.
    
    Se abrirá la interfaz web dentro de la app (no es un navegador externo).
    

---

### 🔹 Paso 2 – Entra en los ajustes avanzados

1. Toca el **icono de la rueda dentada** (⚙️) en la esquina superior derecha.
    
2. Selecciona **"Ajustes"**.
    
3. Ahora estarás en la pantalla de configuración general.
    

---

### 🔹 Paso 3 – Cambiar el puerto de sincronización de dispositivos

1. Ve a la pestaña **"Conexiones"**.
    
2. En el campo **"Direcciones de escucha de protocolo de sincronización"**, estará puesto como `"default"`.
    
3. Cámbialo por algo como:
    
    `tcp://0.0.0.0:22010`
    
    (Puedes usar cualquier puerto **libre** que no esté en uso, como `22020`, `22030`, etc.)
    

---

### 🔹 Paso 4 – Cambiar el puerto de la interfaz web (GUI)

1. En la misma pantalla de ajustes, desplázate hacia abajo a la sección **"Interfaz gráfica del usuario"**.
    
2. En el campo **"Dirección de la interfaz de usuario"**, cambia:
    
    - De: `127.0.0.1:8384`
        
    - A: `127.0.0.1:8385` (o cualquier otro número único, por ejemplo `8386`)
        

---

### 🔹 Paso 5 – Guardar y reiniciar

1. Toca **Guardar**.
    
2. La app reiniciará el servicio Syncthing con los nuevos puertos.
    

---

## 🧪 Verifica que funciona

- Puedes volver a entrar en la **Interfaz gráfica web** desde el mismo menú ☰.
    
- Si cambiaste la interfaz a un puerto diferente (`8385`), asegúrate de que la app lo detecte correctamente (puede que tarde unos segundos en reconectar internamente).
    
- Repite este proceso en los demás perfiles, usando puertos **distintos en cada uno** (ej.: `22010`/`8385`, `22020`/`8386`, etc.).
    

---

## ✅ Resultado

Ahora cada perfil de usuario tiene su instancia de Syncthing funcionando en paralelo, sin interferencias, y puedes sincronizar carpetas entre ellos (por ejemplo, usando Syncthing en el perfil _Owner_ y en un perfil secundario).