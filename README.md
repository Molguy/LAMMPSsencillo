# Instalar LAMMPS de forma sencilla en WSL
Veremos como compilar e instalar LAMMPS en WSL de una forma sencilla y justa para quien este aplicando para un curso o replicando un experimento y apenas se este familiarizando con su uso en linux (Ubuntu) en windows 11

# **Paso 1.**
Descarga LAMMPS desde su pagina de github (debido a que siempre se encontrara la version mas estable)

    https://github.com/lammps/lammps

hay que bucar el boton verde **"[<> Code]"** y desplegarlo para dar click en *Download ZIP,*

# **Paso 2.**
Abra el archivo recien descargado y deposite el folder a su ruta local desde el _Explorador de archivos_ 

    \\wsl.localhost\Ubuntuversion*\home\username*\

renombre el folder _lammps-develop_ a solo *lammps*

# **Paso 3.**
Abrimos el folder que renombramos y en un espacio en blanco donde el puntero no le de sombra a algun folder o archivo, presionamos shift + click derecho y presionar **L** para seleccionar _Abrir shell de Linux aqui_ 

# **Paso 4.**
En la terminal acederemos, y compilaremos las herramientas de lammps de forma manual

    cd ~/lammps/build

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
    
     make -j$(nproc)

     sudo make install

     ls /usr/local/lammps/bin/lmp*

     echo 'export PATH=/usr/local/lammps/bin:$PATH' >> ~/.bashrc

     source ~/.bashrc

