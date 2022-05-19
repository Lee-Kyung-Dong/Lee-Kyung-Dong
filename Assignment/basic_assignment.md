# JAVA 프로그래밍 기초 과제 
## 항해99 부트캠프 ing

### **아래의 정보를 가지는 ‘Bus’ 클래스 모델링**
    - 포함해야 할 정보
        1. 최대 승객수
        2. 현재 승객수
        3. 요금
        4. 버스 번호
        5. 주유량
        6. 현재 속도
        7. 상태
            1.  운행, 차고지 행
    - 기능
        1. 운행
        2. 버스 상태 변경
        3. 승객 탑승
        4. 속도 변경
    
    **요구사항**
    
    - 버스 번호
        - 버스 객체 생성시 번호는 고유값으로 생성되어야 합니다.
    - 버스 상태 변경
        - 버스 객체 생성시 최초 상태는 **‘운행’** 상태가 되며
        - 주유량이 떨어지거나, 운행을 종료할 때 **‘차고지행’** 상태로 변경 합니다.
        - 10미만일 경우 ‘주유가 필요하다’는 메시지를 출력해 주세요
    - 승객 탑승
        - 승객 탑승은 **‘최대 승객수’** 이하까지 가능하며 **‘운행 중’**인 상태의 버스만 가능합니다.
        - 탑승시 현재 승객수가 증가되어야 합니다.
    - 속도 변경
        - 주유 상태를 체크하고 주유량이 10 이상이어야 운행할 수 있습니다.
            - 경고메시지
                - 주유량을 확인해 주세요.
                - print문으로 출력
        - 변경할 속도를 입력 받아 현재 속도에 추가 하거나 뺄 수 있어야 합니다.

### **아래의 정보를 가지는 ‘Taxi’ 클래스 모델링**
    - 포함해야 할 정보
        1. 택시 번호 
        2. 주유량
        3. 현재속도
        4. 목적지 
        5. 기본거리
        6. 목적지까지 거리
        7. 기본 요금
        8. 거리당 요금
        9. 상태 (운행 중, 일반)
    - **기능**
        1. 운행시작
        2. 승객 탑승
        3. 속도 변경
        4. 거리당 요금 추가
        5. 요금 결제
    - **요구 사항**
        - 운행 시작
            - 운행 시작전 주유상태를 체크 하고 주유량이 10 이상이어야 운행 가능
        - 승객탑승
            - 승객 탑승은 택시 상태가 ‘일반'일 때만 가능합니다.
            - 그 외 택시는 ‘탑승 불가’ 처리를 해주세요.
            - ‘일반’ 상태의 택시가 승객을 태우면 ‘운행 중’ 상태로 변경해 주세요
        - 속도 변경
            - 변경할 속도를 입력 받아 현재 속도에 추가 하거나 뺄 수 있어야 합니다.
        - 거리당 요금 추가
            - 기본 거리보다 먼 곳은 추가 요금이 붙습니다.
            - 기본 거리와 추가 요금은 자유롭게 산정해 주세요
        - 요금 결제
            - 최종 요금을 출력하는 것으로 합니다.

### Transportation interface
```JAVA
package assignment;

public interface Transprtation {
    void stop();
    void changeSpeed(int speed);
    void changefuel(int fuel);
}
```

### Bus class
```JAVA
package assignment;

public class Bus implements Transprtation {
    int maxPassengers, currentPassengers, fare, Number, fuel, speed;
    String status;

    //생성자 Taxi()
    //승객탑승 boardPassenger(int people)
    //[주의] run(), stop()은 강제운행

    public Bus() {
        this.maxPassengers = 30;
        this.currentPassengers = 0;
        this.fare = 1000;
        this.Number = (int)(Math.random() * 10000000);
        this.fuel = 100;
        this.speed = 0;
        this.status = "운행";
        System.out.println(Number + "번 버스 생성");
        System.out.println("현재 승객수 : " + currentPassengers);
        System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
        System.out.println("요금 : " + fare);
        System.out.println("주유량 : " + fuel);
        System.out.println("현재 속도 : " + speed);
    }

    public void run() {
        this.status = "운행";
        System.out.println(Number + "번 버스 운행시작");
        System.out.println("현재 승객수 : " + currentPassengers);
        System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
        System.out.println("요금 : " + fare);
        System.out.println("주유량 : " + fuel);
        System.out.println("현재 속도 : " + speed);
        if (fuel < 10) {
            System.out.println("주유가 필요합니다.");
        }
    }

    @Override
    public void stop() {
        this.status = "차고지 행";
        System.out.println(Number + "번 버스 운행 종료 및 차고지 행");
        System.out.println("현재 승객수 : " + currentPassengers);
        System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
        System.out.println("요금 : " + fare);
        System.out.println("주유량 : " + fuel);
        System.out.println("현재 속도 : " + speed);
    }

    public void changeStatus() {
        if (status == "운행") {
            stop();
        } else if (status == "차고지 행") {
            run();
        }
    }

    public void boardPassenger(int people) {
        if (currentPassengers + people >= maxPassengers) {
            System.out.println("최대 승객 수 초과");
        } else if (status.equals("차고지 행")) {
            System.out.println("현재 버스가 운행중이 아닙니다.");
        } else {
            this.currentPassengers += people;
            System.out.println("승객 " + people + "명 탑승");
        }
    }

    @Override
    public void changeSpeed(int speed) {
        if (fuel < 10) {
            System.out.println("주유량을 확인해 주세요.");
        } else if (speed == 0) {
            System.out.println("속도 변화 없음");
        } else {
            this.speed += speed;
            System.out.println(speed > 0 ? speed + "만큼 속도 증가" : -speed + "만큼 속도 감소");
            System.out.println("현재 속도 : " + this.speed);
        }
    }

    @Override
    public void changefuel(int fuel) {
        this.fuel += fuel;
        System.out.println("주유량 : " + this.fuel);
        if (this.fuel < 10) {
            System.out.println("주유가 필요합니다.");
        }
    }
}
```

