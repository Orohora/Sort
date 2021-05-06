# 정렬 알고리즘 성능평가

## 1.1 버블정렬

#### 버블 정렬(Bubble Sort)은 이웃하는 숫자를 비교하여 자은 수를 앞쪽으로 이동시키는 과정을 반복하여 정렬하는 알고리즘이다. 오름차순으로 정렬한다면, 작은 수는 배열의 앞부분으로 이동하는데, 배열을 좌우가 아니라 상하로 그려보며 정렬하는 과정에서 작은 수가 마치 '거품'처럼 위로 올라가는 것을 연상케 한다.



## 1.2 버블정렬 알고리즘

입력: 크기가 n인 배열 A

출력: 정렬된 배열 A

for pass=1 to n-1

​	for i-1 to n-pass

​		if(A[i-1]>A[i])

​			A[i-1]<->A[i]

return 배열 A

### STEP 1

```
 System.out.println("행렬의 크기를 입력하세요");
        int n=scanner.nextInt();
        int A[]=new int[n];

        System.out.println("A의 행렬 값을 입력하세요");
        for(int i=0;i<n;i++) {
            A[i]=scanner.nextInt();
        }
```

#### 크기가 n인 배열을 입력받는다.



### STEP 2

```
int size=a.length;
        for(int i=1; i<size; i++) {
```

#### for 루프문을 통하여 패스 과정을 수행하는데 여기서 i는 pass의 값을 size는 배열의 크기 n에 해당된다.



### STEP 3

```
for(int j=1; j<size-i+1; j++) {
                if(a[j-1] > a[j]) {
                    swap(a,j-1,j);
                }
                System.out.printf("\n\t");
                for(int k=0;k<a.length;k++) {
                    System.out.printf("%3d ", a[k]);
                }

            }
```

#### 이웃하는 원소를 비교하는 과정인데 A[0] 부터 A[n-pass]까지 비교한다. 이때 if문의 조건인 a[j-1]>a[j]를 만족하면 서로의 값을 바꿔주고 그렇지 않는다면 반복문을 계속 진행시킨다.



## 1.3 전체코드 

```
import java.util.Scanner;
public class bubble {

    public void bubbleSort(int a[]) {
        int size=a.length;
        for(int i=1; i<size; i++) {
            System.out.printf("\n패스 %d  : ", i);
            for(int j=1; j<size-i+1; j++) {
                if(a[j-1] > a[j]) {
                    swap(a,j-1,j);
                }
                System.out.printf("\n\t");
                for(int k=0;k<a.length;k++) {
                    System.out.printf("%3d ", a[k]);
                }

            }
        }
        System.out.println();
    }

    public  void swap(int a[], int x, int y) {
        int temp = a[x];
        a[x] = a[y];
        a[y] = temp;
    }




    public static void main(String args[])
    {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        bubble s=new bubble();


        System.out.println("행렬의 크기를 입력하세요");
        int n=scanner.nextInt();
        int A[]=new int[n];

        System.out.println("A의 행렬 값을 입력하세요");
        for(int i=0;i<n;i++) {
            A[i]=scanner.nextInt();
        }

        s.bubbleSort(A);


        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);
    }
}
```



## 1.4 코드 실행결과 및 성능 (교재 P201 예제)

<img width="651" alt="버블정렬" src="https://user-images.githubusercontent.com/80919306/117232327-e3151a00-ae5b-11eb-9052-7f8e65efb87c.PNG">

pass=1이면 n-1, pass=2이면 n-2 비교하므로..... 총 비교 횟수는 (n-1)+(n-2)+ ... +1=n(n-1)/2이므로 버블정렬 알고리즘의 시간복잡도는 다음과 같이 표현할 수 있다.

n(n-1)/2 x O(1) = O(n^2) x O(1) = O(n^2)



## 2.1 선택 정렬

선택 정렬(Selection Sort)은 입력 배열 전체에서 최솟값을, '선택'하여 배열의 0번 원소와 자리를 바꾸고, 다음에는 0번 원소를 제외한 나머지 원소에서 최솟값을 선택하여, 배열의 1번 원소와 자리를 바꾼다. 이러한 방식으로 마지막에 2개의 원소 중에서 작은 값을 선택하여 자리를 바꿈으로써 오름차순 정렬을 마친다.



