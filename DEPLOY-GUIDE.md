# 📨 Formulario de Contacto - Guía de Despliegue en Netlify

Este proyecto incluye un formulario de contacto funcional que envía emails usando **Resend** a través de funciones serverless de **Netlify**.

## 🚀 Pasos para desplegar en Netlify

### 1️⃣ Crear cuenta en Resend

1. Ve a [resend.com](https://resend.com) y crea una cuenta
2. Verifica tu email
3. Ve a **API Keys** y genera una nueva API Key
4. **Guarda la API Key** (solo se muestra una vez)

### 2️⃣ Preparar el proyecto

```bash
# Instalar dependencias
npm install

# (Opcional) Probar localmente con Netlify Dev
npm run dev
```

### 3️⃣ Desplegar en Netlify

#### Opción A: Desde la interfaz web (Recomendado)

1. Ve a [netlify.com](https://netlify.com) y crea una cuenta
2. Click en **"Add new site"** → **"Import an existing project"**
3. Conecta tu repositorio de Git (GitHub, GitLab, Bitbucket)
4. Netlify detectará automáticamente la configuración desde `netlify.toml`
5. Click en **"Deploy site"**

#### Opción B: Desde la terminal

```bash
# Instalar Netlify CLI
npm install -g netlify-cli

# Login en Netlify
netlify login

# Inicializar el sitio
netlify init

# Desplegar
netlify deploy --prod
```

### 4️⃣ Configurar variables de entorno en Netlify

**IMPORTANTE:** Debes configurar tu API Key de Resend en Netlify

1. En tu sitio de Netlify, ve a **Site settings** → **Environment variables**
2. Click en **"Add a variable"**
3. Añade:
   - **Key:** `RESEND_API_KEY`
   - **Value:** `re_tu_api_key_de_resend`
4. Click en **"Save"**

### 5️⃣ Configurar dominio de envío en Resend

Por defecto, Resend usa `onboarding@resend.dev` para testing. Para producción:

1. Ve a tu dashboard de Resend
2. Añade y verifica tu dominio personalizado
3. Actualiza el campo `from` en [netlify/functions/send-email.js](netlify/functions/send-email.js):

```javascript
from: 'contacto@tudominio.com',  // Cambia esto
to: 'tu@email.com',              // Y esto
```

4. Haz commit y push de los cambios
5. Netlify desplegará automáticamente

## 🧪 Probar localmente

```bash
# Instalar dependencias
npm install

# Crear archivo .env en la raíz
echo "RESEND_API_KEY=re_tu_api_key_aqui" > .env

# Iniciar servidor de desarrollo de Netlify
netlify dev
```

Abre tu navegador en `http://localhost:8888`

## 📂 Estructura del proyecto

```
mi-primer-portafolio/
├── netlify/
│   └── functions/
│       └── send-email.js    # Función serverless para enviar emails
├── assets/
│   ├── css/
│   ├── js/
│   │   └── main.js          # JavaScript del formulario
│   └── images/
├── index.html               # Página principal con formulario
├── netlify.toml             # Configuración de Netlify
├── package.json             # Dependencias del proyecto
├── .env.example             # Ejemplo de variables de entorno
└── .gitignore               # Archivos a ignorar en Git
```

## 🔧 Configuración personalizada

### Cambiar email de destino

Edita [netlify/functions/send-email.js](netlify/functions/send-email.js) línea 48:

```javascript
to: 'demo.system.987@gmail.com',  // Cambia por tu email
```

### Personalizar el template del email

El HTML del email está en la misma función. Puedes modificarlo según tus necesidades.

### Agregar más validaciones

Puedes agregar validaciones adicionales en:
- **Frontend:** [assets/js/main.js](assets/js/main.js)
- **Backend:** [netlify/functions/send-email.js](netlify/functions/send-email.js)

## ⚠️ Notas importantes

1. **No subas tu API Key a Git** - Está en `.gitignore`
2. **Límites de Resend:** Plan gratuito permite 100 emails/día
3. **CORS:** Ya configurado en `netlify.toml`
4. **Testing:** Usa emails reales en desarrollo, Resend no tiene modo sandbox

## 🐛 Solución de problemas

### Error: "RESEND_API_KEY is not defined"
- Asegúrate de configurar la variable de entorno en Netlify
- Si es local, crea el archivo `.env` con tu API Key

### Error: "Email not sent"
- Verifica que tu API Key es correcta
- Revisa los logs en Netlify: Functions → Logs

### El formulario no se envía
- Abre la consola del navegador (F12) para ver errores
- Verifica que la URL de la función es correcta

## 📚 Recursos

- [Documentación de Resend](https://resend.com/docs)
- [Netlify Functions](https://docs.netlify.com/functions/overview/)
- [Netlify Deploy](https://docs.netlify.com/site-deploys/overview/)

## 🎉 ¡Listo!

Tu portafolio ahora tiene un formulario de contacto completamente funcional.

**URL de tu sitio:** Lo verás en el dashboard de Netlify después del deploy.
