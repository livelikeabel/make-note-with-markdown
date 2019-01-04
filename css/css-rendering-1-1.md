코드스피츠 css 1회차 1/2

기본적인 배경지식

- - 그래픽스 시스템
  - 렌더링 시스템
  - 스페시픽케이션

**Normal Flow**

- CSS의 고유명사이다.

Position : 어떤 지오메트리의 x, y, width, height을 결정할 때 사용하는 추상적인 의미체계. 추상적인 위치를 결정하게 하는 시스템. 

position에는 Static, relative, absolute, fixed, inherit

=> 다 계산 공식이다. 계산하는 컨텍스트. 일종의 계산식.

normal flow는 position이 static이나 relative일 때만 적용이  된다.

**Normal flow****의** **계산** **공식**

- Block formatting contexts (BFC)
- Inline formatting contexts (IFC)
- Relative positioning(normal flow의 일부이지만 position에서 정의하고 있다.)

**//** **공식****,** **원리**

**BFC** : 부모의 가로 길이를 가득 채운 한 줄(x는 항상 0, width는 항상 부모의 width)

**IFC** : 나의 컨텐츠 크기만큼 가로를 차지한다. 

​	- 그 다음 IFC는 이전 IFC의 가로 길이만큼 떨어진 자리에 x가 결정된다. 

​	- inline width의 합이 부모의 width를 넘기면 다음줄로 넘어간다.

​	- 다음줄로 얼마나 넘어가야하나? => inline을 구성하는 것중 가장 height가 큰것이 lineheight가 되어서 lineheight만큼 y값이 내려온다.

**Baseline**: inline을 구성하는 요소중 제일 큰 것(height가?)이 있으면, 그것을 기준으로 위에만 맞추기, 밑에 맞추기, 가운데 정렬, 세로축 정렬 등의 개념이 생긴다.

(baseline도 inline안에 있는 시스템이다.)

IFC에서 block이 생기면 IFC가 종료되고, 다음번 블록 요소가 만들어 진다.

![Pasted Graphic.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic.png)

Case 1

![Pasted Graphic 1.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%201.png)

div가 block이기 때문에 공간이 남아도 파란div는 아래로 내려온다.

width가 500까지 라는 뜻은, 그림을 그리는 지오메트리의 fragment영역이 500까지라는 것이고, 실제로는 width가 끝까지 적용된다. 

Case 2

![Pasted Graphic 3.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%203.png)

a 는 IFC인데(inline요소) 왜 아래로 안내려 가는가? 부모의 width를 넘어가면 안되는데 왜 뚫고가는 것일까?

![Pasted Graphic 4.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%204.png)

a 를 끊어 놓으면 원하는 대로 그려진다.

왜 a를 붙여 놓으면 뚫고 나오고, a를 끊어 놓으면 제대로 그려지는 것일까

=> 암묵적으로, HTML이 그림을 그릴 때, 공백 문자가 없는 문자를 하나의 IFC섹션으로 보는 것이다.

(첫번째는 span하나, 두번째는 span태그가 3개인 격)

제대로 렌더링 시키려면, 공백문자를 삽입 해야하는 것이다.

공백문자를 삽입하기 싫으면, 부모(div)에 특별한 속성인 wordbreak를 주어야 한다.

Wordbreak: 붙어있는 문자열을 하나의 inline으로 보지 말고 width에 맞추어 쪼개는것. 문자 하나하나를 inline으로 보게 되는 것이다. 당연히 더 느리다. 글자 하나하나를 지오메트리로 보기 때문이다. 급 느려진다. (지오메트리가 많아지기 때문에 계산 할 것이 엄청 많아져서)

Case 3

![Pasted Graphic 5.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%205.png)

어떻게 될까? (예상해 보기. 렌더링 시스템에 대한 이해가 필요하다.)

알고 있어야 하는것.

- 렌더링 시스템과 DOM의 구조는 무관하다 (DOM의 포함관계와 렌더링을 평가할 때 포함관계는 다르다)

렌더링 시스템에 의해서는 (순서대로) BFC, IFC, IFC, BFC, IFC일 뿐이다.

![Pasted Graphic 6.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%206.png)

![Pasted Graphic 7.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%207.png)

Position에 relative를 주게되면 relative position model이 적용 된다. relative는 static으로 그리고나서, 상대적으로 위치를 이동시키는 것이다.

![Pasted Graphic 8.png](/var/folders/gj/t94sdg0545x88k2_vvtkk4k40000gn/T/abnerworks.Typora/05EB5082-AA32-4842-9F43-17F5B9CE8AB3/Pasted%20Graphic%208.png)

static과 relative가 섞여있으면, 무조건 relative가 static 위로 올라온다 (그래서 static인 파란박스와 **이 가려졌다.)

Relative 때문에 박스의 크기가 변하거나 width와 height가 변하는 일이 일어날까?

=> 안일어난다. 그림만 상대적으로 그렸을 뿐이지, 실제로 지오메트리 계산은 모두 static으로 한 것이다. static으로 계산한 시점에 크기가 다 결정된다. 이후, relative로 얼마나 움직여도, width나 height가 변하지 않는다.

Relative는 static으로 그린 다음에 relative하게 옮겨주면 되는것.

여기까지가 nomalflow이다.

- 브라우저에서 가장 많이 그림그릴때 쓰는 공식이다.
- 브라우저 사이즈 변형에 컨텐츠 크기를 예상할 수 있는 이유가 nomalflow를 사용하고 있기 때문.
- absolute나 fixed를 사용하면 normalflow가 더이상 작동하지 않는다. (Width를 주지 않으면 가로 공간이 확보 안됨, 함부로 글자가 내려오거나 height가 확보되지 않는 등의 것들을 경험할 수 있다.)
- Nomalflow 하에서만 자동으로 크기 계산되고, 자동으로 height 계산되고, 위치를 자동으로 잡아주는 것이다. (Nomal flow를 벗어나면 이런 혜택이 다 없어지는것)