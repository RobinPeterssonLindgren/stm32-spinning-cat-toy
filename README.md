# stm32-spinning-cat-toy

## How to Add New Sequences
A sequence is an ordered array of pre-programmed movements (Modes). 
To add a new sequence, follow these steps in main.c:

### 1. Locate the typedef
Locate `/* USER CODE BEGIN PV */`. Create a new `Toystate_t` array with your desired Modes. 
Current existing modes: `{ MODE_WAIT, MODE_TEASE, MODE_CHASE, MODE_FULL_LAP }`

```c
// Existing sequences example...
Toystate_t sequence_4[] = { MODE_FULL_LAP, MODE_FULL_LAP, MODE_TEASE, MODE_CHASE, MODE_WAIT }; // 5 steps
```

### 2. Create the new sequence array
```c
// Create your new sequence (e.g., 6 steps)
Toystate_t sequence_5[] = { MODE_CHASE, MODE_TEASE, MODE_CHASE, MODE_FULL_LAP, MODE_FULL_LAP, MODE_WAIT }; // 6 steps
```

### 3. Add to Controller
```c
// Add your new sequence to ToySequenceController_t
ToySequenceController_t all_squences[] = { 
    // ... existing sequences ...
    { sequence_5, 6 }  // (sequence_name, amount_of_steps)
};
```

## Available Modes
* **MODE_WAIT:** Pauses the motor for 4 seconds.
* **MODE_TEASE:** Small, quick alternating movements (400 steps back and forth)
* **MODE_CHASE:** Long sweep in random direction (700 steps)
* **MODE_FULL_LAP:** One complete 360-degree rotation (4096 steps).


## Hardware & Components

- **Microcontroller:** STM32L433
- **Motor Driver:** ULN2003 (5V)
- **Stepper Motor:** 28BYJ-48
- **Power Supply:** 6xAA 1.5V batteries
- **Voltage Regulator:** MB102 Power Supply Module (9V input, 5V output)
- **CAD Files:** Available in the `cad/` directory (.step files)

## Pinout 

Connect the STM32L433 to the ULN2003 motor driver according to the table below:

| STM32 Pin | ULN2003 Driver Pin |
| :--- | :--- |
| **PC0** | IN4 | 
| **PC1** | IN3 | 
| **PC2** | IN2 | 
| **PC3** | IN1 | 


## Power Distribution

- **9V Input:** MB102 DC Jack (Power from 6x AA batteries)
- **STM32L433 (5V):** Connected to VIN from MB102 module (*Sidenote: check input configuration on the STM32L433*)
- **ULN2003 (5V):** Connected to VCC from MB102 module
- **Ground (GND):** Common Ground across all components from the MB102 Module