---
layout : posts
title : 버블정렬(Bubble Sorting)
categories :
 - SORTING
tag :
 - SORTING
---

## __버블정렬(Bubble Sorting)__
---
`버블정렬(Bubble Sorting)`은 배열에서 인접한 인덱스의 값을 비교하여 오름차순 또는 내림차순으로 정렬하는 방법입니다.<br>

## __버블정렬 알고리즘(Bubble Sorting Algorithm)__
---
- 배열의 처음부터 인접한 두 인덱스의 값 비교한다.
- (n 번째 값 > n+1 번째) => 자리를 바꾼다.
- (n 번째 값 < n+1 번째) => 자리를 바꾸지 않는다.
- 정렬이 완료될 때 까지 반복한다 (배열길이 - 1)번

![bubble-sort-image](https://t1.daumcdn.net/cfile/tistory/216BA54B5356472E1D)


## __버블정렬 예시(Bubble Sorting Example)__
---
```java
//bubble sort
for(int p=0; p<ret.length-1; p++){
	System.out.println((p+1) + "회전");

	for(int i=0; i<ret.length-1-p; i++) {

		if(ret[i] > ret[i+1]) {
			int temp = ret[i+1];
			ret[i+1] = ret[i];
			ret[i] = temp;
		}
    }
 }
     
```
바깥에 있는 반복문은 비교횟수를 정해주는 것입니다.<br>
버블정렬은 한 번에 두개의 인덱스값을 비교하므로 반복횟수는 `(배열길이-1)`번입니다.<br><br>
안쪽에 있는 반복문에서 조건문을 보면 반복횟수가 하나씩 줄어드는 것을 알 수 있습니다.<br>
왜냐하면, 오름차순정렬을 하는경우 배열의 처음부터 끝까지 비교를 마치면(1회전을 마치면) 가장 큰 값이 배열의 끝에 `확정`되게 됩니다.<br>
따라서 1회전을 마칠때 마다 `확정`된 값이 생기고, 그 값은 더 이상 비교할 필요가 없어지는 것입니다<br>
이러한 `확정`을 통해서 불필요한 반복횟수를 줄일 수 있습니다.

`[버블정렬 인접한 인덱스 비교]`
```java
if(ret[i] > ret[i+1]) {
	int temp = ret[i+1];
	ret[i+1] = ret[i];
	ret[i] = temp;
}
```
배열의 인접한 인덱스를 비교하는 부분입니다.<br>
이 부분은 매우 간단합니다.<br>
이 예제의 경우 오름차순이기 때문에 인접한 두 인덱스를 비교하고, 더 큰 값을 뒤로 보내주는 작업을 반복하는 것입니다<br>
