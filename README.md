# effective-java-study

![image](https://github.com/uhanuu/effective-java/assets/110734817/b3de0805-d28d-44f7-af6a-8cf644e8ee80)


<br>

## 목차
<details>
  <summary><a href="https://github.com/SangSangPlus/effective-java-study/tree/main/Chapter_02">Chapter 02 : 객체 생성과 파괴</a></summary>

  - [Item 01 : 생성자 대신 정적 팩토리 메서드를 고려하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%EB%B0%9C%ED%91%9C%EC%9E%90%EB%A3%8C%5Ditem_01_%EC%83%9D%EC%84%B1%EC%9E%90%20%EB%8C%80%EC%8B%A0%20%EC%A0%95%EC%A0%81%20%ED%8C%A9%ED%84%B0%EB%A6%AC%20%EB%A9%94%EC%84%9C%EB%93%9C%EB%A5%BC%20%EA%B3%A0%EB%A0%A4%ED%95%98%EB%9D%BC(%EB%B0%95%ED%98%95%EA%B7%A0).md)
  - [Item 02 : 생성자에 매개변수가 많다면 빌더를 고려하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%EB%B0%9C%ED%91%9C%EC%9E%90%EB%A3%8C%5Ditem_02_%EC%83%9D%EC%84%B1%EC%9E%90%EC%97%90%20%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EA%B0%80%20%EB%A7%8E%EB%8B%A4%EB%A9%B4%20%EB%B9%8C%EB%8D%94%EB%A5%BC%20%EA%B3%A0%EB%A0%A4%ED%95%98%EB%9D%BC(%EB%B0%95%ED%98%95%EA%B7%A0).md)
  - [Item 03 : private 생성자나 열거 타입으로 싱글톤임을 보증하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_03_private_%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC%E1%84%8C%E1%85%A1%E1%84%82%E1%85%A1_%E1%84%8B%E1%85%A7%E1%86%AF%E1%84%80%E1%85%A5_%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9_%E1%84%89%E1%85%B5%E1%86%BC%E1%84%80%E1%85%B3%E1%86%AF%E1%84%90%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%B5%E1%86%B7%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%87%E1%85%A9%E1%84%8C%E1%85%A1%E1%86%BC%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%86%E1%85%A7%E1%86%BC%E1%84%8C%E1%85%B5).pdf)
  - [Item 04 : 인스턴스화를 막으려거든 private 생성자를 사용하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_04_%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%86%AB%E1%84%89%E1%85%B3%E1%84%92%E1%85%AA%E1%84%85%E1%85%B3%E1%86%AF_%E1%84%86%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A7%E1%84%80%E1%85%A5%E1%84%83%E1%85%B3%E1%86%AB_private_%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC%E1%84%8C%E1%85%A1%E1%84%85%E1%85%B3%E1%86%AF_%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%86%E1%85%A7%E1%86%BC%E1%84%8C%E1%85%B5).pdf)
  - [Item 05 : 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_05_%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%8C%E1%85%B5%E1%86%A8%E1%84%8C%E1%85%A5%E1%86%B8_%E1%84%86%E1%85%A7%E1%86%BC%E1%84%89%E1%85%B5%E1%84%92%E1%85%A1%E1%84%8C%E1%85%B5_%E1%84%86%E1%85%A1%E1%86%AF%E1%84%80%E1%85%A9_%E1%84%8B%E1%85%B4%E1%84%8C%E1%85%A9%E1%86%AB_%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6_%E1%84%8C%E1%85%AE%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%A1%E1%86%BC%E1%84%8E%E1%85%A5%E1%86%AF%E1%84%8B%E1%85%AF%E1%86%AB).pdf)
  - [Item 06 : 불필요한 객체 생성을 피하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_06_%E1%84%87%E1%85%AE%E1%86%AF%E1%84%91%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%AD%E1%84%92%E1%85%A1%E1%86%AB_%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6_%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%91%E1%85%B5%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%89%E1%85%AE).pdf)
  - [Item 07 : 다 쓴 객체 참조를 해제하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_07_%E1%84%83%E1%85%A1%20%E1%84%8A%E1%85%B3%E1%86%AB%20%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%20%E1%84%8E%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A9%E1%84%85%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%A2%E1%84%8C%E1%85%A6%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1.(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%89%E1%85%AE).pdf)
  - [Item 08 : finalizer와 cleaner 사용을 피하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_08_finalizer%E1%84%8B%E1%85%AA_cleaner_%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%91%E1%85%B5%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%A1%E1%86%BC%E1%84%8E%E1%85%A5%E1%86%AF%E1%84%8B%E1%85%AF%E1%86%AB).pdf)
  - [Item 09 : try-finally보다는 try-with-resources를 사용하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_02/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_09_try-finally%E1%84%87%E1%85%A9%E1%84%83%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB%20try-with-resources%E1%84%85%E1%85%B3%E1%86%AF%20%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%87%E1%85%A1%E1%86%A8%E1%84%92%E1%85%A7%E1%86%BC%E1%84%80%E1%85%B2%E1%86%AB).pdf)