### Taxi class
```JAVA
package assignment;

public class Taxi implements Transprtation{
    int Number, fuel, speed, basicDistance, totalDistance, basicFare, additionalFare, maxPassengers, currentPassengers;
    String destination, status;

    //생성자 Taxi()
    //승객탑승 및 운행 boardPassenger(int people, int totalDistance, String destination)
    // [주의] run(), stop()은 강제운행

    public Taxi() {
        this.Number = (int)(Math.random() * 10000000);
        this.fuel = 100;
        this.speed = 0;
        this.basicDistance = 1;
        this.totalDistance = 0;
        this.basicFare = 3000;
        this.additionalFare = 1000;
        this.maxPassengers = 4;
        this.currentPassengers = 0;
        this.destination = "";
        this.status = "일반";
        System.out.println(Number + "번 택시 생성");
        System.out.println("현재 승객 수 : " + currentPassengers);
        System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
        System.out.println("목적지 : " + destination);
        System.out.println("기본 거리 : " + basicDistance + "km");
        System.out.println("목적지까지 거리 : " + totalDistance + "km");
        System.out.println("기본 요금 : " + basicFare);
        System.out.println("거리당 추가 요금 : " + additionalFare);
        System.out.println("주유량 : " + fuel);
        System.out.println("현재 속도 : " + speed);
    }

    public void run(int people, int totalDistance, String destination) {
        if (currentPassengers + people >= maxPassengers) {
            System.out.println("최대 승객 수 초과");
        } else if (fuel >= 10) {
            this.totalDistance = totalDistance;
            this.currentPassengers += people;
            this.destination = destination;
            this.status = "운행 중";
            System.out.println(Number + "번 택시 운행 시작");
            System.out.println("현재 승객 수 : " + currentPassengers);
            System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
            System.out.println("목적지 : " + destination);
            System.out.println("기본 거리 : " + basicDistance + "km");
            System.out.println("목적지까지 거리 : " + totalDistance + "km");
            System.out.println("기본 요금 : " + basicFare);
            System.out.println("거리당 추가 요금 : " + additionalFare);
            System.out.println("주유량 : " + fuel);
            System.out.println("현재 속도 : " + speed);

        } else {
            System.out.println("주유가 필요합니다.");
        }
    }

    @Override
    public void stop() {
        this.totalDistance = 0;
        this.currentPassengers = 0;
        this.destination = "";
        this.status = "일반";
        System.out.println(Number + "번 택시 운행 종료");
        System.out.println("현재 승객 수 : " + currentPassengers);
        System.out.println("잔여 승객 수 : " + (maxPassengers - currentPassengers));
        System.out.println("목적지 : " + destination);
        System.out.println("기본 거리 : " + basicDistance);
        System.out.println("목적지까지 거리 : " + totalDistance);
        System.out.println("기본 요금 : " + basicFare);
        System.out.println("거리당 추가 요금 : " + additionalFare);
        System.out.println("주유량 : " + fuel);
        System.out.println("현재 속도 : " + speed);
    }

    public void boardPassenger(int people, int totalDistance, String destination) {
        if (status.equals("운행 중")) {
            System.out.println("탑승 불가");
        } else if (currentPassengers + people >= maxPassengers) {
            System.out.println("최대 승객 수 초과");
        } else {
            System.out.println("승객 " + people + "명 탑승");
            run(people, totalDistance, destination);
        }
    }

    @Override
    public void changeSpeed(int speed) {
        this.speed += speed;
        System.out.println(speed > 0 ? speed + "만큼 속도 증가" : -speed + "만큼 속도 감소");
        System.out.println("현재 속도 : " + this.speed);
    }

    public void pay() {
        if (basicDistance > totalDistance) {
            System.out.println("기본 요금 책정");
            System.out.println("최종 요금 : " + basicFare);
        }
        else {
            System.out.println("추가 요금 발생");
            System.out.println("최종 요금 : " + (additionalFare * (totalDistance - basicDistance) + basicFare));
        }
        stop();
    }

    @Override
    public void changefuel(int fuel) {
        this.fuel += fuel;
        System.out.println("주유량 : " + this.fuel);
        if (this.fuel < 10) {
            System.out.println("주유가 필요합니다.");
        }
    }
}
```