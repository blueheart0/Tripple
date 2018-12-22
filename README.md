Conding Assingment - Triple
===========================
# Coding Assignment 설명
## 실행
1. src/server에서 $ node index.js 입력
2. 예제를 기준으로 원하는 경로 입력 후 'process'를 입력하면 결과 출력
<pre>
4,5
오사카성,2,5
유니버설스튜디오,5,20
도톤보리,1,10
기온,3,20
process

30
</pre>
## 구현 알고리즘
1. 일반적인 Greedy 알고리즘 사용
<pre>
1. 전체 입력 받은 후보지를 만족도 순으로 정렬
2. 정렬 과정에서 만족도가 같은경우 소요시간이 적게 드는 순으로 정렬
    기온,3,20
    유니버설스튜디오,5,20
    도톤보리,1,10
    오사카성,2,5
3. 정렬된 데이터를 순서대로 후보지로 등록, 단, 후보지의 소요시간이 현재 남은 소요시간 보다 클 경우 추가하지 않고 다음 후보지를 탐색
</pre>

# 구현 외 문제
## 특정한 장소를 무조건 방문해야하는 경우
<pre>
1. 가야하는 특정 장소를 먼저 후보지로 등록하고 남은 소요시간 계산
2. 전체 입력 받은 후보지를 만족도 순으로 정렬(이때 후보지로 등록된 장소는 제외)
3. 정렬 과정에서 만족도가 같은경우 소요시간이 적게 드는 순으로 정렬
4. 정렬된 데이터를 순서대로 후보지로 등록, 단, 후보지의 소요시간이 현재 남은 소요시간 보다 클 경우 추가하지 않고 다음 후보지를 탐색
</pre>
## 장소간 이동시간이 주어질때의 고려방법
### 장소간 이동시간이 모두 주어진 경우

1. 장소간 이동시간에 대한 배열을 먼저 만든다.
<table>
    <tr>
        <td>장소</td><td>오사카성</td><td>유니버설스튜디오</td><td>도톤보리</td><td>기온</td>
    </tr>
    <tr>
        <td>오사카성</td><td>INF</td><td>4</td><td>3</td><td>1</td>
    </tr>
    <tr>
        <td>유니버설스튜디오</td><td>3</td><td>INF</td><td>2</td><td>5</td>
    </tr>
    <tr>
        <td>도톤보리</td><td>2</td><td>2</td><td>INF</td><td>6</td>
    </tr>
    <tr>
        <td>기온</td><td>3</td><td>5</td><td>1</td><td>INF</td>
    </tr>
</table>

2. 후보지를 만족도 순으로 정렬한다.
3. 정렬과정에서 만족도가 같은 경우 소요시간이 적게 드는 순으로 정렬한다.
4. 정렬된 데이터의 첫번째 부터 후보지로 등록한다.
5. 등록되지 않은 후보지중 가장 큰 만족도를 주는 곳을 다음 후보지로 선택한다.
    <br/>단, 같은 만족도를 가진 후보지가 여럿 있을 경우, 이동시간에 대한 배열을 참조하여 **현재 위치에서의 이동시간 + 소요시간**의 값으 낮은 곳을 선택한다.
6. 단, 후보지의 **현재 위치에서의 이동시간 + 소요시간**의 값이 현재 남은 소요시간 보다 클 경우 추가하지 않고 다음 후보지를 탐색
### 장소간 이동시간을 매번 확인해야 하는 경우
1. 후보지를 만족도 순으로 정렬한다.
2. 정렬과정에서 만족도가 같은 경우 소요시간이 적게 드는 순으로 정렬한다.
3. 정렬된 데이터의 첫번째 부터 후보지로 등록한다.
4. 등록된 후보지에서 다른 후보지로의 이동시간을 구한다.
4. 등록되지 않은 후보지중 가장 큰 만족도를 주는 곳을 다음 후보지로 선택한다.
    <br/>단, 같은 만족도를 가진 후보지가 여럿 있을 경우, 4.의 과정에서 구한 이동시간을 참조하여 **현재 위치에서의 이동시간 + 소요시간**의 값으 낮은 곳을 선택한다.
6. 단, 후보지의 **현재 위치에서의 이동시간 + 소요시간**의 값이 현재 남은 소요시간 보다 클 경우 추가하지 않고 다음 후보지를 탐색
## 방문하는 순서가 만족도에 영향을 미치는 경우
1. 방문순서에 따른 만족도를 표현하는 배열을 먼저 만든다.
<table>
    <tr>
        <td>장소/방문순서</td><td>1</td><td>2</td><td>3</td><td>4</td>
    </tr>
    <tr>
        <td>오사카성</td><td>5</td><td>4</td><td>6</td><td>20</td>
    </tr>
    <tr>
        <td>유니버설스튜디오</td><td>2</td><td>10</td><td>30</td><td>5</td>
    </tr>
    <tr>
        <td>도톤보리</td><td>1</td><td>5</td><td>9</td><td>10</td>
    </tr>
    <tr>
        <td>기온</td><td>3</td><td>5</td><td>1</td><td>9</td>
    </tr>
</table>

2. 후보지를 방문순서 1의 만족도에 따라 정렬한다.
3. 정렬과정에서 만족도가 같은 경우 소요시간이 적게 드는 순으로 정렬한다.
4. 정렬된 데이터의 첫번째를 등록한다.(단, 소요시간이 남아있는 시간보다 클 경우 다음 후보지를 등록한다)
5. 남은 후보지 데이터를 방문순서 2의 만족도에 따라 정렬한다.
6. 3.에서 5.까지의 과정을 방문순서를 증가하며 수행한다.
