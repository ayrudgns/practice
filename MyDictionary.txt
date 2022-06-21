package koreait.day16;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;

public class MyDictionary {
// 작성자 : juleeus	
	public static void main(String[] args) {
		
		List<Word> mywords = new ArrayList<>();	// *** dic를 mywords로 바꿔서 구현해보기 ***
												// *** TreeMap을 ArrayList로 바꿔서 구현해보기 ***
												// Map의 단점은 정렬이 안된다. List는 정렬이 가능함!
		Scanner sc = new Scanner(System.in);
		String eng;
		String kor;
		int level;
		boolean go = true;
		
		while(go) {			// go가 false가 될 때까지 반복.
			System.out.println("선택 기능 : 1. 단어 저장 | 2. 단어 검색 | 3. 단어장 전체 보기 | 4. 레벨로 검색 | 5. 프로그램 끝내기");
			System.out.print("선택 => ");
			String x = sc.nextLine();
 			switch (x) {		// 입력한 x에 따른 case 분류
				case "1":		
					System.out.print("English => ");	// 영어 단어 입력
					eng = sc.nextLine();
					System.out.print("Korean => ");		// 한글 뜻 입력
					kor = sc.nextLine();
					System.out.print("Level => ");		// 난이도 입력
//					w.setLevel(Integer.parseInt(sc.nextLine()));	// 난이도 저장
//					Word w = new Word(eng, kor);		// Word 객체에 저장
					
					// 강사님이 하신거
					level = Integer.parseInt(sc.nextLine());	// 난이도 저장
					Word w = new Word(eng, kor, level);				// 생성자 3개로 바꿔서 한 것.
					// 여기까지
					
					if(0 < w.getLevel() && 3 >= w.getLevel()) {
						mywords.add(w);				// mywords에 eng, kor, level 저장 완료
						System.out.println("저장되었습니다.");
					} else {
						System.out.println("난이도의 범위는 1 ~ 3 입니다. 저장 실패");	// 난이도 범위 제한하기.
					}
					break;
					
				case "2":
					System.out.print("검색 단어 English => ");	// 영단어 검색
					eng = sc.nextLine();
					
					for(Word e : mywords) {		// 향상된 for문을 활용하는 것이 코드가 더 간단하다. 추천추천
						if(e.getEnglish().equals(eng)) {
							System.out.println("단어장 검색했습니다. 결과 => " + e.getKorean());
						}
					}
					
					// 내가 한거
//					for(int i = 0; i < mywords.size(); i++) {		// mywords 돌리기
//						if(mywords.get(i).getEnglish().equals(eng)) {		// i번째 인덱스 영어랑 입력한 영어랑 같니?
//							System.out.print("단어장 검색했습니다. 결과 => " + mywords.get(i).getKorean());	// 그럼 i번째 한글 내놔
//						} else {
//							System.out.println("null");		// 없음
//						}
//					}
					// 여기까지

					break;
				
				case "3":		
					all(mywords);		// 정렬하고 출력하는 메소드 만들기.
					break;
					
				case "4":		// 추가 => 레벨로 검색하기.
					System.out.print("검색할 레벨 입력(1 ~ 3) -> ");
					int no = Integer.parseInt(sc.nextLine());
					level(mywords, no);
					break;
				
				case "5":		// 손댈거 없음
					go = false;			// go 가 false가 되니까 while문 종료
					break;
	
				default:		// 손댈거 없음
					System.out.println("잘못 입력된 값입니다. 다시 입력하세요. (범위 : 1 ~ 5)");
					break;
			}
		}
	}

	private static void level(List<Word> mywords, int no) {
		
		for(Word w : mywords) {
			if(w.getLevel() == no) {
				System.out.println(w);
			}
		}

	}

	private static void all(List<Word> mywords) {			// mywords를 정렬하고 출력하는 메소드.
		
		mywords.sort(new Comparator<Word>() {
			
			@Override
			public int compare(Word o1, Word o2) {				// mywords 정렬!
				return o1.getEnglish().compareTo(o2.getEnglish());
			}
		});
		
		System.out.println(String.format("%-20s %-20s\t %-10s", "English", "Korean", "level"));	// 예쁘게 출력
		System.out.println("================================================================================");
		for(Word w : mywords) {
			System.out.println(String.format("%-20s %-20s\t %-10d", w.getEnglish(), w.getKorean(), w.getLevel()));
		}
		
	}
}
