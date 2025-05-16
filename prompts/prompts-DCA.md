# Prompts utilizados para la generación del pipeline CI/CD

## 1. Tests de backend

**Prompt:**
> ¿Cómo puedo ejecutar los tests del backend en un proyecto Node.js con Jest usando GitHub Actions?

**Respuesta generada:**
- Usar los comandos `npm install` y `npm run test` en el directorio backend.
- Configurar un job en GitHub Actions que instale dependencias y ejecute los tests.

---

## 2. Generación del build del backend

**Prompt:**
> ¿Cómo puedo generar el build de un backend en Node.js (TypeScript) en GitHub Actions?

**Respuesta generada:**
- Usar el comando `npm run build` en el directorio backend.
- Añadir un job en GitHub Actions que dependa del job de tests y archive el resultado del build.

---

## 3. Despliegue del backend en EC2

**Prompt:**
> ¿Cómo puedo desplegar el build de un backend Node.js en una instancia EC2 usando GitHub Actions, SSH y PM2?

**Respuesta generada:**
- Usar los secrets de GitHub para la clave privada, usuario e IP de la instancia EC2.
- Copiar los archivos generados con `scp` y reiniciar el servicio con `pm2` usando `ssh`.
- Añadir un job en GitHub Actions que descargue el build, lo copie a la instancia EC2 y reinicie el backend con PM2.

---

## 4. Migraciones de base de datos Prisma en EC2

**Prompt:**
> ¿Cómo puedo ejecutar migraciones de base de datos Prisma automáticamente en una instancia EC2 como parte del pipeline de despliegue usando GitHub Actions?

**Respuesta generada:**
- Añadir un paso en el job de deploy que, tras copiar el build, ejecute `npm install --omit=dev` y `npx prisma migrate deploy` vía SSH en la instancia EC2.
- Asegurarse de que el backend tenga acceso a la base de datos y las variables de entorno necesarias.

---

## 5. Notificaciones a Slack con Bot Token

**Prompt:**
> ¿Cómo puedo notificar a un canal de Slack el estado (éxito o fallo) de un pipeline de GitHub Actions usando un bot token, incluyendo información del commit, autor, rama y enlace al workflow?

**Respuesta generada:**
- Utilizar la acción oficial `slackapi/slack-github-action` en el workflow.
- Configurar el secret `SLACK_BOT_TOKEN` en GitHub.
- Añadir dos jobs: uno para notificar éxito (`notify-success`) y otro para fallo (`notify-failure`), ambos con payload enriquecido (repositorio, rama, commit, autor, enlace al workflow).
- Personalizar el canal y el formato del mensaje según las necesidades del equipo.