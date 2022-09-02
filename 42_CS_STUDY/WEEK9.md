# Page 교체 알고리즘

필요한 페이지가 메모리에 없을 때 page-fault가 발생하고 Backing Store에서 해당 페이지를 찾아 빈 프레임에 로딩해햐하는데, 이때 빈 프레임이 없을 경우 희생 당할  프레임을 고르는 알고리즘이 페이지 교체 알고리즘

페이지 교체 알고리즘의 목표는 page-fault 발생 비율을 줄이는 것

## FIFO

![FIFO](https://blog.kakaocdn.net/dn/bGqpiD/btrpdovhuvd/9JIyEkk7DUmK6uCeO2ud40/img.png)
- FIFO 알고리즘은 이름 그대로 가장 먼저 메모리에 올라온 페이지를 가장 먼저 내보내는 알고리즘
- 구현이 간단하지만 성능은 좋지 않음
- 메모리에 적재된 시간을 저장하거나 큐를 이욯해 저장할 수 있음.
- Belady's Anomaly 현상이 발생할 수 있음

* Belady's Anomaly
일반적으로 생각했을 때 사용하는 page frame이 많아질 수록 page fault가 덜 발생할 것이라고 예측하지만 이런 예측과는 다르게 page frame이 높아도 page fault가 더 많이 발생하는 경우가 생기는데 이를 belady's anomaly라고 함
![example](https://mblogthumb-phinf.pstatic.net/data42/2008/11/11/49/belady%2527s-anomaly_cookatrice.gif?type=w800)

## OPT(Optimal) 알고리즘

![OPT](https://blog.kakaocdn.net/dn/etkbwZ/btro8wOpRuo/yrVmZdpsBI8PienpO92bc0/img.png)

