### 유튜브 내용 요약 프로그램

<p align="center">
	<img src = "https://github.com/i-am-shuan/youtube-sumerize-app/assets/161431602/ebca1eb4-de95-4c99-8b73-467eb4f2ba69" width="80%" height="80%">
</p>

---

<p align="center">
	<img src = "https://github.com/i-am-shuan/youtube-sumerize-app/assets/161431602/ac6c2ce9-d1bf-4b9e-8f7d-df3c9fb3c0e1" width="50%" height="50%">
	<img src = "https://github.com/i-am-shuan/youtube-sumerize-app/assets/161431602/f1676062-80a4-4464-82fb-961a5cbf99c0" width="50%" height="50%">
</p>


- 특징
	- max token을 넘어가는 긴 글(유튜브 대본)을 요약한다.
		- 일반적으로 대본 내용이 길어지면 ChatGPT가 수용할 수 있는 max token의 길이가 넘어서 요약이 불가능하다. 이 부분을 LangChain 프레임워크를 사용하여 max token에 제한을 받지않고 긴 글도 요약할 수 있도록 서비스를 제공한다.
	- 위의 기능을 구현하기 위해 LangChain 프레임워크를 사용한다.
- 기능
	- 유튜브 영상 내용 요약
	- 요약 번역
	- 영상 대본 추출
- 코드 리뷰
	- 텍스트 쪼개기
		- from langchain.text_splitter import RecursiveCharacterTextSplitter
	- 사용할 LLM 설정
		- from langchain.chat_models import ChatOpenAI
		- llm = ChatOpenAI(max_tokens=3000,model_name="gpt-3.5-turbo",..)
	- 요약에 사용할 프롬프트
		- from langchain.prompts import PromptTemplate
	- 요약 시작: 다수개의 요약본 하나로 모아서 다시 요약
		- from langchain.chains.summarize import load_summarize_chain
	- 결과 출력
	- 번역하기 (optional)
		- from googletrans import Translator
	- Session State
		- flag
			- 요약 진행 여부를 알려주는 flag
			- 요약이 진행되지 않은 상태라면 true, 이미 완료인 상태면 false
			- 요약이 이미 완료된 상태라면 false로 저장돼서, 무의미한 API 요금 발생 방지
		- OPENAI_API
			- 입력받은 OpenAI API KEY 저장
			- 랭체인을 활용하여 OpenAI API를 입력하기 때문에 
			  랭체인 함수 안에 input 값으로 넣기 위해 별도로 session state로 분리
		- summerize
			- 프로그램 기동중, 다른 이벤트가 발생하더라도 
			  저장된 정보를 사용해서 화면에 송출하는 역할을 하여 반복된 요약 진행을 방지

---


