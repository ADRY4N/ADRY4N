# Digispark

Um Bad USB é um dispositivo USB que atua como um teclado USB para executar um ataque de injeção de teclas, que pode ser usado para abrir um terminal e executar comandos no computador de destino.
Como esses ataques são programados, eles podem acontecer incrivelmente rápido. É uma loucura como um BadUSB com o script certo pode assumir o controle de um computador desbloqueado em apenas 3 segundos!

**Download da IDE**
```
https://www.arduino.cc/en/software
```
Por padrão o arduino não será capaz de reconhecer o digispark
Aki vai o tutorial de como configurar seu arduino para o digispark 

Abra o arduino vá em **Arquivo > preferência** e copie essa URL
```
https://raw.githubusercontent.com/ArminJo/DigistumpArduino/master/package_digistump_index.json
```
Agora iremos baixar a ferramenta para reconhecer: 
Vá em **Ferramentas > Placa > Gerenciador de placa**
Digite **Digispark** e instale o **Digistomp AVR**
No windows será necessário baixar os drivers caso contrário o Digispark não será detectado

**Link para baixar os drivers**
```
https://github.com/digistump/DigistumpArduino/releases/download/1.6.7/Digistump.Drivers.zip
```

![Capturar](https://github.com/user-attachments/assets/2ebeb8b6-d0fd-48be-8648-a9fec9f50f4e)


Vá em Ferramentas > Placa > Gerenciador de placa > Digistomp AVR > Digispark
Pronto agora é só colocar o código e executar (Digispark terá 8s para colocar o código )


# Exemplo de codigo para o digispak:

```
#include "DigiKeyboard.h"

// https://cataas.com/cat/says/YOU%20HAV...!
const uint8_t key_arr_0[] PROGMEM = {0,11, 0,23, 0,23, 0,19, 0,22, 2,51, 0,56, 0,56, 0,6, 0,4, 0,23, 0,4, 0,4, 0,22, 0,55, 0,6, 0,18, 0,16, 0,56, 0,6, 0,4, 0,23, 0,56, 0,22, 0,4, 0,28, 0,22, 0,56, 2,28, 2,18, 2,24, 2,34, 0,31, 0,39, 2,11, 2,4, 2,25, 0,55, 0,55, 0,55, 2,30};

void duckyString(const uint8_t* keys, size_t len) {  
    for(size_t i=0; i<len; i+=2) {
        DigiKeyboard.sendKeyStroke(pgm_read_byte_near(keys + i+1), pgm_read_byte_near(keys + i));
    }
}

void setup() {
    pinMode(1, OUTPUT); // Enable LED
    digitalWrite(1, LOW); // Turn LED off
    DigiKeyboard.sendKeyStroke(0); // Tell computer no key is pressed

    DigiKeyboard.delay(1000); // DELAY 1000
    DigiKeyboard.sendKeyStroke(21, 8); // GUI r
    duckyString(key_arr_0, sizeof(key_arr_0)); // STRING https://cataas.com/cat/says/YOU%20HAV...!
    DigiKeyboard.sendKeyStroke(40, 0); // ENTER
    DigiKeyboard.delay(1000); // DELAY 1000
    DigiKeyboard.sendKeyStroke(68, 0); // F11
}

void loop() {}

```
