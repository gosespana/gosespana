---
title: problemas desbloqueo OEM
tags:
  - grapheneos
---

# Cuando “OEM Unlocking” aparece en gris en un Pixel: causas, soluciones y cómo arreglarlo

### Introducción

> Si tienes un Pixel y estás intentando instalar GrapheneOS, es probable que te hayas encontrado con la frustración de ver que la opción **OEM Unlocking** en _Opciones de desarrollador_ está en gris, o deshabilitada, y que no importa lo que hagas, no puedes activarla. Sin ese paso no puedes desbloquear el bootloader, y por tanto no puedes instalar el sistema. En este post exploraremos por qué sucede esto, qué comprobaciones debes hacer, y te daré una guía paso a paso con soluciones que de verdad han funcionado para otros usuarios (y fuentes oficiales).


---

## ¿Por qué puede estar en gris la opción OEM Unlocking?

Estas son algunas de las causas más comunes que se repiten en foros de GrapheneOS y otras comunidades:

- El software del dispositivo (stock Android) no está actualizado a la versión mínima necesaria para ese modelo.
    
- No hay bloqueo de pantalla configurado (PIN, patrón o contraseña). Sin método de bloqueo, Android no permite cambiar esa opción.
    
- El dispositivo no está conectado a Internet, lo que impide que Android verifique ciertas condiciones necesarias (estado de desbloqueo, políticas de fabricante/carrier).
    
- El teléfono pertenece a un operador/carrier que impone restricciones de fábrica para evitar desbloqueo del bootloader.
    
- El dispositivo venía con alguna versión beta o se registró en Android Beta, lo que puede interferir.
    
- Después de actualizar el software, puede requerirse un restablecimiento de fábrica para "reiniciar" ciertos flags o valores internos que permitan habilitar OEM Unlocking.
    

---

## Soluciones comprobadas que han funcionado

Estas son las soluciones que se han reportado en los foros oficiales de GrapheneOS, Reddit y otros, basadas en casos reales:

