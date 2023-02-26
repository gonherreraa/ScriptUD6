# Script Unidad 6

```bash

#!/bin/bash

funcion_instalar(){
   
    echo "Donde desea instalarlo"
    read directorio
    if [ -e $directorio ]
    then
        echo "$directorio El directorio ya existe"
    else 
        mkdir $directorio
    fi
    echo "Nombre de usuario"
    read nombreUsuario
    useradd $nombreUsuario
    echo "Nombre del grupo"
    read nombreGrupo
    groupadd $nombreGrupo
    usermod -a -G $nombreGrupo $nombreUsuario
    chown $nombreUsuario:$nombreGrupo $directorio
    chmod 777 $directorio
    cp actividadUD6.sh $directorio
    cp pizarra.java $directorio
    test -h /usr/bin/java 
    if [ $? -eq 1 ]
    then
        echo "Instalando java..."
        apt install default-jre
    fi

    echo "INFORME:"
    echo "Directorio creado"
    echo "Usuario: $nombreUsuario"
    echo "Grupo: $nombreGrupo"
    echo "Permisos dados"
    echo "Java comprobado"


}

funcion_ejecutar(){

    echo "introduce un archivo"
    read archivo
    test -f $archivo
    if [ $? -eq 1 ]
    then
        nano $archivo
    fi
    echo "Elige el color R, Y, G"
    read color
    java $directorio pizarra.java $archivo $color
    
}


funcion_desinstalar(){
    
    echo "Esta seguro de que quiere desinstalarlo [y/n]"
    read respuesta
    if [ $respuesta == 'y' ]
    then
        echo "Desinstalando.."
    else
        exit
    fi
    echo "Escriba el directorio donde tienes el archivo"
    read direct
    rm -r $direct
    echo "Desinstalacion completada"
}

case "$1" in


    'instalar')


        funcion_instalar
        ;;


    'desinstalar')
       
        funcion_desinstalar
        ;;
    'ejecutar')


        funcion_ejecutar
        ;;
    *)
        echo "Opcion no valida"
        echo "Introduce una de estas tres opciones:
            -instalar
            -desinstalar
            -ejecutar"
        ;;
esac
```