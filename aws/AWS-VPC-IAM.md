# AWS VPC IAM



> *Virtual Private Cloud*(VPC)는 사용자의 AWS 계정 전용 가상 네트워크입니다. VPC는 AWS 클라우드에서 다른 가상 네트워크와 논리적으로 분리되어 있습니다. Amazon EC2 인스턴스와 같은 AWS 리소스를 VPC에서 실행할 수 있습니다. IP 주소 범위와 VPC 범위를 설정하고 서브넷을 추가하고 보안 그룹을 연결한 다음 라우팅 테이블을 구성합니다.







만들기 전에 vpc 설정. 가장 먼저 해야한다. 네트워크를 설정하는 것이다.



![image](https://user-images.githubusercontent.com/29794325/48182352-3468ef00-e36e-11e8-8d66-e544b72cc7c1.png)



간단하게 vpc 생성 마법사를 통해 만들자. (start VPC Wizard 버튼을 누른다.)



> *VPC : virtual private cloud*















single public network는 간단한거 만들 때 쓴다. 우리가 쓸 것은 **Public and Private Subnet**이다.



![image](https://user-images.githubusercontent.com/29794325/48182429-73974000-e36e-11e8-85bc-aa9f7b090070.png)



public subnet과 private subnet을 나눠준다. private subnet은 <u>외부와 접속을 할 때</u> **NAT 게이트웨이**를 이용해서 접속을 한다.



> NAT(*Network Address Translation*): 외부 네트워크를 뚫어주는 용도















### 연습용으로 스테이징1이라는 VPC환경을 만들어보기







> 첫번째 row의 IPv4 CIDR은 default로 각 리전마다 하나씩 준다.



![image](https://user-images.githubusercontent.com/29794325/48182456-8a3d9700-e36e-11e8-9786-d57dfde8136b.png)



1. IPv4 CIDR의 안겹치는 것으로 만든다. `10.3.0.0/16` 으로 해보자 그리고 VPC name도 입력한다.



![image](https://user-images.githubusercontent.com/29794325/48182476-9de8fd80-e36e-11e8-8266-574af670a706.png)













2. public subnet의 IP에 인터넷 게이트웨이와 엘라스틱 노드밸런서가 들어간다. 그리고 외부에서 바로 접속 가능한 ssh 전용 호스트를 넣는다.



   > CIDR 구조를 보면, 전체 VPC CIDR에서 밑의 것으로 들어간다. 그 구조를 따라야 한다.



![image](https://user-images.githubusercontent.com/29794325/48182497-bb1dcc00-e36e-11e8-98d5-4f1c35ed717c.png)



IPv4 CIDR block은 하나의 network를 구성한 것이고, 내부에서 public subnet과 private subnet을 구분한다.



public subnet도 위와 같은 ip 주소를 갖는다. (위에서는 `10.3.0.0/24`) 이 내부에서 외부로 접속하기 위해서 인터넷 게이트를 달면 되는 것이다. 이 네트워크 자체가 외부와 연결되는 것은 아니다.











3. Availability 선택하기



   > 리전이 있고 리전 내부에서도 Availability Zone이 두개로 나뉘어 진다.(zone a, zone c가 나누어 짐)

   >

   > 예를들어, 한국의 서울 리전이 있고 a라는 데이터센터와 c라는 데이터센터가 있다. 그게 바로 availability zone이다. a가 다운되어도 c가 살아있다. (마법사에서는 1개 밖에 설정 못하는데, 생성을 완료한 다음에 추가하면 된다.)



![image](https://user-images.githubusercontent.com/29794325/48182522-cb35ab80-e36e-11e8-9814-2d1a047df534.png)











4. NAT 게이트웨이 설정



   > private 서브넷에서 쓴다. 예를들면, private 서브넷에 있는 인스턴스들이 업데이트를 해야하는 경우가 있다. (우분투 같은 것) 그런데 private에 있으면 <u>인터넷 접속이 안된다</u>. 업데이트를 할 수 있는 길이 없다. 그럴때  **NAT 게이트웨이를 통해서 업데이트 할 수 있다.** 



   NAT 게이트웨이는 고유한 IP가 필요하다. 이 과정에서 미리 Elastic IP를 설정 해 주어야 한다.







   4-1 VPC 대시보드의 Elastic IPs 에서 new Address 버튼을 눌러 생성한다.



   ![image](https://user-images.githubusercontent.com/29794325/48182534-dd174e80-e36e-11e8-9e3c-b8e09a5b0f96.png)

   ![image](https://user-images.githubusercontent.com/29794325/48182559-f0c2b500-e36e-11e8-9e5b-27e26f154f52.png)







4-2 Elastic IP에 새로 생성한 Allocation ID를 입력한다.



![image](https://user-images.githubusercontent.com/29794325/48182577-00da9480-e36f-11e8-85ea-6101b9fe608a.png)







<u>그리고 create VPC 버튼을 누르면 VPC가 완성이 된다!</u>











5. 추가 작업들



Subnets를 보면, create Subnet 버튼이 있다.



![image](https://user-images.githubusercontent.com/29794325/48182588-118b0a80-e36f-11e8-9bf7-109a5cd19923.png)







Name tag는 최대한 자세하게 써주는 것이 좋다.



![image](https://user-images.githubusercontent.com/29794325/48182613-22d41700-e36f-11e8-9f6a-16b907112980.png)







그리고,  아까 선택하지 못한 나머지 Availability Zone을 선택하고, CIDR block은 기존의 것들과 겹치지 않게 작성해준다.



![image](https://user-images.githubusercontent.com/29794325/48182631-37b0aa80-e36f-11e8-927d-7651721a246b.png)



추가하면 완료!











### Route Table



> 자기 네트워크(사진에서는 `10.3.0.0/16`)로 오는 request는 자기 네트워크 내에서 돌려주고

>

> 그 외(사진에서는 `0.0.0.0/0`)는 전부 인터넷 게이트웨이(사진에서는 `igw-fd24b794`)로 보내준다.



![image](https://user-images.githubusercontent.com/29794325/48182639-45fec680-e36f-11e8-8f14-3ddbe74e0049.png)















### IAM 만들기



> 아마존 aws의 리소스에 접근하거나 수정할 수 있는 권리를 가진 유저를 만들어야 한다. 



이 유저는 ec2가 쓰는 것이다. 서버가 쓰는 어카운트이다. 서버가 s3에 접근해야 해서 그 접근 권한이 있어야 한다. 접근 권한을 가진 어카운트를 만든 다음 할당해야 한다.



정확한 용어는 role 이다. role을 만든 다음에, role을 ec2에 할당해 주면 ec2는 그 role을 가지고 s3에 접근할 수 도 있고, rds에도 접근할 수 있는, 그런 접근 권한을 가질 수 있다.







- 서비스별로, 배포 환경별로 role을 만든다.



  >  지역별이 아닌 이유는,  지역 자체도 aws 리소스 이다. 그래서 따로 두지 않는다.











1. s3 버켓을 만든다.

> 버켓 네임, region을 설정한다.



![image](https://user-images.githubusercontent.com/29794325/48182651-54e57900-e36f-11e8-8e80-42f1635b1dcb.png)







2. policy를 만든다



   ![image](https://user-images.githubusercontent.com/29794325/48182661-63cc2b80-e36f-11e8-8f62-b788d1319f60.png)







​	2-1 policy generator를 이용해서 손쉽게 만들 수 있다.



![image](https://user-images.githubusercontent.com/29794325/48182675-79415580-e36f-11e8-9c8d-72fe72164942.png)







​	2-2 AWS Service는 S3를 선택하고, action은 선택할 수 있다. resource name도 입력한다



![image](https://user-images.githubusercontent.com/29794325/48182705-8cecbc00-e36f-11e8-927e-afada7ba4a51.png)







### 추가로 읽으면 좋을 아티클 



- Amazon VPC란 무엇인가? https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/what-is-amazon-vpc.html


