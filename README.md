Problem 1 :

 static int[] helpPrivateRyan(String S, String[] arr){
    	int M = 1000000007; 
    	S = S.toLowerCase();
    	int[] subsequenceCount = new int[arr.length];
        for (int i=0;i<arr.length;i++) {
        	int n = count(S,arr[i].charAt(0));
        	int sum = (n*(n+1));
        	subsequenceCount[i]=sum%M;	
        }
        return subsequenceCount;
    }
    
    public static int count(String s, char c) 
    { 
        int res = 0; 
        for (int i=0; i<s.length(); i++) 
        { 
            if (s.charAt(i) == c) 
            res++; 
        }  
        return res; 
    } 




**********************************************************************************************************************

Problem 1 Alternate :

    static int[] helpPrivateRyan(String S, String[] arr){
    	int M = 1000000007; 
    	S = S.toLowerCase();
    	int[] subsequenceCount = new int[arr.length];
        for (int i=0;i<arr.length;i++) {
        	Set<String> finalSet = new HashSet<>();
        	int index = S.indexOf(arr[i]);
        	if(index==-1)
        		continue;
        	while(index!=-1) {
        		String[] str = getAllSubstring(S.substring(0, index+1));
					for (String string : str) {
						finalSet.add(string);
					} 
	            	index = S.indexOf(arr[i], S.indexOf(arr[i]) + index);
        		}
        	subsequenceCount[i]=finalSet.size()%M;	
        }
        return subsequenceCount;
    }
    
    static String[] getAllSubstring(String subS){
    	String[] res = new String[subS.length()];
    	int beginIndex = subS.length()-1;
    	for(int i=0;i<subS.length();i++) {
    		res[i] = subS.substring(beginIndex, subS.length());
    		beginIndex--;
    	}
    	return res;
    }
    
    
    
    
*******************************************************************************************************************

Problem 2 :


import java.util.*;
public class As {

	public static void main(String[] arg)  {
        Scanner sc = new Scanner(System.in);
        int y = sc.nextInt();
        int x = sc.nextInt();
		//int[][] matrix = {{ 1, 2, -3 }, { 4, 5, -6 } };
		int[][] matrix = new int[y][x];
		for(int i=0;i<y;i++) {
			for(int j=0;j<x;j++) {
				matrix[i][j] = sc.nextInt();
			}
		}
		int minRowSum = getMinRowSum(matrix,x,y);
		int minColSum = getMinColSum(matrix,x,y);
		int total = getSum(matrix);
		if(minRowSum < 0 && minRowSum < minColSum)
			total = total - minRowSum;
		else if(minColSum <0)
			total = total - minColSum;
		System.out.println(total);
	}


	
	static int getMinRowSum(int[][] matrix, int x, int y) {
		int minRow = Integer.MAX_VALUE;
		for (int i = 0; i < y; i++) {
			if(isNegativeValue(matrix[i])) {
			int rowSum = 0;
			for (int j = 0; j < x; j++) {
				rowSum += matrix[i][j];
			}
			if (rowSum < minRow) {
				minRow = rowSum;
			}	
		 }
		}
		return minRow;

	}

	
	static int getMinColSum(int[][] matrix,  int x, int y) {
		int minCol = Integer.MAX_VALUE;
		for (int i = 0; i < x; i++) {
			int colSum = 0;
			for (int j = 0; j < y; j++) {
				colSum += matrix[j][i];
			}
			if (colSum < minCol) {
				minCol = colSum;
			}	
		}
		return minCol;
	}
	
	
	static boolean isNegativeValue(int[] arr) {
		boolean ispresent = false;
		if (Arrays.stream(arr).filter(i -> i < 0).count() > 0)
			ispresent = true;
		return ispresent;
	}
	
	
	static int getSum(int matrix[][]) {
		int perTotal = 0;
		int numCols = 3;
		int numRows = 2;
		for (int c = 0; c < numCols; c++)
		    perTotal += matrix[0][c] + matrix[numRows-1][c];
		for (int r = 1; r < numRows-1; r++)
		    perTotal += matrix[r][0] + matrix[r][numCols-1];
		return perTotal;
	}

}
