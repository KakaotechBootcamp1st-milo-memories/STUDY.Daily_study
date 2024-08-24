- 카카오테크 부트캠프에서 AI 플랫폼 성과 리더이신 Dennis가 와서 3일간의 클라우드 특강과 3일간의 AI 특강을 해주셨습니다!
- AI 특강을 듣던 중 Prompt Engineering 강의로 [Open AI의 강의](https://learn.deeplearning.ai/courses/chatgpt-prompt-eng/lesson/3/iterative)를 추천해주셔서 이를 들으며 직접 내용을 요약하고 실습을 진행해보려고 합니다! 

# LLM(Large Language Models) 개발의 두 가지 유형

## 1. Base LLM

- 많은 양의 텍스트 traning 데이터를 기반으로 다음 단어를 예측하도록 훈련
- 예를 들어, ‘옛날 옛적에 유니콘이 있었다’라는 프롬프트를 주면 다음 문장으로 ‘마법의 숲에서 모든 유니콘 친구들과 함께 살았다.’라고 예측할 수 있음
- 하지만 ‘프랑스의 수도는 어디인가요?’라는 프롬프트를 주면 인터넷의 기사 등에 따라 ‘프랑스의 가장 큰 도시는 무엇인가요?’나 ‘ 프랑스의 인구는 얼마나 되나요?’ 등으로 이를 완성할 가능성이 높음
    - 인터넷 기사는 프랑스에 대한 퀴즈 질문의 집합일 수 있기 때문

## 2. Instruction Tuned LLM

- 일반적으로 대량의 텍스트 데이터로 훈련된 기본 LLM에서 시작하여 지시사항의 입력과 출력 값을 활용해 더욱 fine-tunning하고 그 후에는 종종 **RLHF**라는 기법을 통해 더욱 세밀하게 fine-tunning하며 시스템에 도움이 되고 지시사항을 따르는 능력을 향상시킴
- ‘프랑스의 수도는 어디인가요?’라고 물으면 ‘프랑스의 수도는 파리입니다.’라고 답할 확률이 더 높음
- 도움이 되고 정직하며 혐오 발언이 없는 텍스트에서 훈련되었기 때문에 기본 LLM에 비해 편견이나 혐오 발언 등의 문제가 될 수 있는 텍스트를 출력할 확률이 적음
- Instruction Tuned LLM을 사용할 때 똑똑하지만 내 작업에 대한 구체적인 내용을 모르는 사람한테 지시한다고 생각하고 지시를 명확하게 해주는 것이 좋음

> **RLHF**는 "Reinforcement Learning from Human Feedback"의 약자로, 인간의 피드백을 활용한 강화 학습을 의미합니다. 이는 기계 학습, 특히 인공지능 모델의 학습에서 중요한 방법론 중 하나입니다.
> 
> 
> ### RLHF의 기본 개념
> 
> - **강화 학습(Reinforcement Learning, RL)**: 강화 학습은 에이전트가 환경과 상호작용하면서 보상을 최대화하기 위해 행동을 학습하는 방법입니다. 에이전트는 행동(action)을 취하고, 그 행동에 대한 결과로 보상(reward)을 받으며, 이 보상을 최대화하는 방향으로 학습합니다.
> - **인간의 피드백(Human Feedback)**: RLHF에서는 에이전트의 행동에 대해 사람이 직접 피드백을 제공합니다. 이 피드백은 에이전트가 올바른 행동을 학습하는 데 중요한 역할을 합니다. 사람이 직접 에이전트의 행동을 평가하고, 그에 따른 보상을 제공하여 에이전트가 더 나은 의사 결정을 할 수 있도록 유도합니다.
> 
> ### RLHF의 적용
> 
> RLHF는 특히 자연어 처리(NLP) 모델의 훈련에 많이 사용됩니다. 예를 들어, 대화형 AI 모델이 특정 질문에 대한 응답을 생성할 때, 인간 피드백을 통해 응답의 적절성, 유용성, 정확성을 평가하고, 이를 바탕으로 모델을 개선할 수 있습니다. 이를 통해 모델은 더 자연스럽고 정확한 응답을 생성하게 됩니다.
> 
> ### 요약
> 
> - **RLHF**는 인간의 피드백을 사용하여 강화 학습을 수행하는 방법입니다.
> - 강화 학습과 인간의 피드백을 결합하여, 에이전트가 더 나은 의사 결정을 할 수 있도록 학습을 진행합니다.
> - 주로 자연어 처리와 같은 분야에서 모델의 성능을 개선하는 데 사용됩니다.
> 
> - ChatGPT 4의 답변 -
> 

# Guidelines for Prompting

대규모 언어 모델에 효과적인 프롬프트를 작성하기 위해 두 가지 프롬프트 원칙과 관련 전략을 연습

### **프롬프트 원칙**

- 원칙 1: 명확하고 구체적인 지시를 작성하는 것
- 원칙 2: 모델에게 생각할 시간을 주는 것

### OpenAI 라이브러리 설치

``` shell
pip install openai
```

![](https://velog.velcdn.com/images/alswp006/post/6c0a7127-7c06-4b39-b779-2aa5a8d77f6b/image.png)


**이렇게 하면 설치 완료!**

### **OpenAI 패키지 초기화**

- 직접 해보실 거면 이리로!
    
    직접 해보실 거면 env파일 등록을 해줘야합니다!
    
    ```python
    import openai
    import os
    
    from dotenv import load_dotenv, find_dotenv_ = load_dotenv(find_dotenv())
    
    openai.api_key  = os.getenv('OPENAI_API_KEY')→ .env 파일에 본인의 key로 설정
    ```
    
    그리고 버전도 다운그레이드 해줘야 합니다!
    
    ```shell
    pip install python-dotenv
    ```
    

• OpenAI API 키는 https://platform.openai.com/account/api-keys 에서 생성 및 확인 가능

![](https://velog.velcdn.com/images/alswp006/post/8ef6c28f-e82a-427f-b85e-8d91748e3627/image.png)


### **Helper function 작성**

`GPT 3.5 Turbo` 모델과  [Chat completions 엔드포인트](https://platform.openai.com/docs/guides/chat)를 사용하며 Chat completions endpoint의 형식과 입력에 대한 더 자세한 내용은 이후에 다룸

Helper Function을 사용하면 프롬프트를 사용하기 쉬워지고, 생성된 출력을 확인할 수 있음

```python
def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=0, # this is the degree of randomness of the model's output
    )
    return response.choices[0].message["content"]
```

- getCompletion은 단순히 프롬프트를 입력받음

# **Principles of Prompting**

## **Principle 1: Write clear and specific instructions (명확하고 구체적인 지침을 작성)**

- 모델이 원하는대로 작동하도록 가능한 명확하고 구체적인 지시를 만들어야 함
- 이렇게 하면 모델이 원하는 출력 방향으로 학습하고 관련 없거나 잘못된 응답을 받을 확률이 줄어듬
- 그렇다고 명확한 프롬프트를 작성하는 것과 짧은 프롬프트를 작성하는 것을 혼동하면 안됨
    - 대부분의 경우 긴 프롬프트가 모델에게 더 많은 명확성과 맥락을 주며 이는 더 상세하고 관련있는 출력을 이끌어냄

### **Tactic 1: Use delimeters (구분자를 사용하여 입력의 구분된 부분을 명확하게 표시)**

- 구분 기호: `````, `"""`, `< >`, `<tag> </tag>`, `:`
- 단락 요약 예시

```python
# 원본
text = f"""
You should express what you want a model to do by \ 
providing instructions that are as clear and \ 
specific as you can possibly make them. \ 
This will guide the model towards the desired output, \ 
and reduce the chances of receiving irrelevant \ 
or incorrect responses. Don't confuse writing a \ 
clear prompt with writing a short prompt. \ 
In many cases, longer prompts provide more clarity \ 
and context for the model, which can lead to \ 
more detailed and relevant outputs.
"""
prompt = f"""
Summarize the text delimited by triple backticks \ 
into a single sentence.
```{text}```
"""
response = get_completion(prompt)
print(response)

# 번역
text = f"""
가능한 한 명확하고 구체적인 지침을 제공하여 모델이 수행하기를 원하는 작업을 표현해야 합니다.
이렇게 하면 모델을 원하는 출력으로 안내하고 관련성이 없거나 잘못된 응답을 받을 가능성을 줄일 수 있습니다.
명확한 프롬프트를 작성하는 것과 짧은 프롬프트를 작성하는 것을 혼동하지 마세요.
대부분의 경우, 긴 프롬프트가 모델에 더 명확하고 맥락을 제공하므로 다음과 같은 결과를 얻을 수 있습니다.
더 상세하고 관련성 높은 출력을 얻을 수 있습니다.
"""

prompt = f"""
백틱 세 개로 구분된 텍스트를 한 문장으로 요약하세요.
```{text}```
"""
response = get_completion(prompt)
print(response)
```

- 결과
    
    ![](https://velog.velcdn.com/images/alswp006/post/09fb9efd-fa1a-4fe7-9b64-b315e04b96f6/image.png)
    
- 우리가 하고자 하는 작업은 text를 요약하는 것
- 그래서 프롬프트에 세 개의 백틱으로 구분된 텍스트를 한 문장으로 요약하라고 명령
    - 그러면 세 개의 백틱이 텍스트를 둘러싸고 형태를 얻게 됨
    - 별도의 섹션을 알려주는 것은 중요
- 그 후 응답을 얻기 위해 getCompletion 헬퍼 함수를 사용 후 응답 출력
- 모델의 작업을 명확하고 구체적으로 표현하고, 긴 프롬프트를 사용하여 모델이 더 명확하고 관련성 높은 출력을 얻을 수 있도록 해야 함
- 구분자를 사용하는 것은 Prompt Injection을 피하는 유용한 기법
    - Prompt Injection이란 사용자가 프롬프트에 어떤 입력을 했을 때 모델에게 충돌된 지시를 주는 것
    이로 인해 모델이 원하는 대로 동작하지 않을 수 있음
- RateLimitError 문제 발생 시
    
    ![](https://velog.velcdn.com/images/alswp006/post/1e5ac828-6db8-4e12-8dd3-498a1d86a34b/image.png)

    
    - 직접 진행해보다가 해당 에러가 발생했습니다!
    - 문제가 발생하신 분은 [https://github.com/alswp006/Trouble-Shooting/blob/main/OpenAI/RateLimitError%3A You exceeded your current quota%2C please check your plan and billing details. For more information on this error.md](https://github.com/alswp006/Trouble-Shooting/blob/main/OpenAI/RateLimitError%3A%20You%20exceeded%20your%20current%20quota%2C%20please%20check%20your%20plan%20and%20billing%20details.%20For%20more%20information%20on%20this%20error.md) 이리로!!

### **Tactic 2: Ask for structured output (구조화된 출력 요청)**

- 모델 출력 구문 분석을 더 쉽게 하기 위해 HTML이나 JSON과 같은 구조화된 출력을 요청하는 것이 도움이 됨
- 이것의 장점은 파이썬에서 이를 DIctionary 또는 List로 읽을 수 있다는 것

```python
# 영어 원문
prompt = f"""
Generate a list of three made-up book titles along \ 
with their authors and genres. 
Provide them in JSON format with the following keys: 
book_id, title, author, genre.
"""
response = get_completion(prompt)
print(response)

# 한글 번역문
prompt = f"""
저자 및 장르와 함께 세 개의 구성 도서 제목 목록을 생성합니다.
다음 키와 함께 JSON 형식으로 제공하세요: 
book_id, 제목, 저자, 장르.
"""
response = get_completion(prompt)
print(response)
```

- 실행 결과
    
    ![](https://velog.velcdn.com/images/alswp006/post/62d087e6-574d-4877-a852-cb35ffd6fc51/image.png)

    

### **Tactic 3: Check whether conditions are satisfied (모델에게 조건이 충족되었는지 확인하도록 요청)**

- 작업이 조건에 부합하지 않는 가정을 한다면 모델에게 가정을 확인하도록 지시할 수 있음
- 그래도 충족되지 않는다면 이를 명시하고 작업 완료 시도를 중단해야함

```python
# 차 한잔을 만드는 프롬프트 예시
text_1 = f"""
Making a cup of tea is easy! First, you need to get some \ 
water boiling. While that's happening, \ 
grab a cup and put a tea bag in it. Once the water is \ 
hot enough, just pour it over the tea bag. \ 
Let it sit for a bit so the tea can steep. After a \ 
few minutes, take out the tea bag. If you \ 
like, you can add some sugar or milk to taste. \ 
And that's it! You've got yourself a delicious \ 
cup of tea to enjoy.
"""
# 지시 사항 순서를 포함하고 있으면 다음 형식으로 지시 사항을 재작성하고 단계를 적음
# 만약 지시 사항 순서를 포함하지 않는다면 "No steps provided" 출력
prompt = f"""
You will be provided with text delimited by triple quotes. 
If it contains a sequence of instructions, \ 
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \ 
then simply write \"No steps provided.\"

\"\"\"{text_1}\"\"\"
"""
response = get_completion(prompt)
print("Completion for Text 1:")
print(response)
```

- 실행 결과 (올바르게 출력)

	![](https://velog.velcdn.com/images/alswp006/post/93f8a061-ecef-4058-92ac-5deb626c9a43/image.png)


```python

text_2 = f"""
The sun is shining brightly today, and the birds are \
singing. It's a beautiful day to go for a \ 
walk in the park. The flowers are blooming, and the \ 
trees are swaying gently in the breeze. People \ 
are out and about, enjoying the lovely weather. \ 
Some are having picnics, while others are playing \ 
games or simply relaxing on the grass. It's a \ 
perfect day to spend time outdoors and appreciate the \ 
beauty of nature.
"""
prompt = f"""
You will be provided with text delimited by triple quotes. 
If it contains a sequence of instructions, \ 
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \ 
then simply write \"No steps provided.\"

\"\"\"{text_2}\"\"\"
"""
response = get_completion(prompt)
print("Completion for Text 2:")
print(response)
```

- 실행 결과 (No steps provided 출력)
    
    ![](https://velog.velcdn.com/images/alswp006/post/86e50b2f-83de-456b-80cd-a55f6dfb7c0c/image.png)

    

### **Tactic 4: "Few-shot" Prompting**

- 원하는 작업의 성공적인 실행 예시 제공
- 모델에게 실제로 원하는 작업을 요청하기 전 실행

```python
# 모델에게 일관된 어조로 답변하도록 지시
prompt = f"""
Your task is to answer in a consistent style.

<child>: Teach me about patience.

<grandparent>: The river that carves the deepest \ 
valley flows from a modest spring; the \ 
grandest symphony originates from a single note; \ 
the most intricate tapestry begins with a solitary thread.

<child>: Teach me about resilience.
"""
response = get_completion(prompt)
print(response)
```

- 실행 결과 (비슷한 어조로 응답)
    ![](https://velog.velcdn.com/images/alswp006/post/dc879e21-6d90-468d-9837-d40a02174c3d/image.png)
    

## **Principle 2: Give the model time to think(모델에게 생각할 시간 주기)**

- 모델에게 짧은 시간이나 적은 단어로 너무 복잡한 작업을 주면 잘못된 추측을 하게 될 가능성이 높음
- 모델이 결론을 서두르다가 잘못된 결론을 내리는 추론 오류를 범한다면 모델에게 문제에 대해 더 오래 생각하도록 지시할 수 있음 → 작업에 더 많은 계산 노력을 쏟음

### Tactic 1: Specify the steps required to complete a task (작업을 완료하는데 필요한 단계를 명시)

```python
text = f"""
In a charming village, siblings Jack and Jill set out on \ 
a quest to fetch water from a hilltop \ 
well. As they climbed, singing joyfully, misfortune \ 
struck—Jack tripped on a stone and tumbled \ 
down the hill, with Jill following suit. \ 
Though slightly battered, the pair returned home to \ 
comforting embraces. Despite the mishap, \ 
their adventurous spirits remained undimmed, and they \ 
continued exploring with delight.
"""
# example 1 (단계 제시)
prompt_1 = f"""
Perform the following actions: 
1 - Summarize the following text delimited by triple \
backticks with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
keys: french_summary, num_names.

Separate your answers with line breaks.

Text:
```{text}```
"""
response = get_completion(prompt_1)
print("Completion for prompt 1:")
print(response)
```

- 실행 결과
    
    ![](https://velog.velcdn.com/images/alswp006/post/039ceb1b-5b6f-4cd1-aeea-2d2cb95539d7/image.png)

    
- 동일한 작업을 완료하기 위한 다른 프롬프트

```python
prompt_2 = f"""
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
"""
response = get_completion(prompt_2)
print("\nCompletion for prompt 2:")
print(response)
```

- 실행 결과
    
    ![](https://velog.velcdn.com/images/alswp006/post/8920d9d8-5445-4a9d-bfaa-3f1fefb70edd/image.png)

    

### Tactic 2: Instruct the model to work out its own solution before rushing to a conclusion (모델이 결론에 도달하기 전 자신만의 해결책을 찾도록 지시)

- 모델에게 실제로 문제를 해결할 시간을 주고 답이 맞는지 아닌지 말하기 전에 문제를 해결하도록
- 학생의 해결책이 정확한지 아닌지 모델에게 판단하게하는 프롬프트

```python
prompt = f"""
Determine if the student's solution is correct or not.

Question:
I'm building a solar power installation and I need \
 help working out the financials. 
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \ 
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations 
as a function of the number of square feet.

Student's Solution:
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
"""
response = get_completion(prompt)
print(response)
```

- 실행 결과 (학생의 잘못된 풀이: 유지비용이 10만 달러 + 100x인데 실제로는 10x가 되어야 함)
    - 그래서 실제로는 Total Cost가 450x + 100,000이 아닌 360x + 100,000이 되어야 함
    
    ![](https://velog.velcdn.com/images/alswp006/post/bd86d6fb-d6e2-49b3-bd67-1078eaf9ac43/image.png)

    
    - 하지만 올바르다고 함
    - 사람도 학생의 풀이만 읽었을 때는 계산을 잘못할 가능성이 큼
- 모델에게 자신만의 풀이를 찾아내고 학생의 풀이와 비교하도록 만듦

```python
prompt = f"""
Your task is to determine if the student's solution \
is correct or not.
To solve the problem do the following:
- First, work out your own solution to the problem including the final total. 
- Then compare your solution to the student's solution \ 
and evaluate if the student's solution is correct or not. 
Don't decide if the student's solution is correct until 
you have done the problem yourself.

Use the following format:
Question:
```
question here
```
Student's solution:
```
student's solution here
```
Actual solution:
```
steps to work out the solution and your solution here
```
Is the student's solution the same as actual solution \
just calculated:
```
yes or no
```
Student grade:
```
correct or incorrect
```

Question:
```
I'm building a solar power installation and I need help \
working out the financials. 
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations \
as a function of the number of square feet.
``` 
Student's solution:
```
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
```
Actual solution:
"""
response = get_completion(prompt)
print(response)
```

- 실행 결과
    - 지시에 따라 모델이 자체적으로 계산 과정을 진행
    - 올바르게 360x를 사용한 값을 얻음
    - 모델에게 직접 계산을 요청하고 작업을 단계별로 분해하며 모델에게 더 많은 시간을 주어 생각하게 함
    
    ![](https://velog.velcdn.com/images/alswp006/post/88b1e2f5-43a7-46b1-9e27-0d3ab4c5d388/image.png)
    

## Model Limitations: Hallicination (모델의 제한 사항)

- 대형 언어 모델을 이용한 앱을 개발할 때 염두에 둬야하는 중요한 사항
- 언어 모델이 훈련 과정에서 막대한 양의 지식을 접했음에도 불구하고 모델이 본 정보를 완벽하게 기억하지 못함
- LLM의 경우 지식의 경계를 잘 알지 못함
    - 잘 알려지지 않은 주제에 대한 질문에 답변을 시도하고 실제로는 사실이 아닌 것을 만들어낼 수 있다는 것을 의미
    - 이를 Hallicination(환영)이라고 부름

### Hallicination 예시

```python
prompt = f"""
Tell me about AeroGlide UltraSlim Smart Toothbrush by Boie
"""
response = get_completion(prompt)
print(response)
```

- 실행 결과
    - 가상의 제품에 대한 현실적인 설명을 제공함
    - 이런 것들은 현실적으로 들리기 때문에 위험
    
    ![](https://velog.velcdn.com/images/alswp006/post/2e246c4f-7e4f-4b72-8488-bec3c0626981/image.png)
    

### Hallicination을 줄이는 전략

- 먼저 모델에게 텍스트에서 관련된 인용구를 찾게 하고, 그 인용구를 사용하여 질문에 답하도록 요청하기
- 답변을 원문에서 추적하는 것이 대부분의 경우 유용하고 Hallicination 현상을 줄이는 데에 도움을 줌
