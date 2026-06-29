Projet ros2_drone_ws - Description des packages (**ROS HUMBLE**)

drone_msgs
Définit le message custom DroneState utilisé par tous les autres packages : pose, vitesse, accélération, force et couple en un seul message horodaté.

drone_description
Contient la description physique du drone (URDF/Xacro) — géométrie quadrirotor, caméra perspective orientée vers le bas — et le monde Gazebo : sol, sphère rouge cible, pylônes de repère.

drone_dynamics
Plugin C++ embarqué dans Gazebo. À chaque step de simulation, il applique les forces/couples reçus au corps du drone et publie l'état complet (pose, vitesse, accélération, force, couple) sur /drone/state.

drone_trajectory
Génère les consignes de vol. Machine d'états simple (décollage → stabilisation → cercle) qui publie sur /drone/reference la position, vitesse et accélération désirées à chaque instant.

drone_control
Contrôleur PD découplé de la trajectoire. Lit l'état courant et la consigne, calcule les forces et couples nécessaires (avec compensation de gravité et feedforward), et les publie sur /drone/cmd_wrench.

drone_plotting
Visualisation et perception. Affiche en temps réel 9 graphes (position, vitesse, accélération, force, couple, trajectoire 3D, pixels). Détecte la sphère rouge dans l'image caméra via OpenCV et publie ses coordonnées pixel sur /drone/pixel_coords.

drone_bringup
Point d'entrée unique du projet. Contient le launch file qui orchestre le démarrage de tous les composants avec les bons délais, et le fichier params.yaml centralisant tous les paramètres réglables.

