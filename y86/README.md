# Preparando el simulador

Bajen el simulador de [nuestro moodle](https://online.uprrp.edu/mod/resource/view.php?id=4535161). Deben tener un archivo `sim.tar` en su carpeta Downloads.

Copien `sim.tar` de su computadora a ada. Pueden usar scp en un terminal:
```
scp Downloads/sim.tar user.name@ada.uprrp.edu:
```
ahora conectense a ada y descompriman el tar:
```
ssh user.name@ada.uprrp.edu

tar xf sim.tar
```

Esto crea una carpeta `sim`, con varias carpetas adentro: `misc`, `seq`, `pipe` ...

Cambiense a sim y compilen el simulador:
```
cd sim
make
```

Cuando terminen, deben tener dos ejecutables `~/sim/misc/yas` y `~/sim/misc/yis`

# Corriendo el simulador

Vimos en clase como correr el simulador de Y86_64:

```
$ ~/sim/misc/yas suma.ys
$ ~/sim/misc/yis suma.yo
Stopped in 33 steps at PC = 0x13.  Status 'HLT', CC Z=1 S=0 O=0
Changes to registers:
%rax:	0x0000000000000000	0xabcdabcdabcdabcd
%rsp:	0x0000000000000000	0x0000000000000100
%rdi:	0x0000000000000000	0x0000000000000038
%r8:	0x0000000000000000	0x0000000000000001
%r9:	0x0000000000000000	0x0000000000000008

Changes to memory:
0x00f0:	0x0000000000000000	0x0000000000000053
0x00f8:	0x0000000000000000	0x0000000000000013
```

Modifiquen el programa en `len.ys` o `suma.ys` para que calcule el maximo de un
arreglo. Por ejemplo, usando el mismo arreglo de cuatro elementos:

```
array:
        .quad 0x000d000d000d000d
        .quad 0x00c000c000c000c0
        .quad 0x0b000b000b000b00
        .quad 0xa000a000a000a000
        .quad 0
```

el maximo debe ser 0x0b000b000b000b00 (porque 0xa000a000a000a000 es negativo en
2's complement).
