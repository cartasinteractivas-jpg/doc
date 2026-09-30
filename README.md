# Documentos IA Chat

Frontend mobile-first para conversar con OpenRouter a través de Supabase Edge Functions.

## Incluye

- Chat de texto conectado a `chat-openrouter`.
- Botón de voz con Web Speech API cuando el navegador lo permite.
- Cambio automático entre micrófono y enviar.
- Memoria local del nombre del dispositivo.
- Panel para guardar y verificar nombre, DNI y datos del dispositivo mediante `device-profile`.
- Selector inicial de archivos PDF, DOCX y XLSX.
- Interfaz preparada para el siguiente módulo de lectura y plantillas JSON.

## Configuración local

Copia el archivo de ejemplo:

```bash
cp .env.example .env.local
```

Completa:

```env
VITE_SUPABASE_URL=https://TU_PROJECT_REF.supabase.co
VITE_SUPABASE_ANON_KEY=TU_ANON_KEY_PUBLICA
```

La anon key pública puede estar en el frontend. Nunca coloques aquí `open_api` ni `SUPABASE_SERVICE_ROLE_KEY`.

## Ejecutar

```bash
pnpm install
pnpm dev
```

## Edge Functions esperadas

El frontend llama a estas funciones:

```text
https://TU_PROJECT_REF.supabase.co/functions/v1/chat-openrouter
https://TU_PROJECT_REF.supabase.co/functions/v1/device-profile
```

Las funciones deben estar desplegadas en Supabase y deben aceptar CORS.

## Flujo actual de datos

- El nombre visible se guarda localmente para el saludo.
- El token aleatorio del dispositivo se guarda localmente.
- El panel de datos llama a `device-profile` para guardar o verificar datos.
- El chat llama a `chat-openrouter` para conversar.
- La firma todavía no se persiste.
- El selector de documentos solo conserva el archivo en la sesión; la lectura y generación de PDF será el siguiente módulo.

## GitHub Pages / hosting estático

Este proyecto es un frontend Vite. Para compilar:

```bash
pnpm build
```

Antes del despliegue, define las variables `VITE_SUPABASE_URL` y `VITE_SUPABASE_ANON_KEY` en el entorno de build. No subas `.env.local` al repositorio.

## Nota de seguridad

La aplicación no utiliza Supabase Auth. El `device_token` asocia el navegador con un dispositivo, pero no es una identidad fuerte. Usa datos de prueba durante el desarrollo y agrega cifrado para datos personales antes de una publicación con DNI o domicilio reales.
