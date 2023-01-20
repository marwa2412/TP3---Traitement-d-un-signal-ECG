# TP3-Traitemen d'un signal ECG

## Objectifs

    1. Suppression du bruit autour du signal produit par un électrocardiographe.

    2. Recherche de la fréquence cardiaque. 
  
## Introduction

    Un électrocardiogramme (ECG) est une représentation graphique de l’activation électrique du cœur à l’aide d’un électrocardiographe.Cette activité est recueillie 
    sur un patient allongé, au repos, par des électrodes posées à la surface de la peau. L’analyse du signal ECG est utile dans le but de diagnostiquer des anomalies 
    cardiaques telles qu’une arythmie, un risque d’infarctus, de maladie cardiaque cardiovasculaire ou encore extracardiaque.

## Réalisation du TP
  ### Partie 1 : Suppression du bruit provoqué par les mouvements du corps
  
        1.1. Chargement du signal à l'aide de la commande **load**
        
        1.2. Traçage du signal dasn le domaine temporel
        
        1.3. Filtrage passe-haut pour supprimer les bruits à très basses fréquences
        
             * Le processus de suppression des bruits à basse fréquence dans un signal ECG:
             
                1.Calcul de la Transformée de Fourier Discrète (TFD) du signal ECG: La TFD est une technique mathématique qui permet de décomposer un signal 
                  temporel en une somme de signaux sinusoïdaux de différentes fréquences, amplitudes et phases. Cette technique est largement utilisée pour 
                  l'analyse spectrale des signaux.
                  
                2.Réglage des fréquences inférieures à 50Hz à zéro: Une fois la TFD calculée, on peut accéder au domaine fréquentiel du signal. Les fréquences 
                  inférieures à 50Hz sont considérées comme des bruits dus aux mouvements du corps, il faut donc les régler à zéro pour les supprimer.
                  
                3.Effectuer une Transformée de Fourier Inverse Discrète (TFDI) : La TFDI est l'opération inverse de la TFD, elle permet de retransformer le 
                signal filtré dans le domaine temporel. En effectuant cette opération, on obtient un signal ECG où les bruits à basse fréquence ont été supprimés.
                
        1.4. Traçage du signal filtré
#### Script partie 1
<img width="893" alt="1" src="https://user-images.githubusercontent.com/86896531/213721522-640af052-0816-4d01-8d97-7968a69e7e16.png">
<img width="893" alt="2" src="https://user-images.githubusercontent.com/86896531/213721556-6f3c6db8-00d1-4882-b346-450e6efb3597.png"> 

