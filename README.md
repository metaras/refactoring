# Refactoring
## Endcrypt Decrypt
From https://github.com/OOP2020/pa2-metaras 
* **Refactor Signs:**
  * Extract class
    In class Crypt contain a lots of method, so move below method to Unicode and Shift class.
    ```Java
    private void endcryptUni()
    private void decryptUni()
    private void endcryptShift()
    private void decryptShift()
    ```
   * Extract method
    The code below are apprear in the Crypt class twice once in ```public static void main(String[] args)``` and another time in  so ```public static void toFile(File in, File out, String key, String alg, String mode) ``` extract them to a method.
      <br> Before:
      ```Java
      if (mode.toLowerCase().contains("enc")) {
         if (alg.toLowerCase().contains("shift")) {
             out = Shift.encryptShift(data, key);
         } else if (alg.toLowerCase().contains("unicode")) {
             out = Unicode.encryptUni(data, key);
          }
      } else if (mode.toLowerCase().contains("dec")) {
          if (alg.toLowerCase().contains("shift")) {
              out = Shift.decryptShift(data, key);
          } else if (alg.toLowerCase().contains("unicode")) {
              out = Unicode.decryptUni(data, key);
          }
      }
      ```
      After:
      ```Java
          private static String setType(String key, String alg, String mode, String sOut, StringBuilder data) {
              if (mode.toLowerCase().contains("enc")){
                  if (alg.toLowerCase().contains("unicode")){
                      sOut = Unicode.encryptUni(data, key);
                  } else if (alg.toLowerCase().contains("shift")){
                      sOut = Shift.encryptShift(data, key);
                  }
              } else if (mode.toLowerCase().contains("dec")){
                  if (alg.toLowerCase().contains("unicode")){
                      sOut = Unicode.decryptUni(data, key);
                  } else if (alg.toLowerCase().contains("shift")){
                      sOut = Shift.decryptShift(data, key);
                  }
              }
              return sOut;
          }
      ```
  * Change "if" to "switch"
    <br>The **if** condition was too long.
    <br>Before:
    ```Java
    for (int i = 0; i < args.length - 1; i++) {
       if (args[i].equals("-mode")) {
           mode = args[i + 1];
       } else if (args[i].equals("-key")) {
           key = args[i + 1];
       } else if (args[i].equals("-data")) {
           data = data + args[i + 1];
       } else if (args[i].equals("-in")) {
           namein = args[i + 1];
       } else if (args[i].equals("-out")) {
           nameOut = args[i + 1];
       } else if (args[i].equals("-alg")) {
           alg = args[i + 1];
       }
     }
    ```
     After:
    ```Java
        for (int i = 0; i < args.length - 1; i++) {
            switch (args[i]) {
               case "-mode" : mode = args[i + 1];
               case "-key" : key = args[i + 1];
               case "-data" : data.append(args[i + 1]);
               case "-in" : namein = args[i + 1];
               case "-out" : nameOut = args[i + 1];
               case "-alg" : alg = args[i + 1];
             }
         }
   * Rename class:
   Crypt to Main
   
