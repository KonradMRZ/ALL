import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class s17227 {
    static int tablica[];
    //testtest

    public static void main(String[] args){
        //===============================================
        //Wczytywanie pliku i tworzenie tablicy liczb
        String path = args[0];
        File plik = new File(path);
        try {
            Scanner in = new Scanner(plik);
            String line = in.nextLine();
            String[] stringTab = line.split(" ");
            tablica = new int[stringTab.length];
            for(int i = 0; i < tablica.length; i++){
                tablica[i] = Integer.parseInt(stringTab[i]);
            }

        } catch (FileNotFoundException e) {
            System.out.println("Nie odnaleziono pliku");
        }
        //===============================================

        //Wykonanie algorytmu
        int[] tab = findBiggestASC(tablica);
        System.out.println(tab[0] +" "+ tab[1]);


    }
    public static int[] findBiggestASC(int[] tab){
        int[] ascMaxTab = new int[2];
        int maxLength = 0;
        int sum;

        int lengthCounter = 0;
        int l = tab[0];

        for(int i = 0; i < tab.length; i++){
            /*
            TESTOWANIE ALGORYTMU LICZB ROSNACYCH
            System.out.println("i = " + i);
            System.out.println("l = " + l);
            System.out.println("lc = " + lengthCounter);
            System.out.println("mx = " + maxLength);
            System.out.println("=================");
            */

            if(tab[i] >= l){
                l = tab[i];
                lengthCounter++;
            }else{
                sum = 0;
                if(lengthCounter > maxLength){
                    for(int j = i-lengthCounter ; j < i-lengthCounter+lengthCounter; j++){
                        sum += tab[j];
                        // TEST ZLICZANIA System.out.println(sum);
                    }
                    ascMaxTab[0] = lengthCounter;
                    ascMaxTab[1] = sum;
                    maxLength = lengthCounter;
                }
                l = tab[i];
                lengthCounter = 1;
            }
        }


        /// DESC
        lengthCounter = 0;
        l = tab[0];

        for(int i = 0; i < tab.length; i++){
            /*
            TESTOWANIE ALGORYTMU LICZB MALEJACYCH
            System.out.println("i = " + i);
            System.out.println("l = " + l);
            System.out.println("lc = " + lengthCounter);
            System.out.println("mx = " + maxLength);
            System.out.println("=================");
            */

            if(tab[i] <= l){
                l = tab[i];
                lengthCounter++;
            }else{
                sum = 0;
                if(lengthCounter > maxLength){
                    for(int j = i-lengthCounter ; j < i-lengthCounter+lengthCounter; j++){
                        sum += tab[j];
                       //TEST ZLICZANIA System.out.println(sum);
                    }
                    ascMaxTab[0] = lengthCounter;
                    ascMaxTab[1] = sum;
                    maxLength = lengthCounter;
                }
                l = tab[i];
                lengthCounter = 1;
            }
        }

        return ascMaxTab;
    }
}