#### Commentaire du script

        Ce code permet de charger un fichier "ecg.mat" contenant un signal ECG, puis d'afficher cette signal dans un graphique. Il effectue également une 
        analyse fréquentielle du signal en utilisant la Transformée de Fourier (FFT), qui est utilisée pour décomposer le signal en une somme de signaux 
        sinusoïdaux de différentes fréquences, amplitudes et phases.

        Les lignes suivantes permettent de définir la fréquence d'échantillonage "fe" et la période d'échantillonage "te" ainsi que le nombre d'échantillons 
        "N" pour le signal ECG. Il est utilisé pour définir le temps "t" en utilisant "t=0:te:(N-1)*te;".

        Ensuite, il utilise la commande "subplot" pour diviser la figure en deux lignes et deux colonnes, et affiche le signal ECG dans la première sous-figure. 
        Il affiche également le spectre du signal ECG dans la deuxième sous-figure en utilisant la commande "plot" et les étiquettes d'axe appropriées.

        Puis, il utilise un filtre passe-haut idéal pour supprimer les fréquences inférieures à 0.5 Hz. Il définit le filtre en mettant à zéro tous les éléments 
        de l'indice inférieur à "indexe_fc" et supérieur à "N-indexe_fc+1". Il multiplie ensuite le filtre par le spectre du signal ECG pour obtenir le spectre 
        filtré, puis il utilise la Transformée de Fourier inverse (IFFT) pour retransformer le signal filtré dans le domaine temporel. Il affiche finalement le 
        signal ECG filtré dans la troisième sous-figure en utilisant la commande "plot" et les étiquettes d'axe appropriées.
 ### Partie 2 : Suppression des interférences des lignes électriques 50Hz
  
      Souvent, l'ECG est contaminé par un bruit du secteur 50 Hz qui doit être supprimé.
      
        2.1. Filtre Notch
        
            * Un filtre notch est un type de filtre passe-bande qui est utilisé pour supprimer une bande étroite de fréquences spécifiques dans un signal. Il est
            également appelé filtre réjecteur de bande ou filtre passe-coupe. Un filtre notch est généralement constitué d'un circuit électronique qui combine un 
            filtre passe-bas et un filtre passe-haut. Le filtre passe-bas bloque les fréquences inférieures à la fréquence cible, tandis que le filtre passe-haut 
            bloque les fréquences supérieures à la fréquence cible. En combinant ces deux filtres, on obtient une bande de fréquences qui est bloquée, ce qui permet
            de supprimer efficacement les interférences électromagnétiques ou les bruits de ligne.
            
        2.2. Traçage du signal filtré
  #### Script partie 2
  <img width="893" alt="3" src="https://user-images.githubusercontent.com/86896531/213724403-0dc4c6ae-ffd5-4ba5-a519-89de3d7e6c98.png">
  
  #### Commentaire du script
  
          Ce code permet de charger un fichier "ecg.mat" contenant un signal ECG, puis d'afficher cette signal dans un graphique. Il effectue également une analyse 
          fréquentielle du signal en utilisant la Transformée de Fourier (FFT), qui est utilisée pour décomposer le signal en une somme de signaux sinusoïdaux de 
          différentes fréquences, amplitudes et phases.

          Il définit d'abord la fréquence d'échantillonage "fe" et la période d'échantillonage "te" ainsi que le nombre d'échantillons "N" pour le signal ECG. 
          Il est utilisé pour définir le temps "t" en utilisant "t=0:te:(N-1)*te;".

          Il utilise un filtre passe-haut idéal pour supprimer les fréquences inférieures à 0.5 Hz. Il définit le filtre en mettant à zéro tous les éléments 
          de l'indice inférieur à "indexe_fc" et supérieur à "N-indexe_fc+1". Il multiplie ensuite le filtre par le spectre du signal ECG pour obtenir le spectre
          filtré, puis il utilise la Transformée de Fourier inverse

  ### Partie 3 : Amélioration du rapport signal sur bruit
  
      Le signal ECG est également atteint par des parasites en provenance de l’activité musculaire extracardiaque du patient. La quantité de bruit est proportionnelle 
      à la largeur de bande du signal ECG. Une bande passante élevée donnera plus de bruit dans les signaux, et limiter la bande passante peut enlever des détails
      importants dusignal. 
      
        3.1. Fréquence de coupure
        
            * La fréquence de coupure est le paramètre qui définit le point où un filtre passe-bas ou passe-haut commence à réduire significativement l'amplitude des 
            fréquences de signal. C'est la fréquence à laquelle le filtre commence à "couper" les fréquences.
            
            * Pour un filtre passe-bas, la fréquence de coupure est la fréquence à laquelle les fréquences inférieures sont transmises avec une amplitude
            relativement élevée et les fréquences supérieures sont atténuées. Pour un filtre passe-haut, c'est l'inverse, les fréquences supérieures sont transmises avec une
            amplitude relativement élevée et les fréquences inférieures sont atténuées.
            
            * Il est important de noter que la fréquence de coupure n'est pas une fréquence unique, mais plutôt une plage de fréquences où la transition entre les 
            fréquences coupées et les fréquences transmises se produit. La largeur de cette plage dépend de la forme du filtre utilisé et est généralement exprimée 
            en termes de bande passante.
            
        3.2. Signal filtré
  #### Script partie 3
  <img width="893" alt="4" src="https://user-images.githubusercontent.com/86896531/213729820-742a7d45-66d3-408b-b9b1-12d579462bea.png">
  
  #### Commentaire du script  
  
          Ce code permet de charger un fichier "ecg.mat" contenant un signal ECG, puis d'afficher cette signal dans un graphique. Il effectue également une 
          analyse fréquentielle du signal en utilisant la Transformée de Fourier (FFT), qui est utilisée pour décomposer le signal en une somme de signaux 
          sinusoïdaux de différentes fréquences, amplitudes et phases.
      
          Il définit d'abord la fréquence d'échantillonage "fe" et la période d'échantillonage "te" ainsi que le nombre d'échantillons "N" pour le signal ECG.
          Il est utilisé pour définir le temps "t" en utilisant "t=0:te:(N-1)*te;".
          
          Il utilise un filtre passe-haut idéal pour supprimer les fréquences inférieures à 0.5 Hz. Il définit le filtre en mettant à zéro tous les éléments de 
          l'indice inférieur à "indexe_fc" et supérieur à "N-indexe_fc+1". Il multiplie ensuite le filtre par le spectre du signal ECG pour obtenir le spectre 
          filtré, puis il utilise la Transformée de Fourier inverse (IFFT) pour retransformer le signal filtré dans le domaine temporel.

          Il utilise ensuite un filtre notch idéal pour supprimer une bande étroite de fréquences spécifiques dans le signal filtré précédemment. Il définit le 
          filtre en mettant à zéro tous les éléments de l'indice "indexe_fc" et "N-indexe_fc+1". Il multiplie ensuite le filtre par le spectre du signal ECG pour
          obtenir le spectre filtré de nouveau, puis il utilise la Transformée de Fourier inverse (IFFT) pour retransformer le signal fil.
  ### Partie 4 : Identification de la fréquence cardiaque avec la fonction d’autocorrélation
  
      La fréquence cardiaque peut être identifiée à partir de la fonction d'autocorrélation du signal ECG. Cela se fait en cherchant le premier maximum local 
      après le maximum global (à tau = 0) de cette fonction.
      
        4.1. Calculer l’autocorrélation du signal ECG
        
            * L'autocorrélation d'un signal ECG est une technique utilisée pour mesurer la similarité entre des parties du signal à des décalages temporels différents. 
            Elle permet de déterminer si le signal contient des motifs répétitifs à des intervalles de temps spécifiques.
            
            * L'autocorrélation d'un signal ECG est utilisée pour détecter les ondes R et T, qui sont des motifs répétitifs caractéristiques du signal ECG. Elle est 
            également utilisée pour détecter les fréquences cardiaques et les instabilités cardiaques. Cependant, il est important de noter que l'autocorrélation n'est 
            pas la seule méthode utilisée pour l'analyse du signal ECG et qu'il peut y avoir des limites à son utilisation en fonction des conditions expérimentales ou 
            des caractéristiques du signal ECG.
            
  #### Script partie 4