## 2.2 선택 정렬 알고리즘

입력: 크기가 n인 배열 A

출력: 정렬된 배열 A

1. for i = 0 to n-2 {

2. min = i

3. for j = i+1 to n-1 {  // A[i]~A[n-1]에서 최솟값을 찾는다.

4. if (A[j] < A[min]) 

5. min = j

​     }

6. A[i] ↔ A[min]   // min이 최솟값이 있는 원소의 인덱스

  }

7. return 배열 A

### STEP 1 배열의 입출력 (위와 동일하니 생략)



### STEP 2

```
for(int i=0; i<a.length-1; i++) {
            int min = i;
            for(int j=i+1; j<a.length; j++) {
                if(a[j] < a[min]) {
                    min = j;
                }
            }
```

#### a.length가 배열 A의 크기 n이므로 i가 0부터 n-2까지 배열할때 배열 A[i] 에서 최솟값을 구하고 원소의 인덱스가 min에 저장된다.



### STEP 3

```
swap(a, min, i);
            System.out.printf("\n선택 정렬 %d 단계 : ", i+1);
            for(int k=0;k<a.length;k++) {
                System.out.printf("%3d ", a[k]);
            }
        }
```

#### for 루프에서 찾은 최솟값 A[min]을 A[i]와 교환하는데 for 반복문에 의해 루프한다.



## 2.3 전체코드

```
import java.util.Scanner;
public class selection {


    public void SelectionSort(int a[]) {

        for(int i=0; i<a.length-1; i++) {
            int min = i;
            for(int j=i+1; j<a.length; j++) {
                if(a[j] < a[min]) {
                    min = j;
                }
            }
            swap(a, min, i);
            System.out.printf("\n선택 정렬 %d 단계 : ", i+1);
            for(int k=0;k<a.length;k++) {
                System.out.printf("%3d ", a[k]);
            }
        }
        System.out.println();
    }




    public  void swap(int a[], int x, int y) {
        int temp = a[x];
        a[x] = a[y];
        a[y] = temp;
    }




    public static void main(String args[])
    {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        selection s=new selection();


        System.out.println("행렬의 크기를 입력하세요");
        int n=scanner.nextInt();
        int A[]=new int[n];

        System.out.println("A의 행렬 값을 입력하세요");
        for(int i=0;i<n;i++) {
            A[i]=scanner.nextInt();
        }


        s.SelectionSort(A);

        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);
    }
}
```



## 2.4 코드 실행결과 및 성능

<img width="470" alt="선택정렬" src="https://user-images.githubusercontent.com/80919306/117232306-dc86a280-ae5b-11eb-9923-7b7a7db7e770.PNG">

#### 선택정렬은 for 루프가 (n-1)번 수행되는데 i=0일 때 (n-1), i=1일 때 (n-2)번... 마지막으로 1번 수행되므로 (n-1)+(n-2)+...+2+1=n(n-1)/2이고 if 조건이 참일 때 자리바꿈으로 O(1)의 시간이 걸리므로 선택 정렬의 시간복잡도는 n(n-1)/2*O(1)=O(n^2)이다.



## 3.1 삽입 정렬

#### 삽입 정렬(Insertion Sort)은 배열을 정렬된 부분(앞부분)과 정렬이 안 된 부분(뒷부분)으로 나누고, 정렬이 안 된 부분의 가장 왼쪽 원소를 정렬된 부분의 적절한 위치에 삽입하여 정렬되도록 하는 과정을 반복한다.



## 3.2 삽입 정렬 알고리즘

1. for i = 1 to n-1 {

2. CurrentElement = A[i] // 정렬 안된 부분의 가장 왼쪽원소

3. j ← i – 1  // 정렬된 부분의 가장 오른쪽 원소로부터 왼쪽 방향으로 삽입할 곳을 탐색하기 위하여 

4. while (j >= 0) and (A[j] > CurrentElement) {

5. A[j+1] = A[j]  // 자리 이동

6. j ← j -1

​    }

7. A [j+1] ← CurrentElement

  }

