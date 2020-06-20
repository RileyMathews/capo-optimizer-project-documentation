# Capo Optimizer Project Docs
This documentation will serve as the overall project documentation that outlines the common design of the 'Capo Optimizer' project.

# Goals
The goal of this project is to take a small but relatively complex musical calculation and implement it across multiple languages and frameworks. The expected output for each language will be as follows.

1. A library that can be consumed by other projects of that language.
1. At least one application using that language which consumes that languages library. This application will present a UI allowing users to select keys and find an optimial capo position for them.

# Models
## Key
### Attributes
* String: root - the string representation of the key.
* Integer: chromatic_index - rhe 0 - 11 index of the root note where 0 = C.

### Constraints
1. The root must be a valid music note
   1. Sharps will be used for all accidentals
   1. Double sharps will not be used
1. The chromatic_index must never be less than 0 or greater than 11

### Methods

#### transpose_up
Transpose the key up by a given number of steps.
* Parameters
  * Integer: steps - The number of steps up the key should be transposed
* Returns
  * Key - A new key object who's root and index are steps up equal to the steps given

#### transpose_down
The logical opposite of 'transpose_up'. Transposes the key down by a given number of steps.
* Parameters
  * Integer: steps - The number of steps down the key should be transposed.
* Returns
  * Key - A new key object who's root and index are steps down equal to the steps given.
  
### Static/Class Methods
#### from_root
Constructs a new key object from a given string representation of a root note.
* Parameters
  * String: root - The string representation of the root note of the key.
* Returns
  * Key - A new key object.

#### from_chromatic_index
Constructs a new key object from a given chromatic index 0 - 11.
* Parameters
  * Integer: chromatic_index - an integer 0 to 11 which will be used to construct the key.
* Returns
  * Key - A new key object.

## Song
A representation of a song and the keys that it is performed in. This is not to say a list of all possible keys it 'could' be played in as that would be all keys. Instead, it holds a list of keys in which the song modulates to throughout one performance of that song.

### Attributes
* List<Key>: keys - a collections of keys.

### Methods
#### transpose_up
Constructs a new song where all keys have been transposed up by the given ammount of steps.
* Parameters
  * Integer: steps - the number of steps the song should be transposed by.
* Returns
  * Song - a new song object.

#### transpose_down
Constructs a new song where all keys have been transposed down by the given ammount of steps.
* Parameters
  * Integer: steps - the number of steps the song should be transposed by.
* Returns
  * Song - a new song object.

## Transposition
### Attributes
* Song: original_song - the original song that will be transposed.
* Song: new_song - the newly transposed song.
* Integer: steps - the number of steps the new song was transposed by.
* Bool: transpose_up - weather or not the song will be transposed up or down. True will transpose up while false will transpose down

# Services
## CapoService
### Methods
#### optimize
Optimizes a song for a particular capo position.
* Parameters
  * Song: song - The song to be optimized
* Returns
  * List<Transposition> - A list of optional transpositions that contain keys that are the easiest to play on guitar.
