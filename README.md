# Fundamentos NestJS — Práctica 01: Configuración e introducción

**Estudiante:** Marco Cobos  
**Curso:** Programación y Plataformas Web

---

## Tabla de contenidos

1. [Verificación de Node.js](#1-verificación-de-nodejs)
2. [Inicio del servidor NestJS](#2-inicio-del-servidor-nestjs)
3. [Endpoint /api/status](#3-endpoint-apistatus)
4. [Estructura del módulo status](#4-estructura-del-módulo-status)
5. [Reflexión del estudiante](#5-reflexión-del-estudiante)

---

## 1. Verificación de Node.js

Verificación de la versión de Node.js instalada mediante el comando `node -v`.

```bash
node -v
```

![Verificación de Node.js](./assets/Captura%20desde%202026-06-18%2018-00-29.png)

> Node.js v24.15.0 instalado correctamente.

---

## 2. Inicio del servidor NestJS

Arranque del servidor en modo estándar con `pnpm start`.

```bash
pnpm start
```

![Servidor NestJS iniciado](./assets/Captura%20desde%202026-06-18%2018-00-59.png)

El log confirma:
- `StatusModule` y `AppModule` inicializados correctamente.
- Ruta `GET /api/status` mapeada por `StatusController`.
- **Nest application successfully started.**

---

## 3. Endpoint /api/status

Verificación del endpoint en el navegador.

**URL:** `http://localhost:3000/api/status`

![Endpoint /api/status](./assets/Captura%20desde%202026-06-18%2017-57-14.png)

Respuesta JSON devuelta por el servidor:

```json
{
  "service": "NestJS API",
  "status": "running",
  "timestamp": "2026-06-18T22:32:53.495Z"
}
```

---

## 4. Estructura del módulo status

Listado de archivos dentro de `src/status/`.

```bash
ls ./src/status/
```

![Estructura del módulo status](./assets/Captura%20desde%202026-06-18%2018-02-08.png)

| Archivo | Descripción |
|---|---|
| `status.controller.ts` | Define la ruta `GET /api/status` |
| `status.controller.spec.ts` | Pruebas unitarias del controlador |
| `status.module.ts` | Módulo que agrupa el controlador |

---

## 5. Reflexión del estudiante

### `@Controller` y `@Get`

`@Controller('api/status')` es un decorador que le indica a NestJS que la clase manejará peticiones HTTP bajo el prefijo `/api/status`. Dentro de esa clase, `@Get()` marca un método para responder a peticiones `GET` en esa ruta. La combinación de ambos define el endpoint completo sin necesidad de registrar rutas manualmente como en Express.

### Módulos en NestJS

Un módulo (`@Module`) es la unidad de organización de la aplicación. Cada módulo declara sus controladores y proveedores, y puede importarse desde otros módulos. El módulo raíz `AppModule` importa `StatusModule`, lo que le permite a NestJS descubrir y registrar automáticamente el `StatusController` y sus rutas al iniciar la aplicación.

### Cómo funciona el servidor NestJS

Al ejecutar `pnpm start`, NestJS construye un grafo de dependencias a partir de los módulos registrados en `AppModule`. Luego levanta un servidor HTTP (por defecto sobre Express) que escucha en el puerto 3000. Cada petición entrante es enrutada al controlador correspondiente según el método HTTP y la ruta declarada con los decoradores.

### Similitudes con Spring Boot

NestJS tiene una correspondencia directa con Spring Boot que facilita su comprensión:

| Spring Boot | NestJS | Función |
|---|---|---|
| `@RestController` | `@Controller` | Declara un controlador HTTP |
| `@GetMapping` | `@Get` | Mapea un método a `GET` |
| `@SpringBootApplication` | `AppModule` | Punto de entrada y configuración raíz |
| `@Component` / `@Service` | `@Injectable` | Inyección de dependencias |
| Módulo Maven/Gradle | Módulo NestJS | Agrupación de componentes |

La principal diferencia es el lenguaje (TypeScript vs Java) y que NestJS usa decoradores de ES en lugar de anotaciones de Java, pero el patrón arquitectónico de controladores, servicios y módulos es prácticamente idéntico.

---

## Instalación y ejecución

```bash
# Instalar dependencias
pnpm install

# Modo desarrollo (con recarga automática)
pnpm start:dev

# Modo estándar
pnpm start
```

---

## Tecnologías utilizadas

- Node.js v24.15.0
- NestJS v11
- TypeScript v5.7
- pnpm