8. return A



### STEP 1 입출력 배열 (위와 동일하니 생략)



### STEP 2 

```
int n = a.length;
        for(int i=1; i<n; i++) {
            int CurrentElement = a[i];
            int j = i-1;
```

정렬된 부분가 그렇지 않는 부분을 나누기 위해 정렬이 안 된 부분의 가장 왼쪽에 있는 원소인 A[i]를 CurrentElement로 놓는다. 또한 j=i-1로 정의한 이유는 j가 정렬된 부분의 가장 오른쪽 원소의 인덱스가 되어 왼쪽 방향으로 삽입할 곳을 탐색하기 위해서다.



### STEP 3

```
while((j>=0) && (a[j]>CurrentElement)) {
                a[j+1] = a[j];
                j--;
            }
```

#### a[j]>CurrentElement는 a[j]가 CurrentElement보다 크면 a[j]를 오른쪽으로 1칸 이동시키기 위해서이다. 이러한 자리이동은 j를 1만큼 감소시켜서 바로 왼쪽 원소에 대한 while 루프를 반복적으로 수행하기 위함이다.



### STEP 4

```
a[j+1] = CurrentElement;
            System.out.printf("\n삽입정렬 %d 단계 : ",i);
            for(int k=0;k<a.length;k++) {
                System.out.printf("%3d ", a[k]);
            }
```

#### while 루프가 끝난 직후에는 a[j]가 CurrentElement보다 크기 않으므로 a[j]의 오른쪽인 a[j+1]에 CurrentElement를 삽입해야 하기 때문에 a[j+1]에 CurrentElement를 저장한다.



## 3.3 전체 코드

```
import java.util.Scanner;
public class insertion {


    public void InsertionSort(int a[]) {
        int n = a.length;
        for(int i=1; i<n; i++) {
            int CurrentElement = a[i];
            int j = i-1;
            while((j>=0) && (a[j]>CurrentElement)) {
                a[j+1] = a[j];
                j--;
            }

            a[j+1] = CurrentElement;
            System.out.printf("\n삽입정렬 %d 단계 : ",i);
            for(int k=0;k<a.length;k++) {
                System.out.printf("%3d ", a[k]);
            }
        }
        System.out.println();
    }




    public  void swap(int a[], int x, int y) {
        int temp = a[x];
        a[x] = a[y];
        a[y] = temp;
    }




    public static void main(String args[])
    {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        insertion s=new insertion();


        System.out.println("행렬의 크기를 입력하세요");
        int n=scanner.nextInt();
        int A[]=new int[n];

        System.out.println("A의 행렬 값을 입력하세요");
        for(int i=0;i<n;i++) {
            A[i]=scanner.nextInt();
        }


        s.InsertionSort(A);

        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);
    }
}
```



## 3.4 코드 실행결과 및 성능

<img width="492" alt="삽입정렬" src="https://user-images.githubusercontent.com/80919306/117232268-c7aa0f00-ae5b-11eb-8693-f211a8d9992a.PNG">

삽입 정렬은 for 루프가 (n-1)번 수행되는데, i=1일 때 while 루프는 1번 수행되고, i=2일 때 최대 2번 수행되고, 마지막으로 최대(n-1)번 수행되므로, while 루프 내부에서 수행되는 총 횟수는 1+2+3+....+(n-2)+(n-1)=n(n-1)/2이다. while 루프 내부의 수행시간 O(1)이므로 삽입 정렬의 시간복잡도는 n(n-1)/2*O(1)=O(n^2)이다



## 4.1 쉘 정렬

#### 쉘 정렬(Shell Sort)은 삽입 정렬을 이용하여 배열 뒷부분의 작은 숫자를 앞부분으로 빠르게 이동시키고, 동시에 큰 숫자는 뒷부분으로 이동시키며, 가장 마지막에는 삽입 정렬을 수행한다.



## 4.2 쉘 정렬 알고리즘

입력: 크기가 n인 배열 A

출력: 정렬된 배열 A



