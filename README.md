# sorts.cpp
merge sort,bucket sort,quicksort,insertion sort, heapsort

#ifndef __SORTS_CPP
#define __SORTS_CPP
#include "sorts.h"

//=====================================================================================
vector<long> InsertionSort(vector<long> nums)
{
     long size = nums.size();
     long *arr = new long[size];
     int i, j, key;
     
     std::copy(nums.begin(), nums.end(), arr);
     
        for (j = 1; j < size; j++)
    {
        key = arr[j];
        i = j - 1;
        while (i >= 0 && arr[i] > key)
        {
            arr[i + 1] = arr[i];
            i = i - 1;
        }
        arr[i + 1] = key;
    }
    
    vector<long> vect;
    vect.insert( vect.begin() , arr , arr + size );
    
    return vect; 
     
     
}


//=====================================================================================



vector<long> MergeSort(vector<long> nums)
{
    
    
    int size = nums.size();
    List<long> l;
    ListItem<long> *temp2 = NULL;
    
    for (std::vector<long>::iterator it = nums.begin() ; it != nums.end(); ++it)
    {
        l.insertAtHead(*it);
    }

    l.sortList();

    
    vector<long> vect;
    
    temp2 = l.getHead();
    while (temp2 != NULL)
    {
        vect.push_back (temp2->value);
        
        temp2 = temp2->next;
    }
    
    return vect;    
}

//=====================================================================================

// Quick Sort array
//=====================================================================================
    


void quickSort( long a[], int first, int last ) 
{
    int pivotElement;
 
    if(first < last)
    {
        pivotElement = pivot(a, first, last);
        quickSort(a, first, pivotElement-1);
        quickSort(a, pivotElement+1, last);
    }
}
 

long pivot(long a[], int first, int last) 
{
    int  p = first;
    long pivotElement = a[first];
 
    for(int i = first+1 ; i <= last ; i++)
    {
        /* If you want to sort the list in the other order, change "<=" to ">" */
        if(a[i] <= pivotElement)
        {
            p++;
            swap(a[i], a[p]);
        }
    }
 
    swap(a[p], a[first]);
 
    return p;
}
 
 
/**
 * Swap the parameters.
 * @param a - The first parameter.
 * @param b - The second parameter.
*/
void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}
 

vector<long> QuickSortArray(vector<long> nums)
{
	
	 long size = nums.size();
     long *arr = new long[size];
     int i, j, key;
     
     std::copy(nums.begin(), nums.end(), arr);
     
     quickSort( arr, 0, size-1 );
  
    vector<long> vect;
    
    vect.insert( vect.begin() , arr , arr + size );
    
    return vect; 
     
	
	
}

//=====================================================================================

// Quick Sort list
//=====================================================================================
    
vector<long> QuickSortList(vector<long> nums)
{

    List<long> l;
    ListItem<long> *temp2 = NULL;
    
    for (std::vector<long>::iterator it = nums.begin() ; it != nums.end(); ++it)
    {
        l.insertAtHead(*it);
    }
    
    l.sort();
    
    vector<long> vect;
    
    temp2 = l.getHead();
    while (temp2 != NULL)
    {
        vect.push_back (temp2->value);
        
        temp2 = temp2->next;
    }
    
    return vect;
    
    
}

//====================================================================================================
// heapsort functions

    void Swap(std::vector<long>& vHeap, std::vector<long>::size_type i, std::vector<long>::size_type j)
{
    if(i == j)
        return;
 
    int temp;
    temp = vHeap[i];
    vHeap[i] = vHeap[j];
    vHeap[j] = temp;
}

 
void Sift(std::vector<long>& vHeap, const std::vector<long>::size_type heapSize, const std::vector<long>::size_type siftNode)
{
    std::vector<long>::size_type i, j;
 
    j = siftNode;
    do
    {
        i = j;
        if(((2*i + 1) < heapSize) && vHeap[j] < vHeap[2*i + 1])
            j = 2*i + 1;
        if(((2*i + 2) < heapSize) && vHeap[j] < vHeap[2*i + 2])
            j = 2*i + 2;
 
        Swap(vHeap, i, j);
    }
    while(i != j);
}
 
void MakeInitialHeap(std::vector<long>& vHeap)
{
    for(int i = vHeap.size() - 1; i >= 0; --i)
    {
        Sift(vHeap, vHeap.size(), i);
    }
}
 
void Heap_Sort(std::vector<long>& vHeap)
{
    MakeInitialHeap(vHeap);
    for(std::vector<long>::size_type i = vHeap.size()-1; i > 0; --i)
    {
        Swap(vHeap, i, 0);
        Sift(vHeap, i, 0);
    }
}




//=====================================================================================
vector<long> HeapSort(vector<long> nums)
{
    Heap_Sort(nums);
    
    return nums;
}


//=====================================================================================

//  BucketSort functions


void BucketSort (long a [], unsigned int n)
{
     long *buckets = new long[n];

    for ( int j = 0; j < n; ++j)
    buckets [j] = 0;
    for ( int i = 0; i < n; ++i)
    ++buckets [a [i]];
    for ( int i = 0, j = 0; j < n; ++j)
    for ( int k = buckets [j]; k > 0; --k)
        a [i++] = j;
}


vector<long> BucketSort(vector<long> nums, int size)
{
    
     size = nums.size();
     long *arr = new long[size];
     long *table = new long[size];
     int i, j, key;
     
     std::copy(nums.begin(), nums.end(), arr);

	
    BucketSort (arr,size);
    
    vector<long> vect;
    vect.insert( vect.begin() , arr , arr + size );
    
    return vect; 

     
}

#endif
