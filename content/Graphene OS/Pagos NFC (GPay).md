---
title: Pagos NFC (GPay)
tags:
  - grapheneos
---


# 🚫 ¿Se puede usar Google Pay (GPay) en GrapheneOS?

## Spoiler: No… pero hay alternativas

Una de las preguntas más comunes entre quienes consideran usar **GrapheneOS** como sistema operativo en su móvil es:

> ¿Puedo seguir pagando con NFC usando Google Pay?

La respuesta corta es: **no se puede hacer funcionar Google Pay (GPay) o Google Wallet en GrapheneOS**.

---

## ❌ ¿Por qué no funciona Google Pay?

Google Pay requiere que el dispositivo pase **SafetyNet**, una verificación de seguridad que valida si el sistema es "oficial" o está modificado.

### 🧪 SafetyNet tiene dos niveles:

- ✅ `BasicIntegrity`: GrapheneOS **sí la pasa**
    
- ❌ `ctsProfileMatch`: GrapheneOS **no puede pasarla**
    

> El motivo es que **Google no incluye a GrapheneOS en su lista blanca oficial**, y sin eso, **Google Pay lo bloquea automáticamente**.

Este comportamiento es intencionado por parte de Google para evitar que sistemas modificados accedan a servicios de pagos certificados.  
Incluso si instalas los **Play Services en un perfil secundario**, **Google Pay no funcionará**.

📚 **Fuente oficial:**  
[https://discuss.grapheneos.org/d/475-wallet-google-pay](https://discuss.grapheneos.org/d/475-wallet-google-pay)

---

## ✅ ¿Qué alternativas existen?

Aunque no puedes usar Google Pay, **sí puedes hacer pagos por NFC** si tu banco o servicio de pagos lo permite. Algunas opciones:

### 💳 1. **Curve Pay**

Una excelente alternativa que **sí funciona en GrapheneOS**, incluso con NFC.

- Puedes vincular tarjetas de débito/crédito de otros bancos
    
- Realiza pagos NFC sin necesidad de SafetyNet
    
- App disponible en [Aurora Store](https://auroraoss.com) (o F-Droid con Obtanium)
    

🔗 [https://www.curve.com/](https://www.curve.com/)

---

### 🔍 2. **¿Y tu app bancaria? Dependerá del banco**

Algunos bancos permiten pagos NFC **directamente desde su app**, sin depender de Google Pay, pero **no todos lo hacen**.

> ⚠️ **IMPORTANTE**: Muchas apps bancarias requieren pasar SafetyNet/Play Integrity, lo cual **GrapheneOS no puede garantizar**.

Por lo tanto:

- Tendrás que **probar manualmente** si tu app bancaria permite pagos sin Google Pay
    
- En muchos casos, la función NFC no estará disponible, aunque la app funcione para otras gestiones (consultas, transferencias…)

---

## 🛠️ Tip: Usa un perfil separado para apps bancarias

En GrapheneOS puedes crear un perfil de usuario **solo para apps de banca o pagos**. Esto ofrece:

- Aislamiento de datos
    
- Instalación opcional de los Google Play Services en ese perfil
    
- Mayor privacidad
    

---

## 📌 Conclusión

- ❌ No puedes usar Google Pay o Wallet en GrapheneOS debido a limitaciones impuestas por Google (SafetyNet `ctsProfileMatch`)
    
- ✅ Puedes usar **alternativas como Curve Pay**
    
- ✅ Algunas apps bancarias permiten pagos NFC directamente sin Google Pay
    
- ✅ Puedes usar un perfil separado para banca si necesitas Play Services
    

GrapheneOS prioriza la **seguridad, el control y la privacidad**, y aunque renuncias a algunos servicios propietarios, existen soluciones viables y funcionales.