| Paso / Solución                                                   | Qué hacer exactamente                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Actualizar el sistema al build mínimo requerido**               | Si el dispositivo viene con la versión stock de fábrica, actualizar vía OTA a la versión recomendada (por ejemplo: para el Pixel 6a, al _build de junio 2022_ o posterior). [GrapheneOS Discussion Forum+2GrapheneOS Discussion Forum+2](https://discuss.grapheneos.org/d/2044-oem-unlocking-greyed-out?utm_source=chatgpt.com)                                                                                     |
| **Restablecimiento de fábrica después de actualizar**             | Después de la actualización, hacer _factory reset_, configurar desde cero, conectar a internet y sólo después activar las opciones de desarrollador. [GrapheneOS Discussion Forum+2GrapheneOS Discussion Forum+2](https://discuss.grapheneos.org/d/469-unlock-pixel-6a-greyed-out-oem-unlocking?utm_source=chatgpt.com)                                                                                             |
| **Conexión a Internet antes de intentar habilitar OEM Unlocking** | Al iniciar el dispositivo, con Wi-Fi o red (aunque no sea con cuenta Google), asegurarse que haya conexión para que el sistema pueda verificar si el dispositivo permite desbloqueo. [GrapheneOS Discussion Forum+2GrapheneOS Discussion Forum+2](https://discuss.grapheneos.org/d/469-unlock-pixel-6a-greyed-out-oem-unlocking?utm_source=chatgpt.com)                                                             |
| **Configurar un método de bloqueo de pantalla**                   | Establecer PIN / patrón / contraseña. Si no lo haces, la opción no se activa. [Reddit+1](https://www.reddit.com/r/GrapheneOS/comments/bo1fhf?utm_source=chatgpt.com)                                                                                                                                                                                                                                                |
| **Desactivar versiones beta / programas beta si están activos**   | En algunos casos el dispositivo estaba inscrito en Beta de Android. Al salirse del programa beta y volver a la versión estable, la opción dejó de estar en gris. [GrapheneOS Discussion Forum](https://discuss.grapheneos.org/d/14509-solved-oem-unlocking-greyed-out-pixel-8-pro-but-might-apply-to-others?utm_source=chatgpt.com)                                                                                 |
| **Verificar que el dispositivo sea OEM / factory _unlockable_**   | A veces un teléfono puede estar “desbloqueado” para sim (carrier unlocked) pero no ser desbloqueable en bootloader (OEM unlock). Si lo compraste a un operador, podría tener restricciones. Si lo compraste directamente de Google Store, suele ser más seguro. [GrapheneOS Discussion Forum+2GrapheneOS Discussion Forum+2](https://discuss.grapheneos.org/d/3204-oem-unlocking-greyed-out?utm_source=chatgpt.com) |

---

## Checklist concreto (paso a paso) para resolverlo

1. **Configurar bloqueo de pantalla**: asegúrate de que el dispositivo tiene PIN, patrón o contraseña.
    
2. **Actualizar el sistema operativo stock** al estado más reciente disponible para ese modelo, al menos al build mínimo que GrapheneOS recomienda.
    
3. **Hacer un restablecimiento de fábrica** _después_ de la actualización.
    
4. Durante el primer arranque tras el reset: **conectar a internet** (Wi-Fi o red móvil) lo antes posible.
    
5. Activar _Opciones de desarrollador_.
    
6. Verificar que la opción _OEM Unlocking_ ya no esté en gris. Si sigue en gris, intenta:
    
    - Desactivar y reactivar las Opciones de desarrollador.
        
    - Reiniciar el dispositivo.
        
    - Esperar algún tiempo con conexión a internet, porque hay reportes de que ciertas verificaciones remotas tardan un poco en completarse. [Android Enthusiasts Stack Exchange+1](https://android.stackexchange.com/questions/257226/pixel-8-oem-unlock-greyed-out?utm_source=chatgpt.com)
        
    - Verificar que no haya estado inscrito en Android Beta; si lo está, salir del programa beta. [GrapheneOS Discussion Forum](https://discuss.grapheneos.org/d/14509-solved-oem-unlocking-greyed-out-pixel-8-pro-but-might-apply-to-others?utm_source=chatgpt.com)
        
7. Verificar que el dispositivo realmente sea “OEM-unlockable” (no esté bloqueado por fabricante o carrier). Si compraste usado o a través de terceros, esto puede no estar garantizado. [GrapheneOS Discussion Forum+1](https://discuss.grapheneos.org/d/3204-oem-unlocking-greyed-out?utm_source=chatgpt.com)
    

---

## Caso especial: Pixel 6a

El Pixel 6a es uno de los casos más documentados con este problema. Aquí lo que muchos han reportado que resolvió el asunto:

- Versiones iniciales de fábrica no permiten habilitar OEM Unlocking hasta actualizar a _la build de junio de 2022 o posterior_. [GrapheneOS Discussion Forum+1](https://discuss.grapheneos.org/d/469-unlock-pixel-6a-greyed-out-oem-unlocking?utm_source=chatgpt.com)
    
- Tras actualizar, hacer reset de fábrica. [GrapheneOS Discussion Forum+1](https://discuss.grapheneos.org/d/469-unlock-pixel-6a-greyed-out-oem-unlocking?utm_source=chatgpt.com)
    
- Conectar a internet después del reset para que Android compruebe los permisos necesarios. [GrapheneOS Discussion Forum](https://discuss.grapheneos.org/d/469-unlock-pixel-6a-greyed-out-oem-unlocking?utm_source=chatgpt.com)

---

### Conclusión

> En la mayoría de los casos, el problema se resuelve asegurando que el teléfono tenga la versión de software correcta, que tenga un método de bloqueo de pantalla, que esté conectado a Internet, y que se haya hecho un reseteo de fábrica después de actualizar. Si aún así OEM Unlocking sigue en gris, lo más probable es que el dispositivo tenga alguna restricción de fábrica/carrier, o que haya algún flag interno (por ejemplo por Beta) que impide activar esa opción. En esos escenarios, revisa la procedencia del dispositivo, intenta salir de cualquier programa Beta, o ponte en contacto con soporte del fabricante/vendedor.
> 
> Recuerda también que, tras instalar GrapheneOS con éxito, es buena práctica **desactivar** OEM Unlocking (y volver a bloquear el bootloader, si es aplicable) para aumentar la seguridad.