# Trimester 3 MCQ Reflection

## TOC ✏️
- Where we left off last time
- What I improved on and what I am proud of
- What I need to improve on
- How I can improve
- Popcorn Hacks

## Last CollegeBoard MCQ

The previous collegeobard MCQ I had gotten a 58/67 and this time I finally got a 65/70 which is a massive improvement. Some things I did to improve include frequent exposure to many aspects of computer science thorugh personal projects. I am proud that I decreased my missed problems.

## Improving

I can improve further by maybe teaching more topics that I know to the class for extra seed points. Especially if its a topic they are not familiar with. Some topics I can teach include understanding C, compilation, macine code, assembly, and how hardware communicates with software. If I am able to, I would teach this some day to the class.

## Popcorn Hacks

### Problem 1

![image](https://github.com/shuban-789/student/assets/67974101/ed23a213-1a51-4a75-b808-c35864607da5)

First when approaching this problem, you need to understand what it is asking for. I did not convert the correct representation of binary because I misread the question. Basically to solve this question, you just need to know binary.

```swift
2^0 --> 1
2^1 --> 2
2^2 --> 4
2^3 --> 8
2^4 --> 16
2^5 --> 32
2^6 --> 64
2^7 --> 128
```

To convert form decimal to binary, you can make a table of 2^n slots with 8 spaces. (The maximum will be 2^7). Then, you try to numerically fill your number form biggest to smallest which fits.

```python
bits = [1,2,4,8,16,32,64,128]
bin = ""
input = int(input("Enter a number: "))
while input != 0:
  if input - bits[len(bits)-1] >= 0:
    bin += "1"
    input -= bits[len(bits)-1]
  else:
    bin += "0"
  bits.pop(len(bits)-1)
print(bin)
```

### Problem 2

![image](https://github.com/shuban-789/student/assets/67974101/139eee6d-3f76-48e9-b2e6-6f83f4e71a15)

I got this one wrong because I did not read the question again. The problem explicitly said "isIncreasing" and I misread this. After re-reading it, it is almost obvious that 12 and 8 should be interchanged

### Problem 3

![image](https://github.com/shuban-789/student/assets/67974101/20be9df1-c704-445b-b69b-bc840cdbfded)

Another theory question. I struggled with the wording for these types of questions last MCQ. All I can do to improve is better test taking skills.

The internet, a vast interconnected network of computers spanning the globe, has revolutionized nearly every aspect of modern life. From communication to commerce, education to entertainment, the internet has become an indispensable tool for billions of people worldwide. Its ability to facilitate instant communication through email, social media platforms, and messaging apps has bridged geographical gaps and connected individuals across continents. Moreover, the internet serves as an inexhaustible repository of information, offering access to knowledge on virtually any topic imaginable. As a catalyst for innovation, it has empowered individuals and businesses alike to create, collaborate, and share ideas on a scale never before possible. However, alongside its myriad benefits, the internet also presents challenges such as privacy concerns, cybersecurity threats, and the proliferation of misinformation. Despite these complexities, the internet remains a transformative force shaping the modern world.

### Problem 4


![image](https://github.com/shuban-789/student/assets/67974101/deaab288-b467-46e2-83e7-dcf92982dada)

Another silly mistake question. I didnt read that the question said "LEAST" likely. It is pretty common sense that the answer is D as it talks about storage security and contradicts the statement

## Conclusion

Overall, I do not have much code in my popcorn hacks because most of what I missed had to do with reading the question again. I can continue to improve with good time management though. They also say that you can learn by teaching so by teaching subjects I am profficient in such as cybersecurity, linux, and compilation I can hopefully strive to do better as well as teach others. Some collegeboard topics I could teach to the class are cryptography, cybersecurity, and maybe as an extra C related topics.


