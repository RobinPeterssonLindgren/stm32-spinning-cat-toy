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
