BinaryTree.java:
---------------
public class BinaryTree {
    public Node root;
    public int maxDepth = 0;
    public int noOfEmpty = 0;
    public int iplSum = 0;
    public int temp = -1;
    public BinaryTree(char d,int dep){
        
        root = new Node (d,dep);
    }
    public void add(char data){
       root= recursiveAdd(root,data);
    }
    public Node recursiveAdd(Node current,char d){
       temp++;
        if(current == null){
            current = new Node(d,temp);
            return current;
        }
        if(current.data >= d){
        current.left = recursiveAdd(current.left,d);
        }else{
        current.right = recursiveAdd(current.right,d);
        }
        if(temp > maxDepth){
            maxDepth = temp;
            temp = -1;
        }else{
            temp = -1;
        }
        return current;
    }
    public int getMaxDepth(){
        return maxDepth;
    }
   public void oneChildShow(){
       find1childNodes(root);
   }
   public boolean find1childNodes(Node current){
       if(current == null){
           
           return true;
       }
     if((current.left == null && current.right != null) || (current.left != null && current.right == null)){
         System.out.print(current.data);
     }
     find1childNodes(current.left);
     find1childNodes(current.right);
       return true;
   }
   public void countEmpty(){
     addEmptyNodes(root);
   } 
    public boolean addEmptyNodes(Node current){
      if(current == null){
          return true;
      }
    if(current.left == null){
        noOfEmpty++;
      
    }
    if(current.right == null){
     
        noOfEmpty++;
    }
    addEmptyNodes(current.left);
    addEmptyNodes(current.right);
    return true;
    }
    public int getNumberOfEmpty(){
        
        return noOfEmpty;
    }
    public void findIPL(){
        calculateIPL(root);
    }
    public boolean calculateIPL(Node current){
        if(current == null){
            return true;
        }
        iplSum = iplSum + current.depth;
        
        calculateIPL(current.left);
        calculateIPL(current.right);
        return true;
    }
    public int getSum(){
        
        return iplSum;
    } 
}

MyProgram.java:
--------------
import java.util.Scanner;

public class MyProgram
{
    public static void main(String[] args)
    {
        System.out.println("Please enter a word");
        Scanner in = new Scanner (System.in);
        String input = in.nextLine();
        BinaryTree tree = new BinaryTree(input.charAt(0),0);
        for(int x = 1; x < input.length(); x++){
       tree.add(input.charAt(x));
        }
        System.out.print("One child nodes = ");
        tree.oneChildShow();
       tree.countEmpty();
       System.out.println("\nEmpties = " + tree.getNumberOfEmpty());
       tree.findIPL();
        System.out.println("IPL = " +tree.getSum());
    }
}

Node.java:
---------
public class Node {
   
   char data;
   Node right = null;
   Node left = null;
   int depth;
   public Node(char d, int dep){
       depth = dep;
       data = d;
   }
}

