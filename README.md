# Instalar LAMMPS de forma sencilla en WSL
Veremos como compilar e instalar LAMMPS en WSL de una forma sencilla y justa para quien este aplicando para un curso o replicando un experimento y apenas se este familiarizando con su uso en linux (Ubuntu) en windows 11

# **Paso 1.**
Descarga LAMMPS desde su pagina de github (debido a que siempre se encontrara la version mas estable)

    https://github.com/lammps/lammps

hay que bucar el boton verde **"[<> Code]"** y desplegarlo para dar click en *Download ZIP,*

# **Paso 2.**
Abra el archivo recien descargado y deposite el folder a su ruta local desde el _Explorador de archivos_ 

    \\wsl.localhost\Ubuntuversion*\home\username*\

renombre el folder _"lammps-develop"_ a solo *"lammps"*

# **Paso 3.**
Abrimos el folder que renombramos y en un espacio en blanco donde el puntero no le de sombra a algun folder o archivo, presionamos shift + click derecho y presionar **L** para seleccionar _Abrir shell de Linux aqui_ 

# **Paso 4.**
En la terminal acederemos, y compilaremos las herramientas de lammps de forma manual.

1 El siguiente comando crea y te ubica en el folder "build"

    cd ~/lammps/build

2 Este comando hace que se use el codigo fuente de LAMMPS ubicado en un nivel anterior -cmake- para generar archivos de compilacion de distintos paquetes de LAMMPS
    
    cmake ../cmake -D BUILD_MPI=on -D BUILD_OMP=on -D LAMMPS_EXCEPTIONS=yes \
      -D CMAKE_INSTALL_PREFIX=/usr/local/lammps \
      -D LAMMPS_MACHINE=mpi -D LAMMPS_MACHINE=serial \
     -D PKG_KOKKOS=on \
     -D PKG_KSPACE=on \
     -D PKG_MOLFILE=on \
     -D PKG_MOLECULE=on \
     -D PKG_EXTRA-MOLECULE=on \
     -D PKG_RIGID=on \
     -D PKG_CLASS2=on \
     -D PKG_GRANULAR=on \
     -D PKG_PERI=on \
     -D PKG_MISC=on \
     -D PKG_BODY=on \
     -D PKG_MANYBODY=on \
     -D PKG_USER-OMP=on \
     -D PKG_USER-MISC=on \
     -D PKG_USER-MOLFILE=on \
     -D PKG_USER-MOLECULE=on \
     -D PKG_USER-REAXC=on \
     -D PKG_USER-OMP=on \
     -D PKG_USER-INTEL=on \
     -D PKG_USER-LB=on \
     -D PKG_USER-DIFFRACTION=on \
     -D PKG_USER-CGDNA=on \
     -D PKG_USER-VTK=on \
     -D PKG_USER-COLVARS=on

3 Ejecuta la compilacion en paralelo usando todos los nucleos del porcesador que esten disponibles
     
     make -j$(nproc)

4 Con permisos de administrador, copia los binarios y archivos necesarios al directorio para su instalacion 
     
     sudo make install

5 Verifica que el binario se haya instalado (lmp_mpi, lmap_serial, etc.)
     
     ls /usr/local/lammps/bin/lmp*

6 Añade la ruta de instalacion de LAMMPS al path en el archivo .bashrc, para que pueda ejecutar lmp desde cualquier carpeta de la terminal sin tener que escribir la ruta completa
     
     echo 'export PATH=/usr/local/lammps/bin:$PATH' >> ~/.bashrc

7 Actualiza cmabios hechos al archivo .bashrc en la terminal actual
     
     source ~/.bashrc


# **Listo**

Reinicie su equipo para aplicar cambios, para este punto LAMMPS ha sido instalado de forma personalizada pero con las utilerias suficientes para funcionar.
