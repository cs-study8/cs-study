## π Tech Blog

* [Notion](https://www.notion.so/1b6da3e4cb96493494fd2d21e43ccb58)
* [Velog](https://velog.io/@kjh03160)
* [Tistory](https://juna-dev.tistory.com/)
---
μμ κ°μ λ³΄λκ±Έ μΆμ²λλ €μ©
---
---

DB μΈλ±μ€μ κ΄ν΄μ μμλ³΄κ³ μ νλ€. μΈλ±μ€λ₯Ό λ³΄κΈ° μ μ DBμμλ μ΄λ»κ² λ°μ΄ν°λ₯Ό μ μ₯νκ³  κ΄λ¦¬νλμ§ κ°λ¨ν λ¨Όμ  μ΄ν΄λ³΄κ³ μ νλ€.

## Data μ μ₯ κ΅¬μ‘°

- λ°μ΄ν°λ² μ΄μ€ : λΈλ‘μ λͺ¨μ
- λΈλ‘ : λμ€ν¬μ μλ λ°μ΄ν° μ μ‘ μ΅μ λ¨μ
- νμ΄μ§ : λ©λͺ¨λ¦¬μ μλ λ°μ΄ν° μ μ‘ μ΅μ λ¨μ
- λ μ½λ : λΈλ‘μ κ΅¬μ±νλ λ°μ΄ν° λ¨μ

### λμ€ν¬ λ°°μΉλ

**λΌλ¦¬μ μΌλ‘ μΈμ ν νμ΄μ§λ€μ ν¬μΈν°λ‘ μ°κ²°**νλ€.

β λ¬Όλ¦¬μ μΌλ‘ μΈμ νμ§ μμ μλ μλ€λ λ»μ΄λ€.

**νμ΄μ§**λ **νμ΄μ§ ν€λ, μ μ΄ μ **λ³΄λ₯Ό μ μ νλ©°,

**ν¬μΈν°**λ **λ€μ νμ΄μ§μ λ¬Όλ¦¬μ  μ£Όμλ₯Ό κ°λ₯΄ν€**λ©° μ΄λ λμ€ν¬ κ΄λ¦¬μκ° κ΄λ¦¬νλ€.

![](https://images.velog.io/images/kjh03160/post/486ea783-d8f2-42a1-951e-ff534031531c/image.png)

### λμ€ν¬ λλ ν λ¦¬ (νμ΄μ§ μΈνΈ λλ ν λ¦¬)

- μ²« νμ΄μ§(μ€λ¦°λ 0, νΈλ 0)μ μμΉ
- **λͺ¨λ  νμ΄μ§ μΈνΈμ λ¦¬μ€νΈμ κ° νμ΄μ§ μΈνΈμ 1λ²μ§Έ νμ΄μ§ ν¬μΈν° μ μ₯ β μ μ΄ μ λ³΄λΌκ³  ν¨.**

![](https://images.velog.io/images/kjh03160/post/e4d1e1bf-3a96-445f-95a7-13671dfc03ad/image.png)

### νμ΄μ§ μ μ₯ κ΄λ¦¬

- νμΌ κ΄λ¦¬μκ° κ΄λ¦¬νλ©°,
- νλμ νμ΄μ§μ μ¬λ¬ κ°μ λ μ½λ μ μ₯
- λ μ½λ μ μ₯ μμΉμ κ΄κ³ μμ΄ **λΌλ¦¬μ μΌλ‘ μ κ·Ό κ°λ₯**
- **μμ  κ³΅κ° β λΉμ΄μλ κ³΅κ°μ λ»νλ€.**

![](https://images.velog.io/images/kjh03160/post/1ca6e8ba-58cf-4121-8d01-6125e72ec0ba/image.png)

### λ μ½λ μ μ₯ κ΅¬μ‘°

- **RID = (νμ΄μ§ λ²νΈ, νμ΄μ§ offset)**μΌλ‘ κ΅¬μ±λμ΄ μλ€.
- μ¦, ν νμ΄μ§ λ΄μμ μ½μ/μ­μ  μ°μ°μΌλ‘ μΈν΄ μμΉκ° λ°λμ΄λ offset κ°λ§ λ°κΏμ£Όλ©΄ λλ€λ κ²μ΄λ€.
- **μ΅μμ κ²½μ° 2λ²μ νμ΄μ§ μ κ·ΌμΌλ‘ μνλ λ μ½λ κ²μμ΄ κ°λ₯νλ€.**
    - 2λ² μ κ·Όνλ κ²½μ°λ ν΄λΉ νμ΄μ§κ° μ€λ²νλ‘μ° β λ μ½λκ° λ€λ₯Έ νμ΄μ§λ‘ μ΄λνμ¬ μ μ₯λ κ²½μ°κ° μλ€.

![](https://images.velog.io/images/kjh03160/post/3f5ac29f-8342-4e0e-8270-b7dbb93ebd65/image.png)

κ·Έλ λ€λ©΄ DBμμ κ°μ μ΄λ»κ² μ½μ΄λ€μ΄λμ§ νλ² μμλ³΄μ

---

## λλ€ I/O vs μμ°¨ I/O

μ»΄ν¨ν°μ CPUλ λ©λͺ¨λ¦¬μ κ°μ μ κΈ°μ  νΉμ±μ λ€ μ₯μΉμ μ±λ₯μ μ§§μ μκ° λμ λ§€μ° λΉ λ₯Έ μλλ‘ λ°μ νμ§λ§ λμ€ν¬μ κ°μ κΈ°κ³μ μ₯μΉμ μ±λ₯μ μλΉν μ νμ μΌλ‘ λ°μ νλ€. λ°μ΄ν°λ² μ΄μ€λ μΏΌλ¦¬ νλμ μ΄λμ λ μ§μμ κ°μΆ μ¬μ©μκ° λ§μ΄ μ κ°νκ³  μλ―μ΄,Β λ°μ΄ν°λ² μ΄μ€μ μ±λ₯ νλμ μ΄λ»κ² λμ€ν¬ I/Oλ₯Ό μ€μ΄λλκ° κ΄κ±΄μΈ κ²λ€μ΄ μλΉν λ§λ€.

λ°μ΄ν°λ₯Ό μ½λ λ€λ κ±΄ λμ€ν¬ λλΌμ΄λΈμ μνμ λλ €μ μ½μ΄μΌ ν  λ°μ΄ν°κ° μ μ₯λ μμΉλ‘ λμ€ν¬ ν€λλ₯Ό μ΄λμν¨ λ€μ λ°μ΄ν°λ₯Ό μ½λ κ²μ μλ―Ένλ€. 

![](https://images.velog.io/images/kjh03160/post/aa35afdd-ffef-45ad-aa28-4f33cd554d09/image.png)
**λλ€ I/O**

- λ μ½λκ° λΌλ¦¬μ , λ¬Όλ¦¬μ μΈ μμλ₯Ό λ°λ₯΄μ§ μκ³ , **ν κ±΄μ μ½κΈ° μν΄ ν λΈλ‘ μ© μ κ·Ό**νλ λ°©μμ΄λ€.
- μ μ¬μ§μμ 1, 2, 3, 4, 6λ²μ ν΄λΉνλ λ°©μμ΄λ€.
- **μ¦, λ°μ΄ν° 1κ°λ§λ€ λμ€ν¬ 1λ²μ μ½λλ€λ κ²μ΄λ€.**

**μμ°¨ I/O**

- μ°μλ νμ΄μ§λ₯Ό μ κ·Όνλ λ°©μ β **λΌλ¦¬μ /λ¬Όλ¦¬μ  μμλ₯Ό λ°λΌ μ°¨λ‘λλ‘ μ½μ΄ λκ°λ λ°©μ**μ΄λ€.
- μ μ¬μ§μμ 5λ²μ ν΄λΉνλ€.
- **μ¦, λ°μ΄ν° μ¬λ¬κ°λ₯Ό μ½λλ° λμ€ν¬λ₯Ό 1λ²λ§ μ½μ΄λ λλ€λ κ²μ΄λ€.**

μ 2κ°μ§ λ°©μμ λ³΄λ©΄ λΉμ°ν λλ€ I/O λ³΄λ€ μμ°¨ I/Oκ° μ’λ€λ κ²μ μ μ μλ€. κ·Έλμ μΏΌλ¦¬ νλμμλ λλ€ I/Oλ₯Ό μ΅μννλ κ²μ΄ μ€μνλ€κ³  ν  μ μλ€. μ΄λ κ³§ μΏΌλ¦¬λ₯Ό μ²λ¦¬νλλ° κΌ­ νμν λ°μ΄ν°λ§ μ½λλ‘ κ°μ νλ κ²μ μλ―Ένλ€.

μ΄νμ λ³΄κ² μ§λ§, **Index Range Scanμ μ£Όλ‘ λλ€ I/O,** **Table Full Scanμ μμ°¨ I/O**λ₯Ό μ¬μ©νλ€. μμΈν μ€λͺμ λ°μμ νλλ‘ νκ³ , μ΄μ  μΈλ±μ€κ° λ¬΄μμΈμ§ λ³΄λλ‘ νμ.

---

## μΈλ±μ€λ?

μΈλ±μ€λ **μΆκ°μ μΈ μ°κΈ° μμκ³Ό μ μ₯ κ³΅κ°μ νμ©**νμ¬ λ°μ΄ν°λ² μ΄μ€ νμ΄λΈμ **κ²μ μλλ₯Ό ν₯μ**μν€κΈ° μν μλ£κ΅¬μ‘°μ΄λ€. μ¦, μ±μ μκ°ν΄λ³΄λ©΄ λ§¨ μμ΄λ λ§¨ λ€μ μλ μ°Ύμλ³΄κΈ°(μμΈ)κ³Ό κ°λ€κ³  λ³Ό μ μλ€. μ± μ μ²΄λ₯Ό μ°Ύμλ³΄μ§ μμλ μμΈμμ κ°λ₯΄ν€λ κ³³μ κ°λ©΄ ν΄λΉ λΆλΆμμ μ°Ύμ μ μλ κ²μ²λΌ, λ°μ΄ν°λ² μ΄μ€μμλ **λ°λ‘ μΈλ±μ€ μ μ₯ κ³΅κ°μ λμ΄** λΉ λ₯΄κ² ν΄λΉ λ°μ΄ν°κ° μλ κ³³μ μ°Ύμκ°λ κ²μ΄λ€. κ·Έλμ κ²μ μλλ₯Ό ν₯μμν¬ μ μλ€λ κ²μ΄λ€. 

νμ§λ§ μΈλ±μ€λ **κ²μ μ΄μΈμ μμμμλ ν¨μ¨μ΄ μ’μ§ μλ€**. μ½μ/λ³κ²½/μ­μ λ₯Ό μκ°ν΄λ³΄μ. 

**μΈλ±μ€λ ν­μ μ λ ¬λ μνλ₯Ό μ **μ§ν΄μΌνλ€. μ±μ μλ μμΈμμλ ν­μ μ€λ¦μ°¨μμΌλ‘ μλ κ²μ μκ°ν΄λ³΄λ©΄ λ  κ²μ΄λ€. μ¬κΈ°μ μΈλ±μ€λ₯Ό νλ μΆκ°/λ³κ²½νλ €κ³  νλ€λ©΄, ν΄λΉ μΈλ±μ€κ° λ€μ΄κ° μμΉλ₯Ό μ°Ύμμ μ½μν λ€μ, λλ¨Έμ§ λ· λΆλΆμ μλ κ²λ€μ λ€ λ€λ‘ λ°μ΄λ΄μΌν  κ²μ΄λ€. μ­μ  λν λ°μ΄ν°λ² μ΄μ€ μΈλ±μ€μμ λ¨μν μμ λ²λ¦¬λ κ²μ΄ μλλΌ, μ¬μ©νμ§ μμμΌλ‘ λλ€. μ΄λ κ³§ μ©λμ μ¦κ°λ₯Ό μλ―Ένλ©° μ½μ/μ­μ κ° λΉλ²νκ² μ΄λ£¨μ΄μ§λ€λ©΄ μ€μ  λ°μ΄ν°λ³΄λ€ μΈλ±μ€ κ°μκ° λͺλ°°λ λ λ§μμ§λ κ²μ΄λ€. κ·Έλ¬λ―λ‘ μΈλ±μ€λ₯Ό μ¬μ©ν  λμλ μ μ€ν κ²°μ ν΄μΌνλ€.

κ·Έλ λ€λ©΄ μΈλ±μ€μ λν΄μ μ’ λ μμΈν μμλ³΄μ

### Clustered vs Non-Clustered Index

μΈλ±μ€ κ΅¬μ‘°μλ ν¬κ² 2κ°μ§λ‘ Clustered Index, Non-Clustered Indexκ° μλ€.

**Clustered Index**

- μ€μ  νμ΄λΈ λ°μ΄ν° μνΈλ¦¬ μμμ λ μ½λ μμκ° κ°λ€. β **λ¬Όλ¦¬μ μΌλ‘ νμ μ¬λ°°μ΄νλ€.**
- λ¬Όλ¦¬μ μΌλ‘ μ λ ¬λμ΄ μκΈ° λλ¬Έμ **Range μΏΌλ¦¬μ ν¨μ¨μ΄ μ’λ€**.
- **νμ΄λΈ λΉ 1κ°μ μΉΌλΌ**λ§ μ€μ  ν  μ μλ€. β μλμΌλ‘ κ·Έ μΉΌλΌ κΈ°μ€μΌλ‘ μ λ ¬λλ€.
- λ³΄ν΅ PKκ° κ±Έλ¦° μΉΌλΌμ΄ defaultλ‘ μ€μ λλ€.

**Non-Clustered Index**

- μ€μ  νμ΄λΈ λ°μ΄ν° μνΈλ¦¬ μμμ λ μ½λ μμκ° κ°μ§ μλ€. β **λΌλ¦¬μ μΌλ‘λ§ νμ΄ μ λ ¬λμ΄ μλ€.**
- **νμ΄λΈ λΉ μ¬λ¬ κ° μΉΌλΌμ λν΄ μ€μ  κ°λ₯**
- Range μΏΌλ¦¬λ₯Ό νλ©΄ κ·Έ κ΅¬κ°μ λ μ½λλ€μ μ½κΈ° μν΄ λ§€λ² λμ€ν¬ λΈλ‘μ μ κ·Ό β ν¨μ¨ μ’μ§ μμ
- Mysql innoDBμμλ unique Contraint, FKλ₯Ό κ±Έλ©΄ μλμΌλ‘ Non-clustered indexκ° μμ±

---

## μΈλ±μ€ μκ³ λ¦¬μ¦

λ°μ΄ν° μ μ₯ λ°©μ(μκ³ λ¦¬μ¦)λ³λ‘ κ΅¬λΆνλ κ²μ μλΉν λ§μ λΆλ₯κ° κ°λ₯νκ² μ§λ§ λνμ μΌλ‘ B-Tree μΈλ±μ€μ Hash μΈλ±μ€λ‘ κ΅¬λΆν  μ μλ€. μ¬κΈ°μ μΈλ±μ€μ μ€μ  λ°μ΄ν°κ° μ μ₯λ λ°μ΄ν°λ λ°λ‘ κ΄λ¦¬λλ€λ μ μ κΈ°μ΅νμ. μ¦, μΈλ±μ€λ₯Ό νκ³  μ°Ύμκ°λ€κ³  ν΄μ κ±°κΈ°μ λ°μ΄ν°κ° μλ κ²μ΄ μλκ³ , λ°μ΄ν°λ₯Ό κ°λ₯΄ν€λ μ£Όμκ° μλ κ²μ΄λ€!

### B-Tree μκ³ λ¦¬μ¦

μΉΌλΌμ κ°μ λ³ννμ§ μκ³  μλμ κ°μ μ΄μ©ν΄ μΈλ±μ± νλ μκ³ λ¦¬μ¦μ΄λ€. μ¬κΈ°μ Bλ Balancedλ₯Ό μλ―Ένλ©°, μ΄λ νΈν₯λ νΈλ¦¬κ° μλλΌ, λμ΄κ° O(log n)μ ν­μ μ μ§νλ νΈλ¦¬λ₯Ό λ§νλ€. 

B-Treeμ κ΅¬μ‘°λ μλμ κ°λ€.

![](https://images.velog.io/images/kjh03160/post/f6ea14d9-0514-4ce0-82b3-762c7e4fe6ff/image.png)
μλ¨μ λΈλλ₯Ό root node, μ€κ° λΈλλ₯Ό branch node, μ΅νλ¨μ λΈλλ₯Ό leaf nodeλΌκ³  λΆλ₯Έλ€. 

![](https://images.velog.io/images/kjh03160/post/7bd74498-4adc-46eb-82c6-aeb4764573bd/image.png)

λΈλμ κ° key κ°μ λ°λΌμ μμ κ²μ μΌμͺ½, ν° κ²μ μ€λ₯Έμͺ½μ μμΉνλ κ²μ λ³Ό μ μλ€. μ΄λ λ°μ΄ν° 1κ±΄ λΉ O(log n)μκ°μ νμμ΄ κ°λ₯νλλ‘ λλ κ²μ μ μ μλ€. B-Treeλ κ° λΈλλ§λ€ ν΄λΉ ν€ κ°μ ν΄λΉνλ λ°μ΄ν°μ μ£Όμλ₯Ό λ΄κ³  μλ€λ κ²μ΄ νΉμ§μ΄λ€.

### B+ Tree μκ³ λ¦¬μ¦

B-Treeμμ λ°μ ν μκ³ λ¦¬μ¦μΌλ‘ λλΆλΆμ λ°μ΄ν°λ² μ΄μ€μμ μΈλ±μ€ μκ³ λ¦¬μ¦μΌλ‘ μ±νν λνμ μΈ μκ³ λ¦¬μ¦μ΄λ€. 

![](https://images.velog.io/images/kjh03160/post/1bb7d383-0d70-42ad-b8d7-1a6bb4877000/image.png)

**B-Treeμλ λ€λ₯Έ μ μ λ¦¬ν λΈλμλ§ keyμ dataλ₯Ό μ μ₯νκ³ , λ¦¬ν λΈλλΌλ¦¬ Linked listλ‘ μ°κ²°λμ΄ μλ€**λ κ²μ΄λ€. μ΄λ κ² ν¨μΌλ‘μ¨μ μ₯μ μ μ€κ° λΈλλ λ¨μν λ€λΉκ²μ΄μ μ­ν λ§ νκΈ° λλ¬Έμ λ λ§μ keyλ€μ μμ©ν  μ μμ΄ νΈλ¦¬μ λμ΄λ₯Ό λ λ?μμ§κ² ν  μ μλ€. λν, μΈλ±μ€ νμ€μΊμ ν  λ, λ¦¬ν λΈλλ μλ‘ μ°κ²°λμ΄ μκΈ° λλ¬Έμ 1λ²μ νμμΌλ‘ μ¬λ¬ κ°μ μΈλ±μ€λ₯Ό νκ³  λμ΄κ° μ μλ€. 

μ΄λ κ³§ Range Scanμ ν¨μ¨μ΄ κ·Ήλν λλ€κ³  λ³Ό μ μλ€. νμ§λ§ 1κ°μ μΈλ±μ€ κ²μμ λ³΄μμ λλ B-Treeκ° λ λΉ λ₯Ό μλ μλ€. μλνλ©΄ B-Treeλ λ¦¬ν λΈλκΉμ§ λ΄λ €κ°μ§ μμλ ν΄λΉ ν€ κ°μ μ°ΎμΌλ©΄ λ°λ‘ κ±°κΈ°μ λ°μ΄ν° μ κ·Όμ΄ κ°λ₯νκΈ° λλ¬Έμ΄λ€.

**μΈλ±μ€ ν€ μΆκ°**

B-Treeμ μ μ₯λ  λλ μ μ₯λ  ν€κ°μ μ΄μ©ν΄ B-Treeμμ μ μ ν μμΉλ₯Ό κ²μν΄μΌ νλ€.

**μ μ₯λ  μμΉκ° κ²°μ λλ©΄ λ μ½λμ ν€κ°κ³Ό λμ λ μ½λμ μ£Όμ μ λ³΄λ₯Ό B-Treeμ λ¦¬ν λΈλμ μ μ₯. λ§μ½ λ¦¬ν λΈλκ° κ½ μ°¨μ λλ μ μ₯ν  μ μμ λλ λ¦¬ν λΈλκ° λΆλ¦¬(Split)λΌμΌ νλλ°, μ΄λ μμ λΈλμΉ λΈλκΉμ§ μ²λ¦¬μ λ²μκ° λμ΄μ§λ€.** μ΄λ¬ν μμ νμ B-Treeλ μλμ μΌλ‘ μ°κΈ° μμ(μλ‘μ΄ ν€λ₯Ό μΆκ°νλ μμ)μ λΉμ©μ΄ λ§μ΄ λλ κ²μΌλ‘ μλ €μ‘λ€. 

λλ΅μ μΌλ‘ νμ΄λΈ λ μ½λ μΆκ°μ λΉμ©μ΄ 1μ΄λΌλ©΄, μΈλ±μ€ μΆκ°λ 1~1.5 μ λλ‘ μμΈ‘νλ€κ³  νλ€. 

μΌλ°μ μΌλ‘ νμ΄λΈμ μΈλ±μ€κ° 3κ°κ° μλ€λ©΄ μ΄λ νμ΄λΈμ μΈλ±μ€κ° νλλ μλ κ²½μ° μμ λΉμ©μ΄ 1μ΄κ³ , 3κ°μΈ κ²½μ°μλ 5.5 μ λμ λΉμ©(1.5*3 + 1) μ λλ‘ μμΈ‘ν΄ λ³Ό μ μλ€.

**μΈλ±μ€ ν€ μ­μ **

ν€ κ°μ μ­μ λ κ°λ¨νλ€. ν΄λΉ λ¦¬ν λΈλμμ ν€ κ°μ μ°Ύμμ μ­μ  λ§ν¬λ§ νλ©΄ λλ€. μ΄λ κ² μ­μ  λ§νΉλ μΈλ±μ€ ν€ κ³΅κ°μ κ·Έλλ‘ λ°©μΉλκ±°λ μ¬νμ© λ  μ μλ€. μ΄ μ­μ λ‘ μΈν λ§νΉ μμ λν λμ€ν¬μ μ°κΈ°κ° νμνλ―λ‘ λμ€ν¬ I/Oκ° νμν μμμ΄λ€.

**μΈλ±μ€ ν€ κ²μ**

μΈλ±μ€ μΆκ° λΉμ©μ κ°λΉνλ©΄μκΉμ§ κ΅¬μΆνλ μ΄μ λ λΉ λ₯Έ κ²μμ μν΄μμ΄λ€. 

B+ Tree μΈλ±μ€λ₯Ό μ΄μ©ν κ²μμ 100% μΌμΉ λλ κ°μ μλΆλΆ(Left-most part)λ§ μΌμΉνλ κ²½μ°μ μ¬μ©ν  μ μλ€. λΆλ±νΈ(`<>`) λΉκ΅λ κ°μ λ·λΆλΆμ΄ μΌμΉνλ κ²½μ°μλ μΈλ±μ€λ₯Ό μ΄μ©ν κ²μμ΄ λΆκ°λ₯νλ―λ‘ νΉν μ£Όμν΄μΌνλ€. 

## Hash μκ³ λ¦¬μ¦

ν΄μ μΈλ±μ€ μκ³ λ¦¬μ¦μ ν€ κ°μ ν΄μ κ°μ κ΅¬ν ν, λ²ν·μ λ΄μ©κ³Ό λΉκ΅νμ¬ λ μ½λ μμΉλ₯Ό μ°Ύμ μ μλ μΈλ±μ€ κΈ°λ²μ΄λ€.

 

![](https://images.velog.io/images/kjh03160/post/41003846-ef3f-431e-867e-eafb34a1ae38/image.png)

ν΄μ μκ³ λ¦¬μ¦μ μ΅λ μ₯μ μ **Equality(=) μ°μ°μλ μ’μ μ±λ₯**μ λ³΄μΈλ€λ κ²μ΄λ€. νμ§λ§ μ΄λ κ³§ **Range Scanμ Full Scanκ³Ό λ€λ₯Ό λ° μλ ν¨μ¨μ΄λΌλ κ²μ μλ―Ένλ€.**

## R Tree

## Fractal Tree

---

## μΈλ±μ€ μ€μΊ (B+ νΈλ¦¬ κΈ°μ€)

μ΄λ€ κ²½μ°μ μΈλ±μ€λ₯Ό μ¬μ©νλλ‘ μ λν μ§, λλ μ¬μ©νμ§ λͺ»νκ² ν μ§ νλ¨νλ €λ©΄ μ΄λ»κ² μΈλ±μ€λ₯Ό μ΄μ©(κ²½μ )ν΄μ μ€μ  λ μ½λλ₯Ό μ½μ΄ λ΄λμ§ μκ³  μμ΄μΌ ν  κ²μ΄λ€. μΈλ±μ€λ₯Ό μ΄μ©νλ λνμ μΈ λ°©λ² 3κ°μ§λ μλμ κ°λ€

- **Index Range Scan**

    μΈλ±μ€ μ κ·Ό λ°©λ² μ€ κ°μ₯ λνμ μΈ λ°©μμ΄λ€. λλ¨Έμ§ 2κ° λ°©μλ³΄λ€λ λΉ λ₯Έ λ°©λ²μ΄κΈ°λ νλ€. λ³Έ ν¬μ€νΈμμλ λ μ½λ 1κ±΄, κ·Έ μ΄μμ μ½λ κ²½μ° λͺ¨λ μΈλ±μ€ λ μΈμ§ μ€μΊμ΄λΌκ³  νκ² λ€. 

    **μΈλ±μ€ λ μΈμ§ μ€μΊμ κ²μν΄μΌ ν  μΈλ±μ€ λ²μκ° κ²°μ λμμ λ μ¬μ©νλ λ°©μμ΄λ€.**

    λ§μ½ SQLμ WHEREλ¬Έμ λ²μ μ°μ°μ΄ λ€μ΄μλ€κ³  μκ°ν΄λ³΄μ

    ```sql
    SELECT * FROM TABLE1 WHERE TABLE1.score > 20;
    ```

    μ΄λ κ² score κ°μ΄ 20λ³΄λ€ ν° λ μ½λλ₯Ό μ°Ύμλ¬λΌλ μ§μλ₯Ό νμ λ, B+νΈλ¦¬λ μ΄λ κ² μ§ννκ² λλ€.

![](https://images.velog.io/images/kjh03160/post/7d7d842d-5ffe-4b55-a389-824a35079ff3/image.png)

    λ£¨νΈ λΈλλ‘λΆν° ν΄λΉ ν€ κ°μ΄ μλ λ¦¬ν λΈλκΉμ§ λ΄λ €κ°λ©΄μ μμν΄μΌλ  μμΉλ₯Ό μ°ΎμΌλ©΄, λ¦¬ν λΈλ μμλλ‘ μ½μΌλ©΄ λλ€. μ΄λ κ² λμ΄μ μ€μΊμ΄λΌκ³  νννλ κ²μ΄λ€. μ΅μ’μ μΌλ‘ μ€μΊμ΄ λλλ μμΉμ λ€λ€λ₯΄λ©΄ μ§κΈκΉμ§ μ½μ λ μ½λλ₯Ό μ¬μ©μμκ² λ°ννλ€. 

    μ¬κΈ°μ νΉμ§μ μΈλ±μ€λ μ λ ¬λμ΄μλ€κ³  νλ€. κΈ°λ³Έμ μΌλ‘ μΈλ±μ€λ μ€λ¦μ°¨μμΌλ‘ μ λ ¬μ΄ λμ΄μλ€. SQLλ¬Έμμ μλ¬΄λ° μ‘°κ±΄μ΄ μλ€λ©΄ μΈλ±μ€ μΉΌλΌμ μ€λ¦μ°¨μμΌλ‘ λ°νμ΄ λλ€.

    κ·Έλ λ€λ©΄ `DESC` μ κ°μ΄ λ΄λ¦Όμ°¨μμ μ΄λ»κ² λ κΉ? μ΄λ κ°λ¨νλ€. λ¦¬ν λΈλλ₯Ό λ€μμλΆν° μ½μΌλ©΄ λλ€. μ΄λ κ² λ³λμ μ λ ¬ κ³Όμ μ΄ νμ μμ΄ μ λ ¬λ μνλ‘ κ°μ Έμ€κ² λλ€. 

    νμ§λ§ **B+ νΈλ¦¬λ Non-Clustered μΈλ±μ€**μ΄λ€. μ¦, **μμ°¨ I/Oκ° μλ λλ€ I/Oλ‘ λ μ½λλ₯Ό μ½μ΄μ¨λ€**. μ¦, λ¦¬ν λΈλμμ λ μ½λ μ£Όμλ₯Ό 1κ°λ₯Ό κ°μ Έμ¬ λλ§λ€ λλ€ I/O, λμ€ν¬ μ½κΈ°λ₯Ό 1λ²μ© μ€ννκ² λλ€.

    κ·Έλμ μΈλ±μ€λ₯Ό ν΅ν μ½λ μμμ λΉμ©μ΄ λ§μ΄ λλ μμμΌλ‘ λΆλ₯λλ κ²μ΄λ€. κ·Έλ¬λ―λ‘ μΈλ±μ€λ₯Ό ν΅ν΄ μ½μ΄μΌν  λ°μ΄ν° λ μ½λκ° 20~25%κ° λμ΄κ°λ©΄ μΈλ±μ€λ₯Ό νλ κ² λ³΄λ€λ **νμ΄λΈμ μ§μ  μ½λ κ²μ΄ λ ν¨μ¨μ μ΄κ² λλ€λ μ μ μμμΌ νλ€.**  

- **Index Full Scan**

    μΈλ±μ€ λ μΈμ§ μ€μΊκ³Ό λ§μ°¬κ°μ§λ‘, μΈλ±μ€λ₯Ό μ¬μ©νμ§λ§ νμ€μΊμ μ²μλΆν° λκΉμ§ λͺ¨λ  κ²μ μ½λ λ°©μμ λ»νλ€. 

    λνμ μΌλ‘ μΏΌλ¦¬ μ‘°κ±΄μ μ μ¬μ©λ μ»¬λΌμ΄ μΈλ±μ€μ μ²«λ²μ§Έ μΉΌλΌμ΄ μλ κ²½μ°μ μλνλ€. μΈλ±μ€κ° (A, B, C) μμλλ‘ μ°μ¬μ Έ μμ§λ§, μΏΌλ¦¬ μ‘°κ±΄μ μμλ BλΆν° μμνλ κ²½μ°μ΄λ€.

![](https://images.velog.io/images/kjh03160/post/0d2398f4-2ebd-4772-a5ac-842f682ee892/image.png)

    μΌλ°μ μΌλ‘ μΈλ±μ€μ ν¬κΈ°λ νμ΄λΈ ν¬κΈ°λ³΄λ€ μμΌλ―λ‘, νμ΄λΈ μ μ²΄λ₯Ό μ½λ κ²λ³΄λ€λ ν¨μ¨μ μ΄λ€. **μΏΌλ¦¬κ° μΈλ±μ€μ λͺμλ μΉΌλΌλ§μΌλ‘ μ‘°κ±΄μ μ²λ¦¬ν  μ μλ κ²½μ°μ μ¬μ©λλ€.**

    νμ§λ§ μ΄ λ°©μμ ν¨μ¨μ μΈ λ°©μμ μλλ―λ‘ μ΅λν νΌν΄μΌ νλ€.

- **Loose Index Scan(Index Skip Scan)**

    λ£¨μ€ μΈλ±μ€ μ€μΊμ΄λ λ¬μ±λ¬μ±νκ² μΈλ±μ€λ₯Ό μ½λ κ²μ μλ―Ένλ€. μΈλ±μ€ λ μΈμ§μ λΉμ·νκ² μλνμ§λ§ μ€κ°λ§λ€ νμνμ§ μμ μΈλ±μ€ ν€ κ°μ μ€ν΅νκ³  λ€μμΌλ‘ λμ΄κ°λ ννλ‘ μ²λ¦¬νλ€. 

    μΌλ°μ μΌλ‘ GROUP BY λλ μ§ν© ν¨μ κ°μ΄λ° MAX() λλ MIN() ν¨μμ λν΄ μ΅μ νλ₯Ό νλ κ²½μ°μ μ¬μ©νλ€. 

![](https://images.velog.io/images/kjh03160/post/a8f3a9fa-5ea1-4a5c-a5b9-53735de2c921/image.png)

---

## λ€μ€ μΉΌλΌ μΈλ±μ€

μΈλ±μ€λ₯Ό 2κ° μ΄μμ μΉΌλΌμ ν¬ν¨νλ λ°©μμ λ§νλ€. 

μ¬κΈ°μ μ€μν μ μ μ²« λ²μ§Έ μΉΌλΌμ λν΄ μ°μ  μ λ ¬λκ³ , μ²« λ²μ§Έ μΉΌλΌμ κ°μ΄ κ°μ κ²½μ°μλ§ λ λ²μ§Έ μΉΌλΌ μ λ ¬μ΄ μνλλ€λ μ μ΄λ€. κ·Έλμ λ€μ€ μΉΌλΌ μΈλ±μ€λ μΈλ±μ€ μ€μ ν  λΉμ μΉΌλΌμ μμκ° μλΉν μ€μνλ€. μΏΌλ¦¬ κ²°κ³Ό λν μ²« λ²μ§Έ μΉΌλΌμ μ λ ¬ μμλ₯Ό λ°λ₯΄κΈ°μ, λ€λ₯Έ μ λ ¬ μμλ₯Ό μνλ€λ©΄ κ·Έ λ§νΌμ λΉμ©μ΄ λ λ€μ΄κ°κΈ° λλ¬Έμ΄λ€.

λν, λ°μμ λμ€κ² μ§λ§ μ€λ³΅λ κ°μ΄ μ μ κ², μ¦ μΉ΄λλλ¦¬ν°κ° λμ κ²μ μ°μ ν΄μΌ ν¨μ¨μ΄ μ’λ€. λ¨Όμ  μ‘°νλλ κ°μ κ°μκ° μ μ΄μΌ κ·Έ λ€μ λ°μ΄ν°λ₯Ό κ±Έλ¬λ΄λλ° λ λΉ λ₯΄μ§ μκ² λκ°?

---

## μ λν¬ μΈλ±μ€

μ λν¬ μΈλ±μ€λ μμμ μ€λͺν B+ νΈλ¦¬ μΈλ±μ€μ κ΅¬μ‘°μ μΌλ‘λ λκ°λ€. μ¬μ€μ μ½κΈ°μ μμ΄μ μ λν¬ μΈλ±μ€μ secondary(μμ λμ΄λμλ μΈλ±μ€ μ’λ₯λ€) μΈλ±μ€μ μ±λ₯μ μ°¨μ΄λ κ±°μ μλ€. νμ§λ§ μ°κΈ°μμλ μ€λ³΅ κ° μ²΄ν¬νλ μμμ΄ μκΈ°μ λ λλ¦¬λ€.

λν, μ λν¬ μΈλ±μ€μμ μ€λ³΅ κ° μ²΄ν¬ μ μ½κΈ° μ κΈ, μ°κΈ° μ μ°κΈ° μ κΈ μ¬μ©μΌλ‘ λ°λλ½λ λΉλ²ν λ°μνλ€.

β λ°λΌμ **μ±λ₯μ΄ μ’μμ§ κ²μΌλ‘ μκ°νκ³  λΆνμνκ² μ λν¬ μΈλ±μ€λ₯Ό μμ±νλ κ²μ μ’μ μ νμ΄ μλλ€!**

---

## μΈλν€

MySQLμμ μΈλν€λ InnoDB μ€ν λ¦¬μ§ μμ§μμλ§ μμ±ν  μ μμΌλ©°, **μΈλν€ μ μ½μ΄ μ€μ λλ©΄ μλμΌλ‘ μ°κ΄λλ νμ΄λΈμ μΉΌλΌμ μΈλ±μ€κΉμ§ μμ±**λλ€. μΈλν€κ° μ κ±°λμ§ μμ μνμμλ μλμΌλ‘ μμ±λ μΈλ±μ€λ₯Ό μ­μ ν  μ μλ€.

- νμ΄λΈμ λ³κ²½(μ°κΈ° μ κΈ)μ΄ λ°μνλ κ²½μ°μλ§ μ κΈ κ²½ν©(μ κΈ λκΈ°)μ΄ λ°μ.
- μΈλν€μ μ°κ΄λμ§ μμ μΉΌλΌμ λ³κ²½μ μ΅λν μ κΈ κ²½ν©(μ κΈ λκΈ°)μ λ°μ X.

---

## μΈλ±μ€ μ ν μ κΈ°μ€

### μΉ΄λλλ¦¬ν°(Cardinality)

μΉ΄λλλ¦¬ν°κ° λμ μλ‘ μΈλ±μ€ μ€μ μ μ’μ μΉΌλΌμ΄λ€. β ν μΉΌλΌμ΄ κ°μ§κ³  μλ μ€λ³΅ κ°μ μ λκ° λ?μ μλ‘ μ’λ€λ κ²μ΄λ€.

μλ₯Ό λ€μ΄, 10κ° rowsλ₯Ό κ°μ§λ βνμβ νμ΄λΈμ βνλ²βκ³Ό βμ΄λ¦β μ»¬λΌμ΄ μλ€κ³  ν΄λ³΄μ.

- βνλ²βμ νμλ§λ€ λΆμ¬ λ°μΌλ―λ‘ 10κ° κ° λͺ¨λ κ³ μ νλ€.
    - **μ€λ³΅ μ λκ° λ?μΌλ―λ‘ μΉ΄λλλ¦¬ν°κ° λ?λ€.**
- βμ΄λ¦βμ λλͺμ΄μΈμ΄ μμ μ μμΌλ 1~10κ° μ¬μ΄μ κ°μ κ°μ§λ€.
    - **μ€λ³΅ μ λκ° βνλ²βμ λΉν΄ λμΌλ―λ‘ μΉ΄λλλ¦¬ν°κ° λλ€κ³  ννν  μ μλ€**

### μ νλ(Selectivity)

μ νλκ° λ?μμλ‘ μΈλ±μ€ μ€μ μ μ’μ μΉΌλΌμ΄λ€ β 5~ 10% μ λκ° μ λΉνλ€κ³  νλ€.

νμ΄λΈμμ νΉμ  κ°μ΄ μΌλ§λ μ μ νλ  μ μλ μ§ λνλ΄λ μ§νμ΄λ€.

μ νλλ μλμ κ°μ΄ κ³μ°νλ€.

```sql
= μ»¬λΌμ νΉμ  κ°μ row μ / νμ΄λΈμ μ΄ row μ * 100
= μ»¬λΌμ κ°λ€μ νκ·  row μ / νμ΄λΈμ μ΄ row μ * 100
```

μλ₯Ό λ€μ΄, 10κ° rowsλ₯Ό κ°μ§λ βνμβ νμ΄λΈμ βνλ²β, βμ΄λ¦β, βμ±λ³β μ»¬λΌμ΄ μλ€κ³  ν΄λ³΄μ.

νλ²μ κ³ μ νκ³ , μ΄λ¦μ 2λͺμ© κ°κ³ , μ±λ³μ λ¨λ 5:5 λΉμ¨.

- βνλ²βμ μ νλ = 1/10*100 = 10%
    - `SELECT COUNT(1) FROM 'νμ' WHERE 'νλ²' = 1;`Β (λͺ¨λ κ³ μ νλ―λ‘ νΉμ  κ°: 1)
- βμ΄λ¦βμ μ νλ = 2/10*100 = 20%
    - `SELECT COUNT(1) FROM 'νμ' WHERE 'μ΄λ¦' = "κΉμ² μ";`Β (2λͺμ© κ°μΌλ―λ‘ νΉμ  κ°: 2)
- βμ±λ³βμ μ νλ = 5/10*100 = 50%
    - `SELECT COUNT(1) FROM 'νμ' WHERE 'μ±λ³' = F;`Β (5λͺμ© κ°μΌλ―λ‘ νΉμ  κ°: 5)

### νμ©λ

λμ νμ©λκ° μ’μ μΈλ±μ€μ΄λ€. ν΄λΉ μΉΌλΌμ΄ μ€μ  μμμμ μΌλ§λ νμ©λλμ§μ λν κ°μ΄λ€.

μ¦, μΏΌλ¦¬ μ‘°κ±΄μ μ μΌλ§λ μμ£Ό νμ©λλμ§ μκ°ν΄λ³΄λ©΄ λλ€

---

## **μΈλ±μ€ μ‘°ν μ μ£Όμ μ¬ν­**

- λ€μ€ μΉΌλΌ μΈλ±μ€λ₯Ό μ€μ  νμ λ,  `between`,Β `like`,Β `<`,Β `>`Β λ± λ²μ μ‘°κ±΄μΒ **ν΄λΉ μ»¬λΌμ μΈλ±μ€λ₯Ό νμ§λ§, κ·Έ λ€ μΈλ±μ€ μ»¬λΌλ€μ μΈλ±μ€κ° μ¬μ©λμ§ μλλ€**.
    - μ¦,Β (A, B, C)λ‘ μΈλ±μ€κ° μ‘νμλλ° μ‘°ν μΏΌλ¦¬λ₯ΌΒ `where A=XX and C=YY and B > ZZ`λ±μΌλ‘ μ‘μΌλ©΄Β B**λ μΈλ±μ€κ° μ¬μ©λμ§ μλλ€**.
- λ°λλ‘Β `=`,Β `in`Β μ λ€μ μ»¬λΌλ μΈλ±μ€λ₯Ό μ¬μ©νλ€.
    - `in`μ κ²°κ΅­Β **`=`λ₯Ό μ¬λ¬λ² μ€ν**μν¨ κ²μ΄κΈ° λλ¬Έμ΄λ€.
    - λ¨,Β `in`μ μΈμκ°μΌλ‘ μμκ° ν¬ν¨λλ©΄ λ¬Έμ  μμ§λ§,Β **μλΈμΏΌλ¦¬λ₯Ό λ£κ²λλ©΄ μ±λ₯ μ μ΄μκ° λ°μ**νλ€.
    - `in`μ μΈμλ‘Β **μλΈμΏΌλ¦¬κ° λ€μ΄κ°λ©΄ μλΈμΏΌλ¦¬μ μΈλΆκ° λ¨Όμ  μ€ν**λκ³ ,Β `in`Β μ μ²΄ν¬μ‘°κ±΄μΌλ‘ μ€νλκΈ° λλ¬Έμ΄λ€.
- `AND`μ°μ°μλ κ° μ‘°κ±΄λ€μ΄ μ½μ΄μμΌν  ROWμλ₯Ό μ€μ΄λ μ­ν μ νμ§λ§,Β **`or`Β μ°μ°μλ λΉκ΅ν΄μΌν  ROWκ° λ λμ΄λκΈ° λλ¬Έμ ν νμ΄λΈ μ€μΊμ΄ λ°μν  νλ₯ **μ΄ λλ€.
- μΈλ±μ€λ‘ μ¬μ©λΒ **μ»¬λΌκ° κ·Έλλ‘ μ¬μ©ν΄μΌλ§ μΈλ±μ€κ° μ¬μ©λλ€**.
    - μΈλ±μ€λ κ°κ³΅λ λ°μ΄ν°λ₯Ό μ μ₯νκ³  μμ§ μλ€.
    - `where salary * 10 > 150000;`λ μΈλ±μ€λ₯Ό λͺ»νμ§λ§,Β `where salary > 150000 / 10;`Β μ μΈλ±μ€λ₯Ό μ¬μ©νλ€.
    - μ»¬λΌμ΄ λ¬Έμμ΄μΈλ° μ«μλ‘ μ‘°ννλ©΄Β **νμμ΄ λ¬λΌ μΈλ±μ€κ° μ¬μ©λμ§ μλλ€**.
- `null κ°μ κ²½μ°Β **is null μ‘°κ±΄μΌλ‘ μΈλ±μ€ λ μΈμ§ μ€μΊ κ°λ₯**`

---

## [μ λ¦¬] μΈλ±μ€ μ₯μ , λ¨μ 

### μΈλ±μ€ μ₯μ 

1. κ²μ ν¨μ¨μ΄ μ’λ€.

### μΈλ±μ€ λ¨μ 

- κ²μ μ΄μΈμ μ²λ¦¬ μλκ° λλ¦¬λ€.

    β νμ΄λΈκ³Όλ λ³λλ‘ λ°μ΄ν°λ₯Ό λμμ μΌλ‘ λ³΄μ νκ³  μκΈ° λλ¬Έμ νμ΄λΈμ λ°μ΄ν°λ₯Ό μΆκ°νλ©΄ μΈλ±μ€μΌλ‘λ λ°μ΄ν°κ° μΆκ°λλ€. 

    β λν λ°μ΄ν°λ₯Ό μΆκ°ν  λλ§λ€ μ λ ¬λ λ€μ μ΄λ£¨μ΄μ§λ€. κ²°κ³Όμ μΌλ‘ λ°μ΄ν°λ₯Ό μΆκ° ν  λ μ²λ¦¬ μλκ° λλ €μ§λ€.

- λ°μ΄ν° λ³κ²½ μμμ΄ μμ£Ό μΌμ΄λ  κ²½μ°μ μΈλ±μ€λ₯Ό μ¬μμ±ν΄μΌ ν  νμκ° μκΈ°μ μ±λ₯μ μν₯μ λΌμΉ  μ μλ€.
- ν° νμ΄λΈμ λλΆλΆμ rowλ₯Ό μ½μ΄λ€μΌ λλ μΈλ±μ€λ₯Ό μ¬μ©νμ§ μλκ² λ«λ€. β μΈλ±μ€λ λλ€ I/Oμ΄λ€.

κ·Έλ¬λ―λ‘,

κΈ°λ³Έμ μΌλ‘ νμ΄λΈ λΉ 3~4κ° κΉμ§λ§ λ§λ€λλ‘ κΆμ₯νλ€. β μΈλ±μ€ κ΅¬μ‘° μ μ₯νλλ°λ μ μ₯ κ³΅κ°μ΄ νμνλ©°, μ€ν κ³νμμ μ΄λ€ μΈλ±μ€λ₯Ό νμΌν μ§ νΌλμ μ€ μ μκΈ° λλ¬Έ

μ νλ, μΉ΄λλλ¦¬ν°λ₯Ό μ κ³ λ €νμ¬ μΈλ±μ€λ₯Ό κ΅¬μ±νμ. β μ νλκ° 15% μ΄μμ΄λ©΄ νμ΄λΈ νμ€μΊμ΄ μ λ¦¬νλ€.

β Table Full Scanμ κ²½μ° μ½κ³ μ νλ λ°μ΄ν°μ λΈλ‘μ Multi Block I/Oλ‘ μ½κΈ° λλ¬Έμ νλ‘μΈμ€κ° λ°μ΄ν°λ₯Ό λ°λ‘ μ²λ¦¬ν  μ μμΌλ, Indexμ κ²½μ° Single Block I/Oλ‘ λ°μ΄ν°λ₯Ό μ½λλ€. κ·Έλ κΈ° λλ¬Έμ λ°μ΄ν°λ₯Ό λͺ¨λ μ½λ I/O Callμ΄ λλ  λκΉμ§ μ μ νλ‘μΈμ€λ λκΈ° μνμ λ€μ΄κ°κΈ° λλ¬Έμ λΉν¨μ¨μ μΈ μνκ° λλ€.



## μ°Έκ³  μλ£

[[mysql] μΈλ±μ€ μ λ¦¬ λ° ν](https://jojoldu.tistory.com/243)

[[Real MySQL] B-Tree μΈλ±μ€](https://12bme.tistory.com/138)

[[db index 2νΈ] index structureμ μ’λ₯ (cluster index, non-cluster index, Hash Index, B Tree, B+ Tree, Fractal-Tree, Adaptive Hash Index)](https://joosjuliet.github.io/index_structure/)