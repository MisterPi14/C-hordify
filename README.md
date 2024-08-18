# Chord++: Random Melody Generator

## Developed by:
- Piña Vargas Edgar Diego

## Project Overview
C++hord is a program designed for recreational use, focused on exploring some basic musical concepts and, most importantly, generating random melodies. The program features three main sections:
1. **Melody Generator:** Create random melodies based on musical scales.
2. **Musical Data Visualization:** View information about musical notes and tonal modes.
3. **Chord Playback:** Listen to the difference between major and minor chords.

Each section provides a brief contextualization of the musical concepts involved.

## Object-Oriented Programming Concepts Used
The development of this program is rooted in several key concepts of object-oriented programming (OOP):

### Classes and Encapsulation
- **Classes:** The program is structured using classes to represent musical notes and data related to them.
- **Encapsulation:** Data within classes is encapsulated to protect and organize the information.
- **Member Functions:** Classes contain member functions to perform actions related to the data.
- **Scope Resolution Operator:** Used to define member functions outside the class definition.
- **Constructors and Destructors:** These are used to initialize objects and manage resource cleanup.

### Inheritance
- **Inheritance:** The program utilizes inheritance to create derived classes that extend the functionality of base classes.

### Templates
- **Templates:** The program includes a template function to handle various data types, demonstrating the flexibility and reusability of code.

### Polymorphism
- **Function Overloading:** The program uses function overloading to handle different types of inputs for similar operations.
- **Operator Overloading:** Operators are overloaded to perform specific tasks, such as generating musical intervals.

## Program Structure

### Base Class: `notas_id`
This class encapsulates basic information about a musical note, including its name and figure (e.g., whole note, half note). It features:
- **Constructor:** Initializes the note with a name and figure.
- **Member Function:** `imprimir()` prints the note's details.

### Derived Class: `notas_data`
Inherits from `notas_id` and adds additional properties such as frequency and duration. It includes:
- **Member Function:** `reproducir()` plays the note using the `Beep` function.
- **Constructor and Destructor:** Manage the creation and destruction of note objects, ensuring proper resource management.

### Melody Generation
The program includes functions to generate random melodies based on a selected musical scale and tempo. It uses randomization to create a sequence of notes that are then played.

### Data Visualization
Two overloaded `DatosMusicales()` functions allow users to visualize the frequency of notes across octaves or find relative modes of a major scale.

### Chord Playback
An interactive section of the program allows users to listen to and compare the sound of major and minor chords by using operator overloading to calculate the appropriate intervals.

## How to Use

To use the Chord++ program, follow these steps:

1. **Open the C++ File:**
   - Locate the C++ source code file (e.g., `C++hord.cpp`) on your computer.

2. **Compile the Program:**
   - Open a terminal or command prompt.
   - Navigate to the directory where the C++ file is located.
   - Compile the program using a C++ compiler. For example, if using `g++`, you would enter:
     ```bash
     g++ -o C++hord C++hord.cpp
     ```
   - This will generate an executable file named `C++hord` (or `C++hord.exe` on Windows).

3. **Run the Program:**
   - Execute the compiled program by entering:
     ```bash
     ./C++hord
     ```
   - On Windows, you can simply double-click the `.exe` file or run it from the command prompt:
     ```bash
     C++hord.exe
     ```

4. **Main Menu Options:**
   - Once the program is running, you will be presented with three main options. You can choose any of these options based on what you want to explore:

   ### Option 1: Generate Melodies
   - Select `1` to enter the Melody Generator.
   - Follow the prompts to choose a musical scale, set the tempo (BPM), and specify the duration.
   - The program will generate and play a random melody.

   ### Option 2: Visualize Musical Data
   - Select `2` to explore musical data.
   - You can choose to view the frequency of a note across octaves or find the relative mode of a major scale.
   - Enter the required information when prompted.

   ### Option 3: Play Chords (Major and Minor)
   - Select `3` to compare major and minor chords.
   - Enter `1` to hear a major chord or `2` to hear a minor chord.
   - The program will play the selected chord, demonstrating the tonal difference.

5. **Return to Main Menu:**
   - After completing your chosen activity, the program will prompt you to return to the main menu. You can choose to explore another option or exit the program.

The program is designed to be interactive and educational, providing both auditory and visual feedback on musical concepts.

Enjoy creating and exploring music with C++hord!
