# Kolsor-Server enpoints

## HTTP

### Login
`/api/login`
Recive `username: string` y `password: string`
Devuelve en caso correcto `token: string | jwt` y `user: string` en caso negativo `error: string`

### Register
`/api/register`
Recive `username: string` y `password: string`
Devuelve en caso correcto `id: string` en caso negativo `error: string`

## WS

### Ping
Comando que se llama de forma periodica desde el cliente
Servidor responde con el timestamp en el que lo recibio

### Auth (Deprecated)
Autentica el usuario mandando el jwt desde el cliente
Ahora la conexion inicial requiere la cookie con el jwt, por lo que auth no es necesario

> [!NOTE]  
> Ahora mismo la conexion permite uso no autenticado, pero esto cambiara

### Connection
Settea el intervalo de pings para un cliente especifico
Se llama automaticamente al establecer conexion, replica `connection` del servidor ws en si

### Matchmaking-search
Evento enviado desde el cliente

Busca salas existentes que tengan un hueco libre, si ninguna se encuentra crea una nueva
Al terminar la asignacion manda el evento `matchmaking-join` con el id de la sala

### Matchmaking-join
Devuelve al cliente la id de la sala encontrada

### Matchmaking-private (No implementado)
Permite crear/unirse a una sala directamente, si no se proporciona codigo o el codigo introducido no existe se crea una sala
Devuelve la id y el codigo de la sala, las publicas el codigo coincide con la id de la sala, por lo que mediante esta llamada puedes unirte a una publica especifica
