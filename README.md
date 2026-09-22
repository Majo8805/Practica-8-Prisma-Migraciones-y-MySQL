# Gimnasio API — Código base (Semana 5)

API REST en NestJS para el gimnasio: `Clases`, `Horarios`, `Miembros` e `Inscripciones`, cada
módulo con dominio, DTOs e infraestructura separados (patrón repositorio + inyección por token).
Los datos viven en memoria — ningún repositorio se conecta todavía a una base de datos real.

Este proyecto es el punto de partida de la Práctica 8 (Prisma) y la Práctica 9 (Blindar la API).

## Cómo correrlo

```bash
npm install
npm run start:dev
```

El servidor levanta en `http://localhost:3000`. En `peticiones.http` está la batería completa de
pruebas (requiere la extensión "REST Client" de VS Code).

## Estructura

```
src/
  clases/        CRUD de clases del gimnasio
  horarios/      CRUD de horarios (día, hora, cupo, entrenador)
  miembros/      CRUD de miembros del gimnasio
  inscripciones/ inscribir a un miembro a un horario, con reglas de cupo y duplicados
  datos/         datos de arranque (seed) que usan Horarios y Miembros
```

Cada módulo sigue la misma forma: `dominio/` (entidades + interfaz del repositorio), `dto/`,
`infra/` (repositorio en memoria) y el token de inyección en `<módulo>.tokens.ts`.

Preguntas:
- ¿Por qué el paquete del adaptador se llama adapter-mariadb si usamos MySQL?
Por que MariaDB es un derivado directo de MySQL
- ¿Editar schema.prisma cambió algo en la base de datos antes de migrar?
No, por que el archivo schema.prisma es solo configuracion local en el codigo. La base de datos real no sufre ninguna cambio hasta que se ejecuta el comando de migracion
- ¿La carpeta de migraciones es una foto del esquema o un historial?
Es un historial
- ¿Por qué Horario.clase sí crea columna y Clase.horarios no?
Porque Horario es el lado que guarda la llave foranea y que tiene el atributo @relation
- ¿De dónde sale la relación de muchos a muchos entre Miembro y Horario, si nunca se declaró?
De el modelo Inscripcion