import sys
import math

#Pour afficher des erreurs :
# print("bonne direction tempo = "+str(tempo), file=sys.stderr)

# nb_floors: number of floors
# width: width of the area
# nb_rounds: maximum number of rounds
# exit_floor: floor on which the exit is found
# exit_pos: position of the exit on its floor
# nb_total_clones: number of generated clones
# nb_additional_elevators: ignore (always zero)
# nb_elevators: number of elevators

#on instancie un dictionnaire qui contiendra l'étage et la position des elevateurs
dico_elevateur={}

nb_floors, width, nb_rounds, exit_floor, exit_pos, nb_total_clones, nb_additional_elevators, nb_elevators = [int(i) for i in input().split()]
for i in range(nb_elevators):
    # elevator_floor: floor on which this elevator is found
    # elevator_pos: position of the elevator on its floor
    elevator_floor, elevator_pos = [int(j) for j in input().split()]

    #on rempli le dictionnaire avec KEY=etage: VALUE=position des elevateurs
    dico_elevateur[elevator_floor]=elevator_pos

#Retourne True si le clone va dans la bonne direction ou False dans la mauvaise direction.
# Params : 
#       Name : clone_floor
#       Type : int
#       Desc : La position du clone courant
#
#       Name : objectif
#       Type : String
#       Value: elevator ou exit
#       Desc : Objectif recherché par le clone dans le niveau courant, la sortie ou un elevateur
def direction_clone(clone_floor,objectif) :
    direction_first_clone = False
    obj = ""
    try :
        if objectif == "elevator" :
            obj = dico_elevateur[clone_floor]
        elif objectif == "exit" :
            obj = exit_pos

        if clone_pos-obj < 0 and direction == "RIGHT" :
            direction_first_clone = True
        elif clone_pos-obj < 0 and direction == "LEFT" :
            direction_first_clone = False
        elif clone_pos-obj > 0 and direction == "RIGHT" :
            direction_first_clone = False
        elif clone_pos-obj > 0 and direction == "LEFT" :
            direction_first_clone = True
        return direction_first_clone
    except :
        return None

#variable qui permet de temporiser le passage de l'elevateur et la mauvaise direction
tempo=0

# game loop
while True:
    inputs = input().split()
    clone_floor = int(inputs[0])  # floor of the leading clone
    clone_pos = int(inputs[1])  # position of the leading clone on its floor
    direction = inputs[2]  # direction of the leading clone: LEFT or RIGHT
    
    #On vérifie que le clone n'est pas sur un des bords de la map sinon on le bloque
    if clone_pos == width-1 or clone_pos == 0 :
        tempo=0
        print("BLOCK")
    else :
        if nb_elevators > 0:
            if clone_floor != nb_floors-1 :
                if direction_clone(clone_floor,"elevator") == False :
                    if tempo < 2 :
                        tempo += 1
                        print("WAIT")
                    elif tempo == 2 :
                        tempo = 0
                        print("BLOCK")
                elif direction_clone(clone_floor,"elevator") == True :
                    if tempo==2: 
                        tempo=0
                    print("WAIT")
            elif clone_floor == exit_floor :
                direct_final = direction_clone(clone_floor,"exit")
                if direct_final == False :
                    print("BLOCK")
                elif direct_final == True :
                    print("WAIT")
            else :
                if tempo==2:
                    tempo=0
                print("WAIT")  
        else:
            if tempo==2:
                tempo=0
            print("WAIT")
