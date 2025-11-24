# Week12

import 'package:flutter/material.dart';
import 'package:get/get.dart';
// BottomNavController 파일을 import 해야 합니다.
import 'common/controller/bottom_nav_controller.dart'; 

class Root extends GetView<BottomNavController> {
  const Root({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // 컨트롤러를 인스턴스화하고 GetX에 등록합니다. 
    // Get.put()을 사용하는 대신, GetView를 사용하면 controller 속성으로 접근 가능합니다.
    
    // 이 예시에서는 GetView<BottomNavController>를 상속받았다고 가정합니다.
    // 만약 GetBuilder나 StatelessWidget을 사용한다면 Get.find<BottomNavController>()로 접근해야 합니다.

    return Scaffold(
      // 탭 전환에 따라 본문 화면이 바뀌는 로직을 여기에 구현합니다.
      // 예: IndexedStack(index: controller.menuIndex.value, children: [Home(), Search(), Profile()])

      // 하단 네비게이션 바
      bottomNavigationBar: Obx(
        () => BottomNavigationBar(
          // 컨트롤러의 현재 인덱스를 BottomNavigationBar의 현재 선택 항목으로 지정
          currentIndex: controller.menuIndex.value,
          
          // 네비게이션 바의 타입 및 색상 설정
          type: BottomNavigationBarType.fixed, // 아이템이 4개 이상일 때 추천
          backgroundColor: const Color(0xff212121), // 어두운 배경색
          selectedItemColor: Colors.white,         // 선택된 아이템 색상
          unselectedItemColor: const Color(0xffffffff).withOpacity(0.5), // 선택되지 않은 아이템 색상 (투명도 조절)
          selectedFontSize: 12.0,
          unselectedFontSize: 11.0,

          // 탭을 눌렀을 때 호출되는 콜백 함수
          onTap: controller.changeBottomNav, 

          // 네비게이션 바 아이템 목록
          items: [
            // 첫 번째 아이템 (예: 홈)
            BottomNavigationBarItem(
              label: '홈', // 아이템 라벨 (텍스트)
              icon: Padding(
                padding: const EdgeInsets.all(8.0),
                // asset 이미지 경로를 실제 경로로 대체해야 합니다. 
                // 예: Image.asset('assets/svgs/icons/home_unselected.svg'),
                // 두 번째 이미지와 유사하게 svg 이미지 위젯을 사용한다고 가정
                child: SizedBox(
                  width: 24, height: 24, 
                  child: Icon(Icons.home), // 임시 아이콘
                ),
              ),
              activeIcon: Padding( // 선택되었을 때의 아이콘
                padding: const EdgeInsets.all(8.0),
                child: SizedBox(
                  width: 24, height: 24, 
                  child: Icon(Icons.home, color: Colors.white), // 임시 아이콘
                ),
              ),
            ),
            
            // 두 번째 아이템 (예: 동네생활)
            BottomNavigationBarItem(
              label: '동네생활',
              icon: Padding(
                padding: const EdgeInsets.all(8.0),
                child: SizedBox(
                  width: 24, height: 24, 
                  child: Icon(Icons.groups), // 임시 아이콘
                ),
              ),
              activeIcon: Padding(
                padding: const EdgeInsets.all(8.0),
                child: SizedBox(
                  width: 24, height: 24, 
                  child: Icon(Icons.groups, color: Colors.white), // 임시 아이콘
                ),
              ),
            ),
            
            // 필요한 만큼 아이템 추가...
            BottomNavigationBarItem(
              label: '내 정보',
              icon: Icon(Icons.person_outline),
              activeIcon: Icon(Icons.person),
            ),
          ],
        ),
      ),
    );
  }
}


bottom :

import 'package:get/get.dart';

class BottomNavController extends GetxController {
 
  RxInt menuIndex = 0.obs;

  void changeBottomNav(int index) {
    menuIndex.value = index;
  
  }
}
