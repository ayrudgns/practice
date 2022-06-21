package koreait.day16;

// 조사하기 : enum(열거형 타입) => 상수만 정의한 클래스
public class Word {
	
	public static final int BASIC = 1;			// 기초
	public static final int PRACTICAL = 2;		// 활용
	public static final int EXPERT = 3;			// 전문가
	// 의미를 잘 파악하기 위해 상수값 대신에 문자 쓰기.
	
	private String english;
	private String korean;
	private int level;
	
	
	@Override
	public String toString() {
		return english + " " + korean + " " + level + "(" + 
				(this.level == Word.BASIC? "기초" : this.level == Word.PRACTICAL? "활용" : "전문가") + ")";
	}

	public Word() {
		
	}
	

	public Word(String english) {
		this.english = english;
	}

	public Word(String english, String korean) {
		this.english = english;
		this.korean = korean;
	}
	
	public Word(String english, String korean, int level) {
		this.english = english;
		this.korean = korean;
		this.level = level;
	}

	public String getEnglish() {
		return english;
	}

	public void setEnglish(String english) {
		this.english = english;
	}

	public String getKorean() {
		return korean;
	}

	public void setKorean(String korean) {
		this.korean = korean;
	}

	public int getLevel() {
		return level;
	}

	public void setLevel(int level) {
		this.level = level;
	}
	

}
