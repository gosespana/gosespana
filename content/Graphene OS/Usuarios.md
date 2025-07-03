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



