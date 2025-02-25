##Solución correcta inicial

```mermaid
classDiagram

class Propietario {
    - nombre : string
    - telefono : string
    - vehiculos : List~VehiculoElectrico~

    + Propietario(nombre : string, telefono : string)
    + getNombre() : string
    + setNombre(nombre : string) : void
    + getTelefono() : string
    + setTelefono(telefono : string) : void
    + getVehiculos() : List~VehiculoElectrico~
    + setVehiculos(vehiculos : List~VehiculoElectrico~) : void
    + mostrarInfo() : void
}

class VehiculoElectrico {
    - marca : string
    - modelo : string
    - capacidadBateria : double

    + VehiculoElectrico(marca : string, modelo : string, capacidadBateria : double)
    + getMarca() : string
    + setMarca(marca : string) : void
    + getModelo() : string
    + setModelo(modelo : string) : void
    + getCapacidadBateria() : double
    + setCapacidadBateria(capacidadBateria : double) : void
    + iniciarRecarga() : void
}

class Recarga {
    - fechaHoraInicio : string
    - fechaHoraFin : string
    - costo : double
    - vehiculo : VehiculoElectrico

    + Recarga(fechaHoraInicio : string, fechaHoraFin : string, costo : double, vehiculo : VehiculoElectrico)
    + getFechaHoraInicio() : string
    + setFechaHoraInicio(fechaHoraInicio : string) : void
    + getFechaHoraFin() : string
    + setFechaHoraFin(fechaHoraFin : string) : void
    + getCosto() : double
    + setCosto(costo : double) : void
    + getVehiculo() : VehiculoElectrico
    + setVehiculo(vehiculo : VehiculoElectrico) : void
    + calcularDuracion() : double
    + generarFactura() : void
}

    %% Relaciones
    Propietario  o--  VehiculoElectrico : "tiene"
    VehiculoElectrico  -->  Recarga : "tiene"
```

# Solución con fallos.
1. los atributos de vehiculo electrico deberían ser privados
2. La flecha de propietario es de agregación y no necesita la de asociación
3. El método + registrarNuevoPropietario (): void en vehículo electrico no tiene funcionalidad por principio de responsabilidad y por las relaciones
4. la clase las_Recargas debería ser un nombre en singular y con mayúscula incial
5. En la clase Recarga deberían estar los get, y los set para los atributos de fecha
6. La clase VehiculoElectrico tiene un atributo de la misma clase y ello no tiene utilidad
7. El propietario tiene un atributo - recarga : List~Recarga~ pero realmente no hay una relación directa de agregación entre Propietario y Recarga
8. El constructor de VehiculoElectrico no se llama igual que la clase

```mermaid
classDiagram
  direction UD

class Propietario {
    - nombre : string
    - telefono : string
    - vehiculos : List~VehiculoElectrico~
    - recarga : List~Recarga~

    + Propietario(nombre : string, telefono : string)
    + getNombre() : string
    + setNombre(nombre : string) : void
    + getTelefono() : string
    + setTelefono(telefono : string) : void
    + getVehiculos() : List~VehiculoElectrico~
    + setVehiculos(vehiculos : List~VehiculoElectrico~) : void
    + mostrarInfo() : void
}

class VehiculoElectrico {
    + marca : string
    + modelo : string
    + capacidadBateria : double
    - vehiculo : VehiculoElectrico

    + Vehiculo(marca : string, modelo : string, capacidadBateria : double)
    + getMarca() : string
    + setMarca(marca : string) : void
    + getModelo() : string
    + setModelo(modelo : string) : void
    + getCapacidadBateria() : double
    + setCapacidadBateria(capacidadBateria : double) : void
    + registrarNuevoPropietario (): void
    + iniciarRecarga() : void
}

class las_Recargas {
    - fechaHoraInicio : string
    - fechaHoraFin : string
    - costo : double
    - vehiculo : VehiculoElectrico

    + Recarga(fechaHoraInicio : string, fechaHoraFin : string, costo : double, vehiculo : VehiculoElectrico)
    + getCosto() : double
    + setCosto(costo : double) : void
    + getVehiculo() : VehiculoElectrico
    + setVehiculo(vehiculo : VehiculoElectrico) : void
    + calcularDuracion() : double
    + generarFactura() : void
}

    %% Relaciones
    Propietario  o-->  VehiculoElectrico : "tiene"
    VehiculoElectrico  -->  las_Recargas : "tiene"
```