</details>

<details>
  <summary><a href="https://github.com/SangSangPlus/effective-java-study/tree/main/Chapter_03">Chapter 03 : 모든 객체의 공통 메서드</a></summary>

  - [Item 10 : equals는 일반 규약을 지켜 재정의하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_03/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_10_equals()%E1%84%82%E1%85%B3%E1%86%AB_%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%87%E1%85%A1%E1%86%AB_%E1%84%80%E1%85%B2%E1%84%8B%E1%85%A3%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF_%E1%84%8C%E1%85%B5%E1%84%8F%E1%85%A7_%E1%84%8C%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%86%E1%85%A7%E1%86%BC%E1%84%8C%E1%85%B5).pdf)
  - [Item 11 : equals를 재정의하려거든 hashCode도 재정의하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_03/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_11_equals%E1%84%85%E1%85%B3%E1%86%AF%20%E1%84%8C%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4%E1%84%92%E1%85%A1%E1%84%85%E1%85%A7%E1%84%80%E1%85%A5%E1%84%83%E1%85%B3%E1%86%AB%20hashCode%E1%84%83%E1%85%A9%20%E1%84%8C%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%87%E1%85%A1%E1%86%A8%E1%84%92%E1%85%A7%E1%86%BC%E1%84%80%E1%85%B2%E1%86%AB).pdf)
  - [Item 12 : toString을 항상 재정의하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_03/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_12_%20toString%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%A1%E1%86%BC%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%8C%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1.(%E1%84%80%E1%85%B5%E1%86%B7%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%89%E1%85%AE).pdf)
  - [Item 13 : clone 재정의는 주의해서 진행하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_03/%5B%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%5Ditem_13_clone_%E1%84%8C%E1%85%A2%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4%E1%84%82%E1%85%B3%E1%86%AB_%E1%84%8C%E1%85%AE%E1%84%8B%E1%85%B4%E1%84%92%E1%85%A2%E1%84%89%E1%85%A5_%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%92%E1%85%A2%E1%86%BC%E1%84%92%E1%85%A1%E1%84%85%E1%85%A1(%E1%84%80%E1%85%A1%E1%86%BC%E1%84%8E%E1%85%A5%E1%86%AF%E1%84%8B%E1%85%AF%E1%86%AB).pdf)
  - [Item 14 : Comparable을 구현할지 고려하라](https://github.com/SangSangPlus/effective-java-study/blob/main/Chapter_03/%5B%EB%B0%9C%ED%91%9C%EC%9E%90%EB%A3%8C%5Ditem_14_Comparable%EC%9D%84_%EA%B5%AC%ED%98%84%ED%95%A0%EC%A7%80_%EA%B3%A0%EB%A0%A4%ED%95%98%EC%9E%90(%EA%B9%80%EB%AA%85%EC%A7%80).pdf)

</details>


## **1주차** ( 01/06 (월) )       

> | Item 1 | Item 2 | Item 3 |Item 4 | Item 5 |Item 6 |
> | :-:| :-: | :-: | :-: | :-: | :-: |
> | 박형균 | 박형균 | 김명지 | 김명지 | 강철원 | 김진수 | 

## **2주차** ( 01/15 (수) )

> | Item 7 | Item 8 | Item 9 | Item 10 |
> |:------:|:------:|:------:|:-------:|
> |  김진수   |  강철원   |  박형균   |   김명지   | 

## **3주차** ( 01/22 (수) )

> | Item 11 | Item 12 | Item 13 | Item 14 |
> |:-------:|:-------:|:-------:|:-------:|
> |   박형균   |   김진수   |   강철원   |   김명지   |


## **4주차** ( 02/03 (월) )

> | Item 15 | Item 16 | Item 17 | Item 18 |
> |:-------:|:-------:|:-------:|:-------:|
> |   박형균   |   강철원   |   김명지   |   김진수   |
   
### 💎 발표자료

<img width="500px" alt="item 1 썸네일" src="https://github.com/uhanuu/effective-java/assets/110734817/7c342a69-ed3b-4c4d-a306-e351bfb68624"> | <img width="500px" alt="item 2 썸네일" src="https://github.com/uhanuu/effective-java/assets/110734817/40c6abe8-0f40-4b1b-8ca6-69d95750ae24"> 
| :---: | :---: |
|[📚 Item 1 생성자 대신 정적 팩터리 메서드를 고려하라] <br> [🎥 Item 1 발표 영상] |  [📚 Item 2 생성자에 매개변수가 많다면 빌더를 고려하라] <br> [🎥 Item 2 발표 영상] |
<img width="500px" alt="Item 3 썸네일" src="https://github.com/uhanuu/effective-java/assets/110734817/89901cc8-6652-4f8e-8259-ed2677c927fd"> |
|[📚 Item 3 생성자나 열거 타입으로 싱글턴임을 보증하라] <br> [🎥 Item 3 발표 영상] |

[📚 Item 1 생성자 대신 정적 팩터리 메서드를 고려하라]: https://github.com/Growth-Hub/Effective-Java/blob/main/Chapter_02/Item_01/%EC%83%9D%EC%84%B1%EC%9E%90_%EB%8C%80%EC%8B%A0_%EC%A0%95%EC%A0%81_%ED%8C%A9%ED%84%B0%EB%A6%AC_%EB%A9%94%EC%84%9C%EB%93%9C%EB%A5%BC_%EA%B3%A0%EB%A0%A4%ED%95%98%EB%9D%BC(%EC%9C%A0%ED%98%84%EC%9A%B0).md
[🎥 Item 1 발표 영상]: https://youtu.be/QO9pVoPIdVU

[📚 Item 2 생성자에 매개변수가 많다면 빌더를 고려하라]: https://github.com/Growth-Hub/Effective-Java/blob/main/Chapter_02/Item_02/%EC%83%9D%EC%84%B1%EC%9E%90%EC%97%90_%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EA%B0%80_%EB%A7%8E%EB%8B%A4%EB%A9%B4_%EB%B9%8C%EB%8D%94%EB%A5%BC_%EA%B3%A0%EB%A0%A4%ED%95%98%EB%9D%BC(%EC%B5%9C%EC%A4%80).md
[🎥 Item 2 발표 영상]: https://youtu.be/jV5usyIrX0g

[📚 Item 3 생성자나 열거 타입으로 싱글턴임을 보증하라]: https://github.com/Growth-Hub/Effective-Java/blob/main/Chapter_02/Item_03/private%EC%83%9D%EC%84%B1%EC%9E%90%EB%82%98_%EC%97%B4%EA%B1%B0_%ED%83%80%EC%9E%85%EC%9C%BC%EB%A1%9C_%EC%8B%B1%EA%B8%80%ED%84%B4%EC%9E%84%EC%9D%84_%EB%B3%B4%EC%A6%9D%ED%95%98%EB%9D%BC(%EA%B0%95%EC%B2%A0%EC%9B%90).md
[🎥 Item 3 발표 영상]: https://youtu.be/F5wguTOt78Q

---
<br>
