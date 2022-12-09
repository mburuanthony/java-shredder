### Java shredded document reader using a Genetic Algorithm

- the fitness function is based on the expected frequency of letter combinations (in english). the function compares the frequencies of letter combinations in the shredded document and compares them to the frequencies you would expect to observe in english.

```java
public static double fitness(char[][] shreds, int[] perm) {
    ...
}
```

- the expected frequency of english character combinations can be found at [english character combinations](http://practicalcryptography.com/cryptanalysis/letter-frequencies-various-languages/english-letter-frequencies/).


``` java
double[][] expectedFrequencies = new double[26][26];
expectedFrequencies['t' - 'a']['h' - 'a'] = 0.027056980400061274; // expected frequency of th
expectedFrequencies['h' - 'a']['e' - 'a'] = 0.0232854497343354; // expected frequency of he
```

- counting the occurence of of character combinations in the de-shredded file

```java
int[][][] charCounts = new int[shreds[0].length][26][26];
int[] totalChars = new int[shreds[0].length];
```

- reading a shredded file from disk using BufferReader().

```java
  public static char[][] getShreddedDocument(String path) {
    ...
  }
```

- unshredding a document based on the provided permutation (int[] perm). where the shredded.length == perm.length

```java
public static char[][] unshred(char[][] shredded, int[] perm) {
    char[][] unshredded = new char[shredded.length][];
    for (int i = 0; i < shredded.length; i++)
      unshredded[i] = shredded[perm[i]].clone();
    return unshredded;
}
```

- pretty printing a document. printing a document in an easily readable style.

```java
public static void prettyPrint(char[][] doc) {
    for (int i = 0; i < doc[0].length; i++) {
      for (int j = 0; j < doc.length; j++) {
        System.out.print(doc[j][i]);
      }
      System.out.println();
    }
    System.out.println();
}
```

- compiling & running

```bash
# compile source code (in terminal)
javac Shredder.java
```

- compiling generates a Shredder.class file, run by

```bash
# run (in terminal)
java Shredder
```

```bash
# sample output
the fitness value for shredded.txt is: 22.98121387283832
the shredded document:
siT s ih
kcaiu q
T t.thse
txiet  s
 riaft s
trooh.s

on unshredding, the fitness value is: 22.28297552751616
the unshredded document:
This is
a quick
test. Th
is text
is far t
o short.
```
