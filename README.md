# Android-Libjpeg-turbo-for-ARM_ABI-
Ceci est le résultat d'une compilation de la librarie libjpeg-turbo pour les architectures ARM_ABI pour un projet android.

# Repository of libjpeg-turbo:
https://github.com/openstf/android-libjpeg-turbo

# Dossier obj/local/
Contient les fichiers ".a" pour les architectures "armabi-v7a, arm64-v8a, x86, x86_64"

# Installation et mise en place de Libjpeg-turbo et Eigen
1- Copiez le dossier "obj/local" dans le projet android "app/src/main"

2- Ajouter ces lignes dans "app/CMakelists.txt":

        add_library(
            libjpeg STATIC IMPORTED
        )

        set_target_properties(libjpeg PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/obj/local/${ANDROID_ABI}/libjpeg-turbo.a)

        target_link_libraries(
            ........
            libjpeg
            ........
            )

3- Copiez le fichier "turbojpeg.h" dans le projet android "app/src/main/jni/include"

4- Copier le dossier "Eigen" dans "app/src/main/cpp"

5- Ajout cette ligne dans "app/CMakelists.txt":

        include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/Eigen)

6 - Editer le ficher "app/src/main/cpp/native_lib.cpp
        Ajouter les lignes suivantes:

        #include "Eigen/Dense"  /* Dense ici c'est pour l'exemple */

        #include "turbojpeg.h"

        Pour le test: 
            void multiply2Matrices(){
                Eigen::MatrixXd M(2,2);
                Eigen::MatrixXd V(2,2);
                /*for (int i = 0;  i<=1; i++){
                    for (int j = 0; j<=1; j++){
                        M(i,j) = 1;
                        V(i,j) = 2;
                    }
                }
                Eigen::MatrixXd Result = M*V; */
            }