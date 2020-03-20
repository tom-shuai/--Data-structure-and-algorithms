# --Data-structure-and-algorithms
记录每天的算法学习

import java.io.*;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class sparseArray {

    public static void main(String[] args) {
        /*
        1.创建原始的棋子的二维数组
        2.0表示没值
        3.1.表示黑棋子：2.表示蓝子
        * */
        int chessarray[][] = new int[11][11];
        //给每个棋子的位置赋值
        chessarray[1][2]=1;
        chessarray[2][3]=2;
        //输出原始的二维数组
        for(int[] row:chessarray){
            for (int data:row){
                System.out.printf("%d\t",data);
            }
                    System.out.println();
        }
        //遍历二维数组拿到的他的有效值个数
        int sum=0;
        for (int i=0;i<chessarray.length;i++){
            for (int j=0;j<chessarray.length;j++){
              if (chessarray[i][j]!=0){
                  sum++;
              }
            }
        }
        //二维数组转稀疏数组
        //创建一个稀疏数组
        int spaArray[][] = new int[sum+1][3];
        spaArray[0][0]=11;
        spaArray[0][1]=11;
        spaArray[0][2]=sum;
        //遍历二维数组将非零数据放入到稀疏数组中
        int count=0;//如果遇到原始数组不为0的数据就做一个自增的记录
        for (int i=0;i<chessarray.length;i++){
            for (int j=0;j<chessarray.length;j++){
                if (chessarray[i][j]!=0){
                    count++;
                    spaArray[count][0]=i;
                    spaArray[count][1]=j;
                    spaArray[count][2]=chessarray[i][j];
                 }
                }
            }
        //输出稀疏数组
        for (int[] srow:spaArray){
            for (int data:srow){
                System.out.printf("%d\t",data);
            }
            System.out.println();
        }

       /*
       稀疏数组还原二维数组
        11	11	2
        1	2	1
        2	3	2
       */
        int newchessarray[][]=new int[spaArray[0][0]][spaArray[0][1]];

        for (int n=1;n<spaArray.length;n++){
            newchessarray[spaArray[n][0]][spaArray[n][1]]=spaArray[n][2];
        }
        //输出转化后的二维数组

        for (int[] row:newchessarray){
            for (int data:row){
                System.out.printf("%d\t",data);
            }
            System.out.println();
        }

        //将稀疏数组存放到磁盘上用的时候再调用
        try {
            String path="C:\\Users\\Administrator\\Desktop\\稀疏数组.txt";
            OutputStream os=new FileOutputStream(path);
          for (int i=0;i<spaArray.length;i++){
              for (int j=0;j<spaArray.length;j++){
                  int z =spaArray[i][j];
                  String s = String.valueOf(z);
                  os.write(s.getBytes());
              }

          }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        //读取磁盘上文件数据
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("C:\\Users\\Administrator\\Desktop\\稀疏数组.txt"));
        } catch (FileNotFoundException ex) {
            ex.printStackTrace();
        }
        String line = null;
        //将读取到的数据写入到list集合中
        List<String> list1=new ArrayList<String>();
        while(true){
            try {
                if (!((line=br.readLine())!=null)) break;
            } catch (IOException ex) {
                ex.printStackTrace();
            }
            list1.add(line);
        }
        //循环输出list集合
        for(int i=0;i<list1.size();i++){
            System.out.print(list1.get(i));
        }
    }
}
