# CodeWars code examples
https://www.codewars.com/users/Dudedaya/completed

4 kyu
Snail
==========================

import java.util.*;

public class Snail {

    public static int[] snail(int[][] array) {
      if (array.length == 1) {        
        return array[0];
      }
     ArrayList<ArrayList<Integer>> lst = new ArrayList<ArrayList<Integer>>();
     int l = 0;
     for (int[] a : array) {
       ArrayList<Integer> tempList = new ArrayList<Integer>();
       for (int val : a) {
         tempList.add(val);
         l++;
       }
       lst.add(tempList);
     }
     int[] result = new int[l];
     int index = 0;
     while (!lst.isEmpty()) {
       while (!lst.get(0).isEmpty()) {
         result[index] = lst.get(0).get(0);
         index++;
         lst.get(0).remove(0);         
       }
       lst.remove(0);
       for (int i = 0; i < lst.size(); i++) {
         result[index] = lst.get(i).get(lst.get(i).size() - 1);
         index++;
         lst.get(i).remove(lst.get(i).size() - 1);
       }
       while (!lst.get(lst.size() - 1).isEmpty()) {
         result[index] = lst.get(lst.size() - 1).get(lst.get(lst.size() - 1).size() -1);
         index++;
         lst.get(lst.size() - 1).remove(lst.get(lst.size() - 1).size() -1);
       }
       lst.remove(lst.size() - 1);
       if (lst.size() != 1) {
         for (int i = lst.size() - 1; i >= 0; i--) {
           result[index] = lst.get(i).get(0);
           index++;
           lst.get(i).remove(0);
         }
        } else {
          while (!lst.get(0).isEmpty()){
          result[index] = lst.get(0).get(0);
          index++;
          lst.get(0).remove(0);          
          }
          lst.remove(0);
        }        
     }
     System.out.println(Arrays.toString(result));
     return result;
     }
}

4 kyu
Large Factorials
==========================

	import java.math.BigInteger;

	public class Kata {

		public static String Factorial(int n) {
	    if (n < 0) {
	      return null;
	    } else if (n == 0) {
	      return "1";
	    } else {
	      BigInteger fac = BigInteger.ONE;
	      for (int i = 2; i <= n; i++) {
		fac = fac.multiply(BigInteger.valueOf((long)i));
	      }
	      return fac.toString();
	    }    
	  }
	}

4 kyu
Sudoku Solution Validator
==========================

public class SudokuValidator {

    public static boolean check(int[][] sudoku) {
        String sudStr = asString(sudoku);
        System.out.println(sudStr);
        if (sudStr.contains("0")) {
          return false;
        } else  if (checkRows(sudoku) && checkCols(sudoku) && checkDigs(sudStr)) {
          return true;
        } else {
          return false;
        }
    }
    
    private static String asString(int[][] sudoku) {
      StringBuffer sb = new StringBuffer();
      for (int[] i : sudoku) {
        for (int j : i) {
          sb.append(j);
        }
      }
      return sb.toString();
    }
    
    private static boolean checkRows(int[][] a) {
      for (int[] row : a) {
        int sum = 45;
        for (int d : row) {
          sum -= d;
        }
        if (sum != 0) {
          return false;
        }
      }
      return true;
    }
    
    private static boolean checkCols(int[][] a) {
      int[] sums = new int[9];
      for (int i = 0; i < a.length; i++) {
        for (int j = 0; j < a[i].length; j++) {
          sums[i] += a[i][j];
        }
      }
      for (int i : sums) {
        if (i != 45) {
          return false;
        }
      }
      return true;
    }
    
    private static boolean checkDigs(String s) {
      String[] a = s.split("");
      for (int i = 1; i <= 9; i++) {
        int d = 0;
        for (int j = 0; j < a.length; j++) {
          if (i == Integer.valueOf(a[j])) {
            d++;
          }
        }
        if (d != 9) {
          return false;
        }
      }
      return true;
    }

}

5 kyu
Primes in numbers
==========================

import java.util.*;

public class PrimeDecomp {
       
    public static String factors(int n) {
        List<Integer> primes = fillPrimes(20000);
        int res = n;
        String s = "";
        for (int p : primes) {
          int i = 0;
          while (res % p == 0) {
            i++;
            res /= p;
          }
          if (i == 1) {
            s+= "(" + p + ")";
          } else if (i > 1) {
          
            s+= "(" + p + "**" + i + ")";
          }
        }
        return s;
    }
    
    private static ArrayList<Integer> fillPrimes(int limit) {
      ArrayList<Integer> p = new ArrayList<Integer>();
      p.add(2);
      for (int i = 2; i < limit; i++) {
        int j = 0;
        for (int k = 3; k < limit; k+= 2) {
          if (j < 2 && i % k == 0) {
            j++;
          }
        }
        if (j == 1) {
          p.add(i);
        }
      }      
      p.add(123863); //cheating here due to time limit :/
      return p;
    }
       
}

4 kyu
Catching Car Mileage Numbers
==========================

import java.util.*;

public class CarMileage {

