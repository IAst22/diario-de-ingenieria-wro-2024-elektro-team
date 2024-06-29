Republica Bolivariana de Venezuela
28-06-2024







Diario de ingeniería Elektro 2024



















1. Gestión de movilidad
Nuestro vehículo se mueve gracias al uso de un motor DC trasero que sirve como tracción y su velocidad torque está al 60% de la capacidad del motor. En la parte delantera, tenemos un servomotor que actúa como dirección y cuando el sensor ultrasónico detecta un obstáculo el motor rota su eje entre 35°-80° dependiendo del sensor. Como fuente de poder utilizamos el modulador Nezha el cual suministra energía a los motores y sensores del vehículo
2. Gestión de energía y sensores
El modulo Nezha incluye una batería de litio de 900 mAh que suministra energía a la placa de microbit. También cuenta con 4 entradas para motores DC y servomotores. Nuestro vehículo está equipado con 4 sensores ultrasónicos: 3 en la parte de adelante y 1 en la parte de atrás. Además, contamos con una cámara, Smartai lens, la cual detecta colores. Todos estos dispositivos están conectados al modulador Nezha para que les suministre energía y puedan ser controlados por la tarjeta micro bit. Nosotros utilizamos los sensores ultrasónicos debido a que nos permiten ver los obstáculos de las paredes de la pista. Éstos se conectan mediante un puerto al Nezha y funcionan arrojando señales de sonido a las paredes cercanas, las cuales rebotan a una bocina que detecta la distancia del obstáculo en cuestión. La cámara funciona conectándose a un puerto Al encenderse la fuente de poder, la cámara se inicia, y cambia su función a detecta colores, entonces esta recibe una imagen del color que nosotros elegimos que detecte de su base de datos y realiza la función que le hemos asignado ya se un giro a la derecha o a la izquierda.
3. Gestión de obstáculos
Nuestra estrategia para evitar los obstáculos es el uso del sensor ultrasónico, ya que este nos ayuda al poder ver las paredes de la pista, también el uso de la cámara para las señales de tráfico al utilizar su modo de detección de color.
 
input.onButtonPressed(Button.A, function () {
    neZha.setMotorSpeed(neZha.MotorList.M1, -60)
})
este codigo le dice al motor dc que arranque hacia adelante
input.onButtonPressed(Button.B, function () {
    neZha.setMotorSpeed(neZha.MotorList.M1, 60)
    neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 130)
    basic.pause(2000)
    neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    neZha.setMotorSpeed(neZha.MotorList.M1, 0)
    basic.pause(500)
    neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 220)
    neZha.setMotorSpeed(neZha.MotorList.M1, -60)
    basic.pause(2200)
    neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    neZha.setMotorSpeed(neZha.MotorList.M1, -60)
})
este codigo le dice al motor que cambie su direccion y luego arranque
let d = 0
let c = 0
let b = 0
let a = 0
neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
PlanetX_AILens.initModule()
PlanetX_AILens.switchfunc(PlanetX_AILens.FuncList.Color)
basic.forever(function () {
    a = PlanetX_Basic.ultrasoundSensor(PlanetX_Basic.DigitalRJPin.J1, PlanetX_Basic.Distance_Unit_List.Distance_Unit_cm)
    b = PlanetX_Basic.ultrasoundSensor(PlanetX_Basic.DigitalRJPin.J3, PlanetX_Basic.Distance_Unit_List.Distance_Unit_cm)
    c = PlanetX_Basic.ultrasoundSensor(PlanetX_Basic.DigitalRJPin.J2, PlanetX_Basic.Distance_Unit_List.Distance_Unit_cm)
    d = PlanetX_Basic.ultrasoundSensor(PlanetX_Basic.DigitalRJPin.J4, PlanetX_Basic.Distance_Unit_List.Distance_Unit_cm)
   estas son las variables que representarian cada sensor ultrasonico
    if (a >= 4 && a <= 45) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 260)
        basic.pause(1600)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    }
    esta parte dice que cuando el sensor detecte un obstaculo dentro de su rango este haga que el motor gire a la derecha para que de la curva
    if (b >= 2 && b <= 8) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 145)
        basic.pause(500)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    }
    este codigo le dice al sensor que cuando detecte algo haga que el servomotor gire un poco para evitarlo
    if (d >= 2 && d <= 6) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 145)
        basic.pause(500)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    }
    este codigo dice que cuando el sensor ultrasonico detecte algo haga que el servomotor gire un poco para evitar el bostaculo
    if (c >= 2 && c <= 8) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 215)
        basic.pause(500)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    }
        este codigo dice que cuando el sensor ultrasonico detecte algo haga que el servomotor gire un poco para evitar el bostaculo

    PlanetX_AILens.cameraImage()
    if (PlanetX_AILens.colorCheck(PlanetX_AILens.ColorLs.red)) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 215)
        basic.pause(2000)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 145)
        basic.pause(2000)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 215)
        basic.pause(1000)
        neZha.setServoAngel(neZha.ServoTypeList._180, neZha.ServoList.S1, 180)
        este codigo dice que cuando la camara detecte el color rojo esta de una curva evitando el obstaculo
    }
    if (PlanetX_AILens.colorCheck(PlanetX_AILens.ColorLs.green)) {
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 145)
        basic.pause(2000)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 215)
        basic.pause(2000)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 145)
        basic.pause(1000)
        neZha.setServoAngel(neZha.ServoTypeList._360, neZha.ServoList.S1, 180)
    }
            este codigo dice que cuando la camara detecte el color verde esta de una curva evitando el obstaculo

})
loops.everyInterval(78000, function () {
    neZha.stopMotor(neZha.MotorList.M1)
})este codigo le dice al motor que luego de 78 segundos este se detenga
4. Fotos equipo y vehículo
 
 
 

 
                                                                       
5. Videos de rendimiento
https://www.youtube.com/watch?v=lLRNFiebKbI
6. Utilización de github
https://github.com/IAst22/diario-de-ingenieria-wro-2024-elektro-team
