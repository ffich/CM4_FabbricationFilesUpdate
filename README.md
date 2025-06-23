# CM4_FabbricationFilesUpdate
Simple script to update the Raspberry Pi CM4/CM5 Fabbrication Files generated with the JLCPCB plugins.

# The Problem
When designin Kicad Based CM4/CM5 systems, a common problem is that the CM4 form factor is made up by two Hirose DF40 series high density connectors, but Kicad only manage to create production files (Bom and position CSV) with one single footprint associated. This can create ambiguities with the assembly service and they can erroneously mount just one connector instead of two.

![image](https://github.com/user-attachments/assets/b9b95255-6a00-41eb-b5c9-eadf77694051)

Here is a simple example of how the Bom and Position file they looks like when you use a CM4 footprint (the official one coming from Raspberry):

![image](https://github.com/user-attachments/assets/8ca89909-624d-4833-b142-abaea27d5c80)

![image](https://github.com/user-attachments/assets/0034acd7-e4e4-4db4-bfa9-b214970de433)

# The Solution
There are many complex approaces to try to solve the problem working on how Kicad associate part footprints, but since they were quite complex I decided to solve the problem with a simple file post processing approach imnstead. To do this I (obviously) decided to go with python. This generarted a script that does the following:

# A. Adaptation of the BOM file
A1. The script looks for the MODULE1 entry inside the file
A2. It duplicates it and rename MODULE1A the original and MODULE1B the new one

# B. Adaptation of the POSITION file
B1. The script looks for the MODULE1 entry inside the file
B2. It duplictes the entry as for the BOM file
B3. It adapts the coordinates of the new entry

Here are the result after running the script in the files of the example above:

![image](https://github.com/user-attachments/assets/c3261b6e-e880-4809-9437-6aca28c6e5dc)

![image](https://github.com/user-attachments/assets/272ead05-de9c-4989-bc5b-c61bfc0095e5)

# How to use it
For JLCPCB Kicad fabbrication script output, simply put the script in a folder inside your project and run it. Have fun!
