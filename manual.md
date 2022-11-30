# Manual de packet tracer

**Equipo `Switch`**

### Entrar en modo EXEC privilegiado

Ejecutar el comando `enable`

```cpp
Switch> enable
Swtich#
```

### Examinar la configuración actual del switch

Ejecutar el comando `show running-config`

```cpp
Switch> show running-config
```

### Asignar un nombre al switch

Ejecutar los comandos `configure terminal`, una vez dentro del módulo de configuración ingresar el comando `hostname` seguido del nombre asignado al switch, una vez asignado al nombre ejecutar `exit` para salir del módulo de configuración del terminal.

```cpp
Switch# configure terminal
Switch(config)# hostname SW-CORE
SW-CORE(config)# exit
SW-CORE>
```

### Proporcionar acceso seguro al modo privilegiado

Establecer una contraseña al modo privilegiado, entrar a la configuración del terminal ingresando `configure terminal`, ejecutar `enable secret o password` seguido de la contraseña a utilizar, salir de la configuración con `exit`

```cpp
SW-CORE> enable
SW-CORE# configure terminal
SW-CORE(config)# enable secret g4rc&a
SW-CORE(config)# exit
S1#
```

**Configurar mensaje del día `MOTD`**

```cpp
SW-CORE> enable
SW-CORE# configure terminal
SW-CORE(config)# banner motd "Message of the day"
SW-CORE(config)# exit
SW-CORE#
```

**Guardar los cambios de la configuración en la NVRAM**

```cpp
SW-CORE> enable
SW-CORE# copy running-configuration starup-configuration
```

**Equipo `Router`**

**Asignar direcciones IP**

```cpp
R1> enable
R1# configure terminal
R1(config)# interface GigabitEthernet0/0 #o la interface a configurar
R1(config-if)#ip address 172.31.1.1 255.255.255.240
R1(config-if)#no shutdown
```

**Habilitar VTY Line para Acceso vía `Telnet` [Router]**

```cpp
Router(config)# line vty 0 4
Router(config-line)# login
Router(config-line)# password p4ssw0rd
Router(config-line)# exit
```

**Habilitar VTY Line para Acceso vía `Telnet` [Switch]**

```cpp
Swtich(config)# line vty 0 15
Swtich(config-line)# login
Swtich(config-line)# password p4ssw0rd
Swtich(config-line)# exit
```

**Interface vlan en un Switch**

```cpp
S3# configure terminal
S3(config)# interface Vlan1
S3(config-if)#ip address 172.31.1.34 255.255.255.240
S3(config-if)#no shutdown
S3(config)#ip default-gateway 172.31.1.33
```

**Configuración `SSH`**

### Pasos para configurar ssh en routers/swtiches

1.- Dominio ejemplo: `ejemplo.com` 2.- Establecer longitud mínima de 7 caracteres para las contraseñas 3.- Clave MD5 `enable secret Garcia123` 4.- Crear usuario, el cual será el `ejemplo.com`, con clave `samgarcia`. 5.- Utilizar llave RSA de 2048 bits, donde el acceso remoto debe ser en la terminal virtual para (3 sesiones). 6.- Mejorar el SSH, utilizando la versión 2, establecer un máximo de 3 reintentos, y un tiempo de espera de 30 segundos.

```cpp
R1(config)#ip domain-name ejemplo.com
R1(config)#service password-encryption
R1(config)#security passwords min-length 7
R1(config)#enable secret Garcia123
```

```cpp
R1(config)# username sam secret garcia
R1(config)# crypto key generate rsa modulus 2048
R1(config)# ip ssh time-out 30
R1(config)# ip ssh authentication-retries 3
R1(config)# ip ssh version 2
```

```cpp
R1(config)# line vty 0 5
R1(config-if)# transport input ssh
R1(config-if)# login local
R1(config)# exit
```