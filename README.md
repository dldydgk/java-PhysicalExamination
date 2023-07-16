# java-PhysicalExamination
Java를 사용하여 신체검사 데이터용 클래스 배열에서 평균 키와 시력의 분포를 구현하기

## 1. 클래스 PhyscDate를 선언하여 이름, 키, 시력을 생성자를 통하여 전달 받는다
## 2. 생성자 PhyscData를 호출하면 기존에 있던 멤버변수와 변수명이 같기 때문에 this를 사용하여 구분할 수 있게 한다
``` java
static class PhyscDate {
		String name;
		int height;
		double vision;
		
		PhyscDate(String name, int height, double vision) {
			this.name = name;
			this.height = height;
			this.vision = vision;
		}
	}
```
PhyscDate 의 클래스로부터 생성된 객체를 가진 배열들
``` java

PhyscData[] pd = {
                new PhyscData("강민하", 162, 0.3),
                new PhyscData("김찬우", 173, 0.7),
                new PhyscData("박준서", 175, 2.0),
                new PhyscData("유서범", 171, 1.5),
                new PhyscData("이수연", 168, 0.4),
                new PhyscData("장경오", 174, 1.2),
                new PhyscData("황지안", 169, 0.8),
        };
```


 매개변수를 통하여 PhyscDate 의 클래스로 부터 생성된 객체를 가진 배열이 매개변수를 통하여 전달 받아 평균 키를 구하는 코드 입니다

``` java
static double aveHeight(PhyscDate[] dat) {
		double sum = 0;
		
		for(int i = 0; i<dat.length; i++) 
			sum += dat[i].height;
		return sum / dat.length;	}
```
final을 사용하여 상수를 만들고 그 상수를 사용하여 시력의 분포를 저장할 배열을 만든다
0.0 ~2.0까지 총 21개의 배열이 필요하다.
``` java
int[] vdist = new int[VMAX];
다음은 학생들의 시력의 값이 담겨있는 배열과 시력의 분포를 저장할 배열을 distVision메소드의 매개변수로 보냅니다.

distVision 메소드는 for문을 이용하여 dist의 모든 방을 0으로 초기화 시킨뒤 다시 for문을 사용하여 dat[i].vision의 10배 즉 vdist의 3번방을 ++하여 시력 분포를 구합니다.

public static void main(String[] args) {
        System.out.println("시력 분포 : ");
        distVision(pd, vdist);
        for (int i = 0; i < vdist.length; i++) {
            if (vdist[i] != 0) {
                System.out.println((double) i / 10 + " / " + vdist[i]);
            }
        }
    }
    static void distVision(physicalExamination.PhyscData[] dat, int[] dist) {
        for(int i =0; i < dat.length; i++){
            dist[i] = 0;
        }
        for (int i = 0; i < dat.length; i++) {
            dist[(int) (dat[i].vision * 10)]++;
        }
    }
```
풀코드
``` java
import java.util.Scanner;

public class PhysicalExamination {
    static final int VMAX = 21;

    static class PhyscData {
        String name;
        int height;
        double vision;

        PhyscData(String name, int height, double vision) {
            this.name = name;
            this.height = height;
            this.vision = vision;
        }
    }

    static double avgHeight(PhyscData[] dat) {
        double sum = 0;
        for (int i = 0; i < dat.length; i++) {
            sum += dat[i].height;
        }
        return sum / dat.length;
    }

    static void distVision(PhyscData[] dat, int[] dist) {
        for(int i =0; i < dat.length; i++){
            dist[i] = 0;
        }
        for (int i = 0; i < dat.length; i++) {
            dist[(int) (dat[i].vision * 10)]++;
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        PhyscData[] pd = {
                new PhyscData("강민하", 162, 0.3),
                new PhyscData("김찬우", 173, 0.7),
                new PhyscData("박준서", 175, 2.0),
                new PhyscData("유서범", 171, 1.5),
                new PhyscData("이수연", 168, 0.4),
                new PhyscData("장경오", 174, 1.2),
                new PhyscData("황지안", 169, 0.8),
        };

        int[] vdist = new int[VMAX];

        System.out.println("신체검사 리스트");
        for (int i = 0; i < pd.length; i++) {
            System.out.printf("이름 : %s , 키 : %d , 시력 : %.1f \n", pd[i].name, pd[i].height, pd[i].vision);
        }
        System.out.printf("키의 평균 : %.1f\n", avgHeight(pd));

        System.out.println("시력 분포 : ");
        distVision(pd, vdist);
        for (int i = 0; i < vdist.length; i++) {
            if (vdist[i] != 0) {
                System.out.println((double) i / 10 + " / " + vdist[i]);
            }
        }
    }
}
```

