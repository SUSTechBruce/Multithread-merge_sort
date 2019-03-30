# report of Multithread_merge_sort

## 1.implementation ideas

- In this lab, I used OpenMP to implement Multithread merge sort, because OpenMP will help me parallelly execute the specific 
 code automatically, it is easy to use and understand, so, here are the concrete methods :

<pre><code>
#pragma omp parallel for   // 在sort部分使用OpenMP
    for (i = 0; i < length/2; i++)
        if (data[i*2] > data[i*2+1]) {
            t = data[i*2];
            data[i*2] = data[i*2+1];
            data[i*2+1] = t;
        }
//merge(arr,l,mid,r);
//merge-----------------------------------------------------------------
    for (i = 2; i < right; i *= 2) {
        #pragma omp parallel for  // 在merge部分使用OpenMP
        for (j = 0; j < right-i; j += i*2) {
             int end = 0;
             if(right > j+i*2){
             end = 2*i+j;
            }else{
             end = right;
}
            merge(j, j+i, end, data, temp);
        }
    }
</code></pre>

## 2. use tables or figures to illustrate your experiment results.
 In the lab, I use a small data to test the performance
 `
 {32,12,56,78,76,45,36,66,44,24,47,11,23,56,89,2,6,1,19,20,10,9,8,7,6,5,4,3,2,1};
 `
- For the results of single thread algorithm(without OpenMP)
![image](https://github.com/SUSTechBruce/Multithread-merge_sort/blob/master/result1.png)

- For the results of multithread algorithm
![image](https://github.com/SUSTechBruce/Multithread-merge_sort/blob/master/result2.png)

- compare the performance difference between single thread and multiple threads.
  Accodring to the results of single and multithread algorithms.
  
Thread               |Average time
------------------|--------
single thread      |36ms
multithread         |8s

-  analyze the relationship between the number of threads and overall performance.
 The multithread code resembles single threads code except openMP methods.
 
- analyze the margin gain2 while every new thread adding into the program.
  For the openMP, Because the timing of thread startup and completion is uncertain, it is not possible to know in advance which thread an iteration is assigned to.