1. for each gap h = [ h0>h1>...>hk=1] // 큰 gap부터 차례로

2. for i = h to n-1 { 

3. CurrentElement=A[i];

4. j = i;

5. while (j>=h) and (A[j-h]>CurrentElement) {

6. A[j]=A[j-h];

7. j=j-h;

​      }

8. A[j]=CurrentElement;

  }

9. return 배열 A



### STEP 1

```
 int n=a.length;
        for(int gap=5;gap>=1;gap--) {
            for (int i = gap; i < n; i++) { //i=10
```

#### 쉘 간격의 크기(gap)을 미리 정해야 한다. 주어진 코드의 경우는 gap의 크기를 5로 정하고 1일 될때까지 루프를 통하여 반복시키도록 하였다.



### STEP 2

```
int CurrentElement = a[i]; //CurrentElement=a[10]=50
                int j = i;
                while ((j >= gap) && (a[j - gap] > CurrentElement)) { //a[5]=80
                    a[j] = a[j - gap];
                    j = j - gap;
                }

                a[j] = CurrentElement;
```

#### 간격의 크기 gap에 대한 삽입 정렬이 수행되는데 그룹별로 삽입 정렬을 수행하지만 자리바꿈을 위한 원소 간의 비교도 동시에 진행된다. while문의 첫 번째 조건(j>=h)는 j가 h보다 작으면 배열 인덱스가 음수가 되어, 배열의 범위를 벗어나는 것을 검사하기 위한 것이다.

## 4.3 전체 코드

```
import java.util.Scanner;
public class shell {


    public void ShellSort(int a[]) {
        int n=a.length;
        for(int gap=5;gap>=1;gap--) {
            for (int i = gap; i < n; i++) { //i=10
                int CurrentElement = a[i]; //CurrentElement=a[10]=50
                int j = i;
                while ((j >= gap) && (a[j - gap] > CurrentElement)) { //a[5]=80
                    a[j] = a[j - gap];
                    j = j - gap;
                }

                a[j] = CurrentElement;

            }
            System.out.printf("\nh=%d일때 : ", gap);
            for (int k = 0; k < a.length; k++) {
                System.out.printf("%3d ", a[k]);
            }
            System.out.println();
        }

    }

    public  void swap(int a[], int x, int y) {
        int temp = a[x];
        a[x] = a[y];
        a[y] = temp;
    }




    public static void main(String args[])
    {
        long beforeTime = System.currentTimeMillis();
        Scanner scanner=new Scanner(System.in);
        shell s=new shell();


        System.out.println("행렬의 크기를 입력하세요");
        int n=scanner.nextInt();
        int A[]=new int[n];

        System.out.println("A의 행렬 값을 입력하세요");
        for(int i=0;i<n;i++) {
            A[i]=scanner.nextInt();
        }


        s.ShellSort(A);

        long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
        long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
        System.out.println("시간차이(m) : "+secDiffTime);
    }
}
```



## 4.4 코드실행 결과 및 성능

<img width="580" alt="쉘정렬" src="https://user-images.githubusercontent.com/80919306/117232245-bd881080-ae5b-11eb-9580-c57e4c1ab803.PNG">

#### 쉘 정렬의 최악 경우의 복잡도는 O(n^2)이다. 히바드(Hibbard)의 간격인 2^k-1을 사용하면, 쉘 정렬의 시간복잡도는 O(n^1.5)이 된다고 밝혀졌다. 또한 다양한 실험을 통한 쉘 정렬의 시간 복잡도는O(n^1.25)으로 알려지고 있다. 그러나 쉘 정렬의 시간복잡도는 아직  풀리지 않는 문제로 남아 있다. 이는 가장 좋은 간격을 알아내야 하는 것이 선행되어야 하기 때문이다



## 5. 결론

### 각각의 정렬을 코드로 구현해 성능을 분석했을 때 결과값을 통하여 시간복잡도 그래프는 다음과 같이 유추할 수 있다.

<img width="1048" alt="시간복잡도" src="https://user-images.githubusercontent.com/80919306/117232032-5e2a0080-ae5b-11eb-852e-86acd8a9ae7c.PNG">

