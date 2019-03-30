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
 `
- For the results of 
