# API REST Bancaria (MongoDB + TypeScript)

API REST para la gestión de clientes, cuentas corrientes/ahorro y movimientos bancarios implementada en TypeScript, Express y MongoDB.

## Requisitos Previos (Ubuntu)

- **Node.js**: v18 o superior
- **npm**: v9 o superior
- **MongoDB**: Instancia local instalada o servicio de MongoDB (v6.0+)

### Instalación de Node.js y MongoDB en Ubuntu

```bash
# Actualizar repositorios
sudo apt update

# Instalar Node.js y npm
sudo apt install -y nodejs npm

# Verificar versiones
node -v
npm -v

# Opción A: Instalar y arrancar MongoDB nativo en Ubuntu
sudo apt install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod

# Opción B (Alternativa): Arrancar MongoDB con Docker
docker run -d --name mongo-banco -p 27017:27017 mongo:latest
```

## Configuración e Instalación

1. **Clonar el repositorio e instalar dependencias:**
   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd banco-api
   npm install
   ```

2. **Configurar variables de entorno (`.env`):**
   ```bash
   cp .env.example .env
   ```
   *Edita `.env` si necesitas cambiar la cadena de conexión o el puerto.*

3. **Ejecución en modo desarrollo:**
   ```bash
   npm run dev
   ```

4. **Compilar y ejecutar en producción:**
   ```bash
   npm run build
   npm start
   ```

## Especificaciones y Reglas de Negocio Implementadas

- **Importes monetarios:** Todos los importes se gestionan obligatoriamente como números enteros en céntimos (`12,50 € = 1250`).
- **Control de IBAN:** Generación y validación automática del código IBAN español (24 caracteres) mediante el algoritmo Módulo 97 (ISO 13616).
- **Límites de Cuentas:** Máximo 3 cuentas activas o bloqueadas por cliente.
- **Límite Diario de Retiradas:** Límite máximo de 100.000 céntimos (1.000,00 €) en retiradas acumuladas por día natural.
- **Comisiones de Transferencia:** 0 % entre cuentas del mismo titular; 0,5 % (mínimo 100 céntimos, redondeado al alza) entre distintos titulares.

