## 코사인 유사도 

코사인 유사도는 벡터 간의 거리를 측정하는데, 

그 중에서도 두 벡터의 사잇각을 구해서 유사도(similarity)로 사용하는 것. 

</br>

![200px-Dot_Product.svg](http://euriion.com/wp-content/uploads/2014/09/200px-Dot_Product.svg_.png)

</br>

두 벡터 A와 B 사이의 사잇각 쎄타를 코사인으로 구함

</br>

문서(document)와 검색어(query)의 유사도를 구해서 가장 유사도가 높은 걸 먼저 보여주기 위한 랭킹 혹은 검색(retrieval) 알고리즘으로 사용됨.

군집화에서도 쓰이긴 쓰인다.

 TF-IDF와 같이 쓰임 

</br>

### 전제 조건 for 코사인 유사도

두 벡터의 원소가 모두 양수여야 함.

벡터의 원소 수가 같아야. 불일치할 경우, 0으로 채우든가 해야 한다. 

원소 수 = 축의 개수 

</br>

### 장점

1사분면 상에서 두 벡터의 코사인 값은 [0,1] (두 벡터가 정확히 직교(orthogonal) 하면 0)

rescailing 없이 바로 쓰기 좋음 

</br>

### 공식

![\text{similarity} = cos(\theta) = {A \cdot B \over |A| |B|} = \frac{ \sum\limits_{i=1}^{n}{A_i \times B_i} }{ \sqrt{\sum\limits_{i=1}^{n}{(A_i)^2}} \times \sqrt{\sum\limits_{i=1}^{n}{(B_i)^2}} }](http://s0.wp.com/latex.php?latex=%5Ctext%7Bsimilarity%7D+%3D+cos%28%5Ctheta%29+%3D+%7BA+%5Ccdot+B+%5Cover+%7CA%7C+%7CB%7C%7D+%3D+%5Cfrac%7B+%5Csum%5Climits_%7Bi%3D1%7D%5E%7Bn%7D%7BA_i+%5Ctimes+B_i%7D+%7D%7B+%5Csqrt%7B%5Csum%5Climits_%7Bi%3D1%7D%5E%7Bn%7D%7B%28A_i%29%5E2%7D%7D+%5Ctimes+%5Csqrt%7B%5Csum%5Climits_%7Bi%3D1%7D%5E%7Bn%7D%7B%28B_i%29%5E2%7D%7D+%7D&bg=T&fg=000000&s=0)



분자 : 벡터의 내적 (dot product) - 두 벡터의 각 원소를 짝에 맞춰 곱하고 결과를 더함

분모 :  두 벡터의 크기(norm - 원점에서의 거리)를 구해서 곱함 

</br>

</br>





---

참고

==> 설명이 친절해서 아주 좋음

<http://euriion.com/?p=548> 

