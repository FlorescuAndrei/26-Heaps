package com.andrei;

//MaxHeap
public class Heap {

    private int[] heap;
    private int size;

    public Heap(int capacity){
        heap  = new int[capacity];
    }

    public boolean isFull(){
        return size == heap.length;
    }

    public boolean isEmpty(){
        return size == 0;
    }

    public int getParent(int index){
        return (index - 1) /2;
    }
    //left child index =  2i + 1; right child index  = 2i + 2 ; where i = parent index
    public int getChild(int index, boolean left){
        return 2 * index + (left ? 1 : 2);
    }

    private void fixHeapAbove(int index){
        int newValue = heap[index];
        while(index > 0 && newValue >  heap[getParent(index)]){

            // we bubble new value up and shift down parents less than it

           heap[index] = heap[getParent(index)];
           index = getParent(index);

        }
        heap[index] = newValue;
    }

    private void fixHeapBelow(int index, int lastHeapIndex){
        // last heap index = size -1

        int childToSwap;

        while (index <= lastHeapIndex){

            //this refers to leftChild index and not value
            // can return an index out of bound, greater than array size, if the child not exist
            int lefChild = getChild(index, true);
            int rightChild = getChild(index, false);

            //check if there are children. Heap is a complete tree so can not have a right child without a left one.
            if(lefChild <= lastHeapIndex){

                //we do not have a right child
                if(rightChild > lastHeapIndex){
                    childToSwap = lefChild;
                }
                else{
                    //we swap with the child that have the largest value
                    childToSwap = (heap[lefChild] > heap[rightChild]) ? lefChild : rightChild;
                }
                //after we decide which child we want to swap with, we compare the value of index with the value of child
                if(heap[index] < heap[childToSwap]){
                    int tmp = heap[index];
                    heap[index] = heap[childToSwap];
                    heap[childToSwap] = tmp;
                }
                // there is no need for swap
                else {
                    break;
                }

                index = childToSwap;
            }
            //there are no  children
            else {
                break;
            }


        }
    }

    public void insert(int value){
        if(isFull()){
            throw new IndexOutOfBoundsException("Heap is full");
        }

        heap[size] = value;

        //we check if is greater than his parent and if it is we swap.
        fixHeapAbove(size);

        size++;
    }
    //we use the index because if  we use the value, we must do a linear search,
    // we can't use a binary search because will need a sorted array and that will blow our heap structure.
    // when working with heaps in general you don't want  a random value, you want the root.
    public int delete(int index){
        if(isEmpty()){
            throw  new IndexOutOfBoundsException("Heap is empty");
        }

        int parent = getParent(index);
        int deletedValue = heap[index];

        //replace the value to delete with the most right leaf of the tree
        heap[index] = heap[size-1];

        if(index == 0 || heap[index] < heap[parent]){
            fixHeapBelow(index, size - 1);
        }
        else {
            fixHeapAbove(index);
        }
        size--;

        return deletedValue;
    }


    public void printHeap(){
        for(int i = 0; i < size; i++){
            System.out.print(heap[i]);
            System.out.print(", ");
        }
        System.out.println();
    }

    public int peek() {
        if (isEmpty()) {
            throw new IndexOutOfBoundsException("Heap is emplty");
        }

        return heap[0];
    }

    //Heap Sort Algorithm
    public void sort(){
        int lastHeapIndex = size-1;
        for(int i = 0; i < lastHeapIndex; i++){
            int temp = heap[0];
            heap[0] = heap[lastHeapIndex-i];
            heap[lastHeapIndex - i] = temp;

            fixHeapBelow(0, lastHeapIndex - i - 1);
        }

    }


}
