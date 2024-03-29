# Autonomiczne Roboty Latające: projekt
Cezary Wawrzyniak 141131, Jakub Sieklucki 140310, Jakub Marciniak 140278

## Założenia projektu  
Projekt zakładał sterowanie lotem dronów z użyciem markerów aruco. 
Markery byłyby umieszczone na ziemi niestety z powodu kąta widzenia kamery musiało to zostać zmienione na pionowe mocowanie. 

## Zadania wykonane
Dron w symulacji porusza się w zadanej kolejnośći pomiędzy wyznaczonymi markerami aruco które wcześniej widział.


## Jak użyć paczki
Należy skożystać z paczki tello_ros (https://github.com/clydemcqueen/tello_ros) i postąpić z jej tutorialem
a następnie sklonować tę paczkę do katalogu src. Całość została uruchomiona w Dockerze, który także powstał według instrukcji z tello_ros.


## Działanie
Dron za pomocą paczki ros2_arcuo dron wykrywa markery aruco i jest w stanie odczytać ich pozycję.  
Paczka g2r_tf_package zamienia dane z G2RRa na tfa. 
Sterowanie odbywa się za pomocą controler_node'a z paczki tello_controller z użyciem kontorlera PID. 
W niej zapisane jest całe sterowanie dronem

![Dron_goes_BRR](https://user-images.githubusercontent.com/80836780/214312763-63d8d503-a1b0-4505-b3c3-7c2f42312d47.gif)

Do uruchomnienia różnych misji w wybranych środowiskach służą dopowiednie pliki launch.
real_launch.py posiada parametry do laboratorium.

Zaprogramowane są 2 misje. Pierwsza z nich uruchamia latanie po trajektorii kwadratu w celu sprawdzenia poprawności działania, a druga odpowiada za latanie pomiędzy markerami Aruco. W plikach launch znajduje się parametr dyktujący czy uruchomiona zostanie tylko pierwsza misja czy całość.



Parametry:
'follow_markers' lista markerów do odwiedzenia  
'drone_topic' topic tello_action
'aruco_topic' topic na którym publikowane są paramtery widzianych aruco  
'position_topic' topic zwracający pozycję (G2RR lub optitrack)  
'second_mission' zmienna 1/0 czy dron ma wykonać drugą misję  
'dev_in_simulation' zmienna 1/0 czy uruchomienie odbywa się w symulacji  


Do uruchomienie symulacji należy:  
1. Uruchomić skrypty start_tello w katalaogu vm_scripts
2. Włączyć G2RR poleceniem ```ros2 run pkg_g2rr g2rr tello_1 ```
3. Uruchomić launcha wchodząc w folder ```tello_controller/launch``` a następnie ```ros2 launch <nazwa launcha>```

![Drone_goes_BRRRR](https://user-images.githubusercontent.com/80836780/214314146-0d52bc7b-6ce6-48a4-8c8f-d90281ab3dc3.gif)

![Drone_goes_BRRRRRR](https://user-images.githubusercontent.com/80836780/214315608-816f0503-9ed1-4b3c-9d14-6c07749dff2d.gif)

Implementacja sterowania dwoma dronami musiała korzystać bezpośrednio z danych pobieranych z kamery ze względu na problemy śledzenia pozycji dwóch jednostek.

![2_Drones_goes_BRR](https://user-images.githubusercontent.com/80836780/214315813-814aed4c-c7f6-4f30-9831-48c51d6bbd7b.gif)

![Drone_goes_BRRRRRRRR](https://user-images.githubusercontent.com/80836780/214401901-26fb3bcc-a1d2-4f25-a639-aa4947aff163.gif)

![Drone_goes_BRRRRRRRRRR](https://user-images.githubusercontent.com/80836780/214401911-49de9de9-726a-4328-b499-f08aea6962e1.gif)

![Huj_robi_reconesans](https://user-images.githubusercontent.com/80836780/214407703-2c7b2742-95f7-4359-bb54-9bf66765ecd5.gif)

![Drone_goes_BRRRRRRRRRRRR](https://user-images.githubusercontent.com/80836780/214411812-c24e581e-b53d-4f0d-8e6d-a602cc91dfba.gif)



Uruchomienie z prawdziwym dronem jest bardzo podobne:
1. Uruchomić teleopa
2. Połączyć się z optitrackiem
3. Uruchomić launcha wchodząc w folder ```tello_controller/launch``` a następnie ```ros2 launch <nazwa launcha>```

Markery aruco zostały w większości wygenerowane samodzielnie.
Zostały również stworzone mapy do łatwiejszego odtworzenia ustawniena markerów w aruco.
![Map1](https://user-images.githubusercontent.com/80836780/214316930-7ff73b32-a685-42ea-91d5-53411110b861.png)

Założenie było aby wykorzystać tfy do ustalenia pozycji markerów oraz drona, jednak nie udało się tego pomysłu zintegrować.
![tfy](https://github.com/czarkoman/ARL_projekt/blob/main/misc/Screenshot_from_2023-01-10_21-17-32.png)

## Użyte paczki
Do sterowania dronem:  
https://github.com/clydemcqueen/tello_ros    
Już w repo  
https://github.com/JMU-ROBOTICS-VIVA/ros2_aruco

## Użyte pakiety:  
Python 3.8.10  
Numpy 1.17.4  
ROS2 Foxy  

