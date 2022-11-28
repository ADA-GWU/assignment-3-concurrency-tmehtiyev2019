# Advanced Software Paradigms - Assignment 3 (Concurrency)

## Description of the task



The main objective in this assignment is to convert grayscale to color using multi-threaded and single-threaded  programming.

The output application is supposed to take three arguments from the command line:
- **filename (directory of the file)**
- **square size**
- **the processing mode**

Example command: `program inputfile.jpg 15 M`

- file name: the name of the **grayscale image** file in jpg format (no size constraints)
- square size: the side of the square
- processing mode: 'S' - single threaded and 'M' - multi threaded



During the execution of the program, the grayscale image is first shown, and the following procedures starts:
- The program converts the grayscale pixels into color from left to right, top to bottom for each of the **(square size) x (square size)** boxes. While converting grayscale to color creativity is considered more important than reproduction of the original from the grayscale. 
- The result of the program is shown by progress, not at once. The result picture is saved to the same directory as `result.jpg` file
- In the multi-processing mode ('M'), the procedure is performed in parallel threads. The number of threads are selected according to the computer's CPU cores. In this assignment **Runtime.getRuntime().availableProcessors()** is used to use number of processors available to the JVM during the runtime.

## Description to run program

Firstly, a program needs to be compiled with the following command:
```
javac Main.java
```

Secondly, for a successfull execution of a program, all three parameters (file name, square size and processing mode) needs to be passed as command line arguments as mentioned in the task description. The parameters should be seperated by a single space. In the examples given below some of the commands to execute the program are given.

- For the command with parameters(file name: SampleInput1.jpg, square size: 15, and processing mode: S) run:
```
java Main.java SampleInput1.jpg 15 S
```

- For the command with parameters(file name: SampleInput2.jpg, square size: 10, and processing mode: M) run:
```
java Main.java SampleInput2.jpg 10 M
```

## Description of program

There are 3 parts of the program:

- `Main.java`
- `Coordinates.java`
- `Processing.java`


## Description of Main Class
Main class takes the arguments from the command line and uses the following methods:

- `convert_image()`
Description: This method the picture in the given command line argument is imported and based on the given processing mode either `singleMode()`or `multiMode()` method is called

- `singleMode()`
Description: This method calls `processing.convert()` method with single thread where the processing of the picture from grayscale to color is happened

- `multiMode()`
Description: This method first creates extra threads with `Runtime.getRuntime().availableProcessors()` and equallly distribute the picture among the threads. This method calls `Coordinates` class where the coordinates for the threads are assigned and `processing.convert()` method where the processing of the picture with multithreads is happened. Seperately processed pieces of picture via multithreads are joined in this method