<img width="893" alt="5 " src="https://user-images.githubusercontent.com/86896531/213730442-d20954aa-90c2-44b7-9588-2d4811c65304.png">
<img width="893" alt="6" src="https://user-images.githubusercontent.com/86896531/213730471-a3c44c32-aa60-4245-b3d5-14a52845b10c.png">

  #### Commentaire du script 
  
          Ces deux lignes de code calculent et affichent l'autocorrélation du signal filtré tmp_ecg3_filre. La fonction "xcorr" calcule l'autocorrélation du signal 
          en utilisant les séries de temps tmp_ecg3_filre et tmp_ecg3_filre, et retourne deux variables: "c" qui contient les valeurs de l'autocorrélation et "lags"
          qui contient les décalages temporels associés aux valeurs d'autocorrélation.
          
          La fonction "stem" est utilisée pour afficher les valeurs de l'autocorrélation en utilisant un diagramme à tiges. Les valeurs de décalages temporels sont 
          divisées par la fréquence d'échantillonnage pour les convertir en unités de temps et sont utilisées comme abscisses pour le diagramme. Les valeurs de 
          l'autocorrélation sont utilisées comme ordonnées pour le diagramme.
          
          En utilisant ces deux lignes, on peut visualiser la similarité temporelle du signal tmp_ecg3_filre par rapport à lui-même en différents décalages 
          temporels. Cela peut aider à identifier des motifs récurrents ou des tendances dans le signal.
## Conclusion

          Les manipulations faites permettent de traiter un signal ECG en utilisant des techniques de filtrage fréquentiel pour supprimer les bruits 
          indésirables. Il utilise d'abord un filtre passe-haut idéal pour supprimer les fréquences inférieures à 0.5 Hz, puis utilise un filtre notch idéal pour 
          supprimer une bande étroite de fréquences spécifiques dans le signal, et enfin utilise un filtre passe-bas idéal pour supprimer les fréquences supérieures 
          à 20 Hz.

          Il utilise également la Transformée de Fourier (FFT) pour analyser le signal ECG dans le domaine fréquentiel et la Transformée de Fourier inverse (IFFT) 
          pour retransformer le signal filtré dans le domaine temporel. Il utilise également l'autocorrélation pour visualiser la similarité temporelle du signal 
          filtré par rapport à lui-même.

          En utilisant ces techniques, on peut améliorer la qualité du signal ECG en supprimant les bruits indésirables tels que les mouvements corporels et les 
          interférences électriques, ce qui facilite la détection et l'analyse des caractéristiques du signal ECG.