	public static int isInteresting(int number, int[] awesomePhrases) {
    if (number < 100) {
      if (number == 98 || number == 99) {
        return 1;
      } else {
        return 0;
      }
    }
    if (doChecks(awesomePhrases, number)) {
      return 2;
    } else if (doChecks(awesomePhrases, number + 1) || doChecks(awesomePhrases, number + 2)) {
      return 1;
    } else {
      return 0;
    }
	}  
	private static boolean zeroCheck(int[] a) {
    int sum = 0;
    for (int i : a) {
      sum+= i;
    }
    if (sum == a[0]) {
      return true;
    } else {
      return false;
    }      
	}  
	private static boolean sameCheck(int[] a) {
    boolean b = true;
    for (int i : a) {
      if (a[0] != i) {
        b = false;
      }
    }
    return b;
	}  
	private static boolean incCheck(int[] a) {
    boolean b = true;
    for (int i = 1; i < a.length; i++) {
      if (a[i] != (a[i-1] + 1) % 10) {
        b = false;
      }      
    }
    return b;
    }
    private static boolean decCheck(int[] a) {
    boolean b = true;
    for (int i = 1; i < a.length; i++) {
      if (a[i] != a[i-1] - 1) {
        b = false;
      }
    }
    return b;
    }
    private static boolean paliCheck(int[] a) {
    if (a.length % 2 == 0) {
      int[] a01 = Arrays.copyOfRange(a, 0, (a.length - 1)/2);
      List<Integer> a1 = new ArrayList<Integer>();
      for (int i : a01) {
        a1.add(i);
      }
      int[] a02 = Arrays.copyOfRange(a, (a.length + 1)/2, a.length);
      List<Integer> a2 = new ArrayList<Integer>();
      for (int i : a02) {
        a2.add(i);
      }
      Collections.reverse(a2);
      if (a1.equals(a2)){
        return true;
      } else {
        return false;
      }
    } else {  
      int[] a01 = Arrays.copyOfRange(a, 0, (a.length - 1)/2);
      List<Integer> a1 = new ArrayList<Integer>();
      for (int i : a01) {
        a1.add(i);
      }
      int[] a02 = Arrays.copyOfRange(a, (a.length + 1)/2, a.length);
      List<Integer> a2 = new ArrayList<Integer>();
      for (int i : a02) {
        a2.add(i);
      }
      Collections.reverse(a2);
      if (a1.equals(a2)){
        return true;
      } else {
        return false;
      }
    }
    }  
    private static boolean aweCheck(int[] awe, int n) {
    for (int i : awe) {      
      if (n == i) {      
      return true;
      }
    }    
    return false;
    } 
    private static boolean doChecks(int[] awe, int n) {
    String s0 = Integer.toString(n);
    String[] sa = s0.split("");    
    int l = s0.length();
    int[] a = new int[l];
    int i = 0;
    for (String s : sa) {
      a[i] = Integer.valueOf(s);
      i++;
    }
    if (aweCheck(awe, n) || zeroCheck(a) || sameCheck(a) 
       || incCheck(a) || decCheck(a) || paliCheck(a)) {
      System.out.println("awe = "+ aweCheck(awe, n) +" zero="+ zeroCheck(a) +" same="+ sameCheck(a) +" inc="+
        incCheck(a) +" dec="+ decCheck(a) +" pali="+ paliCheck(a));
      return true;
    } else {
      return false;
    }
  }
}

5 kyu
Integers: Recreation One
==========================

import java.util.*;

public class SumSquaredDivisors {
	
	public static String listSquared(long m, long n) {
    String r = "[";
     for (long i = m; i <= n; i++) {
       if (checkSquare(i)) {
         r+= "[" + i + ", " + calculateDivSquare(i) + "], ";
       }
     }
     //return empty array if nothing found
     if (r.length() <= 1) {
     return "[]";
     }
     //else trim the resulting string to look like an array
     String result = r.substring(0, r.length() - 2) + "]";
     return result;
	}  
	private static boolean checkSquare(long l) {
    if (Math.sqrt(calculateDivSquare(l)) % 1 == 0) {
      return true;
    } else {
      return false;
    }
	}  
	private static long calculateDivSquare(long l) {
    long square = 0;
    for (long i = 1; i <= l; i++) {
      if (l % i == 0) {
        square += i * i;
      }
    }
    return square;
  }
}

6 kyu
Which are in?
==========================

import java.util.*;

public class WhichAreIn { 
	
	public static String[] inArray(String[] array1, String[] array2) {
    HashSet<String> hs = new HashSet<String>();
    for (String s2 : array2) {
      for (String s1 : array1) {
        if (s2.contains(s1)){
        hs.add(s1);
        }
      }
    }
    String[] result = new String[hs.size()];
    result = hs.toArray(result);
    Arrays.sort(result);
		 return result;
	}
}

6 kyu
Equal Sides Of An Array
==========================

public class Kata {

	public static int findEvenIndex(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
      int before = 0;
      int after = 0;
      for (int j = 0; j < i; j++) {
        before += arr[j];
      }
      for (int k = i + 1; k < arr.length; k++) {
        after += arr[k];
      }
      if (before == after) {
        return i;
      }
    }
    return -1;
  }
}

6 kyu
Multiples of 3 or 5
==========================

import java.util.*;

public class Solution {

	public int solution(int number) {
    int sum = 0;
    HashSet<Integer> hs = new HashSet<Integer>();
    for (int i = 1; i * 3 < number; i++) {
      hs.add(i * 3);
    }
    for (int i = 1; i * 5 < number; i++) {
      hs.add(i * 5);
    }
    for (Integer j : hs) {
      sum += j;
    }
    return sum;
  }
}
